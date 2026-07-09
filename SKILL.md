---
name: "subagent-spawn-book"
description: "Subagent Spawn Book (SSB) is used before creating any subagent, whether the user asks for one, the agent decides to delegate, or a plan includes delegation or fan-out. Select a default model when none is named, name the session, then read the selected model's spawn reference."
metadata:
  author: "Leeor Nahum"
  version: "0.1.0"
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
- Use full permissions for spawned agents unless the selected model reference says a lower permission mode is known to work.
- Read the selected model's reference before spawning it. References are model-specific and teach the exact spawn command.
- If the selected model is not listed here, identify its native owner or primary harness first, then use that harness when available.

## Session Names

When the harness lets you name a spawned session, thread, task, chat, or worker, start the name with the selected model and mode.

```text
(<model> <mode>) <short task name>
```

Use the model name from the selected model section and the mode from the selected reference command. If the user, agent, or plan specifies a different naming shape, use that instead.

## Model Selection

Default to picking the best documented model for the task. Use the descriptions below as the selection policy when the user, agent, or plan requests a subagent without naming one.

### User-Specified Target

If the user names a model, use that model. If the named model is unavailable in its own harness or unsafe for the requested action, say so and choose the closest documented fallback.

### GPT-5.5

Use as a quick, reliable workhorse for precision tasks: direct instructions, bounded local edits, testing, computer use, command-driven debugging, repo inspection, and artifact creation. It needs direct steering. Do not choose it for creative visual work, naming taste, or code beauty.

Read `references/gpt-5.5.md`.

### Claude Sonnet 5

Use for higher-taste execution: UI, visual judgment, naming, code quality, API structure, product flow, and implementation where the shape of the result matters as much as task completion.

Read `references/claude-sonnet-5.md`.
