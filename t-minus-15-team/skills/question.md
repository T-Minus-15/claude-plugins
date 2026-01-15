---
name: question
description: Create, edit, and manage Question work items. Questions are clarifications needed before work can proceed.
allowed-tools: Read, Grep, Glob, Bash, Write, Edit, AskUserQuestion
---

# Question Skill

Create and manage Question work items following T-Minus-15 methodology. Questions are clarifications needed before work can proceed effectively.

## Definition

**Question**: A clarification request that must be answered before work can proceed confidently. Unanswered questions can become blockers.

**Key Distinction**:
- **Question** = Need information to proceed
- **Issue** = Have a problem blocking progress
- **Risk** = Potential future problem

## Question Urgency

| Urgency | Description | Response Time | Example |
|---------|-------------|---------------|---------|
| **Blocking** | Cannot proceed until answered | Same day | "What authentication method should we use?" |
| **Important** | Needed soon, workaround exists | 2-3 days | "Should we support IE11?" |
| **Nice-to-have** | Would help but not critical | Next sprint | "Preference on icon library?" |

## Question Template

### Required Fields

| Field | Description | Required |
|-------|-------------|----------|
| Title | Clear, specific question | Yes |
| Context | Why this question arose | Yes |
| Options | Possible answers (if known) | Yes |
| Impact | What depends on this answer | Yes |
| Directed To | Who can answer this | Yes |
| Needed By | When answer is required | Yes |

### Optional Fields

| Field | Description |
|-------|-------------|
| Related Work Item | User Story/Feature affected |
| Default Answer | What we'll assume if no response |
| Decision Made | Final answer (when resolved) |
| Rationale | Why this answer was chosen |

## Azure DevOps

### Check Process Template

```bash
# Get process template
az devops project show --project "<project>" --query "capabilities.processTemplate.templateName" -o tsv

# List available work item types
az boards work-item type list --project "<project>" --query "[].name" -o tsv
```

**Note:** Most process templates don't have a native "Question" type. Use these alternatives:

| Template | Recommended Approach |
|----------|---------------------|
| **Agile** | Issue with tag "Question" |
| **Scrum** | Product Backlog Item with tag "Question" |
| **CMMI** | Issue or Review with tag "Question" |
| **Basic** | Issue with tag "Question" |

### Create Question

```bash
# Create as Issue with Question tag
az boards work-item create \
  --type "Issue" \
  --title "[Question] What authentication provider should we use?" \
  --project "<project>" \
  --fields "System.Tags=Question,Blocking" \
           "System.AssignedTo=product.owner@example.com" \
           "System.Description=<html>
<h2>Context</h2>
<p>US-123 requires user authentication but doesn't specify the provider.</p>

<h2>Options</h2>
<ol>
<li>Azure AD - Enterprise SSO, existing infrastructure</li>
<li>Auth0 - Flexible, social logins supported</li>
<li>Custom JWT - Full control, more development time</li>
</ol>

<h2>Impact</h2>
<p>Blocks: US-123, US-124, US-125 (all auth-related stories)</p>

<h2>Recommendation</h2>
<p>Azure AD - aligns with existing enterprise infrastructure</p>

<h2>Needed By</h2>
<p>Sprint planning on Monday</p>
</html>"

# Link to affected User Story
az boards work-item relation add \
  --id <question-id> \
  --relation-type "Related" \
  --target-id <user-story-id>
```

### Query Questions

```bash
# All open questions
az boards query --wiql "SELECT [ID], [Title], [Assigned To], [State] FROM WorkItems WHERE [Tags] CONTAINS 'Question' AND [State] <> 'Closed'" -o table

# Blocking questions
az boards query --wiql "SELECT [ID], [Title] FROM WorkItems WHERE [Tags] CONTAINS 'Question' AND [Tags] CONTAINS 'Blocking' AND [State] <> 'Closed'"

# Questions assigned to specific person
az boards query --wiql "SELECT [ID], [Title] FROM WorkItems WHERE [Tags] CONTAINS 'Question' AND [Assigned To] = 'product.owner@example.com' AND [State] <> 'Closed'"

# Stale questions (unanswered for 7+ days)
az boards query --wiql "SELECT [ID], [Title] FROM WorkItems WHERE [Tags] CONTAINS 'Question' AND [State] <> 'Closed' AND [Changed Date] < @Today - 7"
```

## GitHub

