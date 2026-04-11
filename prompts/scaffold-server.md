---
type: prompt
id: scaffold-server
title: "Scaffold Server"
description: "Generates MCP server project structure from a service description"
tags: [Production, Developer, MCP]
inputs:
  service_description:
    label: "Service Description"
    description: "A description of the service or API that the MCP server will wrap, including its purpose and key operations"
    example: "A weather service that provides current conditions, forecasts, and historical data for any location worldwide."
    required: true
    type: text
  target_api:
    label: "Target API"
    description: "The API that the MCP server will integrate with, including authentication method and key endpoints"
    example: "OpenWeatherMap REST API — API key authentication, endpoints for current weather, 5-day forecast, and historical data."
    required: true
    type: text
  desired_tools:
    label: "Desired Tools"
    description: "A list of MCP tools the server should expose, with a brief description of each"
    example: "get_current_weather — fetch current conditions for a location; get_forecast — retrieve 5-day forecast; get_historical — pull historical data for a date range."
    required: true
    type: text
connections:
  - target: server-scaffolding
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the server scaffolding skill to produce a complete MCP server project structure.

## Prompt

You are an expert TypeScript developer specialising in the Model Context Protocol (MCP). Generate a complete project scaffold for an MCP server based on the details below.

### Service Description

{{input.service_description}}

### Target API

{{input.target_api}}

### Desired Tools

{{input.desired_tools}}

### Instructions

Produce the following project files:

1. **package.json** — include the MCP SDK, TypeScript, and any required dependencies. Use a clear project name derived from the service description.
2. **tsconfig.json** — strict TypeScript configuration targeting ES2022 with Node module resolution.
3. **src/index.ts** — entry point that initialises the MCP server, registers all tools, and starts the stdio transport.
4. **src/transport.ts** — transport layer setup with proper error handling and graceful shutdown.
5. **src/types.ts** — shared type definitions for tool inputs and outputs.

### Requirements

- Use the official `@modelcontextprotocol/sdk` package
- Register each desired tool with a proper JSON Schema for its input parameters
- Include proper error handling for API failures and invalid inputs
- Add inline comments explaining key MCP concepts for maintainability
- Use environment variables for API credentials — never hardcode secrets

## Formatting Rules

- Use British English in all comments and documentation strings
- Output each file with its path as a heading followed by the complete file content in a code block
- Include a brief explanation before each file describing its role
