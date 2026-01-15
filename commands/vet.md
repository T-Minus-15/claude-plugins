---
name: vet
description: Invoke Archie the Architect for code review and architecture validation
allowed-tools: Read, Grep, Glob, Bash, Task, WebFetch, Write, Edit, AskUserQuestion
---

# /vet Command

Invokes **Archie the Architect** for comprehensive code review, architecture validation, and documentation management.

## Usage

```
/vet                              # Review current changes
/vet PR #123                      # Review GitHub PR
/vet ADO #456                     # Review Azure DevOps PR
/vet src/components/              # Review specific directory
/vet --pre-push                   # Full pre-push gate check (REQUIRED before push)
/vet --project-setup              # Verify linters, formatters, CI/CD workflows configured
/vet --security                   # Focus on security audit
/vet --docs                       # Review/update architecture docs
/vet --generate-pdf               # Generate PDF from docs/*.adoc
```

**Platform Commands:**
- GitHub: `gh pr view #123`, `gh pr diff #123`
- Azure DevOps: `az repos pr show --id 456`, `az repos pr list`

## Pre-Push Gate (Mandatory)

**All code MUST pass `/vet --pre-push` before pushing to the repository:**

1. No secrets in code (API keys, tokens, passwords)
2. Linting passes (`npm run lint`)
3. Formatting passes (Prettier/format check)
4. Code follows best practices
5. No unnecessary/dead code
6. Code is simplified where possible
7. Existing utilities reused

## Project Setup Verification (`--project-setup`)

Checks that the project has proper infrastructure:
- Linters configured (`.eslintrc.js`, `eslint.config.js`)
- Formatters configured (`.prettierrc`, `prettier.config.js`)
- `README.md` documents lint/format commands
- CI/CD workflows run checks on PRs (GitHub Actions or Azure Pipelines)

## What Archie Reviews

1. **Project Infrastructure** - Linters, formatters, CI/CD workflows configured
2. **Architecture Docs** - Create/review `/docs/*.adoc` files, Mermaid diagrams
3. **Code Quality** - Simplify, remove dead code, check for reuse opportunities
4. **Linting & Formatting** - ESLint, Prettier must pass
5. **Security** - Secrets, injection, auth issues (BLOCKS on secrets)
6. **Error Handling** - Try/catch, logging, user feedback
7. **Consistency** - Patterns, conventions, style
8. **Documentation** - README.md with lint/format commands, up-to-date docs
9. **Accessibility** - Tooltips, keyboard nav, screen readers

## PDF Generation

Generate architecture PDFs from AsciiDoc sources:

```bash
cd docs && ./generate-docs.sh
```

Requires Mermaid CLI: `npm install -g @mermaid-js/mermaid-cli`

## Output

- Structured review report
- Issues categorized by severity (Critical/Warning/Suggestion)
- Specific file locations for each issue
- Approval status recommendation

## Integration

Archie is automatically called:
- Before `/push` - Blocks on critical issues
- Via `/vet` - On-demand comprehensive review
