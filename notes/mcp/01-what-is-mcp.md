# What is MCP (Model Context Protocol)?

> MCP is an open protocol that lets AI models connect to external tools and data sources in a standardized way — think of it as USB-C for AI integrations.

## The Problem MCP Solves

Before MCP, every AI tool had its own way of integrating with external services. Adding a new data source meant writing custom, one-off code for each AI application.

Key pain points:

- **Fragmented integrations** — each app reinvents the wheel
- **No reusability** — a Slack integration for app A couldn't be reused in app B
- **Tight coupling** — changing the AI model often broke all integrations

## What MCP Is

MCP (Model Context Protocol) is an open standard introduced by Anthropic in November 2024. It defines a universal interface between AI models and the outside world.

It has three core components:

| Component | Role | Example |
|-----------|------|---------|
| **Host** | The AI app the user interacts with | Claude Desktop, VS Code |
| **Client** | Lives inside the host, manages connections | Built into Claude Code |
| **Server** | Exposes tools/data to the model | A filesystem MCP server |

> **Key insight:** MCP servers are language-agnostic. You can write one in TypeScript, Python, Go — whatever fits your stack.

## Why MCP Matters for Developers

### 1. Build Once, Use Everywhere

Write an MCP server once and connect it to any MCP-compatible host. A database server you build today works in Claude Desktop, Claude Code, and any future AI tool that adopts the protocol.

### 2. Three Primitives to Learn

MCP exposes only three concepts:

- **Tools** — functions the model can call (e.g., `run_query`, `send_email`)
- **Resources** — data the model can read (e.g., files, database records)
- **Prompts** — reusable prompt templates the model can use

### 3. Local and Remote Servers

MCP servers can run:

- **Locally** — as a subprocess on the user's machine (great for filesystem, local DBs)
- **Remotely** — over HTTP/SSE (great for SaaS integrations, shared team tools)

### 4. Security Model

The host controls what the model can access. Users explicitly approve which MCP servers are connected. This is intentional — it keeps the developer in control.

## A Minimal MCP Server (TypeScript)

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";

const server = new McpServer({ name: "my-server", version: "1.0.0" });

server.tool(
  "get_weather",
  { city: z.string() },
  async ({ city }) => ({
    content: [{ type: "text", text: `Weather in ${city}: sunny, 25°C` }],
  })
);

const transport = new StdioServerTransport();
await server.connect(transport);
```

The model can now call `get_weather` as if it were a native capability.

## MCP vs. Function Calling

Both let models call external code, but they solve different scopes:

| | Function Calling | MCP |
|---|---|---|
| **Scope** | Single app | Cross-app, reusable |
| **Discovery** | Hardcoded in prompt | Dynamic at runtime |
| **Transport** | In-process | Subprocess or HTTP |
| **Reusability** | Low | High |

> **Rule of thumb:** Use function calling for app-specific logic. Use MCP when the tool should be reusable across multiple AI apps or shared with a team.

## Quick Setup in Claude Code

```bash
# Add an MCP server to your project
claude mcp add my-server -- node path/to/server.js

# List connected servers
claude mcp list

# Check server status
claude mcp get my-server
```

## Next:

- `02-building-your-first-mcp-server.md` — hands-on tutorial
- `03-mcp-resources-and-prompts.md` — beyond tools
- `../claude-code/` — how Claude Code uses MCP internally
