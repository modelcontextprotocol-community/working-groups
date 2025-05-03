# MCP Transports Pros/Cons

> This document is intended as a preliminary proposal and does not represent an official statement for the MCP standard.
> Date: Apr 18, 2025

This document aims to provide a basis for evaluating the inclusion of new standard MCP transports by listing the advantages and disadvantages of each.

## STDIO Transport

| Category | Pros | Cons |
|----------|------|------|
| Client/Server Connection Management | Universal, language-agnostic subprocess APIs make spawning and wiring up stdin/stdout trivial. | Requires clients to manage lifecycle and crash recovery, adding complexity. |
| Observability | stderr separation enables clean logging without polluting protocol data. | Lacks out-of-the-box tooling for stream capture and correlation without custom adapters. |
| Authorization | Implicit local trust boundary via pipes means no exposed network port. | No built-in auth or ACLs; must implement custom authorization logic. |
| Scalability | | Not suited for distributed or multi-tenant scenarios without an external dispatcher. |
| Complexity within a Large-Scale Architecture | Deterministic startup/shutdown simplifies orchestration for CLI-first tools | Integration with observability and service discovery tools requires additional adapters. Plus, the overhead of spinning a process per client is huge. |

## HTTP Stream Transport

| Category | Pros | Cons |
|----------|------|------|
| Communication | Simplify client-server communication Handles 90% of the MCP use case with tools/list and tool/calls | |
| Deployment | Can be deployed on the cloud easily. Compatibility with serverless functions | |
| Flexibility | Choose between two modes. Best of both worlds | Implementation complexity on the server side |












