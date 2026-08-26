# GPT-5.6 Sol

## Spawn

Codex CLI is GPT-5.6 Sol's native harness. Use high reasoning for production-quality implementation, testing, verification, and literal conformance deliverables. Medium is enough for routine conformance checks.

```text
codex exec -C "<repo>" --ignore-user-config --dangerously-bypass-approvals-and-sandbox --model "gpt-5.6-sol" -c model_reasoning_effort="high" -o "<result file>" "<task prompt>" < /dev/null
```

If the current harness is Codex and exposes internal GPT-5.6 Sol subagent tooling, use that instead of the command.

## Notes

Close standard input. `codex exec` reads a piped stdin to its end and appends it to the prompt, so a spawn whose stdin is an open pipe waits and never starts. From a POSIX shell append `< /dev/null`. From PowerShell pipe nothing in with `$null | codex exec ...`.

Read the result from the file named by `-o`. It holds the final message and survives a run that is killed or times out.

Use the bypass shape only in a trusted local environment. It avoids non-interactive sandbox write denials that can otherwise stop simple file edits.

If running outside a Git repo, either use `-C "<trusted-repo>"` or pass `--skip-git-repo-check` only when the target directory is intentionally not a repo.
