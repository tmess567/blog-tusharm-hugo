---
title: "When RAG Metrics Disagree: A Controlled Study of Models, Backends, and Evaluation Methods"
author: tusharm
type: post
date: '2026-04-05'
description: "A large-scale evaluation of 5 LLMs across 6 datasets with FAISS retrieval, scored by 10 metrics including a 3-judge panel and RAGAS. Automated metrics and judges disagree on which models are best. Findings on retrieval lift, model selection, multi-hop reasoning, and the limits of evaluation itself."
keywords:
  - RAG evaluation
  - LLM comparison
  - retrieval augmented generation
  - BERTScore
  - LLM as judge
  - RAGAS
  - FAISS
  - hallucination
  - multi-hop reasoning
image: /img/rag-eval-cover.jpg
tags:
  - AI
  - GenAI
  - Research
  - Software Engineering
---

Retrieval-augmented generation (RAG) is the dominant pattern for building LLM applications over private data. You retrieve relevant documents, pass them as context to an LLM, and get a grounded answer. But which LLM should you use? Does the dataset matter? And how do you even measure whether the answers are good?

To answer these questions, I ran 25,600 evaluations: 5 LLMs × 6 datasets × 2 retrieval conditions × 3 random seeds, with every response scored by 10 metrics — automated text similarity, a 3-judge panel, and RAGAS framework scores. The headline finding: **automated metrics and the LLM judges disagree on which models are best.**

<!--more-->

The rank correlation between Token F1 and judge correctness is weak. Any RAG evaluation that relies on a single type of metric is telling an incomplete story.

Four other findings stood out:
1. Retrieval improves answer quality by 40-65% across all 5 models — it's not optional for factual Q&A
2. Model choice drives far more variance than dataset choice within a retrieval condition
3. A 3-judge panel reveals systematic biases in individual judges — Sonnet 4 is the strictest, Llama 70B the most generous
4. RAGAS metrics tell a different story than both automated metrics and judges, adding a third axis of disagreement

## Background

A RAG pipeline has three stages: retrieve relevant documents, combine them with the user's question, and generate an answer with an LLM. Most published evaluations test retrieval or generation in isolation. When they evaluate the full pipeline, they typically use either automated text-similarity metrics or an LLM judge — rarely both, and almost never with multiple judges.

The problem is that these approaches have different biases. Automated metrics like Token F1 reward short, precise answers that match the reference text word-for-word. LLM judges reward detailed, well-structured answers that demonstrate understanding. RAGAS metrics evaluate specific dimensions like faithfulness and context relevance with their own scoring rubrics. A verbose but correct answer scores poorly on Token F1 but well with a judge. A terse answer that happens to use the same words as the reference scores well on Token F1 but may get marked as incomplete by a judge.

This evaluation uses all three approaches on every sample, which lets us identify where they agree (high-confidence findings) and where they disagree (metric-dependent findings that should be treated with skepticism).

## Evaluation Setup

### Models

5 LLMs spanning 3 model families and a range of capability tiers:

| Family | Models |
|--------|--------|
| Anthropic | Claude Haiku 3, Claude Sonnet 4 |
| Amazon | Nova Lite, Nova Pro |
| Meta | Llama 3.1 70B |

All models were called with temperature=0 and max_tokens=512 to ensure deterministic, comparable outputs. Each configuration was run with 3 random seeds to measure variance.

### Retrieval

- **FAISS** — Local vector index using Titan Embed Text V2 (1024-dim). Cosine similarity retrieval, top-5 passages. The question and retrieved passages are passed to the LLM with a simple prompt: *"Answer the question based on the provided context."*
- **No retrieval** — Baseline. The LLM receives only the question with no context. Measures how much retrieval actually helps.

### Datasets

All datasets are publicly available research benchmarks. Questions were sampled with fixed random seeds.

