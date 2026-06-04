# Claude Code Notes Repository

A personal knowledge base documenting my learnings about Claude Code, MCP, Next.js, and AI-augmented development.

## Purpose

This repo serves two goals:
1. **Personal reference** — quick lookup for things I've learned
2. **Public portfolio** — showcase technical writing skills to recruiters

## Repository Structure

- `notes/` - Topic-specific learning notes (Markdown)
  - `claude-code/` - Claude Code, CLAUDE.md, Skills
  - `mcp/` - Model Context Protocol
  - `nextjs/` - Next.js 15 patterns
  - `typescript/` - Advanced TypeScript
- `examples/` - Production-ready code/config examples
  - `claude-md/` - CLAUDE.md templates
  - `skills/` - Custom skill examples
  - `mcp-servers/` - MCP server implementations
- `projects/` - Small standalone projects

## Writing Style for Notes

When creating or editing notes, follow these conventions:

### Markdown Standards

- Start each file with `# Title` (H1)
- Use `##` for major sections
- Use `###` for subsections
- ALWAYS use code blocks with language tags: ` ```bash `, ` ```typescript `
- Use tables for comparisons
- Add `> Quote/Tip` blocks for important callouts

### Content Standards

- **One language per file** — pick English OR Thai, don't mix
- **English is preferred** for technical content (better for portfolio)
- Start with `> Brief description` at the top
- End with `## Sources` or `## Next:` linking to related notes
- Keep paragraphs short (2-3 sentences max)
- Use bullet points liberally for scannable content

### File Naming

- Use kebab-case: `claude-md-best-practices.md`
- Prefix with number for ordering: `01-fundamentals.md`
- Be descriptive: `mcp-server-tutorial.md` not `mcp.md`

## IMPORTANT: Workflow Rules (READ FIRST)

### Scope Control — MUST FOLLOW

- **ONE file per request by default** — If I ask to modify a file, modify ONLY that file
- **DO NOT touch other files** unless I explicitly list them
- If a task seems to require multiple files, STOP and ask for explicit confirmation listing each file
- When in doubt, ASK before acting

### Git Workflow — MUST FOLLOW

- **NEVER auto-commit** changes — I review and commit manually
- **NEVER auto-push** to remote
- **NEVER run `git add`, `git commit`, or `git push`** unless I explicitly say "commit this" or "push this"
- After making file changes, STOP and let me review with `git diff`
- If I want a commit message, I will ask: "suggest a commit message"

### Plan Mode Rules — MUST FOLLOW

- When I use keywords `think`, `think harder`, or `ultrathink`:
  - Show the plan FIRST
  - WAIT for my explicit approval ("yes proceed" / "go ahead")
  - Do NOT execute any changes until approved
- Even after showing a plan, do NOT assume approval — wait for confirmation
- If I say "show me the plan", that means PLAN ONLY — no execution

### Content Rules

- DO NOT mix Thai and English in the same file
- DO NOT commit work-related/confidential information
- DO NOT use raw indented lists (1.1, 1.2) — use proper markdown headers
- ALWAYS use code blocks with syntax highlighting
- ALWAYS test markdown rendering on GitHub before final commit

## Common Commands

```bash
# Preview markdown locally (if using VS Code)
# Press Ctrl+Shift+V (or Cmd+Shift+V on Mac)

# Check what's changed
git status
git diff

# Commit with conventional format (manual only!)
git add <specific-file>
git commit -m "docs: add notes about [topic]"
git push
```

## Commit Convention

Use prefixes:
- `feat:` - New notes, sections, or features
- `docs:` - Documentation updates, README changes
- `refactor:` - Restructuring existing notes
- `fix:` - Typo fixes, broken links
- `chore:` - Setup, config changes

## Goals for This Repo

- Build a knowledge base of 20+ high-quality technical notes by Aug 2026
- Demonstrate consistent learning to recruiters (green squares)
- Help other developers learning the same topics
- Practice writing clear technical English
