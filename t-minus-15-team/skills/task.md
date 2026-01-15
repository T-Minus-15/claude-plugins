---
name: task
description: Create, edit, and manage Task work items. Tasks are discrete pieces of work that implement User Stories.
tools: Read, Grep, Glob, Bash, Write, Edit, AskUserQuestion
---

# Task Skill

Create and manage Task work items following T-Minus-15 methodology. Tasks are discrete pieces of work that contribute to completing a User Story.

## Definition

**Task**: A discrete piece of work assigned to a team member that contributes to completing a User Story. Tasks are the smallest trackable unit of work.

## Task Hierarchy

```
Epic
└── Feature
    └── User Story
        ├── Task (implementation work)
        ├── Task (testing work)
        ├── Bug (if found)
        └── Enhancement (if requested)
```

**Key Rule:** Tasks MUST be children of User Stories. No orphaned tasks.

## Task Types

| Type | Description | Typical Owner |
|------|-------------|---------------|
| **Development** | Code implementation | Ernie |
| **Testing** | Test creation/execution | Teddie |
| **Documentation** | Doc updates | Connie |
| **Design** | UI/UX work | Dannie |
| **DevOps** | Pipeline/infra work | Ollie |
| **Review** | Code/architecture review | Archie |

## Task Template

### Required Fields

| Field | Description | Required |
|-------|-------------|----------|
| Title | Clear action-oriented description | Yes |
| Parent | User Story this task implements | Yes |
| Assigned To | Team member responsible | Yes |
| Effort | Estimated hours (typically 1-8) | Yes |
| State | New/Active/Closed | Yes |

### Optional Fields

| Field | Description |
|-------|-------------|
| Description | Additional details or acceptance criteria |
| Remaining Work | Hours remaining (for burndown) |
| Completed Work | Hours completed |
| Priority | If ordering within Story matters |

## Task Naming Convention

Use action verbs that describe what will be done:

**Good Examples:**
- "Implement login form validation"
- "Create unit tests for UserService"
- "Update API documentation for /auth endpoint"
- "Review PR #123 for security concerns"
- "Deploy v1.2.0 to staging environment"

**Bad Examples:**
- "Login form" (not actionable)
- "Testing" (too vague)
- "Misc work" (meaningless)

## Azure DevOps

### Check Process Template

```bash
# Get project process template
az devops project show --project "<project>" --query "capabilities.processTemplate.templateName" -o tsv
```

**Process Templates:**
- **Agile**: Task (child of User Story)
- **Scrum**: Task (child of Product Backlog Item)
- **CMMI**: Task (child of Requirement)
- **Basic**: Task (child of Issue)

### Create Task

```bash
az boards work-item create \
  --type "Task" \
  --title "Implement login form validation" \
  --project "<project>" \
  --fields "System.AssignedTo=ernie@example.com" \
           "Microsoft.VSTS.Scheduling.OriginalEstimate=4"

# Link to parent User Story (REQUIRED)
az boards work-item relation add \
  --id <task-id> \
  --relation-type "Parent" \
  --target-id <user-story-id>
```

### Query Tasks

```bash
# All active tasks
az boards query --wiql "SELECT [ID], [Title], [Assigned To], [State] FROM WorkItems WHERE [Work Item Type] = 'Task' AND [State] = 'Active'" -o table

# Tasks for a specific User Story
az boards query --wiql "SELECT [ID], [Title], [State] FROM WorkItemLinks WHERE [Source].[ID] = <story-id> AND [Target].[Work Item Type] = 'Task'"

# My tasks
az boards query --wiql "SELECT [ID], [Title], [State] FROM WorkItems WHERE [Work Item Type] = 'Task' AND [Assigned To] = @Me AND [State] <> 'Closed'"

# Orphaned tasks (no parent - BAD!)
az boards query --wiql "SELECT [ID], [Title] FROM WorkItems WHERE [Work Item Type] = 'Task' AND [State] <> 'Closed' AND [Parent] = ''"
```

### Update Task Progress

```bash
# Update remaining work
az boards work-item update \
  --id <task-id> \
  --fields "Microsoft.VSTS.Scheduling.RemainingWork=2"

# Close task
az boards work-item update \
  --id <task-id> \
  --fields "System.State=Closed"
```

## GitHub

GitHub uses Issues with labels for task tracking.

### Create Task Issue

```bash
gh issue create \
  --title "Task: Implement login form validation" \
  --body "## Parent User Story
Part of #<story-issue-number>

## Description
Add client-side validation for login form fields.

## Acceptance Criteria
- [ ] Email format validation
- [ ] Password minimum length check
- [ ] Error messages displayed inline
- [ ] Submit button disabled until valid

## Effort Estimate
4 hours

## Assigned To
@ernie" \
  --label "task" \
  --assignee "ernie"
```

### Query Tasks

```bash
# All open tasks
gh issue list --label "task" --state open

# My tasks
gh issue list --label "task" --assignee "@me" --state open

# Tasks in current milestone
gh issue list --label "task" --milestone "Sprint 5"
```

## Task Breakdown Guidelines

### When Breaking Down User Stories

1. **Identify components** - What parts of the system are affected?
2. **Consider disciplines** - Dev, Test, Docs, DevOps?
3. **Keep tasks small** - 1-8 hours ideal, never >16 hours
4. **Make tasks independent** - Minimize dependencies between tasks
5. **Include all work** - Don't forget testing, documentation, review

### Example Task Breakdown

**User Story:** "As a user, I want to reset my password so I can regain access"

**Tasks:**
1. Implement forgot password API endpoint (4h) - Ernie
2. Create email template for reset link (2h) - Ernie
3. Build password reset form UI (4h) - Ernie
4. Write unit tests for password reset flow (3h) - Teddie
5. Create E2E test for reset workflow (2h) - Teddie
6. Update user documentation (1h) - Connie
7. Code review password reset PR (1h) - Archie

## Task States

| State | Description |
|-------|-------------|
| **New** | Task created but not started |
| **Active** | Work in progress |
| **Closed** | Work completed |

**Note:** Don't use "Blocked" as a state - create an Issue instead.

## Checklist

Before creating a task:
- [ ] Title is action-oriented and specific
- [ ] Linked to parent User Story
- [ ] Assigned to a team member
- [ ] Effort estimated in hours
- [ ] Scope is clear (1-8 hours ideal)
- [ ] No duplicate of existing task

When closing a task:
- [ ] Work is actually complete
- [ ] Any artifacts created are committed/saved
- [ ] Parent User Story progress is updated
- [ ] Related tasks are unblocked (if dependencies exist)

## Tips

- **No orphans** - Every task must have a parent User Story
- **Small is beautiful** - Break large tasks into smaller ones
- **Action verbs** - Start titles with verbs (Implement, Create, Update, Review)
- **Complete before closing** - Don't close tasks that are "mostly done"
- **Track time** - Update remaining work for accurate burndowns
- **One owner** - Each task should have a single assignee
