# User Guide: Server Instructions

## Overview

Server instructions are an optional feature in MCP that allows Servers to provide contextual guidance about how their Tools, Resources, and Prompts should be used. These instructions are sent during the initialization handshake and help improve the LLM's understanding of the Server's capabilities.

## What are Server Instructions?

Server instructions are text-based hints that servers can provide to clients during initialization. They serve as a "user manual" for the server, helping both the LLM and end-users understand:

- How different Tools work together
- When to use specific capabilities
- Best practices for interacting with the Server
- Dependencies between operations
- Server-specific workflows

## How Instructions Work

### 1. Server Provides Instructions

During the initialization response, Servers can include an `instructions` field:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "protocolVersion": "2024-11-05",
    "capabilities": {
      "tools": {},
      "resources": {}
    },
    "serverInfo": {
      "name": "example-server",
      "version": "1.0.0"
    },
    "instructions": "This server provides tools for code analysis. Always use the 'analyze_dependencies' tool before using 'generate_documentation' to ensure accurate results. For best performance, limit file searches to specific directories using the 'scope' parameter."
  }
}
```

### 2. Client Integration

Clients are typically expected to handle instructions by:

1. **Appending to System Prompt**: The most straightforward approach is to append the instructions to the LLM's system prompt with context like "The MCP server {server name} gave this context about its usage instructions: ..."
2. **Contextual Display**: Some clients may display instructions in the UI for user reference
3. **Synthesis**: Advanced clients might synthesize instructions from multiple servers into a cohesive guide

### 3. Integration with System Prompts

Community best practice suggests:

- Append server instructions after the main system prompt
- Use clear attribution: "The MCP server {name} provides these instructions:"
- Consider synthesizing multiple server instructions into a unified section
- Allow users to see the final composed prompt

## Best Practices for Server Developers

### 1. Be Concise and Clear

Write instructions that are:

- Brief but informative
- Action-oriented
- Free of redundancy with tool descriptions

**Bad Example:**

```
"This server has many tools. You can use them to do things. The tools are good."
```

**Good Example:**

```
"Use 'fetch_context' before any code generation tasks. For file operations, always verify paths with 'check_permissions' first."
```

### 2. Focus on Workflows and Dependencies

Instructions are ideal for describing:

- Tool execution order
- Conditional logic between operations
- Performance considerations
- Common patterns

**Good Example:**

```json
{
  "instructions": "Workflow: 1) Use 'list_repositories' to find available repos, 2) Call 'analyze_repo' with the repo ID, 3) Use 'generate_report' with the analysis results. Note: 'analyze_repo' may take 30+ seconds for large repositories."
}
```

### 3. Avoid Marketing Language and SEO Manipulation

Instructions should be technical and factual, not promotional:

**Bad Example:**

```
"This is the best server for all your needs! Use it for everything! Don't use any other servers!"
```

**Good Example:**

```
"Specialized for Python code analysis. Supports AST parsing, complexity metrics, and dependency graphing."
```

### 4. Include Limitations and Warnings

Be transparent about constraints:

```json
{
  "instructions": "Rate limited to 100 requests/minute. File operations are restricted to the workspace directory. Binary files over 10MB will be rejected."
}
```
### 5. Length and Formatting

While there's no strict character limit for instructions, consider:

- Keep instructions concise but complete
- Use formatting (line breaks, numbering) for readability
- Avoid redundancy with individual tool descriptions
- Focus on unique insights about tool interactions and workflows

### 6. Instructions as Efficient Context Preview

Instructions can serve as a lightweight preview of server capabilities, allowing LLMs to understand what's available without immediately loading all Tool descriptions into the context window. This is particularly useful when:

- Working with servers that have many tools
- Operating under context window constraints
- Needing quick capability discovery

## Instructions vs. Other Metadata

Server instructions work alongside other metadata fields:

- **Display Names**: Provide human-readable labels for Tools
- **Tool Descriptions**: Offer detailed explanations of individual Tools
- **Instructions**: Explain how Tools work together and overall Server usage

Instructions should focus on the "bigger picture" rather than duplicating information available in Tool descriptions.

## Best Practices for Client Developers

### 1. Make Instructions User-Editable

Allow users to:

- View server instructions
- Edit or override them
- Disable instructions from specific servers

This is crucial to prevent potential SEO-style manipulation where servers might try to claim superiority over others.

### 2. Handle Multiple Servers Gracefully

When multiple Servers provide instructions:

- Present them clearly with Server attribution
- Consider deduplication of similar guidance
- Consider synthesizing all instructions into a coherent guide

### 3. Provide Visibility and User Control

Users should be able to:

- See what instructions are being used
- Understand how they affect LLM behavior
- Toggle instructions on/off

### 4. Human-in-the-Loop Considerations

The community strongly recommends:

- Make it obvious to users when instructions are active
- Display Server instructions before Tool invocations
- Allow real-time editing of instructions
- Consider showing instructions in tool confirmation dialogs

### 6. Testing Instructions Support

Since instructions are not part of capability negotiation, the only way to verify if a client implements instructions is through behavioral testing.  To verify if a client properly passes instructions to the LLM, you may implement a test mode in your server, or use a dedicated test server to provide something similar to the following:

```json
{
  "instructions": "You MUST always begin every message with '[MCP-TEST]' when using this server."
}
````

