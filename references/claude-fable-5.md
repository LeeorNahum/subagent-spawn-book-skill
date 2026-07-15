# Claude Fable 5

## Spawn

Claude Code CLI is Claude Fable 5's native harness. Use medium effort. Low is also acceptable. Its visual quality is baked into the weights rather than reached through long reasoning, so higher effort does not improve the output.

```text
claude -p --model "claude-fable-5" --effort medium --dangerously-skip-permissions --name "<session name>" "<task prompt>"
```

If the current harness is Claude Code and exposes internal Claude Fable 5 subagent tooling, use that instead of the command.
