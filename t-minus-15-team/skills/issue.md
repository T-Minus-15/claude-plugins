---
name: issue
description: Create, edit, and manage Issue work items. Context-aware for GitHub Issues vs Azure DevOps T-Minus-15 Issues (blockers/impediments).
allowed-tools: Read, Grep, Glob, Bash, Write, Edit, AskUserQuestion
---

# Issue Skill

Create and manage Issue work items. This skill is **context-aware** - it handles both GitHub Issues (general work items) and Azure DevOps T-Minus-15 Issues (blockers/impediments).

## Context Detection

Before creating an Issue, determine the context:

### Check Current Context

```bash
# Check if in a git repo
git remote -v 2>/dev/null

# If GitHub remote found
gh repo view --json name,owner 2>/dev/null

# If Azure DevOps configured
az devops project show --project "<project>" 2>/dev/null
```

### Context Rules

| Context | "Issue" Means | Use Case |
|---------|---------------|----------|
| **GitHub** | General work item | Bugs, features, tasks, discussions |
| **Azure DevOps** | Blocker/Impediment | Problems blocking work progress |

## GitHub Issues

In GitHub context, "Issue" is a general-purpose work item.

### GitHub Issue Types (via labels)

| Label | Purpose |
|-------|---------|
| `bug` | Defect report |
| `enhancement` | Feature request |
| `task` | Work item |
| `question` | Discussion/clarification |
| `risk` | Potential problem |
| `blocker` | Impediment (closest to DevOps Issue) |

### Create GitHub Issue

```bash
# General issue
gh issue create \
  --title "Implement user authentication" \
  --body "## Description
Add OAuth2 authentication flow.

## Acceptance Criteria
- [ ] Google OAuth provider
- [ ] Session management
- [ ] Logout functionality" \
  --label "enhancement"

# Blocker (equivalent to DevOps Issue)
gh issue create \
  --title "[Blocker] Build pipeline failing on main" \
  --body "## Problem
CI pipeline has been failing since commit abc123.

## Impact
- Team cannot merge PRs
- Deployment blocked

## Immediate Action Needed
Investigate test failures in auth module." \
  --label "blocker,urgent"
```

### Query GitHub Issues

```bash
# All open issues
gh issue list --state open

# Issues by label
gh issue list --label "bug" --state open
gh issue list --label "blocker" --state open

# My assigned issues
gh issue list --assignee "@me" --state open

# Issues in milestone
gh issue list --milestone "Sprint 5" --state open
```

## Azure DevOps Issues (T-Minus-15)

In Azure DevOps context, "Issue" specifically means a **blocker or impediment** - a current problem blocking work.

### Definition

**Issue (DevOps)**: A current problem that is blocking or impacting work progress. Unlike Risks (potential problems), Issues are happening NOW.

### Check Process Template

```bash
# Get process template
az devops project show --project "<project>" --query "capabilities.processTemplate.templateName" -o tsv

# List available work item types
az boards work-item type list --project "<project>" --query "[].name" -o tsv
```

**Process Templates:**
- **Agile**: Issue (native type)
- **Scrum**: Impediment (use instead of Issue)
- **CMMI**: Issue (native type)
- **Basic**: Issue (native type)

### Issue Severity

| Severity | Description | Example | Response |
|----------|-------------|---------|----------|
| **Critical** | Complete work stoppage | Build server down | Immediate escalation |
| **Major** | Significant delay | Key resource unavailable | Same day resolution |
| **Minor** | Inconvenience | Tool running slowly | Scheduled fix |

### Issue Template (DevOps)

#### Required Fields

| Field | Description | Required |
|-------|-------------|----------|
| Title | Clear description of the blocker | Yes |
| Description | What is blocked and why | Yes |
| Impact | Teams/Features affected | Yes |
| Severity | Critical/Major/Minor | Yes |
| Assigned To | Person resolving the issue | Yes |

#### Optional Fields

| Field | Description |
|-------|-------------|
| Related Work Items | Features/Stories blocked |
| Root Cause | Why this happened |
| Workaround | Temporary solution if available |
| Resolution | How it was fixed (when closing) |

### Create DevOps Issue

