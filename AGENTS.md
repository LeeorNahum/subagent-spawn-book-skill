# Maintenance Contract: subagent-spawn-book

This file is for agents editing the skill. Keep maintainer rules here, not in `SKILL.md`.

## File Roles

| File | Role |
| --- | --- |
| `SKILL.md` | Trigger, universal spawn rules, lead or orchestrator selection, subagent model selection, reference-loading map |
| `references/<model>.md` | Exact spawn command for that model |
| `README.md` | Short human skim layer |
| `AGENTS.md` | This maintenance contract |

## Ownership Rules

- `SKILL.md` owns broad spawn policy: session naming, lead or orchestrator selection, subagent model selection, and the list of model references.
- `SKILL.md` owns the current model descriptions and what each model is good for, including when a model should lead a session versus handle a delegated spawn.
- `references/` owns only model-specific spawn mechanics: native harness identity, current-harness internal tooling when applicable, command shape, reasoning effort, permission and sandbox settings, and tested command notes.
- Put exact commands, CLI flags, current-harness tool names, setup notes, reasoning effort, permission and sandbox settings, and model-specific failure modes in the model reference file.
- Keep `SKILL.md` free of model-specific spawn settings. It selects the model and routes to its reference, but never states a reasoning effort, permission profile, sandbox setting, CLI flag, or other execution setting.
- When adding a model, document how to recognize whether the current harness is that model's own harness. If it is, use current-harness internal tooling. If it is not, spawn through the model's native harness using the command in the reference.
- When adding a model that is not listed yet, first identify its native owner or primary harness, then document that harness in the model reference.
- Document all-permissions mode for each spawn path unless that path is already known to run without getting stuck.
- Add one reference per model, model role, or harness-specific model path when spawn mechanics differ materially.
- Do not bury a current model favorite in the skill description. The description must stay stable as model rankings change.
- Name models without a version in `SKILL.md`, so each harness picks its current one. Pin a version in a reference command only when pinning is the point, and say why there.
- Order the model sections from the highest tier down by capability, never grouped by vendor, and keep the lead section in the same order.
- Do not add general prompting guidance. Prompting is not this skill's specialty unless a model reference needs a narrow spawn-specific instruction.
- Do not put maintainer guidance in `SKILL.md`. Instructions about how the skill should be edited belong in this file.
- Do not put general model-selection policy in references. References are spawn recipes only.

## Reference Standard

Every model reference should use these sections:

1. `# <Model Or Agent>`
2. `## Spawn`
3. `## Notes` only when the model has real spawn caveats

Keep model references short. Do not repeat the model's strengths, task fit, or settings unless needed inside an exact command.

## File Naming Standard

Reference filenames use the model's public name without a version, lowercase with hyphens for spaces. Where a harness needs a full identifier inside a command, it lives in the command line of the reference and nowhere else, so a new version changes one line.

## Editing Rules

- Version `SKILL.md` at a meaningful checkpoint. During initial creation or an active review loop before commit, keep the draft's version stable unless the user is explicitly preparing the publishable version.
- Keep every frontmatter string quoted.
- Keep examples generic unless the model or harness name is the durable subject.
- Use placeholder paths like `<repo>` and `<task>` in reusable commands.
- Keep bullets capitalized and parallel.
- Do not use em dashes.
- Do not use semicolons to join what should be separate sentences. Use commas, periods, parentheses, or the word "to" instead.
- Do not duplicate a rule across root and references. Put it in one owner and point to it from the loading map.

## Before finishing

- Verify every reference named in `SKILL.md` exists.
- Verify every file in `references/` is a model-specific spawn reference.
- Confirm `metadata.version` in `SKILL.md` was bumped if and only if behavior changed.
