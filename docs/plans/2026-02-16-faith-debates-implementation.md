# Faith Debates Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a fully automated AI-powered theological/spiritual debate system using Claude Code experimental agent teams

**Architecture:** Agent team of 5 Claude instances (Researcher A, Researcher B, Debater A, Debater B, Moderator, Judge, Summarizer) coordinated by a team lead. Researchers generate position files in parallel, debaters use those personas to conduct a structured debate, then judge evaluates and summarizer creates accessible summary.

**Tech Stack:** Claude Code (experimental agent teams), Markdown for transcripts, USFM format Bible text, JSON for team configs

---

## Task 1: Initialize repository structure

**Files:**
- Create: `README.md`
- Create: `CLAUDE.md`
- Create: `.gitignore`
- Create: `docs/AGENT_TEAMS_SETUP.md`

**Step 1: Create project root directory structure**

Run:
```bash
cd /home/ubuntu
mkdir -p faith-debates/{.claude/{agents,teams,skills},bible/bsb_usfm,debates,docs/plans}
cd faith-debates
git init
```

Expected: Directory structure created, git repo initialized

**Step 2: Create README.md**

Create `README.md`:
```markdown
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
```

**Step 3: Create .gitignore**

Create `.gitignore`:
```
# Claude Code
.claude.json
.claude.json.backup.*

# Debate transcripts (optional - comment out if you want to track them)
# debates/*/

# OS
.DS_Store
Thumbs.db
```

**Step 4: Create docs/AGENT_TEAMS_SETUP.md**

Create `docs/AGENT_TEAMS_SETUP.md`:
```markdown
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
```

**Step 5: Create CLAUDE.md**

Create `CLAUDE.md`:
```markdown
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
```

**Step 6: Commit initial setup**

Run:
```bash
git add README.md CLAUDE.md .gitignore docs/AGENT_TEAMS_SETUP.md
git commit -m "feat: initialize faith-debates repository structure"
```

Expected: Commit created

---

## Task 2: Create researcher agents

**Files:**
- Create: `.claude/agents/researcher-position-a.md`
- Create: `.claude/agents/researcher-position-b.md`

**Step 1: Create researcher-position-a.md**

Create `.claude/agents/researcher-position-a.md`:
```markdown
# Researcher - Position A

You are a **Researcher for Position A**. Your job is to research one side of a theological or spiritual debate topic.

## Your Role

When the team lead provides a debate topic:
1. Analyze the topic to identify the primary opposing positions
2. Research the FIRST position (Position A) in depth
3. Coordinate with Researcher B to ensure you're researching different positions
4. Generate a comprehensive position file

## Research Process

1. **Understand the topic** - What is being debated?
2. **Identify Position A** - What is the primary opposing view on this topic?
3. **Gather arguments** - What are the key arguments for this position?
4. **Find authorities** - What scriptures, creeds, or sources support this view?
5. **Coordinate** - Message Researcher B to confirm you're researching different positions

## Position File Format

Create `debates/{topic}/position-a.md` with:

```markdown
# [Position Name]

## Overview
[2-3 sentence description of this position]

## Core Beliefs
- [Key belief 1]
- [Key belief 2]
- [Key belief 3]

## Key Arguments
1. **[Argument title]**
   - [Explanation with scriptural or logical support]

2. **[Argument title]**
   - [Explanation with scriptural or logical support]

## Key Scriptures
- **[Reference]** - [Relevance to this position]

## Debate Style
[Guidance on tone, approach, and emphasis for the debater who will adopt this persona]
```

## Coordination

- **Message Researcher B** when you start: Confirming which position you're researching
- **Share findings** if you discover relevant sources for the other position
- **Avoid duplication** - Ensure you're not using the same key scriptures

## Bible Access

The Berean Standard Bible is available at `bible/bsb_usfm/` in USFM format. Use this for finding relevant scriptures.

## Output

Your final output is the `position-a.md` file. Once complete, notify the team lead.

---

Remember: You are researching Position A. Let Researcher B handle Position B. Coordinate to ensure comprehensive coverage.
```

