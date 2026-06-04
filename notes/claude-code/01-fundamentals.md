# Claude Code Fundamentals: 7 Levels of Mastery

> A progressive learning path from beginner to expert in Claude Code.

## Overview

After studying Claude Code, I've organized the knowledge into 
**7 progressive levels**. Each level builds on the previous one.

---

## Level 1: Foundation — Installing & Running

### Installation Options

**Windows / Cross-platform (via NPM):**

\`\`\`bash
npm install -g @anthropic-ai/claude-code
\`\`\`

**Desktop Application:**

Download from the [official Anthropic website](https://www.anthropic.com/claude-code).

### Verify Installation

\`\`\`bash
claude --version
\`\`\`

---

## Level 2: Pick Your AI Teammate

Choosing the right model is critical for **cost-efficiency**.

| Model | Role | Best For | Token Cost |
|-------|------|----------|------------|
| **Opus 4.8** | Senior Engineer | Planning, ambiguous tasks | High 💰💰💰 |
| **Sonnet 4.6** | Engineer | General work (balanced) | Medium 💰💰 |
| **Haiku 4.5** | Junior | Small, simple tasks | Low 💰 |

> 💡 **Pro Tip:** Start with Sonnet for daily work, switch to Opus for complex planning.

---

## Level 3: Setup AI Team Rules

Create `CLAUDE.md` at project root to instruct Claude.

### Key Principles

- **More detail = better results** (within token limits)
- Add strategies: branching, commit style, coding guidelines, testing rules
- Use `@filename` to import other `.md` files

### Example Structure

\`\`\`markdown
# Project Guidelines

@testing.md
@security.md

## Common Commands
- npm run dev
- npm test
\`\`\`

---

## Level 4: AI Debugging (UI & CSS)

Send **screenshots** to Claude for visual debugging.

**Example use case:**
> "The button color doesn't match this design. Fix it."

Claude can analyze the screenshot and update CSS accordingly.

---

## Level 5: AI-Enhanced Multitasking

**Messaging Queue feature:**
- Type next prompts without waiting for previous to complete
- Claude processes them sequentially

This is huge for productivity — no more waiting!

---

## Level 6: Ultra Planning (Plan Mode) ⭐

Claude's **most powerful feature** — analysis before action.

### 3 Levels of Thinking

| Keyword | Use Case | Token Usage |
|---------|----------|-------------|
| `think` | General analysis | Low |
| `think harder` | Deeper analysis | Medium |
| `ultrathink` | Maximum depth | High |

### Sub-Agents Pattern

Real tasks need multiple roles (Frontend, Backend, DBA).

**How to use:**
\`\`\`text
"Plan this feature using 3 sub-agents:
- Frontend agent for UI
- Backend agent for API
- Database agent for schema"
\`\`\`

Claude will distribute the work automatically.

---

## Level 7: AI-Enhanced Collaboration

### GitHub Integration

Tag `@claude` in PR comments to trigger:
- ✅ Code review
- ✅ Security scans
- ✅ Bug detection

### Example Workflow

\`\`\`text
Comment on PR: "@claude review this PR for security issues"
→ Claude analyzes and replies in the thread
\`\`\`

---

## Key Takeaways

1. ✅ Start simple — NPM install + basic prompts
2. ✅ Match model to task complexity (save tokens)
3. ✅ CLAUDE.md is your foundation
4. ✅ Use `ultrathink` for complex problems
5. ✅ Plan mode prevents wasted work
6. ✅ Integrate with GitHub for team collaboration

## Sources

- [Anthropic Claude Code Documentation](https://docs.claude.com/en/docs/claude-code/overview)
- Personal experimentation (June 2026)

---

> Next: [CLAUDE.md Best Practices](./02-claude-md-best-practices.md)