| Dataset | Source | Task Type | Questions Used |
|---------|--------|-----------|---------------|
| eManual | RAGBench (electronics manuals) | Procedural Q&A | 220 |
| TechQA | RAGBench (IBM tech support) | Single-hop factual | 100 |
| HotpotQA | Bridge-type questions | Multi-hop reasoning | 100 |
| MultiHop RAG | Multi-document reasoning | Multi-hop | 100 |
| MuSiQue | Multi-hop with sub-questions | Compositional reasoning | 166 |
| Spider | Text-to-SQL benchmark | SQL generation | 166 |

The eManual dataset includes an SOP (Standard Operating Procedure) ablation with 4 prompt modes: no SOP, basic SOP, chain-of-thought, and detailed SOP.

### Scoring

Every response was scored on 10 dimensions:

**Automated metrics** (computed locally, no LLM involved):
- **Token F1** — Word overlap between response and ground truth. Precision × recall harmonic mean.
- **ROUGE-L** — Longest common subsequence ratio.

**3-Judge Panel** (each judge scores all 25,600 samples independently):
- **Sonnet 4** — Tends to be the strictest judge
- **Llama 3.1 70B** — Most generous on correctness
- **Haiku 3.5** — Middle ground

Each judge evaluates correctness (are the facts right?) and faithfulness (is the answer grounded in the retrieved context?). The final score is the majority vote across all three judges.

**RAGAS Framework** (4 metrics, each scored 0-1):
- **Faithfulness** — Are claims in the answer supported by the context?
- **Answer Relevancy** — Does the answer address the question asked?
- **Context Precision** — Is the retrieved context relevant to the question?
- **Context Recall** — Does the context contain the information needed to answer?

## Results

### Finding 1: Retrieval Improves Every Model

The most consistent finding: adding FAISS retrieval improves answer quality across all 5 models on every metric.

<canvas id="retrievalLift" width="800" height="400"></canvas>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
new Chart(document.getElementById('retrievalLift'), {
  type: 'bar',
  data: {
    labels: ['Llama 70B','Haiku 3','Sonnet 4','Nova Lite','Nova Pro'],
    datasets: [
      {label:'No Retrieval', data:[0.230,0.148,0.131,0.117,0.098], backgroundColor:'rgba(239,68,68,0.7)'},
      {label:'FAISS Retrieval', data:[0.408,0.237,0.228,0.223,0.200], backgroundColor:'rgba(34,197,94,0.7)'}
    ]
  },
  options: {
    responsive:true,
    plugins:{title:{display:true,text:'Token F1: No Retrieval vs FAISS (sorted by lift)',font:{size:14}}},
    scales:{y:{beginAtZero:true,title:{display:true,text:'Token F1'}}}
  }
});
</script>

The lift ranges from +40% (Haiku 3) to +104% (Nova Pro). Even the strongest model without retrieval (Llama 70B at 0.230) scores below most models *with* retrieval. **Retrieval is not optional for factual Q&A.**

The judge panel confirms this: correctness jumps from 0.612 (no retrieval) to 0.727 (FAISS), and faithfulness from 0.432 to 0.574. RAGAS faithfulness shows the same pattern.

### Finding 2: Automated Metrics and Judges Disagree

Here's the model leaderboard ranked by Token F1 alongside the judge panel's majority correctness score:

<canvas id="leaderboard" width="800" height="400"></canvas>
<script>
new Chart(document.getElementById('leaderboard'), {
  type: 'bar',
  data: {
    labels: ['Llama 70B','Haiku 3','Sonnet 4','Nova Lite','Nova Pro'],
    datasets: [
      {label:'Token F1', data:[0.342,0.205,0.191,0.184,0.162], backgroundColor:'rgba(59,130,246,0.7)', yAxisID:'y'},
      {label:'Judge Correctness (0-1)', data:[0.660,0.642,0.754,0.656,0.712], backgroundColor:'rgba(249,115,22,0.7)', yAxisID:'y1'}
    ]
  },
  options: {
    responsive:true,
    plugins:{title:{display:true,text:'Model Leaderboard: Automated Metric vs 3-Judge Panel',font:{size:14}}},
    scales:{
      y:{beginAtZero:true,max:0.45,position:'left',title:{display:true,text:'Token F1'}},
      y1:{min:0.5,max:0.85,position:'right',title:{display:true,text:'Judge Correctness (majority)'},grid:{drawOnChartArea:false}}
    }
  }
});
</script>