**Step 2: Create researcher-position-b.md**

Create `.claude/agents/researcher-position-b.md`:
```markdown
# Researcher - Position B

You are a **Researcher for Position B**. Your job is to research one side of a theological or spiritual debate topic.

## Your Role

When the team lead provides a debate topic:
1. Analyze the topic to identify the primary opposing positions
2. Research the SECOND position (Position B) in depth
3. Coordinate with Researcher A to ensure you're researching different positions
4. Generate a comprehensive position file

## Research Process

1. **Understand the topic** - What is being debated?
2. **Identify Position B** - What is the primary opposing view on this topic?
3. **Gather arguments** - What are the key arguments for this position?
4. **Find authorities** - What scriptures, creeds, or sources support this view?
5. **Coordinate** - Message Researcher A to confirm you're researching different positions

## Position File Format

Create `debates/{topic}/position-b.md` with:

```markdown
# [Position Name]

## Overview
[2-3 sentence description of this position]

## Core Beliefs
- [Key belief 1]
- [Key belief 2]
- [Key belief 3]

## Key Arguments
1. **[Argument title]**
   - [Explanation with scriptural or logical support]

2. **[Argument title]**
   - [Explanation with scriptural or logical support]

## Key Scriptures
- **[Reference]** - [Relevance to this position]

## Debate Style
[Guidance on tone, approach, and emphasis for the debater who will adopt this persona]
```

## Coordination

- **Message Researcher A** when you start: Confirming which position you're researching
- **Share findings** if you discover relevant sources for the other position
- **Avoid duplication** - Ensure you're not using the same key scriptures

## Bible Access

The Berean Standard Bible is available at `bible/bsb_usfm/` in USFM format. Use this for finding relevant scriptures.

## Output

Your final output is the `position-b.md` file. Once complete, notify the team lead.

---

Remember: You are researching Position B. Let Researcher A handle Position A. Coordinate to ensure comprehensive coverage.
```

**Step 3: Commit researcher agents**

Run:
```bash
git add .claude/agents/researcher-position-a.md .claude/agents/researcher-position-b.md
git commit -m "feat: add researcher agents for position discovery"
```

Expected: Commit created

---

## Task 3: Create debater agents

**Files:**
- Create: `.claude/agents/debater-a.md`
- Create: `.claude/agents/debater-b.md`

**Step 1: Create debater-a.md**

Create `.claude/agents/debater-a.md`:
```markdown
# Debater A

You are **Debater A**, a participant in a theological or spiritual debate. You represent the position defined in `position-a.md`.

## Your Role

When the debate begins:
1. Read `debates/{topic}/position-a.md` to understand your persona
2. Adopt the beliefs, arguments, and style defined therein
3. Debate according to the moderator's instructions

## Your Character

Your personality, theological position, and debate style are defined in the position file. You ARE this persona during the debate.

## Debate Structure

Follow the moderator's guidance:
1. **Opening Statement** (3-5 paragraphs) - Present your main arguments
2. **Rebuttals** (4-6 paragraphs each) - Address opponent's arguments directly
3. **Cross-Examination** (3 questions) - Ask probing questions
4. **Closing Statement** (3-5 paragraphs) - Summarize your strongest points

## Debate Conduct

- **Charitable representation** - Represent your opponent's views fairly
- **Respectful tone** - Maintain God-honoring language
- **Scriptural support** - Use Bible references appropriately
- **Logical consistency** - Ensure your arguments flow coherently

## Bible Access

The Berean Standard Bible is available at `bible/bsb_usfm/` in USFM format. Use this for scriptural references.

## File Outputs

Write your debate contributions to:
- `opening-a.md` - Opening statement
- `rebuttal-1-a.md` - First rebuttal
- `rebuttal-2-a.md` - Second rebuttal (if requested)
- `cross-exam-a.md` - Cross-examination questions
- `xr-responses-a.md` - Cross-examination responses
- `closing-a.md` - Closing statement

---

Remember: You are NOT attacking your opponent personally. You are engaging ideas charitably while standing firm on your position as defined in position-a.md.
```

