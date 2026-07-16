---
name: "subagent-spawn-book"
description: "Subagent Spawn Book (SSB) is used before creating any subagent, whether the user asks for one, the agent decides to delegate, or a plan includes delegation or fan-out. Select a default model when none is named, name the session, then read the selected model's spawn reference."
metadata:
  author: "Leeor Nahum"
  version: "1.2.0"
---

# Subagent Spawn Book

Use this skill before creating any subagent. A subagent is any separate model, agent, task runner, chat, CLI invocation, or orchestrator worker asked to handle part of the work.

You can call this skill `SSB` or `spawn book` in plans and prompts.

This skill is a spawn book. It owns which model to select and how to find the exact spawn instructions. It does not own general prompting technique, task planning, or review method.

## Universal Spawn Rules

- If the user names a specific model or agent, use that target unless it is unavailable in its own harness or unsafe for the requested action.
- Interpret informal model names from context and current provider naming. Do not require an exact reference heading when the user's intent is clear.
- If the user does not name a target, choose from the model section below without asking the user to pick.
- Treat this skill as a set of defaults for concise delegation. User, agent, or plan instructions override the defaults when they specify an undocumented model, mode, permission profile, harness, or spawn method.
- If the current harness is the selected model's own harness, use its internal subagent tooling.
- If the current harness is not the selected model's own harness, spawn the model through its own harness using the selected reference.
- If the user, plan, or orchestrator names a spawn preference, apply it after resolving the model. Do not treat access to a model inside another harness as model ownership.
- Read the selected model's reference before spawning it. References are model-specific and teach the exact spawn command.
- If the selected model is not listed here, identify its native owner or primary harness first, then use that harness when available.

## Session Names

When the harness lets you name a spawned session, thread, task, chat, or worker, start the name with the selected model and mode.

```text
(<model> <mode>) <short task name>
```

Use the model name from the selected model section and the reasoning effort or mode from the selected reference command, so the name carries both the model and its thinking level. If the user, agent, or plan specifies a different naming shape, use that instead.

## Lead Or Orchestrator Selection

Use this section when the user or plan is choosing the session lead or outer orchestrator, not only a delegated worker. Lead choice does not replace per-spawn model selection below.

- Prefer **Claude Fable 5** as lead for constraint-dense, long-horizon product builds, large migrations, multi-day autonomous work, and runs that must keep coherence across growing context while synthesizing conflicting specialist findings.
- Prefer **GPT-5.6 Sol** as lead for shorter tool-heavy agent loops, terminal-first delivery, and runs where literal throughput and structured tool chaining matter more than long-horizon product judgment.
- Do not choose Claude Sonnet 5 or GPT-5.6 Terra as lead. Keep them as delegated workers under Model Selection.

After the lead is chosen, keep using the subagent selection policy for every delegated spawn.

## Model Selection

Default to picking the best documented model for the task. Use the descriptions below as the selection policy when the user, agent, or plan requests a subagent without naming one.

### User-Specified Target

If the user names a model, use that model. If the named model is unavailable in its own harness or unsafe for the requested action, say so and choose the closest documented fallback.

### GPT-5.6 Terra

Use for browser-use tasks: navigating and checking a live web product, reproducing interaction failures, and confirming user-facing flows. Browser use must be exposed by the selected harness. Do not substitute a text-only or shell-only check when the task requires browser evidence.

Also use for quick research and fact-finding tasks: source lookups, documentation checks, version and compatibility sweeps, and small scouting errands where speed matters more than depth.

Read the [GPT-5.6 Terra spawn reference](references/gpt-5.6-terra.md).

### GPT-5.6 Sol

Use for deep implementation, in-depth checks, testing, and verification. It is the default for substantial edits, command-driven debugging, repo inspection, artifact creation, tool-heavy terminal work, and rigorous conformance review against a specification, skill, contract, checklist, or other source of truth. Prefer it when literal instruction following and structured tool chaining matter more than taste.

It needs direct steering. Do not choose it for creative visual work, naming taste, or code beauty.

Read the [GPT-5.6 Sol spawn reference](references/gpt-5.6-sol.md).

### Claude Sonnet 5

Use for higher-taste execution: UI, visual judgment, naming, code quality, API structure, product flow, and implementation where the shape of the result matters as much as task completion.

Also use for wording and creative passes: user-facing copy, naming candidates, coherence review of user-facing text and artifacts, and extra-thinking passes that generate variation or alternatives on an existing draft.

Read the [Claude Sonnet 5 spawn reference](references/claude-sonnet-5.md).

### Claude Fable 5

Use for high-judgment delegated work: architecture critique, multi-constraint review, security or product coherence review, long-context synthesis, and blind high-stakes checking where careful reasoning matters more than speed.

Also use for high-quality frontend work and component design where visual quality is the deliverable, including pixel art and other artifacts judged by eye.

Do not make it the default implementer for ordinary substantial edits when GPT-5.6 Sol fits. Prefer Fable when judgment, coherence, or visual quality is the deliverable.

Read the [Claude Fable 5 spawn reference](references/claude-fable-5.md).
