---
type: workflow
id: mcp-server-builder
title: MCP Server Builder
description: "Design, build, validate, test, and document an MCP server from a service description"
tags: [Production, Developer, MCP, Quality]
connections:
  - target: server-scaffolding
    type: uses
  - target: tool-implementation
    type: uses
  - target: protocol-validation
    type: uses
  - target: integration-testing
    type: uses
  - target: documentation-generation
    type: uses
  - target: llm-service
    type: runs_on
  - target: mcp-server-template
    type: references
metadata:
  estimated_duration: "5-15 minutes"
  trigger: manual
execution:
  - skill: "server-scaffolding"
    step_type: "generation"
  - skill: "tool-implementation"
    step_type: "content"
    input_from: "server-scaffolding"
  - skill: "protocol-validation"
    step_type: "review"
    input_from: "tool-implementation"
  - skill: "integration-testing"
    step_type: "review"
    input_from: "tool-implementation"
  - skill: "documentation-generation"
    step_type: "generation"
    input_from: "tool-implementation"
---

## Overview

This workflow builds a complete, tested MCP server from a service description. It follows a sequential five-stage pipeline: scaffold the project, implement tool handlers, validate protocol compliance, generate integration tests, and produce documentation. Each stage builds on the output of the previous one, with the validation and testing stages acting as quality gates.

## Pipeline Stages

### Stage 1: Server Scaffolding

**Input:** Service description, target API, desired tools

Invoke the **server-scaffolding** skill to generate the complete project structure — package manifest, TypeScript configuration, entry point, transport layer, and type definitions.

**Output:** Scaffolded MCP server project ready for tool implementation.

### Stage 2: Tool Implementation

**Input:** Scaffolded project from Stage 1, target API specification

Invoke the **tool-implementation** skill to build out each tool handler with typed function signatures, Zod input validation, API integration, error handling, and MCP-compliant response formatting.

**Output:** Fully implemented tool handlers wired into the server.

### Stage 3: Protocol Validation

**Input:** Complete server implementation from Stage 2

Invoke the **protocol-validation** skill to check JSON-RPC compliance, tool registration schemas, response structures, error handling patterns, and transport layer correctness.

**Gate:** All hard failures must be resolved before proceeding. Warnings should be addressed but do not block progress.

**Output:** Compliance report and corrected server code.

### Stage 4: Integration Testing

**Input:** Validated server from Stage 3

Invoke the **integration-testing** skill to generate a comprehensive test suite covering tool invocation, input validation, error scenarios, and transport lifecycle.

**Gate:** All tests must pass before proceeding to documentation.

**Output:** Complete test suite with passing results.

### Stage 5: Documentation Generation

**Input:** Tested server from Stage 4

Invoke the **documentation-generation** skill to produce a README, tool reference, setup guide, and troubleshooting documentation.

**Output:** Publish-ready documentation suite.

## Error Handling

- If scaffolding fails due to an unsupported API pattern, simplify the service description and re-run Stage 1
- If protocol validation finds hard failures, fix the issues and re-run from Stage 2 — do not attempt to patch in Stage 3
- If integration tests fail, review the test output and fix the implementation before re-running Stage 4
- If a tool requires capabilities not supported by MCP (e.g., streaming binary data), flag it and suggest an alternative approach

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.service_description}}` | Yes | Description of the service the MCP server will wrap | "A weather service providing current conditions, forecasts, and historical data" |
| `{{input.target_api}}` | Yes | The API to integrate with, including auth and key endpoints | "OpenWeatherMap REST API — API key authentication, JSON responses" |
| `{{input.desired_tools}}` | Yes | List of MCP tools to expose with brief descriptions | "get_weather — current conditions; get_forecast — 5-day forecast" |

## Outputs

| Name | Description |
|------|-------------|
| Server project | Complete TypeScript MCP server with all tool handlers implemented |
| Test suite | Integration tests covering all tools and error scenarios |
| Documentation | README, tool reference, setup guide, and troubleshooting docs |
| Compliance report | Protocol validation results with compliance score |

## Setup

Before running this workflow:

1. **No external services required** — this workflow runs entirely on your configured LLM provider.
2. **Prepare your inputs** — you need a clear service description, target API details, and a list of desired tools.
3. **Review the template** — check the `mcp-server-template` asset to understand the target project structure.

## Provider Notes

- The scaffolding and implementation stages benefit from a model with strong TypeScript and API knowledge.
- Protocol validation requires precise understanding of the MCP specification — use a capable model.
- Documentation generation is a structured writing task — most models handle it well.
- The full pipeline uses moderate to high token counts due to the volume of generated code.

## Example Input

To test this workflow immediately after import:

```
Service description: "A task management service that lets users create, list, update, and delete tasks with priorities and due dates"
Target API: "A simple REST API with bearer token authentication and JSON request/response format"
Desired tools: "create_task — create a new task with title, priority, and due date; list_tasks — list all tasks with optional filtering by status; update_task — update a task's status, priority, or due date; delete_task — remove a task by ID"
```
