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

## Repository Structure

```
/*.md                  # Agent definitions (poppie.md, pennie.md, etc.)
/skills/*.md           # Skill definitions
/commands/*.md         # Slash command definitions
/.claude-plugin/       # Plugin marketplace config
```

## Platforms

Supports both **GitHub** and **Azure DevOps**:
- PRs: `gh pr` / `az repos pr`
- Work Items: GitHub Issues / Azure DevOps Work Items
- Pipelines: GitHub Actions / Azure Pipelines

## License

MIT
