# Claude Opus

## Spawn

Claude Code CLI is Claude Opus's native harness, and the `opus` alias resolves to the latest Opus. Use medium effort for fleet workers running a well-specified role in parallel, for orchestrators that dispatch and validate, and for an adversarial critic with a clear goal. Use high effort for a review pass that changes the rules workers follow. Append `[1m]` to the alias when the worker must hold a very large ledger, transcript, or document set. Effort values are low, medium, high, xhigh, and max.

```text
claude -p --model opus --effort medium --dangerously-skip-permissions --name "<session name>" "<task prompt>"
```

If the current harness is Claude Code and exposes internal Claude Opus subagent tooling, use that instead of the command. In Claude Code, the Agent tool with `model: "opus"` is that tooling.

A `-p` session exits the moment its turn ends, and a subagent or background task it started does not keep it alive. There is no next turn for a notification to land in, so telling it to wait is not enough: tell it in the prompt to run every subagent in the foreground, as a tool call that returns, and never to background one. A session that replied "waiting on" something has stopped, and only a resume continues it.

## Resume

Run with `--output-format json` to get the session id, then resume with a reply and the session keeps everything it read and said:

```text
claude -p --resume <session id> --dangerously-skip-permissions "<reply>"
```

## Notes

When several Opus workers run the same role at once and their outputs will be compared, give every one the same effort. Raising one worker's effort and not the others makes the comparison unfair.

For a critic, put the goal, the actual files, and the numbered claims in the task, and tell it plainly that its job is to find what is wrong, not to validate.
