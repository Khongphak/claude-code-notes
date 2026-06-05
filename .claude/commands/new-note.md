---
description: Create a new technical note following CLAUDE.md writing standards
---

# Create New Note

Topic: $ARGUMENTS

Follow these steps to create a new note:

## 1. Determine Folder

Based on the topic, choose the correct folder:
- Claude Code, CLAUDE.md, Skills → `notes/claude-code/`
- MCP, Model Context Protocol → `notes/mcp/`
- Next.js, React, App Router → `notes/nextjs/`
- TypeScript, Generics, Types → `notes/typescript/`

## 2. Generate Filename

- Check existing files in the chosen folder to find the next number
- Use kebab-case format: `0X-topic-name.md`
- Be descriptive but concise

Examples:
- `02-server-components.md`
- `03-react-hooks-patterns.md`

## 3. Use This Template

```markdown
# [Title]

> [One-sentence description of what this note covers]

## Overview

[2-3 sentences introducing the topic and why it matters]

## [Main Section 1]

[Content with code examples]

\`\`\`typescript
// Example code with language tag
\`\`\`

## [Main Section 2]

[More content - tables, lists, examples]

## Common Pitfalls

- **[Pitfall name]** — [Brief explanation]
- **[Pitfall name]** — [Brief explanation]
- **[Pitfall name]** — [Brief explanation]

## Sources

- [Official documentation link]
- Personal experimentation (June 2026)

## Next

- `0X-next-topic.md` — [What's coming next in this series]
```

## 4. After Creating

- Show me the full file path and content
- DO NOT commit to git
- Wait for my review before any further action