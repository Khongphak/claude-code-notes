# Real-World Examples: Next.js Project

> A complete working setup — CLAUDE.md, imported rule files, and Skills for a production Next.js 15 project.

## CLAUDE.md for a Next.js Project

Place this file at the project root: `my-app/CLAUDE.md`

```markdown
# Project Context
Next.js 15 app using App Router, TypeScript, and Tailwind CSS.
Connected to PostgreSQL via Prisma and uses Auth.js for authentication.

# Tech Stack
- Framework: Next.js 15 (App Router)
- Language: TypeScript (strict mode)
- Styling: Tailwind CSS v4
- DB: PostgreSQL via Prisma ORM
- Auth: Auth.js v5
- Validation: Zod
- State: Zustand (client), React Query (server state)
- Tests: Jest + React Testing Library, Playwright (E2E)

# Architecture Rules
- Default to Server Components. Add "use client" only when necessary.
- Fetch data in Server Components directly — avoid fetching in Client Components unless required.
- Use Server Actions for mutations (form submit, update, delete) instead of API routes.
- API routes (route.ts) are for third-party endpoints or webhooks only.

# Folder Structure
- app/           → pages and layouts (App Router convention)
- app/actions/   → all Server Actions
- components/ui/ → reusable UI components (no business logic)
- components/features/ → feature-specific components
- lib/           → utilities, helpers, constants
- lib/db.ts      → Prisma client singleton
- lib/validations/ → Zod schemas

# Coding Rules
- Every Server Action must validate input with Zod before proceeding.
- Never expose Prisma models directly to the client — select only the fields needed.
- All images must use next/image. Never use a raw <img> tag.
- All links must use next/link. Never use a raw <a> tag.
- No console.log in production. Use the logger from lib/logger.ts.
- Every route segment layout must include an Error Boundary.

# Git Convention
- Branches: feature/xxx, fix/xxx, chore/xxx
- Commits: "feat: ...", "fix: ...", "chore: ..."
- Never push directly to main. All changes go through a PR.
- PRs require at least one reviewer before merging.

# Testing Rules
@.claude/testing.md

# Security Rules
@.claude/security.md
```

## Sub-Files Imported by CLAUDE.md

### `.claude/testing.md` — Test rules

```markdown
# Testing Rules

## Unit & Integration (Jest + RTL)
- Every Server Action must have a unit test.
- Every component with logic must have an RTL test.
- Test files live alongside source: components/features/LoginForm.test.tsx
- Always mock next/navigation and next/headers in tests.
- Test behavior the user sees, not implementation details.

## E2E (Playwright)
- Every critical user flow must have a Playwright test.
- Examples: login, checkout, create/edit/delete content.
- Tests live in tests/e2e/ and run on CI before every deploy.
- Minimum 70% coverage for Server Actions.
```

### `.claude/security.md` — Security rules

```markdown
# Security Rules
- Every Server Action must verify the session before executing (never trust the client).
- Never log sensitive data (passwords, tokens, card numbers).
- All input must be sanitized through Zod before querying the database.
- Never write raw SQL — use Prisma exclusively.
- Variables prefixed with NEXT_PUBLIC_ are exposed to the client. Never put secrets in them.
- Content Security Policy must be enabled in next.config.ts.
```

## Skills (`.claude/commands/`)

### `pr.md` — Auto-generate PR descriptions

```markdown
You are a senior Next.js developer on this team.

Read the git diff for this branch and generate a PR description in this format:

## What Changed
(Summarize what was changed and why)

## Type of Change
- [ ] New feature
- [ ] Bug fix
- [ ] Refactor
- [ ] Performance improvement

## How to Test
(Step-by-step testing instructions, including URLs to open)

## Breaking Changes
(List any, or state "None")

## Checklist
- [ ] Tests added/updated
- [ ] No console.log left
- [ ] Server/Client components used correctly
- [ ] Prisma migration included (if schema changed)
- [ ] No secrets in NEXT_PUBLIC_ vars
```

