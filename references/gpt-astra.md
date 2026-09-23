# GPT Astra

## Spawn

Codex CLI is GPT Astra's native harness. Use low reasoning for a clearly scoped task with a known target. Use medium when it has to find something or complete a multi-step task. Effort values are low, medium, high, xhigh, max, and ultra.

```text
codex exec -C "<repo>" --dangerously-bypass-approvals-and-sandbox --model "gpt-6-astra" -c model_reasoning_effort="low" -o "<result file>" "<task prompt>" < /dev/null
```

Codex has no alias without a version, so the identifier above is the current one and changes when Codex does.

Start it as a background command and read the final message from the `-o` file. If the current harness is Codex and exposes internal Astra subagent tooling, use that instead of the command.

## Resume

The session id is printed on the run's output. Resume with a reply and the session keeps everything it read and said:

```text
codex exec resume <session id> --dangerously-bypass-approvals-and-sandbox -o "<result file>" "<reply>" < /dev/null
```

## Notes

Keep `< /dev/null`. With an open stdin the command waits and never starts. From PowerShell, use `$null | codex exec ...` instead.

Browser and computer use come from the tools connected to the spawned session, such as the user's signed-in browser and desktop connection. Do not add `--ignore-user-config` when the task needs them, because that drops the user's connected tools. Before assigning such a task, confirm the tools are present. If they are absent, report the missing capability instead of treating a shell-only check as that evidence.

When the spawned session has the user's browser, tell it which tab or account to use and to leave other tabs alone. It has no memory of the calling session, so give it the full task each time.

Use the bypass shape only in a trusted local environment. If running outside a Git repo, either use `-C "<trusted-repo>"` or pass `--skip-git-repo-check` only when the target directory is intentionally not a repo.
