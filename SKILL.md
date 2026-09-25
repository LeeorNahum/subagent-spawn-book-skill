---
name: "subagent-spawn-book"
description: "Subagent Spawn Book (SSB). Use before creating any subagent and before choosing which model leads a session or orchestrates a run: whenever the user asks for one, a plan includes delegation or fan-out, or the work at hand would go better in another session, such as research, a browser or computer-use task, a review or critique, a visual check, a bulk job, or anything another model would do better."
metadata:
  author: "Leeor Nahum"
  version: "2.1.1"
---

# Subagent Spawn Book

Use this skill before creating any subagent. A subagent is any separate model, agent, task runner, chat, CLI invocation, or orchestrator worker asked to handle part of the work, including a session that will run the work itself and delegate further.

This skill is a spawn book. It owns which model to select and how to find the exact spawn instructions. It does not own general prompting technique, task planning, or review method.

## Universal Spawn Rules

- Apply this skill at every spawn point, not once per session. Having read it earlier does not cover a later spawn: an orchestrator that fans out repeatedly, a mind that spawns its own researchers, or a plan step that delegates each re-applies the selection and naming rules to the spawn at hand.
- If the user names a specific model or agent, use that target unless it is unavailable in its own harness or unsafe for the requested action.
- Interpret informal model names from context and current provider naming. Do not require an exact reference heading when the user's intent is clear.
- If the user does not name a target, choose from the model section below without asking the user to pick.
- Treat this skill as a set of defaults for concise delegation. User, agent, plan, or project instructions override the defaults when they specify an undocumented model, mode, permission profile, harness, fan-out shape, or spawn method. When a project pins a model or a fan-out shape, follow it and say so at the spawn point rather than silently skipping this skill.
- A critic is spawned on a different provider than the work it checks, and is given the goal and the work rather than the builder's framing, so it does not inherit the builder's assumptions. When only one provider is reachable, use that provider's next-best model and say in the report that the check was same-provider, because it is weaker.
- If the current harness is the selected model's own harness, or the current session genuinely serves the selected model, use its internal subagent tooling. Confirm the internal tooling actually spawns the selected model. If internal subagents are pinned to a different model, that does not count.
- If the current harness is not the selected model's own harness, spawn the model through its own harness using the selected reference.
- If the user, plan, or orchestrator names a spawn preference, apply it after resolving the model. Do not treat access to a model inside another harness as model ownership.
- Read the selected model's reference before spawning it. References are model-specific and teach the exact spawn command and how to resume the session.
- A spawned session can be resumed by its id with a reply, and it keeps its context. Use that for a back-and-forth, such as a critic answering the builder's response, instead of starting over.
- A correction that arrives while a session runs reaches it only if its harness has an inbox. A Claude session accepts a message mid-run. A Codex exec session does not, so a correction waits for it to end and goes into the resume. Put what the session must not do in the first prompt.
- If the selected model is not listed here, identify its native owner or primary harness first, then use that harness when available.
- Each agent may directly spawn at most 10 subagents during a run. Every descendant has the same independent limit, so delegation may branch recursively but no agent may create an eleventh direct child.

## Session Names

When the harness lets you name a spawned session, thread, task, chat, or worker, start the name with the selected model and mode.

```text
(<model> <mode>) <short task name>
```

Use the model name from the selected model section and the reasoning effort or mode from the selected reference command, so the name carries both the model and its thinking level. If the user, agent, or plan specifies a different naming shape, use that instead.

## Lead Or Orchestrator Selection

Use this section when the user or plan is choosing the session lead or outer orchestrator, not only a delegated worker. Lead choice does not replace per-spawn model selection below.

- **Claude Fable** leads. It reads the intent behind an underspecified ask, makes the final calls, and keeps coherence across a long run with conflicting specialist findings.
- **GPT Astra** orchestrates work that lives in a browser or a desktop app, where it does better than the Claude models.
- **Claude Opus** runs a sub-orchestration under a lead and is the everyday workhorse: dispatching parallel workers, validating their returns, doing substantial work from a clear brief, and holding a large ledger or transcript in context. It does the work it is given and leaves the calls to the lead.

After the lead is chosen, keep using the subagent selection policy for every delegated spawn.

## Model Selection

Models are listed from the highest tier down. A section that names a role for the task at hand, such as the critic from the other provider, wins. When no section names the role, default to the highest listed model whose section fits the task.

### User-Specified Target

If the user names a model, use that model. If the named model is unavailable in its own harness or unsafe for the requested action, say so and choose the closest documented fallback.

### Claude Fable

Use for high-judgment delegated work: architecture critique, multi-constraint review, security or product coherence review, long-context synthesis, and blind high-stakes checking where careful reasoning matters more than speed. It is the model that makes a decision when the ask leaves room for one.

Also use for high-quality frontend work and component design where visual quality is the deliverable, including pixel art and other artifacts judged by eye.

Do not make it the default implementer for ordinary substantial edits that Astra can do from a clear specification. Prefer Fable when judgment, coherence, or visual quality is the deliverable.

Read the [Claude Fable spawn reference](references/claude-fable.md).

### GPT Astra

Use for anything that lives in a browser or a desktop app: navigating and checking a live product, testing an app that was just built, finding the bugs in it, filling in something specific, reproducing an interaction failure, and looking at rendered output for a visual pass. Those tools must be exposed to the spawned session. Astra does this work better than the Claude models, so send it there without hesitation. Do not substitute a text-only or shell-only check when the task requires that evidence.

Also use for 3D modeling and any other work in a 3D tool, where it is far ahead of every other model, as the critic from the other provider when a Claude model built the work, and for a long, specified job whose tools live in the browser. It reads intent nearly as well as Fable and follows a brief more literally, so spell the task out.

Read the [GPT Astra spawn reference](references/gpt-astra.md).

### Claude Opus

The workhorse. Use for substantial work from a clear brief, research sweeps that read many sources and return findings, and parallel fleets of workers that each need real judgment and a large context: competing agents whose outputs are scored against each other, and any fan-out where the same role runs several times at once and the results must be comparable. Its one-million-token context makes it the choice when a worker has to hold a long ledger, transcript, or document set while it works.

Also use for the adversarial critic when a GPT model built the work, as the next-best check when no other provider is reachable and a Fable session must not grade itself, and for a coherence review of prose another agent wrote.

Do not choose it for the single high-stakes call that Fable owns. Prefer Opus when the work is many parallel instances of a disciplined, well-specified role, or an independent check.

Read the [Claude Opus spawn reference](references/claude-opus.md).

### GPT Sol

Use for quick, small, well-defined jobs: a lookup, a one-file change, a check with a fixed answer, where Astra would be more model than the job needs and the work is not something the Claude models should do.

Read the [GPT Sol spawn reference](references/gpt-sol.md).

### GPT Luna

Rarely. Use for many tiny jobs with a fixed answer shape, such as extraction, classification, or bulk checks a rubric decides, where volume and cost matter more than anything else. Do not choose it for judgment, code, long tool chains, or anything a person will read as written.

Read the [GPT Luna spawn reference](references/gpt-luna.md).
