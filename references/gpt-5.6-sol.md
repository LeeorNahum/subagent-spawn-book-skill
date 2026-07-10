# GPT-5.6 Sol

## Spawn

Codex CLI is GPT-5.6 Sol's native harness. Use medium reasoning.

```text
codex exec -C "<repo>" --ignore-user-config --dangerously-bypass-approvals-and-sandbox --model "gpt-5.6-sol" -c model_reasoning_effort="medium" "<task prompt>"
```

If the current harness is Codex and exposes internal GPT-5.6 Sol subagent tooling, use that instead of the command.

## Notes

Use the bypass shape only in a trusted local environment. It avoids non-interactive sandbox write denials that can otherwise stop simple file edits.

If running outside a Git repo, either use `-C "<trusted-repo>"` or pass `--skip-git-repo-check` only when the target directory is intentionally not a repo.
