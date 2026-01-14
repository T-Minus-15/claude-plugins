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

## Contributing to Marketplace Repos

When improvements apply to shared/marketplace repositories (e.g., T-Minus-15, skill templates), offer to contribute back:

### Identifying Marketplace Improvements

Look for improvements that would benefit others:
- T-Minus-15 process template updates (https://github.com/BenGWeeks/T-Minus-15)
- Skill templates that could be shared
- Documentation patterns others could use

### Proposing Contributions

Use AskUserQuestion to offer contribution options:

```typescript
AskUserQuestion({
  questions: [{
    question: "This improvement to AMP format could benefit the T-Minus-15 template. How would you like to contribute?",
    header: "Contribute",
    options: [
      { label: "Create Issue", description: "Open a GitHub issue describing the improvement" },
      { label: "Create PR", description: "Create a simple PR with the change" },
      { label: "Local only", description: "Keep this change local, don't contribute" }
    ],
    multiSelect: false
  }]
});
```

### Creating Issues

When creating an issue:
1. Use `gh issue create` command
2. Provide clear title describing the improvement
3. Include context on why this helps
4. Reference any relevant examples

```bash
gh issue create --repo BenGWeeks/T-Minus-15 \
  --title "Add Gherkin format requirement to AMP acceptance criteria" \
  --body "$(cat <<'EOF'
## Suggestion
Add explicit guidance that acceptance criteria should use Gherkin format (GIVEN/WHEN/THEN).

## Rationale
- Makes criteria verifiable by development agents
- Provides consistent structure across all User Stories
- Enables automated test generation

## Example
```gherkin
SCENARIO: User logs in successfully
GIVEN I am on the login page
WHEN I enter valid credentials
THEN I am redirected to the dashboard
```
EOF
)"
```

### Creating PRs

When creating a PR, keep it **simple and focused**:

1. **One change per PR** - Don't bundle multiple improvements
2. **Small diff** - Easy to review means faster merge
3. **Clear description** - Explain what and why
4. **No scope creep** - Resist adding "while I'm here" changes

```bash
# Fork, clone, branch, make change, then:
gh pr create --repo BenGWeeks/T-Minus-15 \
  --title "Add Gherkin format guidance to user-story-metadata" \
  --body "$(cat <<'EOF'
## Summary
Adds explicit guidance that acceptance criteria should use Gherkin syntax.

## Changes
- Added Gherkin keyword reference to user-story-metadata.adoc
- Added example scenario format

## Why
Makes acceptance criteria verifiable and enables test automation.
EOF
)"
```

### Contribution Checklist

Before contributing:
- [ ] Is this improvement general enough to benefit others?
- [ ] Is the change small and focused?
- [ ] Does it follow the repo's contribution guidelines?
- [ ] Is the description clear and concise?

## Tips

- Be specific - don't just say "improve documentation", specify what to document
- Prioritize - focus on changes that will have the most impact
- Be concise - the reflection itself shouldn't be longer than necessary
- Use AskUserQuestion - always get approval via the tool before modifying files
- Group related changes - use multiSelect for related improvements
- Provide context - each option should explain what will happen
- Contribute back - improvements to shared templates benefit everyone
- Keep PRs simple - one focused change is easier to review and merge
