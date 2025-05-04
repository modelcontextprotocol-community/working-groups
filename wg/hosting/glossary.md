# MCP Hosting WG - Glossary

Here are some terms to define for the MCP Hosting WG glossary based on initial vision and roadmap:

## Hosting Provider
An organization or service that offers infrastructure (cloud, on-premise, or local) where MCP servers can be deployed, managed, and scaled. Examples include Glama, Blaxel, ToolBase, AWS, Google, Microsoft…

## Multi-Tenancy
MCP multi-tenancy is the ability to have multiple MCPs (like MCP A and MCP B) serving different tenants (like tenant A and tenant B) on the same server.

## MCP Packaging
A defined format that bundles an MCP server’s binary/artifacts along with metadata, dependencies, and configuration so it can be deployed reliably across environments.

## MCP Server Metadata
Descriptive information about a packaged MCP server—such as version, supported transports, and required runtime parameters—that helps deployment tools automate installation and configuration.

## Runtime Pluggable Transport
An architectural approach whereby transport protocols can be added, removed, or swapped at server startup or even at runtime, via a plugin API or registry mechanism, without modifying core server code.

## Server Discovery
Mechanisms by which clients or other servers locate available MCP instances on a network—often via DNS records, a centralized registry, or a well-known URI directory (e.g., .well-known/mcp).

## Workstream
A focused sub-group within the WG dedicated to a specific topic (e.g., transport protocols, packaging, discovery), responsible for drafting proposals, reference implementations, or best-practice guides.

## Reference Implementation
A canonical, working software example that demonstrates how to implement a proposed standard or best practice—used as a template and test-bed for community review and pilot deployments.