The disagreements are striking:

- **Llama 70B** ranks 1st on Token F1 (0.342) but only 4th on judge correctness (0.660). It produces concise answers that match the reference text well, but the judges rate them as less complete.
- **Sonnet 4** ranks 3rd on Token F1 (0.191) but 1st on judge correctness (0.754). It produces verbose, well-structured responses that contain the right information but don't match the ground truth phrasing.
- **Nova Pro** ranks last on Token F1 (0.162) but 2nd on judge correctness (0.712). Same pattern — detailed answers penalized by word-overlap metrics.

**What this means in practice:** If you evaluate your RAG pipeline using only Token F1 or only an LLM judge, you'll get a confident but potentially misleading ranking. Use multiple metrics with different biases, and only trust conclusions where they agree.

### Finding 3: The 3-Judge Panel Reveals Systematic Bias

Using a single LLM judge is common practice. But when we compare three judges scoring the same 25,600 samples, systematic biases emerge:

<canvas id="judgeChart" width="800" height="400"></canvas>
<script>
new Chart(document.getElementById('judgeChart'), {
  type: 'bar',
  data: {
    labels: ['Sonnet 4','Haiku 3.5','Llama 70B'],
    datasets: [
      {label:'Correctness', data:[0.653,0.692,0.709], backgroundColor:'rgba(59,130,246,0.7)'},
      {label:'Faithfulness', data:[0.518,0.446,0.601], backgroundColor:'rgba(168,85,247,0.7)'}
    ]
  },
  options: {
    responsive:true,
    plugins:{title:{display:true,text:'Judge Bias: Same 25,600 Samples, Different Verdicts',font:{size:14}}},
    scales:{y:{beginAtZero:true,max:0.85,title:{display:true,text:'Score (0-1)'}}}
  }
});
</script>

Key patterns:
- **Llama 70B is the most generous judge** — highest correctness (0.709) and highest faithfulness (0.601)
- **Sonnet 4 is the strictest on correctness** (0.653) but moderate on faithfulness (0.518)
- **Haiku 3.5 is the strictest on faithfulness** (0.446) — it flags unfaithful answers that the other two judges let pass

The majority vote (0.685 correctness, 0.522 faithfulness) smooths out individual biases. But if you're using a single judge, your evaluation results depend heavily on *which* judge you pick. A study using only Llama 70B as judge would report 8% higher correctness than one using only Sonnet 4.

### Finding 4: RAGAS Adds a Third Axis of Disagreement

RAGAS metrics evaluate different dimensions than either automated metrics or judges. Here's how the models rank on RAGAS answer relevancy vs the other approaches:

<canvas id="ragasChart" width="800" height="400"></canvas>
<script>
new Chart(document.getElementById('ragasChart'), {
  type: 'bar',
  data: {
    labels: ['Nova Pro','Nova Lite','Sonnet 4','Llama 70B','Haiku 3'],
    datasets: [
      {label:'RAGAS Relevancy', data:[0.947,0.944,0.827,0.823,0.820], backgroundColor:'rgba(34,197,94,0.7)'},
      {label:'RAGAS Faithfulness', data:[0.660,0.655,0.686,0.624,0.668], backgroundColor:'rgba(168,85,247,0.7)'},
      {label:'Token F1', data:[0.162,0.184,0.191,0.342,0.205], backgroundColor:'rgba(59,130,246,0.4)'}
    ]
  },
  options: {
    responsive:true,
    plugins:{title:{display:true,text:'RAGAS Metrics vs Token F1',font:{size:14}}},
    scales:{y:{beginAtZero:true,title:{display:true,text:'Score'}}}
  }
});
</script>

RAGAS tells yet another story:
- **Nova models dominate on relevancy** (0.944-0.947) — they consistently answer the question asked, even when the answer is wrong
- **Sonnet 4 leads on RAGAS faithfulness** (0.686) — its answers are most grounded in the retrieved context
- **Llama 70B, the Token F1 champion, scores lowest on RAGAS faithfulness** (0.624) — it produces accurate text matches but draws more from parametric knowledge than context