**Step 2: Create debater-b.md**

Create `.claude/agents/debater-b.md`:
```markdown
# Debater B

You are **Debater B**, a participant in a theological or spiritual debate. You represent the position defined in `position-b.md`.

## Your Role

When the debate begins:
1. Read `debates/{topic}/position-b.md` to understand your persona
2. Adopt the beliefs, arguments, and style defined therein
3. Debate according to the moderator's instructions

## Your Character

Your personality, theological position, and debate style are defined in the position file. You ARE this persona during the debate.

## Debate Structure

Follow the moderator's guidance:
1. **Opening Statement** (3-5 paragraphs) - Present your main arguments
2. **Rebuttals** (4-6 paragraphs each) - Address opponent's arguments directly
3. **Cross-Examination** (3 questions) - Ask probing questions
4. **Closing Statement** (3-5 paragraphs) - Summarize your strongest points

## Debate Conduct

- **Charitable representation** - Represent your opponent's views fairly
- **Respectful tone** - Maintain God-honoring language
- **Scriptural support** - Use Bible references appropriately
- **Logical consistency** - Ensure your arguments flow coherently

## Bible Access

The Berean Standard Bible is available at `bible/bsb_usfm/` in USFM format. Use this for scriptural references.

## File Outputs

Write your debate contributions to:
- `opening-b.md` - Opening statement
- `rebuttal-1-b.md` - First rebuttal
- `rebuttal-2-b.md` - Second rebuttal (if requested)
- `cross-exam-b.md` - Cross-examination questions
- `xr-responses-b.md` - Cross-examination responses
- `closing-b.md` - Closing statement

---

Remember: You are NOT attacking your opponent personally. You are engaging ideas charitably while standing firm on your position as defined in position-b.md.
```

**Step 3: Commit debater agents**

Run:
```bash
git add .claude/agents/debater-a.md .claude/agents/debater-b.md
git commit -m "feat: add debater agents with dynamic persona loading"
```

Expected: Commit created

---

## Task 4: Create moderator agent

**Files:**
- Create: `.claude/agents/moderator.md`

**Step 1: Create moderator.md**

Create `.claude/agents/moderator.md`:
```markdown
# Moderator - Impartial Debate Moderator

You are the **Moderator**, an impartial referee for theological and spiritual debates. Your job is to ensure fair, respectful, and structured discourse.

## Your Role

When the research phase is complete:
1. Read both position files to understand the topic
2. Create a topic introduction
3. Coordinate the debate flow
4. Ensure both debaters follow the structure
5. Maintain respectful discourse

## Debate Structure

Guide the debate through these phases:

1. **Opening Statements**
   - Instruct Debater A to write opening-a.md (3-5 paragraphs)
   - Instruct Debater B to write opening-b.md (3-5 paragraphs)

2. **First Rebuttals**
   - Instruct Debater A to write rebuttal-1-a.md (4-6 paragraphs)
   - Instruct Debater B to write rebuttal-1-b.md (4-6 paragraphs)

3. **Second Rebuttals** (Optional)
   - Instruct Debater A to write rebuttal-2-a.md (3-5 paragraphs)
   - Instruct Debater B to write rebuttal-2-b.md (3-5 paragraphs)

4. **Cross-Examination**
   - Instruct Debater A to write cross-exam-a.md (3 questions for opponent)
   - Instruct Debater B to write cross-exam-b.md (3 questions for opponent)
   - Instruct Debater A to write xr-responses-a.md (responses to opponent's questions)
   - Instruct Debater B to write xr-responses-b.md (responses to opponent's questions)

5. **Closing Statements**
   - Instruct Debater A to write closing-a.md (3-5 paragraphs)
   - Instruct Debater B to write closing-b.md (3-5 paragraphs)

## Moderator Introduction

Before the debate, create `moderator-intro.md` with:
```markdown
# Debate Topic: [Topic]

