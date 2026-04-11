---
type: asset
id: mcp-server-template
title: MCP Server Template
description: "Template showing the standard MCP server project structure with TypeScript"
tags: [Production, Developer, MCP]
connections: []
---

## Purpose

Reference template for the standard MCP server project layout. Used by the scaffolding stage as a structural guide when generating new server projects.

## Project Structure

```
my-mcp-server/
├── package.json
├── tsconfig.json
├── .env.example
├── src/
│   ├── index.ts          # Entry point — server initialisation and tool registration
│   ├── transport.ts      # Transport layer (stdio) with error handling
│   ├── types.ts          # Shared type definitions
│   └── tools/
│       ├── index.ts      # Tool registry — exports all tool handlers
│       └── example.ts    # Individual tool handler template
└── tests/
    ├── setup.ts          # Test configuration and shared fixtures
    └── tools/
        └── example.test.ts
```

## package.json Template

```json
{
  "name": "my-mcp-server",
  "version": "1.0.0",
  "description": "MCP server for [service name]",
  "type": "module",
  "main": "dist/index.js",
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js",
    "dev": "tsx src/index.ts",
    "test": "vitest run"
  },
  "dependencies": {
    "@modelcontextprotocol/sdk": "^1.0.0",
    "zod": "^3.22.0"
  },
  "devDependencies": {
    "typescript": "^5.3.0",
    "tsx": "^4.0.0",
    "vitest": "^1.0.0"
  }
}
```

## Entry Point Template

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new McpServer({
  name: "my-mcp-server",
  version: "1.0.0",
});

// Register tools here
// server.tool("tool-name", "Tool description", inputSchema, handler);

async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
}

main().catch(console.error);
```

## Tool Handler Template

```typescript
import { z } from "zod";

export const inputSchema = {
  param_name: z.string().describe("Description of the parameter"),
};

export async function handler(params: { param_name: string }) {
  // Tool implementation here
  return {
    content: [
      {
        type: "text" as const,
        text: "Tool response here",
      },
    ],
  };
}
```

## Environment Variables

```
# .env.example
API_KEY=your-api-key-here
API_BASE_URL=the-api-base-endpoint
```

## Key Conventions

- One file per tool handler in `src/tools/`
- All inputs validated with Zod schemas before processing
- Environment variables for all secrets and configuration
- Structured error responses with descriptive messages
- British English in all user-facing strings and documentation
