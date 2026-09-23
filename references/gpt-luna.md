# GPT Luna

## Spawn

Codex CLI is GPT Luna's native harness. Use low reasoning for bulk extraction, classification, and summarization. Use medium when the rubric has judgment in it. Effort values are low, medium, high, xhigh, and max.

```text
codex exec -C "<repo>" --ignore-user-config --dangerously-bypass-approvals-and-sandbox --model "gpt-6-luna" -c model_reasoning_effort="low" -o "<result file>" "<task prompt>" < /dev/null
```

Codex has no alias without a version, so the identifier above is the current one and changes when Codex does.

Start it as a background command and read the final message from the `-o` file. If the current harness is Codex and exposes internal Luna subagent tooling, use that instead of the command.

## Resume

The session id is printed on the run's output. Resume with a reply and the session keeps everything it read and said:

```text
codex exec resume <session id> --ignore-user-config --dangerously-bypass-approvals-and-sandbox -o "<result file>" "<reply>" < /dev/null
```

## Notes

Keep `< /dev/null`. With an open stdin the command waits and never starts. From PowerShell, use `$null | codex exec ...` instead.

Give it a fixed output shape in the prompt, since its value is volume, and read the output as data.