RAGAS context precision is remarkably uniform across models (0.651-0.657), suggesting that retrieval quality is consistent regardless of which model consumes the context. Context recall (0.553-0.562) is also uniform and moderate — the FAISS index retrieves about half the information needed for a complete answer.

### Finding 5: Multi-Hop Reasoning Remains Hard

<canvas id="datasetChart" width="800" height="400"></canvas>
<script>
new Chart(document.getElementById('datasetChart'), {
  type: 'bar',
  data: {
    labels: ['eManual','TechQA','HotpotQA','Spider','MultiHop','MuSiQue'],
    datasets: [
      {label:'Token F1', data:[0.369,0.359,0.292,0.133,0.078,0.051], backgroundColor:'rgba(59,130,246,0.7)'},
      {label:'Judge Correctness', data:[0.779,0.769,0.708,0.556,0.725,0.600], backgroundColor:'rgba(249,115,22,0.7)'}
    ]
  },
  options: {
    responsive:true,
    plugins:{title:{display:true,text:'Dataset Difficulty — Average Across All Models',font:{size:14}}},
    scales:{y:{beginAtZero:true,title:{display:true,text:'Score'}}}
  }
});
</script>

Single-hop datasets (eManual, TechQA) are dramatically easier than multi-hop ones. MuSiQue is the hardest — Token F1 of 0.051 means models produce almost no word overlap with the ground truth.

The judge tells a different story for MultiHop: correctness of 0.725 despite Token F1 of only 0.078. Multi-hop answers tend to be longer and more explanatory. The judge gives credit for partial correctness and reasoning chains; Token F1 only counts exact word matches.

**Spider (text-to-SQL)** is interesting: low Token F1 (0.133) but moderate judge correctness (0.556). SQL generation is a format-sensitive task where minor syntactic differences tank Token F1 even when the query is semantically correct.

MuSiQue is genuinely hard by both measures — it requires composing answers from multiple documents where each sub-question depends on the previous answer. Current RAG pipelines retrieve documents independently for the full question rather than decomposing it into sub-queries, which limits their ability to find all the pieces needed for a correct answer.

### Finding 6: Structured Prompts Hurt Most Models

We tested four prompt modes on the eManual dataset with all 5 models:

- **No SOP** — Simple prompt: "Answer based on the context"
- **Basic SOP** — 3-step reasoning instruction
- **Chain of Thought** — Step-by-step reasoning
- **Detailed SOP** — Full agent persona with multi-stage workflow

<canvas id="sopChart" width="800" height="350"></canvas>
<script>
new Chart(document.getElementById('sopChart'), {
  type: 'bar',
  data: {
    labels: ['No SOP','Basic SOP','Detailed SOP','Chain of Thought'],
    datasets: [{
      label:'Token F1 (averaged across 5 models)',
      data:[0.245,0.234,0.232,0.223],
      backgroundColor:['rgba(34,197,94,0.8)','rgba(59,130,246,0.8)','rgba(249,115,22,0.8)','rgba(239,68,68,0.8)']
    }]
  },
  options: {
    responsive:true,
    plugins:{title:{display:true,text:'SOP Ablation — Token F1 on eManual',font:{size:14}},legend:{display:false}},
    scales:{y:{beginAtZero:true,max:0.3,title:{display:true,text:'Token F1'}}}
  }
});
</script>

The plain prompt wins. Every structured prompt mode reduces Token F1 compared to the simple baseline. Chain of thought performs worst (-9%).

Why do SOPs hurt? Two factors:

1. **Cognitive overhead.** Instructions like "verify your answer against the context" and "think step by step" cause the model to spend tokens on meta-reasoning — restating the question, listing caveats, adding structure — instead of answering directly. For straightforward factual Q&A where the answer is in the context, this overhead doesn't add value.

2. **Format mismatch.** SOP-guided responses are longer and more structured. The ground truth answers in eManual are short and direct ("Press and hold the power button for 3 seconds"). The extra structure in SOP responses gets penalized by Token F1 even when the core answer is correct.