```bash
# Agile/CMMI/Basic - native Issue type
az boards work-item create \
  --type "Issue" \
  --title "Build pipeline failing on main branch" \
  --project "<project>" \
  --fields "Microsoft.VSTS.Common.Priority=1" \
           "System.Description=<html><h2>Problem</h2><p>CI pipeline failing since 9am</p><h2>Impact</h2><p>All PRs blocked, deployment halted</p><h2>Affected</h2><p>Feature #123, Feature #124</p></html>"

# Scrum - use Impediment instead
az boards work-item create \
  --type "Impediment" \
  --title "Build pipeline failing on main branch" \
  --project "<project>" \
  --fields "Microsoft.VSTS.Common.Priority=1"
```

### Link Issue to Blocked Work

```bash
# Link issue to affected Feature
az boards work-item relation add \
  --id <issue-id> \
  --relation-type "Related" \
  --target-id <feature-id>
```

### Query DevOps Issues

```bash
# All open issues (Agile/CMMI/Basic)
az boards query --wiql "SELECT [ID], [Title], [Priority], [State] FROM WorkItems WHERE [Work Item Type] = 'Issue' AND [State] <> 'Closed'" -o table

# All open impediments (Scrum)
az boards query --wiql "SELECT [ID], [Title], [Priority], [State] FROM WorkItems WHERE [Work Item Type] = 'Impediment' AND [State] <> 'Closed'" -o table

# Critical issues only
az boards query --wiql "SELECT [ID], [Title] FROM WorkItems WHERE [Work Item Type] = 'Issue' AND [Priority] = 1 AND [State] <> 'Closed'"

# Issues blocking a specific Feature
az boards query --wiql "SELECT [ID], [Title] FROM WorkItemLinks WHERE [Target].[ID] = <feature-id> AND [Source].[Work Item Type] = 'Issue' AND [Source].[State] <> 'Closed'"
```

## Issue Resolution

### Resolution Template

When closing an Issue, document:

```markdown
## Resolution

**Root Cause:** [Why did this happen?]

**Fix Applied:** [What was done to resolve it?]

**Prevention:** [How do we prevent recurrence?]

**Resolved By:** [Name] on [Date]
```

### Close Issue

```bash
# Azure DevOps
az boards work-item update \
  --id <issue-id> \
  --fields "System.State=Closed" \
           "Microsoft.VSTS.Common.ResolvedReason=Fixed"

# GitHub
gh issue close <issue-number> --comment "Resolved: [brief explanation]"
```

## Issue vs Other Work Items

| Work Item | Timing | Purpose |
|-----------|--------|---------|
| **Risk** | Future | Potential problem to mitigate |
| **Issue** | Now | Current blocker to resolve |
| **Bug** | Now | Defect in delivered functionality |
| **Task** | Planned | Work to be done |

## Escalation Guidelines

### When to Escalate

| Condition | Action |
|-----------|--------|
| Issue unresolved >4 hours | Notify Poppie |
| Multiple teams blocked | Escalate to stakeholders |
| No owner assigned | Poppie assigns immediately |
| Workaround unavailable | Priority 1 response |

### Escalation Path

1. **Agent level** - Try to resolve within team
2. **Poppie** - Coordinate cross-team resolution
3. **Stakeholders** - Business decision required
4. **External** - Vendor/third-party involvement

## Checklist

Before creating an issue:
- [ ] Confirmed this is a CURRENT problem (not a future Risk)
- [ ] Clear description of what is blocked
- [ ] Impact assessed and documented
- [ ] Severity assigned appropriately
- [ ] Owner assigned for resolution
- [ ] Related work items linked
- [ ] Not a duplicate of existing issue

When closing an issue:
- [ ] Root cause documented
- [ ] Fix applied and verified
- [ ] Prevention measures identified
- [ ] Related work items unblocked
- [ ] Stakeholders notified if needed

## Tips

- **Act fast** - Issues are blockers; time matters
- **Be specific** - What exactly is blocked and why?
- **Assign ownership** - Unowned issues don't get resolved
- **Document resolution** - Help prevent recurrence
- **Don't confuse with Risk** - Risk = might happen; Issue = happening now
- **Link related items** - Show what's affected
