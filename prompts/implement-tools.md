---
type: prompt
id: implement-tools
title: "Implement Tools"
description: "Builds MCP tool handlers with function signatures, input validation, and response formatting"
tags: [Production, Developer, MCP]
inputs:
  target_api:
    label: "Target API"
    description: "The API specification including endpoints, authentication, and response formats for the tool implementations"
    example: "OpenWeatherMap REST API — API key via query parameter, JSON responses, rate limited to 60 calls per minute."
    required: true
    type: text
connections:
  - target: tool-implementation
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the tool implementation skill to produce complete MCP tool handlers from the scaffolded project.

## Prompt

You are an expert TypeScript developer specialising in MCP tool implementation. Using the scaffolded project structure below, implement the full tool handlers.

### Scaffolded Project

{{steps.previous.output}}

### Target API

{{input.target_api}}

### Instructions

For each registered tool, produce a complete handler implementation:

1. **Input schema** — define a Zod validation schema matching the tool's JSON Schema registration
2. **Handler function** — implement the tool logic with proper async/await patterns
3. **API integration** — make the actual API calls using fetch, handling authentication and rate limiting
4. **Error handling** — catch API errors, validation failures, and timeouts; return structured MCP error responses
5. **Response formatting** — return results as properly structured MCP tool responses with content arrays

### Requirements

- Validate all inputs before making API calls
- Use descriptive error messages that help users understand what went wrong
- Handle network timeouts with a configurable timeout value
- Log important events (tool invocation, API calls, errors) for debugging
- Keep each tool handler in its own file under `src/tools/`

### Output

Return the COMPLETE updated project — all tool handler files plus any modified files from the scaffold. Output each file with its path as a heading followed by the complete file content in a code block. Do not return partial implementations or just the changed sections.

## Formatting Rules

- Use British English in all comments and documentation strings
- Include a brief explanation before each file describing its role
