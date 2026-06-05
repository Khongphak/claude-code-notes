---
description: Create a new technical note following CLAUDE.md writing standards
---

# Create New Note

Topic: $ARGUMENTS

Create a new note file with the following structure:

1. Determine the correct folder based on the topic:
   - Claude Code related → `notes/claude-code/`
   - MCP related → `notes/mcp/`
   - Next.js related → `notes/nextjs/`
   - TypeScript related → `notes/typescript/`

2. Generate a filename:
   - Check existing files in the folder for the next number
   - Use kebab-case: `0X-topic-name.md`
   - Be descriptive

3. Use this template:

```markdown
# [Title]

> [One-sentence description of what this note covers]

## Overview

[2-3 sentences introducing the topic and why it matters]

## [Main Section 1]

[Content with code examples]

## [Main Section 2]

[More content]

## Common Pitfalls

- **[Pitfall name]** — [Explanation]
- **[Pitfall name]** — [Explanation]

## Sources

- [Official documentation link]
- Personal experimentation (June 2026)

## Next

- `0X-next-topic.md` — [What's coming next]
```

4. Show me the file path and content
5. DO NOT commit — wait for my review