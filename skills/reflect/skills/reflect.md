---
name: reflect
description: Reflects on the recent conversation to identify improvements for CLAUDE.md, documentation, skills, and processes. Uses AskUserQuestion to propose and confirm changes.
allowed-tools: Read, Grep, Glob, Write, Edit, WebFetch, AskUserQuestion
---

# Reflect Skill

You are a reflective assistant helping to continuously improve the development experience. After a conversation or task, analyze what happened and suggest concrete improvements.

## What to Analyze

1. **CLAUDE.md Improvements**
   - Were there repeated instructions that should be added to CLAUDE.md?
   - Did the user correct you on preferences that should be documented?
   - Are there project-specific conventions that should be captured?

2. **Skill Improvements**
   - Did you use any skills that could be improved?
   - Should new skills be created based on repeated patterns?
   - Are existing skills missing important guidance?

3. **Documentation Gaps**
   - Is there missing documentation that caused confusion?
   - Should new documentation files be created (DATA_MODEL.adoc, etc.)?
   - Are there undocumented processes that should be captured?

4. **Process Improvements**
   - Were there inefficient patterns that could be streamlined?
   - Did you make mistakes that could be prevented with better guidance?
   - Are there templates or scripts that would help future work?

## Output Format

Provide a structured reflection:

```markdown
## Reflection Summary

### Key Learnings
- [What was learned during this conversation]

### Suggested Improvements

#### CLAUDE.md Updates
- [ ] [Specific addition or change]

#### Skill Updates
- [ ] [Skill name]: [What to add/change]

#### Documentation to Create/Update
- [ ] [File path]: [What to document]

#### Process Improvements
- [ ] [Improvement description]

### Immediate Actions
[List any changes you can make right now with user approval]
```

## Workflow

1. **Review the conversation** - Look at what was discussed, what worked, what didn't
2. **Identify patterns** - Find repeated corrections, preferences, or processes
3. **Categorize improvements** - Group by CLAUDE.md, Skills, Documentation, Process
4. **Use AskUserQuestion to propose each category** - Get user approval interactively
5. **Implement approved changes** - Only modify files after user confirmation

## Using AskUserQuestion for Proposals

After analyzing the conversation, use AskUserQuestion to propose improvements:

```typescript
// Example: Propose CLAUDE.md updates
AskUserQuestion({
  questions: [{
    question: "Should I add this guidance to CLAUDE.md: 'User Stories must be child work items, not embedded in descriptions'?",
    header: "CLAUDE.md",
    options: [
      { label: "Yes, add it", description: "Add to CLAUDE.md project instructions" },
      { label: "No, skip", description: "Don't add this guidance" },
      { label: "Modify first", description: "Let me review the wording" }
    ],
    multiSelect: false
  }]
});
```

### Question Categories

1. **CLAUDE.md Updates** - Propose specific additions/changes
2. **Skill Updates** - Propose skill modifications or new skills
3. **Documentation** - Propose new docs or updates
4. **Process Improvements** - Propose workflow changes

### Example Multi-Question Flow

```typescript
AskUserQuestion({
  questions: [
    {
      question: "Add 'AMP format required for all acceptance criteria' to CLAUDE.md?",
      header: "CLAUDE.md",
      options: [
        { label: "Yes", description: "Add this rule" },
        { label: "No", description: "Skip" }
      ],
      multiSelect: false
    },
    {
      question: "Create a new 'create-playwright-tests' skill?",
      header: "New Skill",
      options: [
        { label: "Yes, create it", description: "Create the skill now" },
        { label: "No", description: "Don't create" }
      ],
      multiSelect: false
    }
  ]
});
```

## Contributing to T-Minus-15 Plugin Marketplace

When you identify improvements that could benefit the T-Minus-15 agents or skills, offer to submit an issue to the plugin marketplace repository.

### What to Look For

- Agent improvements (Poppie, Pennie, Dannie, Ernie, Archie, Teddie, Ollie)
- Skill enhancements (epic, feature, user-story, e2e-tests, pr-review, reflect, tech-stack)
- New skills that would benefit T-Minus-15 users
- Bug fixes or corrections
- Documentation improvements

### Proposing Plugin Improvements

Use `AskUserQuestion` to ask if the user wants to submit an issue:

```typescript
AskUserQuestion({
  questions: [{
    question: "This improvement could benefit the T-Minus-15 plugins. Would you like to submit an issue to the marketplace repo?",
    header: "Contribute",
    options: [
      { label: "[ENHANCEMENT]", description: "Improve existing agent/skill functionality" },
      { label: "[BUG]", description: "Report a bug or incorrect behaviour" },
      { label: "[FEATURE]", description: "Request a new feature or capability" },
      { label: "Skip", description: "Don't submit an issue" }
    ],
    multiSelect: false
  }]
});
```

### Issue Prefixes

Always prefix issue titles with the appropriate tag:

| Prefix | Use When |
|--------|----------|
| `[ENHANCEMENT]` | Improving existing functionality (most common) |
| `[BUG]` | Reporting incorrect behaviour or errors |
| `[FEATURE]` | Requesting new agents, skills, or capabilities |

### Creating Plugin Issues

```bash
gh issue create --repo T-Minus-15/t-15-claude-plugins \
  --title "[ENHANCEMENT] Add validation guidance to user-story skill" \
  --body "$(cat <<'EOF'
## Summary
Add guidance for validating User Story acceptance criteria format.

## Current Behaviour
The user-story skill doesn't validate AMP format.

## Suggested Improvement
Add validation checklist to ensure:
- Each story has Acceptance criteria
- Measures are quantifiable
- Proof methods are defined

## Benefit
Helps ensure consistent, testable User Stories across projects.
EOF
)"
```

### Example Improvements to Suggest

| Agent/Skill | Example Enhancement |
|-------------|---------------------|
| Archie | Add new security checklist items |
| Teddie | Include visual regression testing guidance |
| tech-stack | Add alternative stacks for mobile/serverless |
| user-story | Improve AMP criteria examples |
| reflect | Add more reflection prompts |

## Contributing to T-Minus-15 Book

For improvements to the T-Minus-15 methodology itself (not the plugins), submit to the book repo:

```bash
gh issue create --repo T-Minus-15/book \
  --title "[ENHANCEMENT] Clarify sprint planning guidance" \
  --body "..."
```

### Contribution Checklist

Before contributing:
- [ ] Is this improvement general enough to benefit others?
- [ ] Have you chosen the correct prefix ([ENHANCEMENT], [BUG], [FEATURE])?
- [ ] Is the description clear and actionable?
- [ ] Have you specified which agent/skill is affected?

## Tips

- Be specific - don't just say "improve documentation", specify what to document
- Prioritize - focus on changes that will have the most impact
- Be concise - the reflection itself shouldn't be longer than necessary
- Use AskUserQuestion - always get approval via the tool before modifying files
- Group related changes - use multiSelect for related improvements
- Provide context - each option should explain what will happen
- Contribute back - improvements to shared templates benefit everyone
- Keep PRs simple - one focused change is easier to review and merge
