---
type: skill
id: integration-testing
title: Integration Testing
description: "Generates and runs integration tests against the MCP server to verify tool behaviour and protocol compliance"
tags: [Tested, Quality, MCP]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Produces a comprehensive integration test suite for an MCP server. Generates test cases covering tool invocation, input validation, error scenarios, and transport layer behaviour. Tests verify both happy-path responses and edge cases.

## When to Use

- After protocol validation passes and you need to verify runtime behaviour
- When adding new tools to an existing server and need regression tests
- Before publishing to ensure all tools respond correctly

## Inputs

Validated MCP server source code and tool specifications

## Outputs

Complete test suite with test files, test runner configuration, and a summary of expected pass/fail results for each tool
