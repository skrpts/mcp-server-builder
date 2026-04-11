---
type: prompt
id: test-server
title: "Test Server"
description: "Generates integration tests for the MCP server"
tags: [Quality, Developer, MCP]
connections:
  - target: integration-testing
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the integration testing skill to produce a comprehensive test suite for the MCP server.

## Prompt

You are a senior test engineer specialising in MCP server testing. Using the validated server implementation below, generate a complete integration test suite.

### Validated Server

{{steps.previous.output}}

### Instructions

Produce test files covering:

1. **Tool invocation tests** — call each tool with valid inputs and verify the response structure, content type, and values
2. **Input validation tests** — send invalid, missing, and edge-case inputs to each tool and verify proper error responses
3. **Error handling tests** — simulate API failures, timeouts, and authentication errors; verify graceful degradation
4. **Transport tests** — verify the server handles connection lifecycle (initialise, tool calls, shutdown) correctly
5. **Schema tests** — verify that tool registrations match their actual input expectations

### Test Structure

- Use a standard test runner (Vitest or similar)
- Organise tests by tool, with shared fixtures and helpers
- Include a test runner configuration file
- Add setup and teardown for any shared state

### Requirements

- Each test must have a clear name describing what it verifies
- Use descriptive assertion messages so failures are easy to diagnose
- Include at least 3 test cases per tool (happy path, invalid input, error scenario)
- Mock external API calls — tests must not require live API access
- Include a test summary at the end listing all test cases and expected outcomes

## Formatting Rules

- Use British English in all test descriptions and comments
- Output each file with its path as a heading followed by the complete file content in a code block
