# T-Minus-15 Claude Plugins

Persona-based AI agents for the complete software development lifecycle, following the [T-Minus-15](https://github.com/T-Minus-15/book) methodology.

## Meet the Team

| Agent | Role | Phase | Description |
|-------|------|-------|-------------|
| **Poppie** | Planner | Planning | Creates Epics with full T-Minus-15 metadata |
| **Pennie** | Prepper | Prep | Breaks down Features and User Stories |
| **Dannie** | Designer | Design | Handles UX/UI design and brand guidelines |
| **Ernie** | Engineer | Engineer | Implements code and builds features |
| **Archie** | Architect | Review | Code review, security audit, architecture validation |
| **Teddie** | Tester | Test | Generates and runs E2E tests |
| **Ollie** | Operator | Operate | Manages deployment and operations |

## Installation

### Install Everything

```bash
/plugin marketplace add T-Minus-15/t-15-claude-plugins
/plugin install t-minus-15
```

### Install Individual Agents

```bash
/plugin install poppie@t-minus-15    # Planning agent
/plugin install pennie@t-minus-15    # Prep agent
/plugin install archie@t-minus-15    # Code review agent
/plugin install teddie@t-minus-15    # Testing agent
```

Installing an agent automatically installs its required skills.

### Install Skills Only

```bash
/plugin install epic@t-minus-15
/plugin install feature@t-minus-15
/plugin install user-story@t-minus-15
/plugin install e2e-tests@t-minus-15
/plugin install pr-review@t-minus-15
/plugin install reflect@t-minus-15
/plugin install tech-stack@t-minus-15
```

## Usage

### Slash Commands

Each agent provides a slash command:

```bash
/plan      # Invoke Poppie for Epic planning
/prep      # Invoke Pennie for Feature/Story prep
/design    # Invoke Dannie for design work
/engineer  # Invoke Ernie for engineering tasks
/vet       # Invoke Archie for code review
/test      # Invoke Teddie for testing
/operate   # Invoke Ollie for operations
```

### Skills

Skills are invoked via the standard skill mechanism:

```bash
/epic          # Create/edit Epics
/feature       # Create/edit Features
/user-story    # Create/edit User Stories
/e2e-tests     # Create/run Playwright tests
/pr-review     # Review pull requests
/reflect       # Reflect on improvements
/tech-stack    # Default web app technology stack
```

## Agent Dependencies

| Agent | Required Skills |
|-------|----------------|
| Poppie | `epic` |
| Pennie | `feature`, `user-story` |
| Dannie | `user-story` |
| Ernie | `tech-stack` |
| Archie | `pr-review`, `tech-stack` |
| Teddie | `e2e-tests` |
| Ollie | `reflect` |

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

## About T-Minus-15

T-Minus-15 is an open-source DevOps methodology that provides practical guidance for development teams. The name comes from the phases: **P**REP-**D**ESIGN-**E**NGINEER-**T**EST-**O**PERATE.

Learn more: [T-Minus-15 Book](https://github.com/T-Minus-15/book)

## License

MIT
