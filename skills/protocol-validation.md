---
type: skill
id: protocol-validation
title: Protocol Validation
description: "Checks MCP protocol compliance including JSON-RPC correctness, tool and resource schemas, and error handling"
tags: [Tested, Quality, MCP]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Reviews MCP server code for protocol compliance. Validates JSON-RPC message formats, tool registration schemas, resource definitions, error response structures, and transport layer correctness against the MCP specification.

## When to Use

- After implementing tool handlers to verify protocol correctness
- Before publishing an MCP server to catch compliance issues
- When debugging unexpected behaviour from MCP clients

## Inputs

Complete MCP server source code including tool handlers and transport setup

## Outputs

Compliance report listing any protocol violations, schema errors, or missing required fields, with specific line references and recommended fixes
