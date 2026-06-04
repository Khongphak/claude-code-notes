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

## IMPORTANT: Things to Watch Out For

- DO NOT mix Thai and English in the same file
- DO NOT commit work-related/confidential information
- DO NOT use raw indented lists (1.1, 1.2) — use proper markdown headers
- ALWAYS use code blocks with syntax highlighting
- ALWAYS test markdown rendering on GitHub before final commit

## Common Commands

```bash
# Preview markdown locally (if using VS Code)
# Press Ctrl+Shift+V (or Cmd+Shift+V on Mac)

# Commit with conventional format
git add .
git commit -m "docs: add notes about [topic]"
git push

# Check what's changed
git status
git diff
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