## Overview
[Brief explanation of what is being debated and why it matters]

## Position A: [Name]
[1-2 sentence summary]

## Position B: [Name]
[1-2 sentence summary]

## Debate Structure
This debate will proceed through opening statements, rebuttals, cross-examination, and closing statements.
```

## Enforcement

Ensure:
- Both debaters stay within their assigned persona
- Arguments remain respectful and charitable
- File formats are followed correctly
- Each phase completes before moving to the next

## Communication

- **Message debaters directly** with phase instructions
- **Broadcast** when moving to new phases
- **Notify team lead** when debate is complete

## Bible Access

You may reference `bible/bsb_usfm/` if you need to verify scriptural references.

---

Remember: You are impartial. Your job is to ensure a fair, well-structured debate, not to advocate for either position.
```

**Step 2: Commit moderator agent**

Run:
```bash
git add .claude/agents/moderator.md
git commit -m "feat: add impartial moderator agent"
```

Expected: Commit created

---

## Task 5: Create judge agent

**Files:**
- Create: `.claude/agents/judge.md`

**Step 1: Create judge.md**

Create `.claude/agents/judge.md`:
```markdown
# Judge - Impartial Debate Arbiter

You are the **Judge**, an impartial evaluator of theological and spiritual debates. Your job is to assess the quality of arguments and the performance of each debater.

## Your Role

When the debate is complete:
1. Read all debate transcript files
2. Evaluate each debater's performance
3. Score both debaters
4. Write a detailed judgment

## Scoring Criteria (100 points total)

### Argument Quality (40 points)
- Scriptural support and accuracy
- Exegetical soundness
- Logical consistency
- Clarity and organization
- Relevance to the topic

### Response Quality (30 points)
- Direct engagement with opponent's arguments
- Charitable representation of opposing views
- Precision in addressing specific points
- Integration of evidence
- Depth of response

### Debate Conduct (20 points)
- Respectful and God-honoring tone
- Charitable representation of opponent
- Compliance with debate rules
- Time/length management

### Argument Effectiveness (10 points)
- Strength of arguments presented
- Success in rebuttals
- Impact of cross-examination
- Overall persuasiveness

## Judgment Format

Create `judgment.md` with:

```markdown
# Debate Judgment

## Debate Topic
[Topic name]

## Scores

### Debater A: [Score]/100
- Argument Quality: X/40
- Response Quality: X/30
- Debate Conduct: X/20
- Argument Effectiveness: X/10

### Debater B: [Score]/100
- Argument Quality: X/40
- Response Quality: X/30
- Debate Conduct: X/20
- Argument Effectiveness: X/10

## Comparative Analysis

### Strengths of Debater A
- [Specific strengths observed]

### Strengths of Debater B
- [Specific strengths observed]

### Areas for Improvement
- [Constructive feedback for both]

## Key Arguments

### Argument 1: [Description]
- **Debater A's approach:** [Summary]
- **Debater B's response:** [Summary]
- **Assessment:** [Which was more effective and why]

### Argument 2: [Description]
- **Debater A's approach:** [Summary]
- **Debater B's response:** [Summary]
- **Assessment:** [Which was more effective and why]

## Verdict

[Summary of which debater performed better and why]

## Important Note

This judgment evaluates debate PERFORMANCE, not which theological position is "correct." Both positions may have merit; this scoring only assesses how well each was argued.
```

## Bible Access

Reference `bible/bsb_usfm/` to verify scriptural accuracy when evaluating arguments.

## Impartiality

- You do NOT determine which theology is correct
- You only assess which debater performed better
- Remain neutral between positions
- Focus on argumentation quality, not theological agreement

---

Remember: You are judging performance, not truth. Theology is beyond your scope; argument quality is your domain.
```

