[
**_DISCLAIMER:_** **This is not (yet) an actual Working Group, and has not gone through all of the preparatory steps. It was recommended to me by a core contributor that I open this up for discussion by opening a draft. The intention of this document is to clarify what a Validation Working Group would be like, what purpose it would serve, what goals it would have, and so on. All of this is subject to change if and when a group is formed. Obviously I have used the [Hosting WG](../hosting/README.md) README as a template.**
]

This working group is hosted by @TBD

---

# **MCP Validation Working Group (WG) – Vision & Roadmap**

This document is intended as a preliminary proposal and does not represent an official statement or policy of any organization.

**Prepared by:** [Jesse Rappaport] (@hesreallyhim)
**Date:** June 13, 2025

The current [Roadmap](https://modelcontextprotocol.io/development/roadmap#validation) published on the [MCP website](https://modelcontextprotocol.io/) (albeit non-committal), states:

```
Validation

To foster a robust developer ecosystem, we plan to invest in:

* Reference Client Implementations: demonstrating protocol features with high-quality AI applications
* Compliance Test Suites: automated verification that clients, servers, and SDKs properly implement the specification

These tools will help developers confidently implement MCP while ensuring consistent behavior across the ecosystem.
```

MCP, insofar as it is a protocol, defines a set of "rules" or constraints on how two parties, an MCP client and an MCP server, must, should, or may interact. The "prime directive" of these rules is to facilitate _interoperation_. By declaring a common set of conventions that parties must follow, this enables each party to act independently of the other, and build applications, software, and other advanced technology, without the need to coordinate ahead of time on every implementation detail, because compliance with the protocol means that certain things can be taken for granted. Ultimately, although it is a set of _constraints_, this creates a space that _empowers_ technologists to innovate and build technology more rapidly, and ultimately enables more freedom for the evolving A.I. ecosystem. In some ways, one could argue that regardless of whether or not MCP is a "good" protocol, in its current shape (which is not to imply that it isn't), setting a foundation where people can express their interests and collaboratively define what this emergent technology should look like, is intrinsicably beneficial.

### **Background**

The proliferation of MCP implementations - servers, clients, server/client generators, and SDKs - has grown extremely rapidly since it was first launched. However, there is a dearth of resourcese available for developers to use to validate whether their implementation in fact complies with the Protocol or not. Although some open-source and proprietary tools/services exist, these tools themselves have not, to my knowledge, been vetted by the MCP standards body. Many of the existing reference implementations have been archived. [FastMCP](https://github.com/jlowin/fastmcp), a library that is incorporated into the official Python SDK (in its v1), has since seemed to have "spun off" from the MCP SDK, is now in v2, and effectively brands itself as "the actively maintained version" of the Python SDK. Without some authoritative "stamp of approval" from the MCP group, the Protocol will inevitably lose its status as a standard, and the ecosystem will evolve in a more fractured way, hence impeding interoperation.

To that end, I believe that the goal stated in the (provisional) roadmap of developing a set of resources for validating compliance with MCP, is of critical importance. The Protocol describes a range of incredible capacities that could empower the growth and adoption of A.I. applications in a way that is both innovative and safe (secure). Yet, I think to many developers, MCP is a fancy way of implementing "LLM tools via an API" - which is a pretty nice thing to have, but is only one part of what this Protocol encapsulates.

Reference implementations that showcase the full scope of capabilities that MCP describes would go a long way in expanding people's understanding of it. However, I believe that developing the basic tools for validating compliance are the most important step forward to keeping this Protocol alive and making it accessible to the community at large. We must always be clear that the goal is to promote ineroperation, and not to be an authority for the sake of name recognition. Interoperation means a common language, and common conventions - when it comes to a technical Protocol, these conventions should be clear enough that, in general, they can be validated with automatic tooling.

### **Scope of Work**

The following is a list of resources that I think can be built, tested, and deployed relatively quickly, and would provide a lot of value. The categories would divide into client validators, server validators, SDK validators, and (potentially) MCP-generator validators. There are various ways to tackle these problems:

- Static analysis libraries
- Fully validated official SDK's
- Solutions that incorporate "LLM-as-judge" type testing
- A publicly accessible server that client implementers can communicate with to test out their implementations, and perhaps a similar resource for client implementers

For a concrete proposal, given the current state of the spec, I think a great approach would be a scenario testing framework, where messaging flows/scenarios are defined, enabling implementers to "plug in" their implementation client/server to different scenarios (e.g., an "Initialization Scenario", a "Tools Listing Scenario", etc.), and would effectively be an endpoint where the implementor engages in some communication flow, and we have defined a set of Scenarios that would inform them whether the messages they are sending, and the way they are responding, conforms to the Protocol or not.

Postman, for instance, is already ahead of the game, in this respect. They have dedicated [resources](https://learning.postman.com/docs/postman-ai-agent-builder/mcp-requests/interact/) for implementing MCP, generating MCPs, testing APIs, and a system they call "Flows" for defining Scenarios for API interactions. Although I believe this is a paid service, there are open-source frameworks available that offer comparable functionality. If we adopted one of these frameworks (I haven't done any comparison shopping), we could incrementally build a suite of scenario tests that developers could stand up on their own machines locally, or in some cloud instance, and test their implementations. More abstract solutions could be built on top of that for MCP-generators or for SDK's. And the test suite could be built out incrementally, allowing us to start rolling out a library that hopefully could be viewed as the "definitive" evaluation framework for MCP compliance. It could even validate whether a server/client who announces that they support a certain capability really does support that capability. Then, if I visit a registry, instead of seeing some letter grades, that I don't really understand what they're based on, we have a common set of metrics that are actually meaningful and documented.

Without these tools, MCP will become just whatever Postman, OpenAI, Anthropic, FastMCP, etc., decide it is. And maybe if that's what's best for the growth of this technology in a democratic and safe way, then maybe that's for the best. But I still think the MCP standards body could provide a better space for developing this technology - and to that end, I think building these tools is very urgent.

I'll end here, as I think I've made the case for why validation tools are worth actually investing resources into, and I've laid out a few concrete proposals, as well as one specific place that I think would be a great starting point. If anyone is persuaded by the first part, but has different or better ideas regarding implementation, I hope some of you will join me in this effort. The details of this document are entirely preliminary.

Since this is only a draft of a draft of a Working Group statement, I'll not go into more detail. For those who are interested, or at least for the sake of posterity, I'll also try to put together a supplementary document regarding what I see as some fundamental flaws in the existing Protocol (in regards to its status as a specification, not its technical merits), in particular with respect to the question of _source of truth_, but I have tried to raise this in a number of places, and so far I haven't received much engagement.
