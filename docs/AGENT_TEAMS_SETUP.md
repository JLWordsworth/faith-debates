# Agent Teams Setup

This project requires Claude Code's experimental agent teams feature.

## Enable Agent Teams

Add to your environment:

```bash
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS="1"
```

Or add to `~/.claude/settings.json`:

```json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

## Verify It's Working

Start Claude Code and check that agent teams are enabled:

```
You: Create an agent team to test
Claude: [Should create teammates without error]
```

## Display Modes

### In-Process (Default)
All teammates run in your main terminal. Use Shift+Up/Down to cycle through teammates.

### Split Panes
Each teammate gets its own pane. Requires tmux or iTerm2.

Add to `~/.claude/settings.json`:
```json
{
  "teammateMode": "tmux"
}
```

## Troubleshooting

### Teammates not appearing
- Verify environment variable is set: `echo $CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS`
- Try restarting Claude Code

### Too many permission prompts
- Pre-approve common operations in your permission settings

See [Claude Code documentation](https://code.claude.com/docs/agent-teams) for more details.
