---
title: "Building AI Agents That Actually Do Things: Lessons from the Payments Domain"
author: tusharm
type: post
date: '2026-04-01'
image: /img/ai-agents-tool-use.png
tags:
  - AI
  - LLM
  - GenAI
  - Software Engineering
---

There's a growing gap in the AI agent conversation. Everyone's talking about agents — autonomous systems that can reason, plan, and act. But most demos stop at "the agent wrote a nice email" or "it summarized a document." The real challenge starts when you need an agent to interact with production backend systems, handle authentication, deal with partial failures, and return structured results that downstream systems can consume.

Over the past several months, I've been building exactly this: tool-equipped LLM agents operating in the payments domain. These agents can query transaction systems, look up order histories, check workflow statuses, retrieve standard operating procedures, and interact with ticketing systems — all through structured tool interfaces that the model invokes autonomously.

Here's what I've learned.

<!--more-->

## The Hard Part Isn't the LLM

When people think about building AI agents, they focus on the model: which LLM to use, how to write the system prompt, how to handle multi-turn conversations. Those things matter, but they're maybe 20% of the work.

The other 80% is the tooling layer — the infrastructure that sits between the model's intent and the actual backend systems it needs to interact with. This is where the real engineering complexity lives.

### Schema Design Is Your Contract

Every tool an agent can use needs a well-defined schema. We used OpenAPI specifications to define our tool interfaces. This serves a dual purpose: the model uses the schema to understand what parameters it needs to provide, and the backend uses it to validate and route requests.

Getting these schemas right is critical. Too vague, and the model will hallucinate parameter values. Too rigid, and the model can't adapt to variations in user requests. We found that including clear descriptions, enums for constrained fields, and explicit examples in the schema dramatically improved the model's tool-use accuracy.

### Authentication Across Multiple Services

In any enterprise environment, the tools your agent calls don't all live behind the same auth boundary. One tool might need service-to-service credentials, another might need user-context tokens, and a third might need role-based access to a cloud resource.

We built an abstraction layer that handles credential resolution per-tool, so the agent framework doesn't need to know about auth details. Each tool provider is responsible for its own authentication, and the framework just passes through the execution context.

### Bulk Operations Change Everything

Early on, our agents would make one API call per item — look up one order, check one workflow, retrieve one document. This worked fine for simple queries but fell apart when users asked things like "check the status of all open workflows for this account."

We built a bulk operation mode into our tool provider abstraction. The same tool definition can operate in single-item or bulk mode, and the agent framework transparently handles batching, pagination, and result aggregation. This was one of the highest-impact changes we made — it reduced latency for multi-item queries by an order of magnitude and significantly cut our API call volume.

### Partial Failures Are the Norm

When your agent is calling 5 different backend services in a single conversation turn, some of them will fail. Maybe one service is slow, another returns a 500, and a third has stale data.

You can't just throw an error and give up. We built retry logic, graceful degradation, and partial-result handling into the tool execution layer. If 4 out of 5 tool calls succeed, the agent should present what it has and explain what it couldn't retrieve. This mirrors how a human expert would handle the same situation.

## Integration Testing Is Non-Negotiable

We invested heavily in integration tests that run against staging and production environments. These aren't unit tests with mocked responses — they're end-to-end tests that exercise the full path from agent invocation through tool execution to backend response.

A few things we learned about testing agentic systems:

- **Make tests dynamic.** Don't hardcode test data that can go stale. Query for valid test entities at runtime.
- **Test across environments.** A tool that works in staging might fail in production due to different data distributions, auth configurations, or rate limits.
- **Test the failure paths.** Deliberately test with invalid inputs, expired credentials, and unavailable services. Your agent's error handling is part of the user experience.

## The Plumbing Is the Product

If there's one takeaway from this work, it's this: in agentic AI systems, the infrastructure around the model is more important than the model itself. Models will keep getting better. But the patterns for reliable tool execution, schema management, auth handling, and failure recovery — those are engineering problems that require engineering solutions.

The "boring" parts of building AI agents are actually the most interesting ones.

---

*This post reflects my personal experience and opinions. No confidential or proprietary information is disclosed.*
