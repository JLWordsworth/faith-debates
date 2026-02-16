# Faith Debates

An automated AI-powered theological and spiritual debate system using Claude Code experimental agent teams.

## Quick Start

1. **Enable experimental agent teams:**
   ```bash
   export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS="1"
   ```

2. **Create a debate:**
   ```
   Create a debate on whether Christians can lose their salvation
   ```

## Example Debates

Try these topics:
- "Can Christians lose their salvation?"
- "Are spiritual gifts for today?"
- "Faith vs. Works in salvation"
- "Free will vs. God's sovereignty"
- "Pretribulation vs. Amillennialism"

## How It Works

```
User topic -> Research (parallel) -> Position files -> Debate -> Judge -> Summary
     |              |                    |              |        |         |
  One command    2 agents          2 files         2 agents  1 agent  1 agent
```

### Phase 1: Research (Parallel)
- Researcher A and Researcher B work simultaneously
- Each researches one side of the topic
- Generate position-a.md and position-b.md

### Phase 2: Debate
1. Opening statements
2. First rebuttals
3. Second rebuttals (optional)
4. Cross-examination
5. Closing statements

### Phase 3: Evaluation
- Judge scores both debaters (100-point system)
- Summarizer creates accessible summary

## Output Structure

Each debate creates a folder under `debates/`:

```
debates/{topic}/
├── position-a.md          # First position (researcher-generated)
├── position-b.md          # Second position (researcher-generated)
├── moderator-intro.md     # Topic introduction
├── opening-a.md           # Debater A opening
├── opening-b.md           # Debater B opening
├── rebuttal-1-a.md        # Debater A first rebuttal
├── rebuttal-1-b.md        # Debater B first rebuttal
├── cross-exam-a.md        # Debater A questions
├── cross-exam-b.md        # Debater B questions
├── xr-responses-a.md      # Debater A responses
├── xr-responses-b.md      # Debater B responses
├── closing-a.md           # Debater A closing
├── closing-b.md           # Debater B closing
├── judgment.md            # Judge's evaluation
└── summary.md             # Accessible summary
```

## Documentation

- [Setup Guide](docs/AGENT_TEAMS_SETUP.md) - Enable agent teams
- [Usage Guide](docs/USAGE.md) - Detailed usage instructions
- [CLAUDE.md](CLAUDE.md) - Project documentation for Claude

## Architecture

- **7 specialized agents:** Researcher A, Researcher B, Moderator, Debater A, Debater B, Judge, Summarizer
- **Dynamic personas:** Position files generated per topic, not hardcoded
- **Agent teams:** Uses Claude Code experimental feature for parallel work

## License

MIT
