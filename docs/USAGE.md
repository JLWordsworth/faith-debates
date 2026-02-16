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
