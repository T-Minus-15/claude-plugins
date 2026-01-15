# T-Minus-15 Claude Plugins

AI agents implementing **'T-Minus-15: Secrets of an Elite DevOps Team'** — the Prep → Design → Engineer → Test → Operate methodology with quality gates, structured work items (Epics, Features, User Stories with AMP criteria), and cross-functional collaboration.

Learn more: [T-Minus-15 Book](https://github.com/T-Minus-15/book)

## Meet the Team

| Agent | Role | Command | Phase |
|-------|------|---------|-------|
| **Poppie** | Planner | `/plan` | Planning & orchestration |
| **Pennie** | Prepper | `/prep` | Requirements & backlog |
| **Dannie** | Designer | `/design` | UX/UI & brand guidelines |
| **Ernie** | Engineer | `/engineer` | Code implementation |
| **Archie** | Architect | `/vet` | Code review & architecture |
| **Teddie** | Tester | `/test` | E2E tests & QA |
| **Ollie** | Operator | `/operate` | Deployment & monitoring |
| **Connie** | Copywriter | `/copy` | Documentation quality |

## Installation

```bash
/plugin marketplace add T-Minus-15/claude-plugins
/plugin install t-minus-15
```

## Skills

### Work Items
| Skill | Description |
|-------|-------------|
| `/epic` | Epics with lean business case |
| `/feature` | Features with MoSCoW prioritization |
| `/user-story` | User Stories with AMP acceptance criteria |
| `/bug` | Bug reports |
| `/enhancement` | Enhancement requests |
| `/task` | Task work items |
| `/risk` | Risk management |
| `/issue` | Issue tracking |
| `/question` | Questions requiring answers |

### Development
| Skill | Description |
|-------|-------------|
| `/e2e-tests` | Playwright E2E test management |
| `/pr-review` | Code review workflows |
| `/tech-stack` | Default technology stack |
| `/documentation` | Standard docs structure |
| `/brand-guidelines` | Extract/create brand guidelines |
| `/wireframe` | ASCII wireframe components |
| `/lean-business-case` | Business case for Epics |
| `/reflect` | Continuous improvement |

## Default Technology Stack

The `tech-stack` skill defines our default stack for web applications, optimised for AI-assisted development:

| Technology | Purpose |
|------------|---------|
| Bun | Package manager (5-10x faster than npm) |
| Next.js 15 | App Router with Fast Refresh |
| TypeScript 5 | Strict mode for AI accuracy |
| React 19 | Server Components |
| Tailwind CSS 4 | Utility-first CSS |
| shadcn/ui | Customisable components |
| Vitest + Playwright | Fast testing |
| NextAuth.js v5 | Flexible authentication |

*Note: Agents will confirm technology choices before implementing.*

## Optional Enhancements

These plugins and MCP servers enhance agent capabilities but are not required:

### Plugins

| Plugin | Agents | Description |
|--------|--------|-------------|
| `frontend-design` | Dannie, Ernie | Production-grade frontend interfaces with high design quality |
| `code-simplifier` | Ernie, Archie | Code simplification and quality improvements |

Install with:
```bash
/plugin install frontend-design
/plugin install code-simplifier
```

### MCP Servers

| MCP Server | Agents | Description |
|------------|--------|-------------|
| Playwright | Teddie | Interactive browser automation for E2E testing |

Install Playwright MCP:
```bash
npx @anthropic/claude-code mcp add playwright -- npx @anthropic/mcp-server-playwright
```

*Agents will prompt you to install these when relevant functionality is needed.*

## Repository Structure

```
/t-minus-15-team/      # Plugin folder
  plugin.json          # Plugin configuration
  agents/*.md          # Agent definitions
  commands/*.md        # Slash commands
  skills/*.md          # Skill definitions
/.claude-plugin/       # Marketplace config
```

### Agents

| Agent | Command | Description |
|-------|---------|-------------|
| Poppie the Planner | `/plan` | Planning & orchestration |
| Pennie the Prepper | `/prep` | Requirements & backlog |
| Dannie the Designer | `/design` | UX/UI & brand guidelines |
| Ernie the Engineer | `/engineer` | Code implementation |
| Archie the Architect | `/vet` | Code review & architecture |
| Teddie the Tester | `/test` | E2E tests & QA |
| Ollie the Operator | `/operate` | Deployment & monitoring |
| Connie the Copywriter | `/copy` | Documentation quality |

## Platforms

Supports both **GitHub** and **Azure DevOps**:
- PRs: `gh pr` / `az repos pr`
- Work Items: GitHub Issues / Azure DevOps Work Items
- Pipelines: GitHub Actions / Azure Pipelines

## License

MIT