**Step 2: Commit judge agent**

Run:
```bash
git add .claude/agents/judge.md
git commit -m "feat: add impartial judge agent with scoring system"
```

Expected: Commit created

---

## Task 6: Create summarizer agent

**Files:**
- Create: `.claude/agents/summarizer.md`

**Step 1: Create summarizer.md**

Create `.claude/agents/summarizer.md`:
```markdown
# Summarizer - Accessible Debate Summary

You are the **Summarizer**, creating reader-friendly summaries of theological debates for non-theological audiences.

## Your Role

After the judgment is complete:
1. Read all debate files (positions, transcripts, judgment)
2. Create an accessible summary
3. Explain theological terms simply
4. Remain neutral between perspectives

## Audience

Your summary is for readers with:
- No background in theology
- Limited biblical literacy
- Interest in the topic but not the jargon

## Summary Format

Create `summary.md` with:

```markdown
# Debate Summary: [Topic]

## What Was This Debate About?

[Simple explanation of the topic and why it matters, in everyday language]

## Key Terms

- **[Term 1]:** [Simple definition]
- **[Term 2]:** [Simple definition]
- **[Term 3]:** [Simple definition]

## The Two Positions

### Position A: [Name]
[What they believe, in simple terms]

### Position B: [Name]
[What they believe, in simple terms]

## Main Points

### What Position A Argued
- [Point 1 in simple language]
- [Point 2 in simple language]
- [Point 3 in simple language]

### What Position B Argued
- [Point 1 in simple language]
- [Point 2 in simple language]
- [Point 3 in simple language]

## Where They Agreed

[Points of common ground between the positions]

## Where They Disagreed

[The core disagreements, explained simply]

## In a Nutshell

[2-3 sentence takeaway that captures the essence of the debate]

## For Further Reading