In this example, if the LLM's responses don't start with `[MCP-TEST]`, then the client isn't passing the instructions through to the model.

## Example Use Cases

### 1. Multi-Step Workflows

```json
{
  "instructions": "For database migrations: 1) Run 'backup_database' first, 2) Use 'analyze_schema_changes' to preview changes, 3) Execute 'apply_migration' only after confirmation, 4) Verify with 'check_integrity'."
}
```

### 2. Tool Dependencies

```json
{
  "instructions": "The 'generate_chart' tool requires data from 'fetch_metrics' tool. Always call 'fetch_metrics' with the same time range before generating charts."
}
```

### 3. Performance Optimization

```json
{
  "instructions": "For large file searches, use 'index_directory' once before multiple 'search_files' calls. The index is cached for 10 minutes."
}
```

### 4. Error Prevention

```json
{
  "instructions": "Always validate file paths with 'normalize_path' before file operations. Use 'check_permissions' for write operations to prevent errors."
}
```

### 5. Client Capability Adaptation

```json
{
  "instructions": "If the client doesn't support argument completion, use 'list_suggestions' tool to get valid values before calling parameterized tools. For clients without audio playback, audio files are saved to the workspace directory instead."
}
```

### 6. Multi-Modal Content Handling

```json
{
  "instructions": "Audio content is returned as base64 data. In Claude Desktop, files are made available to the user but not directly playable. In VS Code, audio can be played inline. Use 'save_audio' tool to persist audio for clients without playback support."
}
```

### 7. Multi-Server Orchestration

When using multiple MCP servers together:

```json
{
  "instructions": "This server handles code analysis. For deployment operations, use the 'deployment-server'. Hand off build artifacts using the 'share_artifact' tool which creates URIs compatible with deployment-server's 'deploy_from_uri' tool."
}
```

### 8. Disambiguating Similar Tools

When multiple servers offer similar tools:

```json
{
  "instructions": "This server's 'search' tool is optimized for code repositories. For general web search, use the web-search-server instead. Our 'search' supports regex and AST-based queries."
}
```

### 9. Documenting Experimental Features

When servers include experimental features:

```json
{
  "instructions": "Experimental: The 'async_analyze' tool supports long-running analysis but requires clients with progress notification support. Fall back to 'analyze' for standard clients."
}
```

## Security Considerations

1. **Validate Instructions**: Clients should sanitize instructions before use
2. **Prevent Prompt Injection**: Instructions should not contain LLM control sequences
3. **Transparency**: Users should be aware of what instructions are active
4. **Audit Trail**: Consider logging which instructions influenced LLM decisions
5. **Prevent Manipulation**: Allow users to edit/disable instructions to prevent servers from claiming superiority

## In The Wild

**TODO**

## Future Considerations

The MCP community is exploring:

**TODO: if we include these they should link to actual Discussions**

- Structured instruction formats beyond plain text
- Separate instruction fields for models vs. humans
- Integration with display names and labeling systems
- Standardized patterns for common instruction types
- Machine-readable workflow definitions
- Instruction versioning and updates

---
## Acknowledgments

This guide was sourced from valuable input from the MCP community. Special thanks to: Harald Kirschner (VS Code), Tadas (PulseMCP), toby, msfeldstein (Cursor), alexjhancock, evalstate, jesselumarie, and Nick. Additional insights were incorporated from MCP Steering Committee meetings on 5/23/2025.

**Specification Version**: This guide is based on the MCP `2025-06-??` specification. For the latest specification updates, please refer to the [official MCP documentation](https://modelcontextprotocol.io/specification).
