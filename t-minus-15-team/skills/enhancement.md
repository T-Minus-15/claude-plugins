---
name: enhancement
description: Create, edit, and manage Enhancement work items. Enhancements are improvements that don't block User Story acceptance.
allowed-tools: Read, Grep, Glob, Bash, Write, Edit, AskUserQuestion
---

# Enhancement Skill

Create and manage Enhancement work items following T-Minus-15 methodology. Enhancements are improvement requests that do NOT block acceptance criteria.

## Definition

**Enhancement**: An improvement request that was NOT part of the original acceptance criteria. Enhancements do not block User Story acceptance.

**Key Distinction**:
- If it blocks acceptance criteria → **Bug**
- If it's an improvement beyond original scope → **Enhancement**
- If it's >4 hours of work → Consider creating a new **User Story**

## Enhancement vs Bug

| Aspect | Bug | Enhancement |
|--------|-----|-------------|
| Blocks acceptance | Yes | No |
| Part of original AC | Yes (failure to meet) | No (beyond scope) |
| Priority | Based on severity | Lower than bugs |
| Sprint inclusion | Usually this sprint | Often deferred |

## Severity Classification

| Severity | Description | Example |
|----------|-------------|---------|
| **Minor** | Nice-to-have improvement | Better error message wording |
| **Cosmetic** | Polish/refinement | Slightly larger button padding |

**Note:** Enhancements are typically Minor or Cosmetic. If it's Critical or Major, it's likely a Bug or should be a new User Story.

## Enhancement Template

### Required Fields

| Field | Description | Required |
|-------|-------------|----------|
| Title | Clear description of the improvement | Yes |
| User Story | Parent User Story this enhancement relates to | Yes |
| Description | What improvement is being requested | Yes |
| Benefit | Why this improvement would be valuable | Yes |
| Effort Estimate | Rough estimate (should be <4 hours) | Yes |

### Optional Fields

| Field | Description |
|-------|-------------|
| Mockup/Screenshot | Visual showing desired improvement |
| Priority | Minor/Cosmetic |
| Assigned To | Developer if scheduled |

## Azure DevOps

### Check Process Template

```bash
# Get project process template
az devops project show --project "<project>" --query "capabilities.processTemplate.templateName" -o tsv

# List available work item types
az boards work-item type list --project "<project>" --query "[].name" -o tsv
```

**Note:** Not all process templates have an "Enhancement" type. Alternatives:
- **Agile**: Use Bug with tag "Enhancement" or custom work item type
- **Scrum**: Use Product Backlog Item with tag "Enhancement"
- **CMMI**: Use Change Request
- **Basic**: Use Issue with tag "Enhancement"

### Create Enhancement

```bash
# If Enhancement type exists
az boards work-item create \
  --type "Enhancement" \
  --title "Improve error message clarity on login form" \
  --project "<project>" \
  --fields "System.Description=<html><p>Current error message is generic. Suggest specific guidance.</p></html>"

# Link to parent User Story
az boards work-item relation add \
  --id <enhancement-id> \
  --relation-type "Parent" \
  --target-id <user-story-id>

# Alternative: Use Bug with tag
az boards work-item create \
  --type "Bug" \
  --title "[Enhancement] Improve error message clarity" \
  --project "<project>" \
  --fields "System.Tags=Enhancement"
```

### Query Enhancements

```bash
# If Enhancement type exists
az boards query --wiql "SELECT [ID], [Title], [State] FROM WorkItems WHERE [Work Item Type] = 'Enhancement' AND [State] <> 'Closed'"

# If using tags
az boards query --wiql "SELECT [ID], [Title] FROM WorkItems WHERE [Tags] CONTAINS 'Enhancement' AND [State] <> 'Closed'"
```

## GitHub

GitHub uses Issues with labels for enhancement tracking.

### Create Enhancement Issue

```bash
gh issue create \
  --title "[Enhancement] Improve error message clarity on login form" \
  --body "## User Story
Relates to #<story-issue-number>

## Current Behavior
Error message shows: \"Login failed\"

## Proposed Improvement
Show specific reason: \"Invalid password\" or \"Account not found\"

## Benefit
Users will understand why login failed and what action to take

## Effort Estimate
~2 hours

## Mockup
[Optional: attach mockup or screenshot]" \
  --label "enhancement,minor"
```

### Query Enhancements

```bash
# All open enhancements
gh issue list --label "enhancement" --state open

# Enhancements for current milestone
gh issue list --label "enhancement" --milestone "Sprint 5"
```

## When to Create an Enhancement vs New Story

| Scenario | Action |
|----------|--------|
| Small improvement (<4 hours) | Create Enhancement |
| Significant new capability (>4 hours) | Create new User Story |
| Changes acceptance criteria | Discuss with Pennie - may need Story update |
| Multiple related improvements | Consider grouping into User Story |

## Checklist

Before submitting an enhancement:
- [ ] Confirmed this is NOT blocking acceptance criteria (otherwise it's a Bug)
- [ ] Linked to parent User Story
- [ ] Clear description of current vs proposed behavior
- [ ] Benefit/value articulated
- [ ] Effort estimate provided (<4 hours)
- [ ] Not a duplicate of existing enhancement
- [ ] Discussed with Product Owner if prioritization needed

## Tips

- **Don't get hung up on classification** - Work in order of severity
- **Keep scope small** - If it's big, make it a User Story
- **Link to parent** - Enhancements must be children of User Stories
- **Document the "why"** - Explain the benefit, not just the change
- **Consider timing** - Enhancements often get deferred; that's OK
