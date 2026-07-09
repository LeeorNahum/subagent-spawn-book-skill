# Maintenance Contract: subagent-spawn-book

This file is for agents editing the skill. Keep maintainer rules here, not in `SKILL.md`.

## File Roles

| File | Role |
| --- | --- |
| `SKILL.md` | Trigger, universal spawn rules, model selection, reference-loading map |
| `references/<model>.md` | Exact spawn command for that model |
| `README.md` | Short human skim layer |

## Ownership Rules

- `SKILL.md` owns broad spawn policy: session naming, model selection, and the list of model references.
- `SKILL.md` owns the current model descriptions and what each model is good for.
- `references/` owns only model-specific spawn mechanics: native harness identity, current-harness internal tooling when applicable, command shape, default mode, and tested command notes.
- Put exact commands, CLI flags, current-harness tool names, setup notes, and model-specific failure modes in the model reference file.
- When adding a model, document how to recognize whether the current harness is that model's own harness. If it is, use current-harness internal tooling. If it is not, spawn through the model's native harness using the command in the reference.
- When adding a model that is not listed yet, first identify its native owner or primary harness, then document that harness in the model reference.
- Document all-permissions mode for each spawn path unless that path is already known to run without getting stuck.
- Add one reference per model family, model role, or harness-specific model path when spawn mechanics differ materially.
- Do not bury a current model favorite in the skill description. The description must stay stable as model rankings change.
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

Reference filenames use the model's canonical public name normalized only as much as needed for a readable lowercase filename. Keep meaningful model punctuation such as decimal points when it is part of the model name. Use hyphens for spaces and word separators, not to rewrite the model's version number.

## Editing Rules

- Version `SKILL.md` at a meaningful checkpoint. During initial creation or an active review loop before commit, keep the draft's version stable unless the user is explicitly preparing the publishable version.
- Keep every frontmatter string quoted.
- Keep examples generic unless the model or harness name is the durable subject.
- Use placeholder paths like `<repo>` and `<task>` in reusable commands.
- Keep bullets capitalized and parallel.
- Do not use em dashes.
- Do not duplicate a rule across root and references. Put it in one owner and point to it from the loading map.
- Verify every reference named in `SKILL.md` exists.
- Verify every file in `references/` is a model-specific spawn reference.