This doesn't mean SOPs are useless — they may help on complex multi-step tasks where reasoning structure matters. But for factual Q&A with clear answers in the context, keep prompts simple.

## Evaluation Design Lessons

Running 25,600 evaluations across 5 models and 6 datasets taught several things about RAG evaluation methodology:

**Use a judge panel, not a single judge.** Individual judges have systematic biases that shift model rankings by up to 8%. A 3-judge majority vote produces more stable rankings. If you can only afford one judge, at least report which model you used — it matters.

**Use metrics with opposing biases.** Token F1 favors brevity; LLM judges favor verbosity; RAGAS evaluates specific dimensions like faithfulness and relevancy. When all three agree, you can be confident. When they disagree, flag the result as inconclusive rather than picking the metric that tells the story you prefer.

**The no-retrieval baseline is essential.** Without it, you can't quantify how much retrieval helps. The +40% to +104% lift we measured is the strongest argument for RAG in this study — and you'd miss it entirely without the baseline.

**Run multiple seeds.** A single evaluation run can produce noisy estimates. Running 3 seeds per configuration stabilizes rankings and lets you distinguish real differences from noise.

**RAGAS context metrics are model-independent.** Context precision and recall were nearly identical across all 5 models (within 1%). This makes sense — these metrics evaluate retrieval quality, not generation quality. But it also means RAGAS context metrics won't help you choose between models.

**Report disagreements, not just averages.** The most interesting finding in this study isn't any single ranking — it's that the rankings change depending on how you measure. That's the finding that should inform how you evaluate your own RAG pipeline.

## Limitations

**LLM-as-judge is not human evaluation.** Even with a 3-judge panel, all three judges are LLMs with their own biases. The panel reduces but doesn't eliminate this problem. Human evaluation remains the gold standard.

**Two retrieval conditions.** We tested FAISS and no-retrieval. Other backends (managed services, graph-based retrieval, hybrid search) may produce different results. The finding that retrieval helps is robust; the specific magnitude of improvement is FAISS-specific.

**Automated metrics have known biases.** Token F1 and ROUGE-L penalize verbose answers. Using multiple metrics with opposing biases mitigates but doesn't eliminate this problem.

**RAGAS scoring depends on the evaluator model.** Different evaluator models may produce different RAGAS scores. We used a single evaluator for consistency, but the absolute scores should be interpreted as relative comparisons between models rather than absolute quality measures.

**SOP ablation is dataset-specific.** We tested SOPs only on eManual (procedural Q&A). SOPs may help more on complex reasoning tasks or agentic workflows where structured thinking adds value.

## Summary

| Finding | Confidence | Evidence |
|---------|-----------|----------|
| Retrieval improves all models (+40% to +104%) | High | All metrics agree, all 5 models consistent, 3 seeds |
| Automated metrics and judges disagree | High | Direct measurement, 25,600 samples, 3 judges |
| Individual judges have systematic bias (up to 8%) | High | 3-judge panel on identical samples |
| RAGAS adds a third axis of disagreement | High | 4 RAGAS metrics on all 25,600 samples |
| Multi-hop reasoning is hard to measure | Medium | Metrics disagree most on these datasets |
| SOPs hurt on factual Q&A | Medium | Token F1 consistent across 4 prompt modes |

The clearest takeaway: **don't trust a single evaluation metric or a single judge.** The models that look best on Token F1 look mediocre to the judges, and vice versa. RAGAS tells yet another story. If you're building a RAG pipeline, evaluate with multiple approaches and be honest about where they disagree. The disagreements are where the interesting engineering decisions live.

---

*Evaluation conducted April 2026. 5 models were evaluated with temperature=0 and max_tokens=512. Each configuration was run with 3 random seeds. Datasets used: RAGBench TechQA, RAGBench eManual, HotpotQA, MultiHop RAG, MuSiQue, and Spider — all publicly available research benchmarks. Scoring: Token F1, ROUGE-L, 3-judge panel (correctness + faithfulness), and RAGAS (faithfulness, relevancy, context precision, context recall).*