GitHub uses Issues with labels for question tracking.

### Create Question Issue

```bash
gh issue create \
  --title "[Question] What authentication provider should we use?" \
  --body "## Context
US-123 requires user authentication but doesn't specify the provider.

## Options
1. **Azure AD** - Enterprise SSO, existing infrastructure
2. **Auth0** - Flexible, social logins supported
3. **Custom JWT** - Full control, more development time

## Impact
Blocks:
- #123 User login story
- #124 User registration story
- #125 Password reset story

## Recommendation
Azure AD - aligns with existing enterprise infrastructure

## Directed To
@product-owner

## Needed By
Sprint planning on Monday (Jan 20)

## Default if No Response
Will proceed with Azure AD recommendation on Tuesday if no response." \
  --label "question,blocking" \
  --assignee "product-owner"
```

### Query Questions

```bash
# All open questions
gh issue list --label "question" --state open

# Blocking questions
gh issue list --label "question,blocking" --state open

# Questions assigned to specific person
gh issue list --label "question" --assignee "product-owner" --state open
```

## Question Lifecycle

### 1. Identification

Questions arise during:
- Backlog refinement (Pennie)
- Design reviews (Dannie)
- Implementation (Ernie)
- Testing (Teddie)
- Deployment planning (Ollie)

### 2. Documentation

Good questions include:
- **Specific phrasing** - Not "What about auth?" but "Which auth provider?"
- **Context** - Why does this matter?
- **Options** - What are the choices?
- **Recommendation** - What does the team suggest?
- **Deadline** - When do we need the answer?

### 3. Routing

Direct questions to the right person:

| Question Type | Route To |
|---------------|----------|
| Business requirements | Product Owner |
| Technical architecture | Archie |
| Design decisions | Dannie |
| User research | Pennie |
| Testing approach | Teddie |
| Deployment concerns | Ollie |

### 4. Follow-up

If questions go unanswered:
- Day 1: Initial question submitted
- Day 3: Gentle reminder
- Day 5: Escalate to Poppie
- Day 7: Flag as blocker, use default answer

### 5. Documentation of Answer

When answered, document:
```markdown
## Decision Made
Azure AD will be used for authentication.

## Rationale
- Existing enterprise infrastructure
- IT team has expertise
- Meets security requirements

## Decided By
@product-owner on 2024-01-15

## Impact on Work
- US-123 can proceed
- Update technical design doc
- Ernie to implement
```

## Question to Issue Conversion

If an unanswered question becomes a blocker:

```bash
# Azure DevOps - update tags
az boards work-item update \
  --id <question-id> \
  --fields "System.Tags=Question,Blocker" \
           "Microsoft.VSTS.Common.Priority=1"

# GitHub - add blocker label
gh issue edit <question-number> --add-label "blocker"
```

## Best Practices

### Writing Good Questions

**Good:**
- "Should the session timeout be 30 minutes or 8 hours for the admin portal?"
- "Which date format should we use: MM/DD/YYYY or DD/MM/YYYY?"
- "Is IE11 support required for the initial release?"

**Bad:**
- "What should we do about dates?" (too vague)
- "Auth?" (not a question)
- "Can you tell me everything about the login flow?" (too broad)

### Managing Questions

- **Don't let questions age** - Unanswered questions become blockers
- **Provide options** - Make it easy to decide
- **Set defaults** - "We'll do X unless we hear otherwise"
- **Track dependencies** - Know what's waiting on each answer
- **Document decisions** - Answers inform future work

## Checklist

Before creating a question:
- [ ] Question is specific and answerable
- [ ] Context provided (why are we asking?)
- [ ] Options listed with pros/cons
- [ ] Impact documented (what's waiting?)
- [ ] Directed to the right person
- [ ] Deadline specified
- [ ] Default answer proposed (if applicable)
- [ ] Not a duplicate of existing question

When closing a question:
- [ ] Answer is documented clearly
- [ ] Rationale is captured
- [ ] Decision maker noted
- [ ] Related work items updated
- [ ] Blocked work can now proceed

## Tips

- **Ask early** - Questions discovered in PREP are cheaper than in TEST
- **Be specific** - Vague questions get vague answers
- **Propose answers** - "Should we do A or B?" is better than "What should we do?"
- **Set deadlines** - Open-ended questions never get answered
- **Document everything** - Future you will thank present you
- **Follow up** - Don't assume silence means agreement