Usage: type `/pr` in Claude Code.

### `component.md` — Create a new component

```markdown
Create a Next.js component named $ARGUMENTS following this project's conventions.

Ask yourself first:
- Does it need interactivity? → If no → Server Component
- Does it need useState/useEffect/event handlers? → Client Component

File location:
- Reusable UI → components/ui/$ARGUMENTS.tsx
- Feature-specific → components/features/$ARGUMENTS.tsx

Every component must include:
1. A TypeScript interface for props
2. Named export (not default export)
3. A paired test file (.test.tsx)
```

Usage: type `/component ProductCard`

### `action.md` — Create a new Server Action

```markdown
Create a Server Action for $ARGUMENTS in app/actions/ following this pattern:

1. File: app/actions/$ARGUMENTS.ts
2. Start with "use server"
3. Validate input with Zod before any logic
4. Check session before every mutation
5. Always return { success, data?, error? } — never throw to the client
6. Call revalidatePath or revalidateTag after a successful mutation
7. Create a unit test alongside the action file
```

Usage: type `/action createProduct`

### `review.md` — Review code before merging

```markdown
Review the diff for this branch in this order:

1. Next.js-specific: Are Server/Client components used correctly? Any unnecessary "use client"?
2. Security: Do Server Actions check auth? Any exposed secrets? Is Zod validation complete?
3. Performance: Any duplicate fetches? Are images using next/image? Missing Suspense boundaries?
4. Code quality: Does everything follow the rules in CLAUDE.md?

Summarize findings as:
🔴 Critical (must fix before merge)
🟡 Warning (should fix)
🟢 Suggestion (fix if convenient)
```

Usage: type `/review` before pushing a PR.

## Recommended Folder Structure

```
my-app/
├── CLAUDE.md                          ← team-wide rules
├── .claude/
│   ├── testing.md                     ← test rules (imported by CLAUDE.md)
│   ├── security.md                    ← security rules (imported by CLAUDE.md)
│   └── commands/
│       ├── pr.md                      ← /pr
│       ├── component.md               ← /component
│       ├── action.md                  ← /action
│       └── review.md                  ← /review
├── app/
│   ├── actions/                       ← all Server Actions
│   └── ...
├── components/
│   ├── ui/                            ← reusable UI
│   └── features/                      ← feature-specific
└── lib/
    ├── db.ts                          ← Prisma singleton
    ├── logger.ts
    └── validations/                   ← Zod schemas
```

## Daily Workflow

| Task | Command |
|------|---------|
| Add a new component | `/component ProductCard` |
| Add a feature with DB changes | `/action createProduct` |
| Before pushing | `/review` to let Claude scan the diff |
| Opening a PR | `/pr` then copy the output to GitHub |

## Common Pitfalls

- **Copying this CLAUDE.md verbatim without adapting it** — A good CLAUDE.md reflects your actual project. Remove any section that does not apply to your stack, or Claude will follow irrelevant rules.

- **Putting secrets in `NEXT_PUBLIC_` variables** — These are bundled into client-side JavaScript. Anyone who opens browser DevTools can read them.

- **Adding `"use client"` to every file "just to be safe"** — Server Components are the better default for performance. Unnecessary `"use client"` eliminates server-side rendering and increases bundle size.

- **Running `/review` after pushing** — The `/review` Skill is designed to catch issues before the PR is open. Running it after means another push and another review cycle.

- **Writing raw SQL instead of using Prisma** — Even when it looks simpler, raw SQL bypasses Prisma's type safety and introduces SQL injection risk. Use `$queryRaw` only when Prisma genuinely cannot express the query.

- **Not updating Skills when project conventions change** — Skills that reference old folder paths or deprecated patterns will produce wrong output. Treat Skills as code — update them during every major refactor.

## Sources

- [Anthropic Claude Code Documentation](https://docs.claude.com/en/docs/claude-code/overview)
- Personal experimentation (June 2026)

---

> Previous: [Skills vs CLAUDE.md](./03-skills-vs-claude-md.md)
