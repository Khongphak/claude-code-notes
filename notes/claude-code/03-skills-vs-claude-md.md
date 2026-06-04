# Custom Slash Commands (Skills)

> Skills are reusable prompts you invoke with `/command-name` — the practical difference between always-on rules and on-demand automation.

## What Are Skills?

A Skill is a `.md` file you create to serve as a reusable prompt for tasks you repeat often.

- Invoked in Claude Code by typing `/filename`
- Unlike CLAUDE.md — which applies to every session automatically — Skills are called only when you need them

> Think of CLAUDE.md as the employee handbook (always in effect) and Skills as SOPs you run on demand.

## Creating Skills

### Scope options

| Scope | Location | Who can use it |
|-------|----------|----------------|
| Project | `.claude/commands/<name>.md` | Anyone who clones the repo |
| User | `~/.claude/commands/<name>.md` | You, across all your projects |

### Passing arguments

Skills accept input via `$ARGUMENTS`:

```markdown
Review PR #$ARGUMENTS for security issues
```

Invoked with: `/security-review 42`

## Real-World Examples

### `/pr-description`

Instead of writing PR context manually every time:
- Reads `git diff` and generates a PR description automatically
- Includes summary, test plan, and breaking changes section

### `/security-review`

Run before every merge:
- Scans the current diff for OWASP Top 10 vulnerabilities, exposed secrets, and SQL injection

### `/onboard`

For new team members:
- Reads the codebase and generates a summary of architecture, conventions, and gotchas to know

### `/migrate $ARGUMENTS`

For database migrations — e.g., `/migrate add_user_table`:
- Creates the migration file, rollback script, and seed data together in one step

## Skills vs CLAUDE.md

| Aspect | CLAUDE.md | Skill |
|--------|-----------|-------|
| When it runs | Every session, automatically | Only when you type `/name` |
| Purpose | Rules, context, conventions | Ready-made prompt for repeated tasks |
| Analogy | Employee handbook | Macro / SOP |
| Example | "Never push directly to main" | `/pr-description` generates a PR description |

- **CLAUDE.md** = "What Claude must always know"
- **Skill** = "What Claude must do when I ask"

> If a deploy process has 10 steps, put it in a Skill — not in CLAUDE.md. CLAUDE.md is read on every session, even when you are just fixing a typo.

## Common Pitfalls

- **Placing a Skill in the wrong scope** — A project Skill meant for your team must be in `.claude/commands/` and committed to git. If it lives in `~/.claude/commands/`, teammates will not have access to it.

- **Putting multi-step processes into CLAUDE.md** — A 10-step deploy process in CLAUDE.md means Claude reads all 10 steps on every session, even for a trivial fix. Move processes like this into a Skill.

- **Forgetting to pass `$ARGUMENTS`** — Typing `/migrate` without a table name forces Claude to guess. Design Skills to either prompt for missing arguments or include a sensible default example.

- **Building one Skill that does too much** — A single Skill that reviews code, writes PR descriptions, and runs security scans is hard to debug when the output is wrong. Keep Skills focused and single-purpose.

- **Not updating Skills when conventions change** — A Skill referencing an old folder structure or deprecated pattern will produce incorrect output. Treat Skills as code: update them during every major refactor.

## Sources

- [Anthropic Claude Code Documentation — Slash Commands](https://docs.claude.com/en/docs/claude-code/slash-commands)
- Personal experimentation (June 2026)

---

> Previous: [CLAUDE.md Best Practices](./02-claude-md-best-practices.md) | Next: [Real-World Examples](./04-claude-example.md)
