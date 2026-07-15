# GPT-5.6 Terra

## Spawn

Codex CLI is GPT-5.6 Terra's native harness. Use low reasoning for quick research and fact-finding errands. Use medium reasoning for browser-use tasks.

```text
codex exec -C "<repo>" --ignore-user-config --dangerously-bypass-approvals-and-sandbox --model "gpt-5.6-terra" -c model_reasoning_effort="low" "<task prompt>"
```

If the current harness exposes browser-use tools and internal GPT-5.6 Terra subagent tooling, use that internal tooling instead of the command.

## Notes

Browser use requires browser tools in the spawned session. Before assigning a browser-use task, confirm that those tools are available. If they are absent, report the missing capability instead of treating a shell-only check as browser verification.

Use the bypass shape only in a trusted local environment. It avoids non-interactive sandbox write denials that can otherwise stop simple file edits.

If running outside a Git repo, either use `-C "<trusted-repo>"` or pass `--skip-git-repo-check` only when the target directory is intentionally not a repo.
