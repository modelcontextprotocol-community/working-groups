# **MCP Hosting Working Group (WG) \- Meeting Notes**

**WG proposal:** [MCP Hosting Working Group (WG) – Vision & Roadmap](../README.md)  
**Chairs:** TBD  
**Discord:** [https://discord.com/invite/dV44HsCKwh](https://discord.com/invite/dV44HsCKwh)  
**Google group for shared invitations:** [https://groups.google.com/g/mcp-hosting-wg](https://groups.google.com/g/mcp-hosting-wg)

Apr 17, 2025 9:00 AM PDT  
Note taker: [Christophe Ploujoux]

Suggested agenda:

- Introductions & Google Group \- [Join the MCP Hosting WG Google Group](https://groups.google.com/g/mcp-hosting-wg)
- Access to documents and meeting notes
- Receive calendar invites for recurring meetings
- Review & discuss WG proposal/scope/charter
  - [MCP Hosting Working Group (WG) – Vision & Roadmap](../README.md)
  - Should we reduce the scope of work, given that some areas are already covered by other Community Working Groups?
    - Transports:
      - It's a good idea to share/open source non-standard implementations \- and a potential way for hosting implementors to value-add.
      - Make it pluggable instead of having one protocol for a server. Handle the transport in the sdk ? Define a standard
      - Hackathon for transports
    - Multi-tenancy
      - We need to build a glossary document
    - Packaging
      - JB: Think standardising docker is the way to go, but DSP has already commented that he does not want direct docker interfaces in the official SDKs
      - JG: mixed feelings on Docker. On the one hand, it's pretty great for the web deploying world. on the other it's not useful to mobile or embedded really at all
      - BC: there might be a middle-ground where the launch invocation is standardized (like a common launcher binary or packaging process) but the runtime could be a container or some other micro-vm or even servelet like mcp.run
      - JB: fastmcp2 has introduced the option to mount servers and expose them via any transport supported by fastmcp. you could build on this for the other transports
- Should we set the recurring meeting duration to 30 minutes every 2 weeks?
  - 30 minutes every week on a suggestion basis, meaning if you want to talk about a subject add it to the agenda. Add a recording disclosed to everyone

Apr 10, 2025 9:00 AM PDT  
_Poll closed \- ~~Poll to determine the meeting date: [https://github.com/modelcontextprotocol/specification/discussions/220\#discussioncomment-12694134](https://github.com/modelcontextprotocol/specification/discussions/220#discussioncomment-12694134)~~_

Suggested agenda:

- Community Working Groups
  1. **[\[Public\] MCP CWG Discord Charter](https://docs.google.com/document/d/1wwniFi4IfXx0FwOdutbDp1-An7LHSygDHt8vqZHTRgM/edit?usp=sharing)**
- Hosting Working Group Introductions
- Review & discuss WG proposal/scope/charter ([MCP Hosting Working Group (WG) – Vision & Roadmap](../README.md))
- Agree on communication channels
- Discuss initial roadmap themes & priorities
  1. Multi-tenancy
  2. Discovery
  3. Transport
     1. Websocket
        1. Websocket open for discussion
        2. Tadas proposed to give what has been said on websocket on github to people interested in
  4. Improve shape of the tool structure on the server side
     1. Metadata
     2. Telemetry
     3. Permissions
- Schedule recurring meeting
  1. Thursday 9AM PDT every week
  2. 30 min
  3. Important: goal is to use Discord beforehand of the meeting to have a concise and efficient 30 min

Add sub-topics you want to discuss to each section in the following format:

- Your name \- Topic
