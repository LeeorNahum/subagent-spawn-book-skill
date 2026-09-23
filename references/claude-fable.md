# Claude Fable

## Spawn

Claude Code CLI is Claude Fable's native harness, and the `fable` alias resolves to the latest Fable. Use high effort for architecture judgment, multi-constraint review, long synthesis, and other reasoning-heavy delegated work. Use medium effort for frontend and visual deliverables. Low is also acceptable for visual work. Effort values are low, medium, high, xhigh, and max.

```text
claude -p --model fable --effort high --dangerously-skip-permissions --name "<session name>" "<task prompt>"
```

If the current harness is Claude Code and exposes internal Claude Fable subagent tooling, use that instead of the command.

## Resume

Run with `--output-format json` to get the session id, then resume with a reply and the session keeps everything it read and said:

```text
claude -p --resume <session id> --dangerously-skip-permissions "<reply>"
```
