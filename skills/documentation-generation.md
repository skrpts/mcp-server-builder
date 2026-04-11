---
type: skill
id: documentation-generation
title: Documentation Generation
description: "Produces README, tool descriptions, usage examples, and setup instructions for an MCP server"
tags: [Tested, Developer, Documentation]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Generates comprehensive documentation for an MCP server project. Produces a README with setup instructions, a tool reference with descriptions and examples, configuration guidance, and troubleshooting notes.

## When to Use

- After the server is built and tested, as the final production step
- When updating documentation after adding new tools
- When preparing an MCP server for public distribution

## Inputs

Complete MCP server source code, test results, and tool specifications

## Outputs

README file, tool reference documentation, usage examples for each tool, setup and configuration guide, and troubleshooting section
