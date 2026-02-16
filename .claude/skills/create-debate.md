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
