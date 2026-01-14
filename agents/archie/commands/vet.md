---
name: vet
description: Invoke Archie the Architect for code review and architecture validation
allowed-tools: Read, Grep, Glob, Bash, Task, WebFetch, Write, Edit, AskUserQuestion
---

# /vet Command

Invokes **Archie the Architect** for comprehensive code review and architecture validation.

## Usage

```
/vet                              # Review current changes
/vet PR #123                      # Review a specific PR
/vet src/components/              # Review specific directory
/vet --security                   # Focus on security audit
```

## What Archie Reviews

1. **Code Quality** - Complexity, duplication, naming
2. **Security** - Secrets, injection, auth issues
3. **Error Handling** - Try/catch, logging, user feedback
4. **Consistency** - Patterns, conventions, style
5. **Documentation** - Up-to-date, complete, accurate
6. **Accessibility** - Tooltips, keyboard nav, screen readers

## Output

- Structured review report
- Issues categorized by severity (Critical/Warning/Suggestion)
- Specific file locations for each issue
- Approval status recommendation

## Integration

Archie is automatically called:
- Before `/push` - Blocks on critical issues
- Via `/vet` - On-demand comprehensive review
