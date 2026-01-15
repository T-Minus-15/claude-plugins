---
name: bug
description: Create, edit, and manage Bug work items with severity classification. Bugs represent failures to meet User Story acceptance criteria.
tools: Read, Grep, Glob, Bash, Write, Edit, AskUserQuestion
---

# Bug Skill

Create and manage Bug work items following T-Minus-15 methodology. Bugs are defects that cause User Stories to fail their acceptance criteria.

## Definition

**Bug**: A failure to meet a User Story and its acceptance criteria. Bugs block acceptance until resolved.

**Key Distinction**: If it wasn't in the original acceptance criteria, it's an Enhancement, not a Bug.

## Severity Classification

| Severity | Description | Example | SLA |
|----------|-------------|---------|-----|
| **Critical** | Core functionality broken, no workaround | Application crashes on load | Immediate |
| **Major** | Functionality works incorrectly, workaround exists | Wrong calculation result | This sprint |
| **Minor** | Inconvenience, no significant impact | Button alignment off by 5px | Next sprint |
| **Cosmetic** | Visual/polish issues only | Font weight slightly different | Best effort |

## Bug Template

### Required Fields

| Field | Description | Required |
|-------|-------------|----------|
| Title | `[Severity] Brief description` - understandable without reading body | Yes |
| User Story | Parent User Story this bug relates to | Yes |
| Severity | Critical/Major/Minor/Cosmetic | Yes |
| Steps to Reproduce | Numbered steps to recreate the issue | Yes |
| Expected Result | What should happen | Yes |
| Actual Result | What actually happens | Yes |
| Screenshot | Visual evidence of the failure | Yes |
| Environment | Browser/OS/Version/Environment | Yes |

### Optional Fields

| Field | Description |
|-------|-------------|
| Assigned To | Developer responsible for fix |
| Root Cause | Technical explanation of why it occurred |
| Related Bugs | Links to similar or related issues |

## Azure DevOps

### Check Process Template

Before creating bugs, verify the work item type exists:

```bash
# Get project process template
az devops project show --project "<project>" --query "capabilities.processTemplate.templateName" -o tsv

# List available work item types
az boards work-item type list --project "<project>" --query "[].name" -o tsv
```

**Process Templates:**
- **Agile**: Bug (child of User Story)
- **Scrum**: Bug (child of Product Backlog Item)
- **CMMI**: Bug (child of Requirement)
- **Basic**: Issue (no Bug type - use Issue instead)

### Create Bug

```bash
az boards work-item create \
  --type "Bug" \
  --title "[Critical] Login form crashes on submit" \
  --project "<project>" \
  --fields "Microsoft.VSTS.Common.Severity=1 - Critical" \
            "Microsoft.VSTS.TCM.ReproSteps=<html><ol><li>Step 1</li><li>Step 2</li></ol></html>"

# Link to parent User Story
az boards work-item relation add \
  --id <bug-id> \
  --relation-type "Parent" \
  --target-id <user-story-id>
```

### Query Bugs

```bash
# All open bugs
az boards query --wiql "SELECT [ID], [Title], [Severity], [State] FROM WorkItems WHERE [Work Item Type] = 'Bug' AND [State] <> 'Closed'" -o table

# Critical/Major bugs only
az boards query --wiql "SELECT [ID], [Title] FROM WorkItems WHERE [Work Item Type] = 'Bug' AND [State] <> 'Closed' AND ([Severity] = '1 - Critical' OR [Severity] = '2 - High')"

# Bugs for a specific User Story
az boards query --wiql "SELECT [ID], [Title] FROM WorkItemLinks WHERE [Source].[ID] = <story-id> AND [Target].[Work Item Type] = 'Bug'"
```

## GitHub

GitHub uses Issues with labels for bug tracking.

### Create Bug Issue

```bash
gh issue create \
  --title "[Critical] Login form crashes on submit" \
  --body "## User Story
Relates to #<story-issue-number>

## Severity
Critical

## Steps to Reproduce
1. Navigate to login page
2. Enter valid credentials
3. Click Submit

## Expected Result
User is logged in and redirected to dashboard

## Actual Result
Application crashes with error 500

## Environment
- Browser: Chrome 120
- OS: macOS 14.2
- Environment: Staging

## Screenshot
[Attach screenshot]" \
  --label "bug,critical"
```

### Query Bugs

```bash
# All open bugs
gh issue list --label "bug" --state open

# Critical bugs
gh issue list --label "bug,critical" --state open

# Bugs in a milestone
gh issue list --label "bug" --milestone "Sprint 5"
```

## Bug Resolution

### When Closing a Bug

The resolution MUST include:
- [ ] Root cause identified and documented
- [ ] Changes made described specifically
- [ ] Related components/files noted
- [ ] Regression test added (if applicable)
- [ ] Verified by Tester (NOT the developer who fixed it)

### Resolution Template

```markdown
## Resolution

**Root Cause:** [Technical explanation of why this occurred]

**Changes Made:**
- [File/component 1]: [What was changed]
- [File/component 2]: [What was changed]

**Related Components:** [List any related areas that may be affected]

**Regression Test:** [Link to test case or describe manual verification]

**Verified By:** [Tester name] on [date]
```

## Feature Completion Gate

A Feature is NOT complete until:
- **100%** of Critical bugs resolved
- **100%** of Major bugs resolved
- **50%** of Minor bugs resolved (at PO discretion)
- **Cosmetic** bugs at best effort

## Checklist

Before submitting a bug:
- [ ] Title includes severity and is understandable alone
- [ ] Linked to parent User Story
- [ ] Clear reproduction steps provided
- [ ] Expected vs Actual results documented
- [ ] Screenshot attached
- [ ] Environment details included
- [ ] Severity assigned appropriately
- [ ] Not a duplicate of existing bug

## Tips

- **Screenshots are mandatory** - Always include visual evidence
- **Be specific** - "It doesn't work" is not helpful
- **One bug per issue** - Don't combine multiple issues
- **Check for duplicates** - Search before creating
- **Include context** - What were you trying to accomplish?
- **Reproduction matters** - If it can't be reproduced, it can't be fixed
