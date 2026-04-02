---
title: "The Delegation Gap: Why AI Coding Agents Aren't as Autonomous as You Think"
author: tusharm
type: post
date: '2026-04-02'
image: /img/delegation-gap-hero.png
tags:
  - AI
  - Developer Productivity
  - GenAI
  - Software Engineering
  - Research
---

<div class="modern-post">

Anthropic's 2026 report says developers use AI in 60% of their work but can fully delegate only 0-20% of tasks <sup>[[1]](#references)</sup>. That's a massive gap. I dug into the public research to understand why — and the answer isn't what most people assume.

As someone who uses AI coding agents daily, I assumed the bottleneck was model capability. It's not. The research points to something more fundamental.

## The Conversation Depth Problem

Most AI coding conversations are shockingly short. Looking at three large public datasets of real developer-AI interactions <sup>[[2]](#references)[[3]](#references)[[4]](#references)</sup>:
{{< chart id="turnChart" width="750" height="380" >}}
new Chart(document.getElementById('turnChart'), {
  type: 'bar',
  data: {
    labels: ['1-2', '3-5', '6-10', '11-20', '20+'],
    datasets: [
      {label: 'LMSYS Chatbot Arena (33K)', data: [90, 6, 3, 0, 0], backgroundColor: 'rgba(239,68,68,0.75)', borderColor: 'rgba(239,68,68,1)', borderWidth: 1},
      {label: 'WildChat / ChatGPT (50K)', data: [52, 17, 19, 10, 4], backgroundColor: 'rgba(34,197,94,0.75)', borderColor: 'rgba(34,197,94,1)', borderWidth: 1},
      {label: 'DevGPT / GitHub PRs (3.8K)', data: [65, 20, 10, 4, 1], backgroundColor: 'rgba(59,130,246,0.75)', borderColor: 'rgba(59,130,246,1)', borderWidth: 1}
    ]
  },
  options: {
    events: [],
    responsive: true,
    plugins: {
      title: {display: true, text: ['Conversation Depth Across 3 Public Datasets','86K+ real developer-AI coding conversations'], font: {size: 14}, padding: {bottom: 15}},
      subtitle: {display: true, text: 'Most coding conversations are 1-2 turns — quick Q&A, not sustained collaboration', font: {size: 12, style: 'italic'}, color: '#888', padding: {bottom: 10}},
      datalabels: {display: function(ctx) { return ctx.dataset.data[ctx.dataIndex] > 15; }, anchor: 'end', align: 'top', font: {size: 10, weight: 'bold'}, formatter: function(v) { return v + '%'; }}
    },
    scales: {
      y: {title: {display: true, text: '% of sessions'}, max: 100, grid: {color: 'rgba(0,0,0,0.06)'}},
      x: {title: {display: true, text: 'Conversation turns'}, grid: {display: false}}
    }
  }
});
{{< /chart >}}
Across all three datasets, the pattern is consistent: **the vast majority of coding conversations are 1-2 turns.** In LMSYS, it's 90%. In WildChat, 52%. Even in DevGPT (conversations shared in GitHub PRs and issues — presumably more complex tasks), 65% are just a question and an answer.

This tells us something important: most developers are using AI for quick lookups and one-shot code generation, not for sustained collaboration on complex tasks. The "AI pair programmer" narrative doesn't match how people actually use these tools.

This matches my own experience. I use AI coding agents daily — for everything from debugging production incidents to multi-day feature migrations. But when I look honestly at how I use them, the majority of my sessions are short: a quick lookup, a one-shot code generation, a "what does this error mean?" And the sessions that *are* long tend to be long not because they're productive, but because I'm afraid to close them.

## 78% of AI Failures Are Invisible

A Stanford/Bigspin study analyzed 196,000 real ChatGPT conversations <sup>[[5]](#references)</sup>:
{{< chart id="qualityChart" width="750" height="340" >}}
new Chart(document.getElementById('qualityChart'), {
  type: 'bar',
  data: {
    labels: ['All Conversations', 'Failures Only (16%)'],
    datasets: [
      {label: 'Good (63%)', data: [63, 0], backgroundColor: 'rgba(34,197,94,0.85)'},
      {label: 'Acceptable — hidden issues (21%)', data: [21, 0], backgroundColor: 'rgba(234,179,8,0.85)'},
      {label: 'Failed (16%)', data: [16, 0], backgroundColor: 'rgba(239,68,68,0.5)', borderColor: 'rgba(239,68,68,0.8)', borderWidth: 1},
      {label: 'Invisible — user didn\'t notice (78%)', data: [0, 78], backgroundColor: 'rgba(239,68,68,0.85)'},
      {label: 'Visible — user reacted (22%)', data: [0, 22], backgroundColor: 'rgba(59,130,246,0.85)'}
    ]
  },
  options: {
    events: [],
    indexAxis: 'y',
    responsive: true,
    plugins: {
      title: {display: true, text: 'The Quality Iceberg: What Happens in 196K Conversations', font: {size: 15, weight: 'bold'}},
      subtitle: {display: true, text: 'Top: all conversations. Bottom: zooming into the 16% that failed.', font: {size: 12, style: 'italic'}, color: '#888', padding: {bottom: 8}},
      datalabels: {display: function(ctx) { return ctx.dataset.data[ctx.dataIndex] > 5; }, color: '#fff', font: {size: 13, weight: 'bold'}, formatter: function(v, ctx) { return v + '%'; }},
    },
    scales: {
      x: {stacked: true, max: 100, title: {display: true, text: '%'}, grid: {color: 'rgba(0,0,0,0.06)'}},
      y: {stacked: true, grid: {display: false}}
    }
  }
});
{{< /chart >}}
The bottom bar zooms into the 16% that failed — **78% of those failures were invisible.** The user accepted wrong code, fabricated citations, or missed requirements without pushing back.

I've caught myself doing this. An AI agent generates a plausible-looking fix, I skim it, it compiles, I move on. It's only later — sometimes days later — that I realize it silently broke an edge case or introduced a subtle regression. The failure wasn't loud. It was *fluent*.

The researchers found that **94% of these invisible failures would persist with a more capable model** <sup>[[5]](#references)</sup>. The #1 pattern (79% of failures): the model generates fluent output instead of asking for clarification.

## The Eight Failure Archetypes

The study identified eight recurring patterns of invisible failure <sup>[[5]](#references)</sup>:
{{< chart id="archetypeChart" width="700" height="400" >}}
new Chart(document.getElementById('archetypeChart'), {
  type: 'bar',
  data: {
    labels: ['The Drift', 'Confidence Trap', 'Mystery Failure', 'Death Spiral', 'Partial Recovery', 'Walkaway', 'Silent Mismatch', 'Contradiction'],
    datasets: [{
      label: '% of invisible failures',
      data: [32, 28, 18, 13, 5, 6, 4, 3],
      backgroundColor: [
        'rgba(239,68,68,0.8)','rgba(249,115,22,0.8)','rgba(156,163,175,0.8)',
        'rgba(234,179,8,0.8)','rgba(34,197,94,0.7)','rgba(59,130,246,0.7)',
        'rgba(99,102,241,0.7)','rgba(168,85,247,0.7)'
      ]
    }]
  },
  options: {
    events: [],
    indexAxis: 'y',
    responsive: true,
    plugins: {
      title: {display: true, text: 'Invisible Failure Archetypes (from 196K ChatGPT conversations)', font: {size: 15}},
      legend: {display: false}
    },
    scales: {x: {title: {display: true, text: '% of invisible failures'}}}
  }
});
{{< /chart >}}
**The Drift** is the most common: the AI addresses a related but different goal than what the user asked for. It's gradual, plausible-sounding, and hard to catch. **The Confidence Trap** is the most dangerous: the AI gives a wrong answer with complete certainty, and the user accepts it.

Software development was the only domain with a high rate of *visible* failures — developers push back when code doesn't work. In creative writing, education, and general knowledge, failures go almost entirely undetected.

## The Vicious Cycle

Martin Fowler's team published ["Context Anchoring"](https://martinfowler.com/articles/reduce-friction-ai/context-anchoring.html) in March 2026 <sup>[[6]](#references)</sup>, describing a dynamic that anyone who's used an AI coding agent will recognize: developers keep conversations running far longer than they should — not because long sessions are productive, but because closing the session means losing everything.

They call it a **vicious cycle**. The context lives only in the chat. There's no external record. So the conversation stretches on while the AI's ability to recall earlier decisions quietly degrades. And when you finally close the session, you start from zero.

I've lived this cycle. I once ran a multi-day code migration that spawned dozens of sessions with an AI agent. Each new session started with me re-explaining the same architecture, the same constraints, the same decisions we'd already made. The agent was helpful within each session — but it couldn't carry anything across them. I was the memory. And I'm not a great database.

## Context Rot Is Real — and Measured

This isn't just a feeling. Researchers have now quantified it. A study evaluating Claude, GPT-4.1, Llama 4, and o4-mini on long-context tasks found that **success rates drop from 40-50% to less than 10%** as context length increases <sup>[[7]](#references)</sup>. The phenomenon has a name: **context rot**.
{{< chart id="contextRotChart" width="700" height="400" >}}
new Chart(document.getElementById('contextRotChart'), {
  type: 'line',
  data: {
    labels: ['Baseline', '2x context', '4x context', '8x context', 'Full session'],
    datasets: [{
      label: 'Task success rate',
      data: [45, 35, 22, 14, 8],
      borderColor: 'rgba(239,68,68,1)',
      backgroundColor: 'rgba(239,68,68,0.08)',
      fill: true,
      tension: 0.3,
      pointRadius: 6,
      pointBackgroundColor: ['rgba(34,197,94,1)','rgba(234,179,8,1)','rgba(249,115,22,1)','rgba(239,68,68,1)','rgba(185,28,28,1)'],
      pointBorderColor: '#fff',
      pointBorderWidth: 2
    }]
  },
  options: {
    events: [],
    responsive: true,
    layout: {padding: {top: 25}},
    plugins: {
      title: {display: true, text: 'Context Rot: How Agent Performance Degrades', font: {size: 14}},
      subtitle: {display: true, text: 'arxiv:2512.04307 — Claude 3.7, GPT-4.1, Llama 4, o4-mini', font: {size: 11, style: 'italic'}, color: '#888', padding: {bottom: 15}},
      legend: {display: false},
      datalabels: {anchor: 'end', align: 'top', offset: 4, font: {size: 11, weight: 'bold'}, color: '#555', formatter: function(v) { return v + '%'; }}
    },
    scales: {
      y: {title: {display: true, text: 'Success rate (%)'}, min: 0, max: 55, grid: {color: 'rgba(0,0,0,0.06)'}},
      x: {grid: {display: false}}
    }
  }
});
{{< /chart >}}
Another study found that degradation starts in as few as **two turns** — driven by three mechanisms: context compression discards critical state, reasoning coherence fragments as token budgets shrink, and coordination breaks down without shared ground truth <sup>[[7]](#references)</sup>. The model literally thinks less as the conversation grows.

Longer context windows don't fix this. A 1M-token window just means you can accumulate more noise before the model collapses.
{{< mermaid >}}
graph TD
    A[Start new session] --> B[Re-explain context]
    B --> C[AI works on task]
    C --> D{Context degrades?}
    D -->|Yes| E[AI drifts / makes errors]
    E --> F{Fix in-session?}
    F -->|Too degraded| G[Abandon session]
    G --> A
    F -->|Possible| C
    D -->|No| H{Task complete?}
    H -->|No| C
    H -->|Yes| I[Done ✓]
    style G fill:#ef4444,color:#fff
    style I fill:#22c55e,color:#fff
    style A fill:#3b82f6,color:#fff
{{< /mermaid >}}
This maps to the "Lost in the Middle" research from Stanford <sup>[[8]](#references)</sup> — LLMs perform significantly worse on information placed in the middle of long contexts. The reasoning behind decisions degrades faster than the decisions themselves. The AI remembers *what* you chose but forgets *why*.

## Programming Is Now 50% of All LLM Usage

The OpenRouter 100-trillion-token study (covering 5M+ developers across 300+ models) shows the scale of this problem <sup>[[9]](#references)</sup>:
{{< chart id="usageChart" width="700" height="350" >}}
new Chart(document.getElementById('usageChart'), {
  type: 'line',
  data: {
    labels: ['Jan 2025', 'Mar', 'May', 'Jul', 'Sep', 'Nov 2025'],
    datasets: [{
      label: 'Programming (% of all LLM usage)',
      data: [11, 18, 28, 35, 42, 50],
      borderColor: 'rgba(59,130,246,1)',
      backgroundColor: 'rgba(59,130,246,0.1)',
      fill: true,
      tension: 0.3
    },{
      label: 'Avg prompt length (K tokens)',
      data: [1.5, 2.2, 3.0, 4.0, 5.0, 6.0],
      borderColor: 'rgba(234,179,8,1)',
      backgroundColor: 'rgba(234,179,8,0.1)',
      fill: true,
      tension: 0.3,
      yAxisID: 'y1'
    }]
  },
  options: {
    events: [],
    responsive: true,
    plugins: {
      title: {display: true, text: 'Programming Dominance + Prompt Growth (OpenRouter, 100T tokens)', font: {size: 15}},
    },
    scales: {
      y: {title: {display: true, text: '% of total usage'}, min: 0, max: 60, position: 'left'},
      y1: {title: {display: true, text: 'Avg prompt tokens (K)'}, min: 0, max: 8, position: 'right', grid: {drawOnChartArea: false}}
    }
  }
});
{{< /chart >}}
Programming went from 11% to over 50% of all LLM token usage in a single year — and prompts grew 4x in length alongside it. Coding prompts are 3-4x longer than general prompts. On OpenRouter alone, Anthropic's Claude handles over 60% of programming spend <sup>[[9]](#references)</sup>. Agentic inference — multi-step, tool-calling workflows — is becoming the default.

Meanwhile, the AIDev dataset shows that **932,000 agent-authored pull requests** have already landed on GitHub from tools like Codex, Devin, Copilot, Cursor, and Claude Code <sup>[[10]](#references)</sup> — and their code is accepted less frequently than human-authored code, revealing a persistent trust gap.

## The Trust Gap in Agent-Authored Code

That AIDev dataset deserves a closer look:
{{< chart id="trustChart" width="700" height="320" >}}
new Chart(document.getElementById('trustChart'), {
  type: 'bar',
  data: {
    labels: ['Speed (time to PR)', 'PR Acceptance Rate', 'Benchmark Accuracy', 'Hard Feature Pass@3'],
    datasets: [{
      label: 'Agent performance (%)',
      data: [85, 45, 69, 22],
      backgroundColor: ['rgba(34,197,94,0.8)','rgba(239,68,68,0.8)','rgba(234,179,8,0.8)','rgba(185,28,28,0.8)'],
      borderColor: ['rgba(34,197,94,1)','rgba(239,68,68,1)','rgba(234,179,8,1)','rgba(185,28,28,1)'],
      borderWidth: 1
    }]
  },
  options: {
    events: [],
    indexAxis: 'y',
    responsive: true,
    plugins: {
      title: {display: true, text: 'The Agent Trust Gap', font: {size: 14}},
      subtitle: {display: true, text: '932K GitHub PRs (AIDev) + SWE-Dev + Coding Benchmarks', font: {size: 11, style: 'italic'}, color: '#888'},
      legend: {display: false},
      datalabels: {anchor: 'end', align: 'right', font: {size: 12, weight: 'bold'}, formatter: function(v) { return v + '%'; }}
    },
    scales: {
      x: {min: 0, max: 100, grid: {color: 'rgba(0,0,0,0.06)'}},
      y: {grid: {display: false}}
    }
  }
});
{{< /chart >}}
Agents are fast — they outperform humans on time-to-PR. But their code is **accepted less frequently** than human-authored code <sup>[[10]](#references)</sup>. The best models top out at 69% accuracy on coding benchmarks <sup>[[11]](#references)</sup>. And on hard feature development tasks (not bug fixes — actual new features), the best single model succeeds on just **22% of hard tasks** (even with 3 attempts) <sup>[[12]](#references)</sup>.

The delegation ceiling isn't 0-20% because models are dumb. It's because the tasks that matter most — multi-file features, architectural decisions, long-running migrations — are exactly the tasks where context rot, trust gaps, and interaction failures compound.

## A Delegation Decision Framework

Based on the research above, here's my practical framework for when to delegate vs supervise:
{{< mermaid >}}
graph TD
    A[New Task] --> B{Spans multiple sessions?}
    B -->|No| C{Structured I/O?}
    C -->|Yes| D[✅ Full Delegation<br/>Status checks, searches, lookups]
    C -->|No| E{Creative/low-risk?}
    E -->|Yes| F[✅ Full Delegation<br/>Writing, research, recommendations]
    E -->|No| G[👀 Supervised<br/>Single-session code changes, bug fixes]
    B -->|Yes| H{Can you externalize context?}
    H -->|Yes| I[👀 Supervised + Context Doc<br/>Use Fowler's context anchoring pattern]
    H -->|No| J[⚠️ Heavy Supervision<br/>Expect restarts. Budget for re-explanation.]
    style D fill:#22c55e,color:#fff
    style F fill:#22c55e,color:#fff
    style G fill:#3b82f6,color:#fff
    style I fill:#3b82f6,color:#fff
    style J fill:#ef4444,color:#fff
{{< /mermaid >}}
The key insight from Fowler: if you can close your AI session and start a new one without anxiety — without feeling you'd lose something important — your context is properly anchored. If closing the session feels risky, that's the signal that decisions exist only in the conversation, and the conversation is the wrong place for them to live.

## What I've Learned Using AI Agents Daily

I've been using AI coding agents as my primary development tool for months now. Not as a novelty — as a daily driver for production work. Here's what I've noticed:

**The tasks I delegate most successfully are the ones I'd describe as "boring."** Searching tickets, checking pipeline status, looking up metrics, generating boilerplate. These are structured-input, structured-output tasks. The AI handles them perfectly because there's no ambiguity and no accumulated context to lose.

**Writing and research delegate surprisingly well.** This blog post is a good example — I used an AI agent to help find papers, extract data, build charts, and iterate on drafts. The key difference from coding: writing is low-stakes to review. I can read a paragraph and know instantly if it's wrong. I can't always do that with code.

**Incident response is where supervised collaboration shines.** During a production incident, I provide the context (what service, what symptoms, what changed) and the AI investigates — pulling logs, querying metrics, suggesting hypotheses. Neither of us could do it as fast alone. But I'd never let the AI run an incident unsupervised.

**Multi-day feature work is where everything breaks down.** I've had migrations that spanned weeks of sessions. Each new session, I'd spend the first 10-15 minutes re-explaining the architecture, the constraints, the decisions we'd already made. The agent was productive within each session but had zero memory across them. I was the continuity layer — and I'm lossy.

**The biggest surprise: I delegate non-coding tasks more successfully than coding tasks.** Document review, research synthesis, writing drafts, even analyzing lease agreements. These tasks have clear success criteria and are easy to verify. Code, paradoxically, is harder to delegate because failures are silent and verification requires running the code, not just reading it.

## What Needs to Change

The delegation gap won't close with better models. It'll close with better interaction design. The good news: the industry is already moving.

- **Session memory is evolving fast.** The first generation was static rules files — Cursor's `.cursorrules`, Copilot's `instructions.md`, Claude Code's `CLAUDE.md`. Useful, but they're "here's my preferences," not "here's what we decided." The next generation is more interesting: Claude Code now has auto-memory that accumulates project knowledge across sessions without you writing anything down. Google's Antigravity generates its own context artifacts — task checklists, implementation plans, walkthroughs — that persist as the agent's memory for future sessions. Anthropic's Cowork gives agents persistent workspaces with dedicated storage, scheduled tasks, and project-scoped memory that survives between sessions. These are real steps toward Fowler's context anchoring vision <sup>[[6]](#references)</sup> — but they're still early. The gap between "remembers my code style" and "remembers why we chose this architecture three sessions ago" remains wide.
- **Failure detection**: 78% of failures are invisible because the AI never signals uncertainty. We need proactive drift detection — not just confident-sounding output.
- **Clarification over generation**: The #1 failure pattern (79% of cases) is the model generating fluent output instead of asking for clarification <sup>[[5]](#references)</sup>. Models that say "did you mean X or Y?" will outperform models that guess.

The model isn't the bottleneck. The session is. But the session is getting smarter.

---

### References

1. Anthropic, ["Eight Trends Defining How Software Gets Built in 2026"](https://claude.com/blog/eight-trends-defining-how-software-gets-built-in-2026), 2026.
2. LMSYS, [Chatbot Arena Conversations](https://huggingface.co/datasets/lmsys/chatbot_arena_conversations) — 33K multi-turn conversations, HuggingFace.
3. Zhao et al., ["WildChat: 1M ChatGPT Interaction Logs in the Wild"](https://arxiv.org/abs/2405.01470), 2024 — 50K sample analyzed.
4. Xiao et al., ["DevGPT: Studying Developer-ChatGPT Conversations"](https://arxiv.org/abs/2309.03914), 2023 — 3.8K GitHub-linked conversations.
5. Potts & Sudhof, ["Invisible Failures in Human-AI Interactions"](https://arxiv.org/abs/2603.15423), Stanford/Bigspin, 2026 — 196K annotated ChatGPT transcripts.
6. Fowler et al., ["Context Anchoring"](https://martinfowler.com/articles/reduce-friction-ai/context-anchoring.html), martinfowler.com, March 2026.
7. Levy et al., ["Long-Context Reasoning Degradation in Web Agents"](https://arxiv.org/abs/2512.04307), 2025 — context rot measurement across Claude 3.7, GPT-4.1, Llama 4, o4-mini.
8. Liu et al., ["Lost in the Middle: How Language Models Use Long Contexts"](https://arxiv.org/abs/2307.03172), Stanford, 2023.
9. Willison et al., ["State of AI: 100 Trillion Token Study"](https://arxiv.org/abs/2601.10088), OpenRouter/a16z, 2025 — 5M+ developers, 300+ models.
10. Murali et al., ["AIDev: AI Coding Agents on GitHub"](https://arxiv.org/abs/2602.09185), 2026 — 932K agent-authored pull requests.
11. Jain et al., ["AI Coding Assistant Benchmark"](https://arxiv.org/abs/2601.16456), 2025 — Grok 4 (69.3%), Claude Opus 4 (68.5%), GPT-5 (67.8%).
12. Mundler et al., ["SWE-Dev: Evaluating LLMs on Real Feature Development"](https://arxiv.org/abs/2505.16975), 2025 — 14K feature dev tasks, Claude 3.7 Sonnet 22% Pass@3 on hard split.

*No confidential or proprietary information is disclosed in this post.*

</div>
