---
name: prep
description: Invoke Pennie the Prepper for backlog review and requirements preparation
allowed-tools: Read, Grep, Glob, Bash, Task, WebFetch, Write, Edit, AskUserQuestion
---

# /prep Command

Invokes **Pennie the Prepper** to review backlogs and prepare requirements.

## Usage

```
/prep                              # Start prep session
/prep --review                     # Review backlog for completeness
/prep --review ADO #123            # Review Azure DevOps work item
/prep --review GH #456             # Review GitHub issue
/prep --sync                       # Sync discussion to backlog
/prep Create a Feature for...      # Create a specific Feature
/prep Break down this screen...    # Generate User Stories from UI
/prep Add acceptance criteria...   # Add AMP criteria to stories
```

## Backlog Review (Azure DevOps & GitHub)

Pennie reviews work items against T-Minus-15 principles:

**Azure DevOps** (uses `az` CLI):
```bash
az boards work-item show --id <id>
az boards query --wiql "SELECT ... FROM WorkItems"
```

**GitHub** (uses `gh` CLI):
```bash
gh issue view <number>
gh issue list --label "feature"
```

Pennie will:
1. Check the process template (Agile/Scrum/CMMI/Basic)
2. Verify required fields are populated
3. Identify missing acceptance criteria
4. Ask clarifying questions via `AskUserQuestion`
5. Suggest improvements

## Development Workflow

**Documentation First (Recommended):**
- Requirements fully documented before development
- Better testing outcomes

**Free-Flowing Development:**
- Rapid prototyping with high-level requirements
- Pennie asks: "Would you like me to update the backlog with changes discussed?"
- Keeps backlog in sync for traceability

## What Pennie Does

1. **Reviews backlogs** for T-Minus-15 completeness
2. Creates Features with T-Minus-15 metadata
3. Analyzes UI screens for components
4. Generates User Stories with AMP acceptance criteria
5. Writes Gherkin scenarios (GIVEN/WHEN/THEN)
6. **Syncs discussions** back to backlog

## Output

- Backlog review report with gaps identified
- Complete Feature definition
- User Stories as child work items
- AMP acceptance criteria (Acceptance/Measure/Proof)
- Test cases for each scenario
