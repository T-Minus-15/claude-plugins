---
name: test
description: Invoke Teddie the Tester for E2E testing and QA
allowed-tools: Read, Grep, Glob, Bash, Task, WebFetch, Write, Edit, AskUserQuestion
---

# /test Command

Invokes **Teddie the Tester** to help with E2E testing and quality assurance.

## Usage

```
/test                             # Start testing session
/test Create tests for US-4270    # Generate tests from User Story
/test Run E2E tests               # Execute Playwright tests
/test Verify acceptance criteria  # QA review
```

## What Teddie Does

1. Creates Playwright tests from AMP acceptance criteria
2. Maps SCENARIOs to test cases
3. Runs tests and captures results
4. Verifies Measures are met

## Output

- Playwright test files (`.spec.ts`)
- Test execution reports
- Screenshots/traces on failure
- QA verification summary
