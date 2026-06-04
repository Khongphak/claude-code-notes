# CLAUDE.md Best Practices

> How to write effective CLAUDE.md files — covering the memory hierarchy, writing rules, and token efficiency.

## What is CLAUDE.md?

Without CLAUDE.md, you are sending Claude into a project with no briefing. It defines your architecture, coding standards, and known constraints — functioning as Claude Code's persistent memory system for every session.

## Memory Hierarchy

Claude Code reads CLAUDE.md files from multiple locations. When rules conflict, higher priority wins.

| Priority | Scope | Location |
|----------|-------|----------|
| 1 (Highest) | Organization — all users | `C:\Program Files\ClaudeCode\CLAUDE.md` (Windows) |
| 2 | User — all your projects | `~/.claude/CLAUDE.md` |
| 3 | Project — team-shared via git | `./CLAUDE.md` or `./.claude/CLAUDE.md` |
| 4 (Lowest) | Local — just you, this project | `./CLAUDE.local.md` |

> Add `CLAUDE.local.md` to `.gitignore` — it holds personal preferences that should not affect the rest of the team.

Claude can import other files using `@filename`, keeping the root file clean while pulling in detailed rules from separate files:

```markdown
@testing.md
@security.md
```

## Writing Best Practices

### Keep it short

Stay under 300 lines. The longer the file, the less accurately Claude follows it. If content grows, split it into separate files and import them with `@filename`.

### Never use `/claude init` as-is

The `init` command generates a starting point, not a finished product. Always review and prune what it generates before committing. Treat the output as a draft.

### Do not include formatter or linter rules

Avoid putting ESLint, Prettier, or similar rules in CLAUDE.md — they waste tokens on every session. Use the actual VS Code extensions or CLI tools directly instead.

### The 3 core sections every CLAUDE.md needs

1. **One-line project description** — what this codebase does
2. **Common commands** — `npm run dev`, `npm test`, `docker compose up`, etc.
3. **Non-obvious warnings** — constraints, gotchas, and decisions not visible from reading the code

### Use conditional rules for rare cases

For rules that only apply to specific file types, create a separate file in a `rules/` directory with a `paths:` YAML frontmatter:

```markdown
---
paths:
  - "**/*.spec.ts"
---

# Testing Guidelines
...
```

This prevents Claude from reading rare-case rules on every session, saving tokens.

### Prioritize by importance

- Put the most critical rules at the very top
- Use `IMPORTANT` or `YOU MUST` in capitals to flag constraints Claude must not ignore

## Common Pitfalls

- **Writing more than 300 lines** — Claude's instruction-following accuracy degrades with length. Split growing content into separate files with `@import` instead.

- **Using `/claude init` without editing** — The generated output is a template. Treat it as a draft and remove anything irrelevant to your actual stack before committing.

- **Adding linting or formatting rules** — ESLint and Prettier rules waste tokens on every session. Let the actual tools handle enforcement.

- **Not knowing which CLAUDE.md wins when rules conflict** — Priority order is Managed > User > Project > Local. The higher-priority file always wins.

- **Burying critical rules at the bottom** — Claude reads top-to-bottom. The most important constraints belong at the top, marked with `IMPORTANT` or `MUST`.

- **Not using conditional rules for rare cases** — Rules that only apply to specific file patterns should live in `rules/` with a `paths:` field, not in the root CLAUDE.md where they consume tokens every session.

## Sources

- [Anthropic Claude Code Documentation — CLAUDE.md](https://docs.claude.com/en/docs/claude-code/memory)
- Personal experimentation (June 2026)

---

> Next: [Skills vs CLAUDE.md](./03-skills-vs-claude-md.md)
