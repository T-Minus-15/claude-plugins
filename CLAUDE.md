# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

T-Minus-15 Claude Plugins is a suite of AI agents and skills implementing the T-Minus-15 DevOps methodology. This is a **plugin repository**, not a traditional application—there are no build/test/lint commands. Plugins are markdown documents with JSON manifests installed via Claude's `/plugin` system.

### Supported Platforms

T-Minus-15 supports both **GitHub** and **Azure DevOps**:
- **PRs**: `gh pr` (GitHub) / `az repos pr` (Azure DevOps)
- **Workflows**: GitHub Actions / Azure Pipelines
- **Issues**: GitHub Issues / Azure DevOps Work Items

## Architecture

### PDETO Lifecycle Agents (in `/agents/`)

| Agent | Role | Command | Depends On |
|-------|------|---------|------------|
| Poppie | Planner | `/plan` | epic |
| Pennie | Prepper | `/prep` | feature |
| Dannie | Designer | `/design` | user-story |
| Ernie | Engineer | `/engineer` | user-story, tech-stack |
| Archie | Architect | `/vet` | pr-review |
| Teddie | Tester | `/test` | e2e-tests |
| Ollie | Operator | `/operate` | — |

**Archie** owns architecture documentation in `/docs/*.adoc` and generates PDFs via `cd docs && ./generate-docs.sh`.

### Skills (in `/skills/`)

- **epic** - Create/edit Epics with T-Minus-15 metadata
- **feature** - Features with MoSCoW prioritization
- **user-story** - User Stories with AMP acceptance criteria (Acceptance/Measure/Proof)
- **e2e-tests** - Playwright E2E test management
- **pr-review** - Code review workflows
- **reflect** - Continuous improvement and contribution
- **tech-stack** - Default stack: Bun, Next.js 15, TypeScript 5, React 19, Tailwind 4, shadcn/ui

### Plugin Structure

```
agents/[name]/
├── .claude-plugin/plugin.json   # Manifest with dependencies
├── agents/[name].md             # Agent personality & capabilities
└── commands/[cmd].md            # Command definition

skills/[name]/
├── .claude-plugin/plugin.json   # Manifest
└── skills/[name].md             # Operations, templates, guidelines
```

### Marketplace Bundle

`/t-minus-15/.claude-plugin/plugin.json` - Master bundle installing all agents/skills together.

## Key Conventions

### Work Item Hierarchy

Epics → Features → User Stories → Tasks

User Stories are child items linked by reference, never embedded in parent descriptions.

### AMP Acceptance Criteria Format

All User Stories require:
- **Acceptance**: What must be true when complete
- **Measure**: Quantifiable metric
- **Proof**: How to validate

### Plugin Manifest Format

```json
{
  "name": "plugin-name",
  "version": "1.0.0",
  "description": "Description",
  "keywords": ["t-minus-15", "category"],
  "dependencies": { "required-skill": "^1.0.0" }
}
```

### Marketplace Hooks

The marketplace supports hooks for lifecycle events:

```json
{
  "hooks": {
    "conversationStart": {
      "dynamic": true,
      "context": {
        "git_repo": "git remote get-url origin 2>/dev/null",
        "git_branch": "git branch --show-current 2>/dev/null"
      },
      "message": "Welcome! Working on `{{git_repo}}` branch `{{git_branch}}`"
    }
  }
}
```

**Hook Properties:**
- `dynamic` - If true, runs context commands and interpolates `{{variables}}`
- `context` - Map of variable names to bash commands
- `message` - Template with `{{variable}}` placeholders

Available hooks:
- `conversationStart` - Displays a welcome message at conversation start (Poppie introduces the team)

## Testing Plugins Locally

```bash
/plugin marketplace add T-Minus-15/t-15-claude-plugins
/plugin install t-minus-15          # Install all
/plugin install poppie@t-minus-15   # Install single agent
```

## Contributing

Use the **reflect** skill to propose improvements. Issues go to:
- Plugin issues: `T-Minus-15/t-15-claude-plugins`
- Methodology issues: `T-Minus-15/book`

Prefix issues with: `[ENHANCEMENT]`, `[BUG]`, or `[FEATURE]`
