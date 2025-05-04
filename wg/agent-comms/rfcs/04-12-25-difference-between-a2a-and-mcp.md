# Difference between A2A and MCP

The goal of this document is to summarize the fundamentals differences between [A2A](https://google.github.io/A2A/#/) and [MCP](https://modelcontextprotocol.io/introduction). Understanding these differences will help us determine whether Agent-to-Agent communication can be supported within the MCP specification, rather than requiring the creation of a new standard.

| Feature | A2A | MCP | Notes | Opportunity for extension of MCP |
| --- | --- | --- | --- | --- |
| Discovery | Agent card | Capability metadata | Agent card is richer than capability metadata in that it offers more useful details. | [https://github.com/orgs/modelcontextprotocol/discussions/84](https://github.com/orgs/modelcontextprotocol/discussions/84) |
| Request Structure | Task, message, part | Per capability, sampling/prompt is like message, tools is more open ended | A2A enforces a very specific structure on requests via its Task, Message, and Part objects. This presents a downside that to use A2A people need to coerce their agent request/responses into that structure |  |
| Communication Types | Stateless, Stateful, Streaming, Push notifications | Stateless, Stateful, Streaming, notifications (via SSE) |  |  |
| Multi-turn/job semantics | Supported | Partial support via progress notifications | This also enables A2A to provide human in the loop via input_required, progress notifications are limited in MCP | [https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/314](https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/314) |
| Streaming partial response | Supported | Not supported | MCP supports SSE, but each message represents a complete payload | [https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/314](https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/314) |
| Async requests | Supported with GET task | Not supported | There is not GET request semantics in MCP | [https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/314](https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/314) |
| Webhooks | Supported | Not supported, SSE notifications are supported | A2A supports webhooks, MCP only supports bi-directional notifications | MCP could offer webhook URL as a capability that servers can offer. [https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/266](https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/266) |
| Response structure | Client can prescribe an output schema structure | Tools don’t have a strict structure | | [https://github.com/modelcontextprotocol/modelcontextprotocol/issues/97](https://github.com/modelcontextprotocol/modelcontextprotocol/issues/97), [https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/315](https://github.com/modelcontextprotocol/modelcontextprotocol/discussions/315) |


