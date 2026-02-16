# CLAUDE.md - Faith Debates System

## Project Overview

This is an automated AI-powered theological/spiritual debate system. Users provide a debate topic, and Claude Code agent teams:
1. Research both positions in parallel
2. Generate position/persona files
3. Conduct a structured debate
4. Evaluate and score the debate
5. Create an accessible summary

## Key Concept: Dynamic Personas

Unlike the calv-v-arm repo (hardcoded Calvin vs Arminius), this system:
- Accepts ANY debate topic
- Researchers generate position files dynamically
- Debaters adopt personas from those generated files

## Repository Structure

```
faith-debates/
├── CLAUDE.md                  # This file
├── README.md                  # User documentation
├── .claude/
│   ├── agents/                # Agent definitions
│   │   ├── researcher-position-a.md
│   │   ├── researcher-position-b.md
│   │   ├── debater-a.md
│   │   ├── debater-b.md
│   │   ├── moderator.md
│   │   ├── judge.md
│   │   └── summarizer.md
│   ├── teams/
│   │   ├── debate.json        # Full debate team
│   │   └── research.json      # Research team
│   └── skills/
│       └── create-debate.md   # "Create a debate" skill
├── bible/bsb_usfm/            # Berean Standard Bible (USFM)
├── debates/
│   └── {topic-slug}/          # Auto-created per debate
│       ├── position-a.md      # Generated: first position
│       ├── position-b.md      # Generated: second position
│       ├── moderator-intro.md # Generated: topic intro
│       ├── {transcripts}      # Generated: debate files
│       ├── judgment.md        # Generated: judge evaluation
│       └── summary.md         # Generated: accessible summary
└── docs/
    ├── plans/                 # Implementation plans
    └── AGENT_TEAMS_SETUP.md   # Setup instructions
```

## Debate Flow

### Phase 1: Research (Parallel)
- Researcher A and Researcher B work simultaneously
- Each researches one side of the topic
- They coordinate via messaging to avoid overlap
- Output: `position-a.md`, `position-b.md`

### Phase 2: Debate (Structured)
1. Opening statements (3-5 paragraphs each)
2. First rebuttals (4-6 paragraphs each)
3. Second rebuttals (3-5 paragraphs each, optional)
4. Cross-examination (3 questions per side)
5. Closing statements (3-5 paragraphs each)

### Phase 3: Evaluation
- Judge scores debate (100-point system)
- Summarizer creates accessible summary

## Agent System

### Researcher A / Researcher B
- Research one side of the debate
- Generate position file with:
  - Position name
  - Core beliefs/arguments
  - Key scriptures
  - Debate style guidance

### Debater A / Debater B
- Load persona from position file
- Debate according to that persona
- Reference Bible at `bible/bsb_usfm/`
- Maintain charitable discourse

### Moderator
- Ensure fair conduct
- Manage debate flow
- Enforce structure

### Judge
- Score both debaters
- Provide detailed analysis
- Write judgment.md

### Summarizer
- Create summary.md
- Explain terms simply
- Maintain neutrality

## Common Tasks

### Starting a Debate

User provides topic, Claude Code:
1. Creates debates/{topic}/ folder
2. Spawns agent team
3. Coordinates workflow

### Reading Debate Files

```bash
ls debates/{topic-name}/
cat debates/{topic-name}/summary.md
```

## Team Configuration

Teams are defined in `.claude/teams/*.json`:
- `debate.json` - Full team with all agents
- `research.json` - Research-only team

## Environment Requirements

```bash
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS="1"
```

## Testing

Run a test debate:
```
Create a debate on a simple topic like "Is coffee good for you?"
```

## Project-Specific Notes

- This is a **generic debate system** - not tied to any specific theology
- Position files are **auto-generated** by researchers
- All agents use **direct messaging** for coordination
- Team lead handles orchestration; teammates handle content
