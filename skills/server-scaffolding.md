---
type: skill
id: server-scaffolding
title: Server Scaffolding
description: "Generates MCP server project structure including package manifest, TypeScript configuration, entry point, and transport setup"
tags: [Tested, Developer, MCP]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Produces a complete MCP server project scaffold from a service description. Generates the package manifest, TypeScript configuration, entry point file, and transport layer setup with correct MCP SDK imports and initialisation.

## When to Use

- Starting a new MCP server project from scratch
- Wrapping an existing API as an MCP-compatible tool provider
- Setting up the boilerplate before implementing tool handlers

## Inputs

Service description, target API details, list of desired tools

## Outputs

Complete project directory structure with package manifest, TypeScript config, entry point, and transport configuration ready for tool implementation
