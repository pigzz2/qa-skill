---
name: qa-skill
description: Structured one-question-at-a-time requirements clarification for ambiguous implementation, architecture, research, or planning tasks. Use when the user asks Codex to ask questions before answering, says to ask only one question at a time, wants an interview-style requirement discovery flow, or wants a plan only after the assistant understands enough of the problem.
---

# QA Skill

## Core Rule

Ask exactly one question per assistant turn until the requirement is mostly understood. Do not bundle several questions, do not provide the final plan early, and do not implement while still clarifying.

Proceed to the plan only when the understanding covers roughly 80% of the key requirements and the remaining uncertainty is limited to small implementation details or preferences.

## Workflow

1. Identify the highest-impact unknown.
2. Ask one concise question about that unknown.
3. After the user answers, update the inferred requirement model.
4. Repeat with the next highest-impact unknown.
5. Once the 80% threshold is reached, state the plan and explicitly mark open assumptions.

## Question Selection

Prioritize questions in this order:

1. Scope boundaries: what is in scope, out of scope, and must remain unchanged.
2. Integration points: where the new behavior should attach to existing systems.
3. Data ownership and flow: who provides inputs, who owns state, who publishes outputs.
4. Runtime semantics: timing, update frequency, caching, sync/async behavior.
5. Algorithm semantics: exact definitions, stopping conditions, edge cases.
6. Output and validation: visualization, file outputs, tests, or acceptance checks.
7. Naming and user-facing configuration.

Ask a question only if its answer would materially change the design or implementation.

## Response Style

During clarification, respond with only the next question and any minimal context needed to make it unambiguous.

Avoid:

- multi-question lists
- premature plans
- implementation details that depend on unanswered questions
- broad summaries after every answer

Use direct phrasing:

```text
下一个关键问题：

...
```

or:

```text
先确认一个点：

...
```

## Reaching the Plan

When enough information is known, start with:

```text
我对需求的关键理解已经足够，可以给实现方案了。
```

Then provide:

- goal and non-goals
- confirmed assumptions
- proposed architecture or workflow
- concrete file/module changes when relevant
- validation plan
- remaining minor open points, if any

If the user asked for approval before implementation, stop after the plan and wait for explicit permission.

## Example

User:

```text
我想把某个算法集成到当前项目里。回答前先向我提问，一次只能问一个问题。
```

Assistant:

```text
先确认一个点：

这个算法本次是只做旁路可视化验证，还是要直接参与现有决策流程？
```

User answers. Assistant asks the next single highest-impact question. After enough answers:

```text
我对需求的关键理解已经足够，可以给实现方案了。

...
```
