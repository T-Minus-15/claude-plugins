---
name: tech-stack
description: Default technology stack for web applications optimised for AI-assisted development workflows
allowed-tools: AskUserQuestion
---

# Technology Stack Skill (T-Minus-15)

This skill defines the default technology stack for new web application projects, optimised for AI-assisted development workflows.

## Why This Stack?

AI coding tools work best when they can iterate quickly and get immediate feedback. These choices prioritise:
- **Fast installs** - Reduced waiting time between iterations
- **Instant hot reload** - Immediate feedback on changes
- **Strong type safety** - AI generates correct code first time

## Default Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| **Bun** | Latest | Package manager (5-10x faster than npm) |
| **Next.js** | 15 | App Router with Fast Refresh |
| **TypeScript** | 5 (strict mode) | Type safety for AI accuracy |
| **React** | 19 | UI library with Server Components |
| **Tailwind CSS** | 4 | Utility-first CSS (AI-friendly) |
| **shadcn/ui** | Latest | Copy-paste components we own |
| **Chart.js** | Latest | Integrated reporting |
| **Vitest** | Latest | Fast unit testing |
| **Playwright** | Latest | Reliable E2E testing |
| **NextAuth.js** | v5 | Flexible auth (Azure AD, GitHub, etc.) |

## Usage Guidelines

### Always Confirm First

**IMPORTANT:** Use `AskUserQuestion` to confirm the technology approach before recommending or implementing. Example:

```
AskUserQuestion:
  question: "For this web application, shall we use our default T-Minus-15 stack?"
  options:
    - "Yes, use default stack (Next.js 15, TypeScript, Tailwind, shadcn/ui)"
    - "Modify stack (let me specify)"
    - "Use existing project technologies"
```

### When to Use Defaults

Use the default stack when:
- Starting a new web application project
- No existing technology constraints
- User hasn't specified preferences
- AI-assisted development is the primary workflow

### When to Deviate

Consider alternatives when:
- User explicitly requests different technologies
- Project has existing tech stack to maintain
- Enterprise/client constraints require specific technologies
- Project type doesn't suit the stack (mobile app, CLI tool, etc.)
- Legacy integration requirements

## Stack Details

### Bun (Package Manager)

```bash
# Install dependencies
bun install

# Run dev server
bun dev

# Run tests
bun test
```

**Why:** 5-10x faster installs than npm. AI workflows involve frequent dependency changes - speed matters.

### Next.js 15 (Framework)

```bash
# Create new project
bunx create-next-app@latest my-app --typescript --tailwind --app
```

**Key features:**
- App Router for modern patterns
- Fast Refresh for instant feedback
- Server Components for performance
- Built-in API routes

### TypeScript 5 (Strict Mode)

```json
// tsconfig.json
{
  "compilerOptions": {
    "strict": true,
    "noUncheckedIndexedAccess": true
  }
}
```

**Why:** Strict mode catches errors at compile time. AI generates more accurate code with strong types.

### Tailwind CSS 4

```bash
# Already included with create-next-app --tailwind
```

**Why:** Utility classes are predictable and AI tools handle them well. No context-switching to CSS files.

### shadcn/ui (Components)

```bash
# Initialize
bunx shadcn@latest init

# Add components
bunx shadcn@latest add button card dialog
```

**Why:** We own the code. Components are copied into our project, not imported from node_modules. Full customisation control.

### Testing Stack

```bash
# Unit tests with Vitest
bun add -d vitest @testing-library/react

# E2E tests with Playwright
bun add -d @playwright/test
bunx playwright install
```

### NextAuth.js v5 (Authentication)

```bash
bun add next-auth@beta
```

**Supports:**
- Azure AD / Entra ID
- GitHub
- Google
- Credentials
- Custom providers

## Project Structure

```
my-app/
├── app/                    # Next.js App Router
│   ├── layout.tsx
│   ├── page.tsx
│   └── api/               # API routes
├── components/
│   └── ui/                # shadcn/ui components
├── lib/                   # Utilities
├── tests/
│   ├── unit/             # Vitest tests
│   └── e2e/              # Playwright tests
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

## Quick Start Template

When starting a new project with this stack:

```bash
# 1. Create Next.js app with TypeScript and Tailwind
bunx create-next-app@latest my-app --typescript --tailwind --app --src-dir

# 2. Navigate to project
cd my-app

# 3. Initialize shadcn/ui
bunx shadcn@latest init

# 4. Add common components
bunx shadcn@latest add button card input label dialog

# 5. Add testing
bun add -d vitest @testing-library/react @playwright/test

# 6. Add auth (if needed)
bun add next-auth@beta

# 7. Start development
bun dev
```

## Tips

- **Don't mix package managers** - Stick with Bun throughout
- **Use strict TypeScript** - It helps AI generate better code
- **Prefer shadcn/ui** - Over other component libraries we don't control
- **Test early** - Set up Vitest and Playwright from the start
- **Confirm with user** - Always ask before assuming the stack
