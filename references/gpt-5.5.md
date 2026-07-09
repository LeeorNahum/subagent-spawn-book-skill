# GPT-5.5

## Spawn

Codex CLI is GPT-5.5's native harness. Use medium.

```text
codex exec -C "<repo>" --ignore-user-config --dangerously-bypass-approvals-and-sandbox --model "gpt-5.5" "<task prompt>"
```

If the current harness is Codex and exposes internal GPT-5.5 subagent tooling, use that instead of the command.

## Notes

Use the bypass shape only in a trusted local environment. It avoids non-interactive sandbox write denials that can otherwise stop simple file edits.

If running outside a Git repo, either use `-C "<trusted-repo>"` or pass `--skip-git-repo-check` only when the target directory is intentionally not a repo.
