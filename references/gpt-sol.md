# GPT Sol

## Spawn

Codex CLI is GPT Sol's native harness. Use low reasoning for a lookup or a check with a fixed answer. Use medium for a small change that has to be right. Effort values are low, medium, high, xhigh, max, and ultra.

```text
codex exec -C "<repo>" --dangerously-bypass-approvals-and-sandbox --model "gpt-6-sol" -c model_reasoning_effort="low" -o "<result file>" "<task prompt>" < /dev/null
```

Codex has no alias without a version, so the identifier above is the current one and changes when Codex does.

Start it as a background command and read the final message from the `-o` file. If the current harness is Codex and exposes internal Sol subagent tooling, use that instead of the command.

## Resume

The session id is printed on the run's output. Resume with a reply and the session keeps everything it read and said:

```text
codex exec resume <session id> --dangerously-bypass-approvals-and-sandbox -o "<result file>" "<reply>" < /dev/null
```

## Notes

Keep `< /dev/null`. With an open stdin the command waits and never starts. From PowerShell, use `$null | codex exec ...` instead.

Use the bypass shape only in a trusted local environment. If running outside a Git repo, either use `-C "<trusted-repo>"` or pass `--skip-git-repo-check` only when the target directory is intentionally not a repo.
