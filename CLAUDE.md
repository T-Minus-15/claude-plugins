# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

T-Minus-15 Claude Plugins implements **'T-Minus-15: Secrets of an Elite DevOps Team'** — AI agents for the complete software development lifecycle. This is a **plugin repository**, not a traditional application—there are no build/test/lint commands.

Book: https://github.com/T-Minus-15/book

### Supported Platforms

- **GitHub**: `gh pr`, GitHub Issues, GitHub Actions
- **Azure DevOps**: `az repos pr`, Work Items, Azure Pipelines

## Repository Structure

```
/t-minus-15-team/      # Plugin folder
  plugin.json          # Declares agents/commands/skills paths
  agents/*.md          # Agent definitions (poppie.md, pennie.md, etc.)
  commands/*.md        # Slash commands (plan.md, prep.md, etc.)
  skills/*.md          # Skill definitions (epic.md, feature.md, etc.)
/.claude-plugin/       # Marketplace configuration
```

## Agents

| Agent | Role | Command | Phase |
|-------|------|---------|-------|
| Poppie | Planner | `/plan` | Planning & orchestration |
| Pennie | Prepper | `/prep` | Requirements & backlog |
| Dannie | Designer | `/design` | UX/UI & brand guidelines |
| Ernie | Engineer | `/engineer` | Code implementation |
| Archie | Architect | `/vet` | Code review & architecture |
| Teddie | Tester | `/test` | E2E tests & QA |
| Ollie | Operator | `/operate` | Deployment & monitoring |
| Connie | Copywriter | `/copy` | Documentation quality |

## Skills

**Work Items:** epic, feature, user-story, bug, enhancement, task, risk, issue, question

**Development:** e2e-tests, pr-review, tech-stack, documentation, brand-guidelines, wireframe, lean-business-case, reflect

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

### Marketplace Schema (`.claude-plugin/marketplace.json`)

The marketplace manifest requires these fields:

```json
{
  "name": "marketplace-name",
  "owner": {
    "name": "Owner Name",
    "email": "owner@example.com"
  },
  "plugins": [
    {
      "name": "plugin-name",
      "description": "Plugin description",
      "version": "1.0.0",
      "source": {
        "source": "github",
        "repo": "owner/repo-name",
        "path": "path/to/plugin"
      }
    }
  ]
}
```

**Required Fields:**
- `name` - Top-level marketplace name (string, required)
- `owner` - Object with `name` (required) and optional `email`
- `plugins` - Array of plugin objects

**Plugin Object Fields:**
- `name` - Plugin identifier (kebab-case)
- `description` - Human-readable description
- `version` - Semver version
- `source` - Source object (see below)

**Source Formats:**

Relative path (no `../` traversal allowed):
```json
{ "source": "./plugins/my-plugin" }
```

GitHub repository:
```json
{
  "source": {
    "source": "github",
    "repo": "owner/repo-name",
    "path": "path/within/repo"
  }
}
```

Git URL:
```json
{
  "source": {
    "source": "url",
    "url": "https://gitlab.com/team/plugin.git"
  }
}
```

**Hook Properties (optional):**
- `dynamic` - If true, runs context commands and interpolates `{{variables}}`
- `context` - Map of variable names to bash commands
- `message` - Template with `{{variable}}` placeholders

Available hooks:
- `conversationStart` - Displays a welcome message at conversation start (Poppie introduces the team)

## Installation

```bash
/plugin marketplace add T-Minus-15/claude-plugins
/plugin install t-minus-15
```

## Contributing

Use the **reflect** skill to propose improvements. Issues go to:
- Plugin issues: `T-Minus-15/claude-plugins`
- Methodology issues: `T-Minus-15/book`

Prefix issues with: `[ENHANCEMENT]`, `[BUG]`, or `[FEATURE]`
