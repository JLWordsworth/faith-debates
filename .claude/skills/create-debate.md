---
name: create-debate
description: Create a fully automated theological/spiritual debate from a single topic
---

Usage: "Create a debate on [topic]" or "debate [topic]"
Options: Add "in series", "sequentially", or "with minimal resources" to run agents one at a time (recommended for system stability)

## What This Does

Given a debate topic, this skill:
1. Creates a debate folder under debates/
2. Spawns an agent team to research, debate, evaluate, and summarize
3. Produces a complete debate transcript with judgment and summary

## Execution Mode

**Parallel (default):** Agents run simultaneously when possible. Faster but may cause system crashes on resource-constrained systems.

**Series (recommended):** Run "Create a debate on [topic] in series" or "Create a debate on [topic] sequentially" to execute agents one at a time. More stable, prevents crashes, each agent shuts down before the next starts.

**Resource-Constrained (minimal CPU/memory):** Run "Create a debate on [topic] with minimal resources" to use an even more efficient sequential workflow. This method:
- Spawns agents as independent subagents (not teammates)
- No team creation overhead
- Explicit verification of shutdown between each agent
- Direct file operations without task list coordination
- Best for systems that have crashed under previous debate workflows

## Requirements

- CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS must be enabled
- All agent files must be present in .claude/agents/

## Workflow

### 0. Determine Execution Mode

Check if user specified:
- "in series", "sequentially", or "one at a time" → Use series execution
- "with minimal resources" or "resource-constrained" → Use minimal resource execution
- Otherwise → Default to parallel

**Series mode benefits:** Each agent completes and shuts down before next starts, preventing resource overload and system crashes.

**Minimal resource mode benefits:** Independent subagents (no team overhead), file verification between steps, lowest memory footprint. Best for systems that have crashed previously.

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

**Parallel mode (default):**
- Send topic to researcher-a and researcher-b simultaneously
- Wait for both position files
- Send position files to debater-a and debater-b simultaneously
- Coordinate with moderator through debate phases
- Send all transcripts to judge
- Send all files to summarizer

**Series mode:**
1. Spawn researcher-a, wait for completion, shutdown
2. Spawn researcher-b, wait for completion, shutdown
3. Spawn moderator (generates intro), shutdown
4. Spawn debater-a (writes opening, waits for B), shutdown after phase
5. Spawn debater-b (writes opening, waits for A), shutdown after phase
6. Continue alternating through all debate phases
7. Spawn judge, wait for evaluation, shutdown
8. Spawn summarizer, wait for summary, shutdown

**Key for series mode:** Always use SendMessage with type "shutdown_request" after each agent completes their work. Wait for approval confirmation before spawning the next agent.

**Resource-constrained mode (minimal):**
1. Do NOT create a team - spawn agents as independent subagents using Task tool
2. Each agent is a discrete invocation with subagent_type="general-purpose" and name="[role-name]"
3. Sequence: Researcher A → verify file → Researcher B → verify file → Moderator → verify → Debater A (opening) → verify → Debater B (opening) → verify → continue through all debate phases
4. After each agent completes, they auto-shutdown (no SendMessage needed for independent subagents)
5. Verify each file exists before proceeding to next agent
6. Final commit after all files complete

**Key difference:** Resource-constrained mode uses independent Task invocations instead of TeamCreate/teammates, eliminating team coordination overhead.

### 6. Report Results

When complete, report to user with:
- Debate topic
- Execution mode used (parallel/series)
- Scores from judge
- Links to full transcript and summary

## Cleanup

After debate is complete and user is satisfied, clean up the team:
```bash
TeamDelete
```

## Example Usage

**Parallel (default):**
User: "Create a debate on whether Christians can lose their salvation"
Claude:
1. Creates debates/can-lose-salvation/
2. Spawns agent team, runs researchers in parallel
3. Coordinates research → debate → evaluation
4. Reports results

**Series (recommended for stability):**
User: "Create a debate on whether Christians can lose their salvation in series"
User: "Create a debate on whether Christians can lose their salvation sequentially"
Claude:
1. Creates debates/can-lose-salvation/
2. Spawns agents one at a time, each completes before next starts
3. Researcher A → completes → shuts down
4. Researcher B → completes → shuts down
5. Debaters alternate through phases, each shutting down after their contribution
6. Judge → completes → shuts down
7. Summarizer → completes → shuts down
8. Reports results

**Resource-constrained (minimal CPU/memory):**
User: "Create a debate on whether Christians can lose their salvation with minimal resources"
Claude:
1. Creates debates/can-lose-salvation/
2. Spawns independent subagents (no team creation)
3. Researcher A (Task tool) → verify file → Researcher B → verify file → continue through all phases
4. Each agent auto-shutdowns after completing work
5. Judge and Summarizer follow same pattern
6. Final git commit
7. Reports results
