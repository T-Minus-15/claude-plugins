---
name: plan
description: Invoke Poppie the Planner for Epic planning and roadmap creation
allowed-tools: Read, Grep, Glob, Bash, Task, WebFetch, Write, Edit, AskUserQuestion
---

# /plan Command

Invokes **Poppie the Planner** to help with Epic planning and roadmap creation.

## Usage

```
/plan                           # Start planning session
/plan Create an Epic for...     # Create a specific Epic
/plan What Epics do we need...  # Roadmap planning
```

## What Poppie Does

1. Understands your business initiative
2. Creates Epics with full T-Minus-15 metadata
3. Breaks Epics into Features
4. Defines delivery strategy and milestones

## Output

- Complete Epic definition (Azure DevOps compatible)
- Feature breakdown with MoSCoW priorities
- Delivery milestones and checkpoints
