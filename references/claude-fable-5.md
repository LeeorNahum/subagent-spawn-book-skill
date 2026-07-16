# Claude Fable 5

## Spawn

Claude Code CLI is Claude Fable 5's native harness. Use high effort for architecture judgment, multi-constraint review, long synthesis, and other reasoning-heavy delegated work. Use medium effort for frontend and visual deliverables. Low is also acceptable for visual work. Visual quality is largely baked into the weights, so higher effort does not reliably improve pixel-level output.

```text
claude -p --model "claude-fable-5" --effort high --dangerously-skip-permissions --name "<session name>" "<task prompt>"
```

If the current harness is Claude Code and exposes internal Claude Fable 5 subagent tooling, use that instead of the command.
