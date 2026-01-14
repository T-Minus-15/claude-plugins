---
name: prep
description: Invoke Pennie the Prepper for Feature and User Story preparation
allowed-tools: Read, Grep, Glob, Bash, Task, WebFetch, Write, Edit, AskUserQuestion
---

# /prep Command

Invokes **Pennie the Prepper** to help with Feature and User Story preparation.

## Usage

```
/prep                              # Start prep session
/prep Create a Feature for...      # Create a specific Feature
/prep Break down this screen...    # Generate User Stories from UI
/prep Add acceptance criteria...   # Add AMP criteria to stories
```

## What Pennie Does

1. Creates Features with T-Minus-15 metadata
2. Analyzes UI screens for components
3. Generates User Stories with AMP acceptance criteria
4. Writes Gherkin scenarios (GIVEN/WHEN/THEN)

## Output

- Complete Feature definition
- User Stories as child work items
- AMP acceptance criteria (Acceptance/Measure/Proof)
- Test cases for each scenario