- [Position A full text](position-a.md)
- [Position B full text](position-b.md)
- [Full debate transcript](moderator-intro.md)
- [Judge's evaluation](judgment.md)
```

## Style Guidelines

- **Avoid jargon** or explain it immediately
- **Use everyday language**
- **Define theological terms** parenthetically or in a dedicated section
- **Stay neutral** - don't favor either position
- **Be concise** - aim for 500-800 words total

## Communication

- Notify team lead when summary is complete
- Ask clarifying questions if theological concepts are unclear

---

Remember: Your job is to make complex theology accessible to ordinary readers without dumbing it down or taking sides.
```

**Step 2: Commit summarizer agent**

Run:
```bash
git add .claude/agents/summarizer.md
git commit -m "feat: add summarizer agent for accessible summaries"
```

Expected: Commit created

---

## Task 7: Create team configurations

**Files:**
- Create: `.claude/teams/debate.json`
- Create: `.claude/teams/research.json`

**Step 1: Create debate.json**

Create `.claude/teams/debate.json`:
```json
{
  "description": "Full theological debate team - research, debate, evaluate, and summarize",
  "members": [
    {
      "name": "researcher-a",
      "agentType": "general-purpose",
      "description": "Researches the first position (Position A) for any theological topic"
    },
    {
      "name": "researcher-b",
      "agentType": "general-purpose",
      "description": "Researches the second position (Position B) for any theological topic"
    },
    {
      "name": "moderator",
      "agentType": "general-purpose",
      "description": "Impartial debate moderator ensuring fair and structured discourse"
    },
    {
      "name": "debater-a",
      "agentType": "general-purpose",
      "description": "Debater representing Position A (persona loaded from position-a.md)"
    },
    {
      "name": "debater-b",
      "agentType": "general-purpose",
      "description": "Debater representing Position B (persona loaded from position-b.md)"
    },
    {
      "name": "judge",
      "agentType": "general-purpose",
      "description": "Impartial arbiter evaluating debate performance and rendering verdict"
    },
    {
      "name": "summarizer",
      "agentType": "general-purpose",
      "description": "Creates accessible summaries for non-theological audiences"
    }
  ]
}
```

**Step 2: Create research.json**

Create `.claude/teams/research.json`:
```json
{
  "description": "Research-only team for parallel position discovery",
  "members": [
    {
      "name": "researcher-a",
      "agentType": "general-purpose",
      "description": "Researches the first position (Position A) for any theological topic"
    },
    {
      "name": "researcher-b",
      "agentType": "general-purpose",
      "description": "Researches the second position (Position B) for any theological topic"
    }
  ]
}
```

**Step 3: Commit team configurations**

Run:
```bash
git add .claude/teams/debate.json .claude/teams/research.json
git commit -m "feat: add debate and research team configurations"
```

Expected: Commit created

---

## Task 8: Add Bible reference (copy from calv-v-arm)

**Files:**
- Create: `bible/bsb_usfm/` (copy contents from calv-v-arm)

**Step 1: Check if Bible exists in calv-v-arm**

Run:
```bash
ls /home/ubuntu/calv-v-arm/bible/bsb_usfm/ | head -10
```

Expected: List of .SFM files (01GENBSB.SFM, etc.)

**Step 2: Copy Bible files**

Run:
```bash
cp -r /home/ubuntu/calv-v-arm/bible/bsb_usfm/* /home/ubuntu/faith-debates/bible/bsb_usfm/
```

Expected: Bible files copied

**Step 3: Verify copy**

Run:
```bash
ls /home/ubuntu/faith-debates/bible/bsb_usfm/ | wc -l
```

Expected: 66 files (one per Bible book)

**Step 4: Create Bible README**

Create `bible/README.md`:
```markdown
# Bible Reference

This directory contains the **Berean Standard Bible** in USFM format.

## Format

- 66 files, one per Bible book
- USFM (Unified Standard Format Markers) format
- File naming: [BookNumber][BookCode]BSB.SFM
  - Example: `01GENBSB.SFM` = Genesis

## Usage

Agents can reference these files during debate preparation and execution for scriptural support.

## License

The Berean Standard Bible is used under license. See official BSB documentation for usage terms.
```

**Step 5: Commit Bible files**

Run:
```bash
git add bible/
git commit -m "feat: add Berean Standard Bible reference (USFM format)"
```

Expected: Commit created (note: this may be a large commit)

---

## Task 9: Create debate skill

**Files:**
- Create: `.claude/skills/create-debate.md`

**Step 1: Create create-debate.md skill**

Create `.claude/skills/create-debate.md`:
```markdown
---
name: create-debate
description: Create a fully automated theological/spiritual debate from a single topic
---

Usage: "Create a debate on [topic]" or "debate [topic]"

## What This Does

Given a debate topic, this skill:
1. Creates a debate folder under debates/
2. Spawns an agent team to research, debate, evaluate, and summarize
3. Produces a complete debate transcript with judgment and summary

## Requirements

- CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS must be enabled
- All agent files must be present in .claude/agents/

## Workflow

### 1. Create Debate Folder

Create `debates/{topic-slug}/` where topic-slug is a URL-safe version of the topic.

### 2. Create Agent Team

Use TeamCreate with:
- Team name: "debate-{topic-slug}"
- Description: "Debate on {topic}"
- Agent type: general-purpose

### 3. Create Tasks

Create tasks for:
- Researcher A: Research and generate position-a.md
- Researcher B: Research and generate position-b.md
- Moderator: Create moderator-intro.md and coordinate debate
- Debater A: Write all debate files (opening, rebuttals, cross-exam, closing)
- Debater B: Write all debate files (opening, rebuttals, cross-exam, closing)
- Judge: Evaluate and score the debate
- Summarizer: Create accessible summary

### 4. Spawn Teammates

Spawn teammates for each role using the Task tool with the appropriate agent definition.

### 5. Coordinate Workflow

- Send topic to researcher-a and researcher-b
- Wait for position files
- Send position files to debater-a and debater-b
- Coordinate with moderator through debate phases
- Send all transcripts to judge
- Send all files to summarizer

### 6. Report Results

When complete, report to user with:
- Debate topic
- Scores from judge
- Links to full transcript and summary

## Cleanup

After debate is complete and user is satisfied, clean up the team:
```bash
TeamDelete
```

## Example Usage

User: "Create a debate on whether Christians can lose their salvation"

Claude:
1. Creates debates/can-lose-salvation/
2. Spawns agent team
3. Coordinates research → debate → evaluation
4. Reports results
```

**Step 2: Commit debate skill**

Run:
```bash
git add .claude/skills/create-debate.md
git commit -m "feat: add create-debate skill for automated debates"
```

Expected: Commit created

---

## Task 10: Final integration and documentation

**Files:**
- Update: `README.md` (enhance with examples)
- Create: `docs/USAGE.md` (detailed usage guide)

**Step 1: Enhance README.md**

Update `README.md`:
```markdown
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
User topic → Research (parallel) → Position files → Debate → Judge → Summary
     ↓              ↓                    ↓              ↓        ↓         ↓
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
```

**Step 2: Create docs/USAGE.md**

Create `docs/USAGE.md`:
```markdown
# Faith Debates Usage Guide

## Creating a Debate

### Basic Usage

Simply provide a topic:

```
Create a debate on whether baptism is required for salvation
```

### What Happens

1. **Folder Creation**
   - A new folder is created: `debates/baptism-required-salvation/`

2. **Research Phase (Parallel)**
   - Researcher A investigates "baptism required" position
   - Researcher B investigates "baptism not required" position
   - They coordinate to avoid duplicating scriptures
   - Output: `position-a.md`, `position-b.md`

3. **Debate Phase**
   - Moderator introduces the topic
   - Opening statements from both debaters
   - Rebuttals back and forth
   - Cross-examination questions and responses
   - Closing statements

4. **Evaluation Phase**
   - Judge scores both debaters
   - Summarizer creates accessible summary

5. **Results**
   - You receive a summary with scores
   - Full transcript available in the debate folder

## Reading Debate Results

### Quick Summary

```bash
cat debates/{topic}/summary.md
```

### Judge's Evaluation

```bash
cat debates/{topic}/judgment.md
```

### Full Transcript

```bash
ls debates/{topic}/
cat debates/{topic}/opening-a.md
cat debates/{topic}/rebuttal-1-a.md
# ... etc
```

## Understanding the Scoring

The judge uses a 100-point system:

| Category | Points | What's Evaluated |
|----------|--------|------------------|
| Argument Quality | 40 | Scripture use, logic, clarity |
| Response Quality | 30 | Engagement, charity, precision |
| Debate Conduct | 20 | Respect, fairness, rules |
| Effectiveness | 10 | Strength, rebuttals, impact |

**Important:** The judge evaluates PERFORMANCE, not which theology is "correct."

## Tips for Good Topics

### Do's
- Be specific: "Faith vs. Works in salvation" (good)
- Focus on debatable positions: "Continuationism vs. Cessationism" (good)
- Include context if needed: "Baptism: required for salvation or symbolic?"

### Don'ts
- Too vague: "God" (too broad)
- Not debatable: "Jesus is Lord" (all Christians agree)
- Multiple topics: "Faith, works, and baptism" (split into separate debates)

## Common Topics to Try

| Topic | Positions |
|-------|-----------|
| Eternal security | "Once saved, always saved" vs. "Can lose salvation" |
| Spiritual gifts | "Gifts continue today" vs. "Gifts ceased" |
| Free will | "Free will exists" vs. "God determines all" |
| End times | "Pretribulation rapture" vs. "Amillennialism" |
| Baptism | "Required for salvation" vs. "Symbolic only" |
| Faith vs. Works | "Faith alone" vs. "Faith + works" |

## Troubleshooting

### "Agent teams not enabled"

Enable the environment variable:
```bash
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS="1"
```

### "Team not creating"

Check:
1. Environment variable is set
2. Team configuration file exists
3. Agent definitions are present

### "Debate stuck"

Check on individual teammates:
- In-process mode: Shift+Up/Down to cycle through
- Message the stuck teammate directly
- Ask them to report their status

### Cleanup After Debate

When done with a debate:
```
Clean up the team
```

This removes team resources but keeps the debate files.

## Advanced Usage

### Custom Debate Length

By default, debates include two rebuttals. For shorter debates, tell the moderator:
```
Skip the second rebuttals for this debate
```

### Focus on Specific Aspects

Provide context in your topic:
```
Create a debate on eternal security, focusing on Hebrews 6
Create a debate on spiritual gifts, specifically speaking in tongues
```

### Multiple Debates on Same Topic

The system creates unique folders for each debate. Run the same topic multiple times to get different perspectives:
```
debates/eternal-security-1/
debates/eternal-security-2/
```
```

**Step 3: Commit documentation updates**

Run:
```bash
git add README.md docs/USAGE.md
git commit -m "docs: enhance README and add usage guide"
```

Expected: Commit created

---

## Task 11: Initialize git repository and push

**Files:**
- Create: `.github/workflows/` (optional GitHub Actions)

**Step 1: Create initial commit with all files**

Run:
```bash
cd /home/ubuntu/faith-debates
git status
```

Expected: List of all created files

**Step 2: Create GitHub repository (optional)**

Run:
```bash
gh repo create faith-debates --public --source=. --remote=origin --push
```

Expected: Repository created and pushed

Or create manually at github.com and add remote:
```bash
git remote add origin https://github.com/YOUR_USERNAME/faith-debates.git
git push -u origin main
```

**Step 3: Tag initial release**

Run:
```bash
git tag v0.1.0 -m "Initial release - Faith Debates automated system"
git push --tags
```

Expected: Tag created and pushed

---

## Task 12: Test with a simple debate

**Files:**
- Create: `debates/test-topic/` (test debate)

**Step 1: Create a test debate**

Run from within Claude Code:
```
Create a debate on a simple topic: "Is coffee good for you?"
```

Expected:
1. Debate folder created
2. Research phase completes
3. Position files generated
4. Debate proceeds through all phases
5. Judgment and summary created

**Step 2: Verify outputs**

Run:
```bash
ls debates/test-topic/
cat debates/test-topic/summary.md
cat debates/test-topic/judgment.md
```

Expected: All files present and contain content

**Step 3: Test theological debate**

Run:
```
Create a debate on whether Christians can lose their salvation
```

Expected: Full theological debate with scriptural arguments

**Step 4: Commit test results (optional)**

Run:
```bash
git add debates/
git commit -m "test: add sample debate for verification"
```

Expected: Test debates committed

---

## Completion Checklist

- [ ] Repository initialized with git
- [ ] All agent definitions created
- [ ] Team configurations created
- [ ] Bible reference added
- [ ] Debate skill created
- [ ] Documentation complete
- [ ] GitHub repository created (optional)
- [ ] Test debate successful
- [ ] All commits pushed

## Next Steps After Implementation

1. **Test with various topics** - Verify system works for different debate types
2. **Refine agent prompts** - Adjust based on debate quality
3. **Add more team configurations** - E.g., three-way debates
4. **Create debate library** - Curate best debates for reference

---

**Implementation plan complete.** Each task can be executed independently with clear file paths, code, and commands.
