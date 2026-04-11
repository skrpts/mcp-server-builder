---
type: prompt
id: validate-protocol
title: "Validate Protocol"
description: "Checks MCP protocol compliance across the server implementation"
tags: [Quality, Developer, MCP]
connections:
  - target: protocol-validation
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the protocol validation skill to verify MCP compliance of the implemented server.

## Prompt

You are an MCP protocol expert. Review the server implementation below for full protocol compliance.

### Server Implementation

{{steps.previous.output}}

### Validation Checklist

Check each of the following areas and report any violations:

1. **JSON-RPC compliance** — all messages must follow JSON-RPC 2.0 format with correct `jsonrpc`, `method`, `params`, `id`, `result`, and `error` fields
2. **Tool registration** — each tool must have a unique name, a valid JSON Schema for `inputSchema`, and a clear description
3. **Tool responses** — must return `content` arrays with typed items (`text`, `image`, `resource`), never raw values
4. **Error handling** — must use standard MCP error codes and include descriptive messages; must not leak internal details
5. **Transport layer** — stdio transport must handle partial reads, newline-delimited JSON, and graceful shutdown
6. **Server metadata** — `server_info` must include name and version; capabilities must accurately reflect supported features
7. **Input validation** — all tool inputs must be validated against their declared schemas before processing

### Output Format

For each area:
- **Status:** Pass, Fail, or Warning
- **Details:** What was checked and the result
- **Fix:** If Fail or Warning, the specific change needed with a code example

End with a summary table and an overall compliance score (0-100).

## Formatting Rules

- Use British English throughout
- Be precise — reference specific files and line numbers where issues occur
- Distinguish between hard failures (protocol violations) and soft warnings (best-practice suggestions)
