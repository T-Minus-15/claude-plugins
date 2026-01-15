---
name: checkpoint
description: Poppie reviews current progress, summarizes what's been done, identifies blockers, and suggests next steps. Use periodically during long sessions or when switching context.
allowed-tools: Bash, Read, Glob, Grep
---

# Checkpoint Skill

Poppie pauses to review progress and ensure the team is on track.

## When to Use

- After completing a significant piece of work
- Before switching to a different task
- When the user asks "where are we?" or "what's next?"
- Periodically during long sessions
- When resuming after a break

## Gather Context

```bash
# Recent git activity
git log --oneline -10 2>/dev/null
git status --short 2>/dev/null

# Check for uncommitted work
git diff --stat 2>/dev/null
```

## Checkpoint Review

Provide a brief summary covering:

### 1. What We've Done
- List completed tasks/changes in this session
- Reference any commits made

### 2. Current State
- What files are modified but uncommitted?
- Are there any failing tests or build issues?
- What branch are we on?

### 3. Blockers or Concerns
- Any issues that need attention?
- Questions that need answering?
- Dependencies waiting on others?

### 4. Suggested Next Steps
- What should we work on next?
- Any tasks that were started but not finished?
- Recommend whether to commit, test, or continue

## Tone

Be concise and action-oriented. This is a quick status check, not a detailed report. Use bullet points. End with a clear recommendation for what to do next.

## Example Output

```
## Checkpoint

**Done:**
- Created user authentication module
- Added login/logout endpoints
- Wrote unit tests for auth service

**Current State:**
- Branch: `feature/auth`
- 3 files modified, not yet committed
- All tests passing

**Next Steps:**
1. Commit current changes
2. Create PR for review
3. Start on password reset feature

Ready to commit? Or continue with password reset?
```
