---
type: skill
id: tool-implementation
title: Tool Implementation
description: "Builds MCP tool handlers from a service description with function signatures, input validation, and response formatting"
tags: [Tested, Developer, MCP]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Generates MCP tool handler implementations from the scaffolded project and service description. Produces typed function signatures, Zod input validation schemas, error handling, and properly formatted MCP tool responses.

## When to Use

- After scaffolding is complete and you need to add tool logic
- Wrapping API endpoints as individual MCP tools
- Adding new tools to an existing MCP server

## Inputs

Scaffolded project structure, target API specification, list of tools to implement

## Outputs

Complete tool handler files with typed signatures, input validation, API integration, error handling, and MCP-compliant response formatting
