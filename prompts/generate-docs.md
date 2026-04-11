---
type: prompt
id: generate-docs
title: "Generate Docs"
description: "Produces comprehensive documentation for the MCP server"
tags: [Production, Developer, Documentation]
connections:
  - target: documentation-generation
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the documentation generation skill to produce complete project documentation for the MCP server.

## Prompt

You are a technical writer specialising in developer tools and MCP integrations. Using the tested server implementation below, produce comprehensive documentation.

### Tested Server

{{steps.previous.output}}

### Instructions

Generate the following documentation files:

1. **README.md** — project overview, quick start guide, installation instructions, and configuration
2. **TOOLS.md** — detailed reference for each tool including:
   - Tool name and description
   - Input parameters with types, descriptions, and examples
   - Example request and response
   - Error codes and their meanings
3. **SETUP.md** — step-by-step setup guide covering:
   - Prerequisites and dependencies
   - Environment variable configuration
   - Building and running the server
   - Connecting from an MCP client
4. **TROUBLESHOOTING.md** — common issues and their solutions

### Requirements

- Write for a developer audience — assume familiarity with TypeScript and npm but not necessarily with MCP
- Include copy-pasteable code examples and configuration snippets
- Document every environment variable the server requires
- Include a table of contents in the README
- Add a "Contributing" section with development setup instructions

## Formatting Rules

- Use British English throughout
- Use clear headings and consistent formatting
- Keep paragraphs short and scannable
- Include code blocks with language annotations for syntax highlighting
