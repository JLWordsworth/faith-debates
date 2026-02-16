# Faith Debates

An automated AI-powered theological and spiritual debate system using Claude Code experimental agent teams.

## Quick Start

1. Enable experimental agent teams:
   ```bash
   export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS="1"
   ```

2. Create a debate:
   ```
   Create a debate on whether Christians can lose their salvation
   ```

## How It Works

1. User provides a debate topic
2. Two research agents work in parallel to research both positions
3. Position files are auto-generated
4. Debater agents adopt the researched personas
5. A structured debate proceeds (openings → rebuttals → cross-exam → closing)
6. Judge evaluates and scores the debate
7. Summarizer creates an accessible summary

## Repository Structure

```
faith-debates/
├── README.md              # This file
├── CLAUDE.md              # Project guidance
├── bible/bsb_usfm/        # Bible reference (USFM format)
├── debates/               # Debate transcripts (auto-created)
└── .claude/               # Agent and team configurations
```

See [docs/AGENT_TEAMS_SETUP.md](docs/AGENT_TEAMS_SETUP.md) for detailed setup instructions.

## License

MIT
