# Welcome to the MCP Hosting Working Group

There are our current topics:

Contact @

-
# **MCP Hosting Working Group (WG) – Vision & Roadmap**

This document is intended as a preliminary proposal and does not represent an official statement or policy of any organization.

**Prepared by:** [Mathis Joffre] (Blaxel)  
**Date:** March 24, 2025

The Model Context Protocol (MCP) has seen significant adoption, driven largely by the needs of consumers and server authors. However, as MCP deployments scale and diversify, hosting challenges have emerged that require a dedicated focus from across the ecosystem. This document outlines an expanded vision for forming an MCP Hosting Working Group (WG) dedicated to collaboratively addressing these evolving challenges.

### **Background** 

The current MCP ecosystem is evolving rapidly:

* **Scaling Requirements:** As usage grows, deploying, managing, and scaling MCP servers effectively across various environments (cloud, on-premise, local) presents new technical hurdles.  
* **Community Feedback:** Recent discussions underscore the importance of incorporating diverse perspectives, including those of hosting providers and large-scale deployers, into the ongoing development of the MCP specification and related tooling. There's a growing need to address topics beyond the core protocol, such as multi-tenancy, standardized deployment, and operational concerns.

### **Scope of Work** 

The WG will focus on a range of key areas crucial for robust MCP hosting. While priorities will be determined collectively, potential topics include, but are not limited to:

* **Transport Protocol Enhancements & Standardization:**  
  * Evaluating, standardizing and improving approaches for various transport protocols (e.g., SSE, Plain HTTP, Websockets, MQTT, …) within MCP environments.  
  * Developing documentation, RFCs, and best practices for implementation.

***Related issues/discussions:***

* Add Event Subscription and Publishing Support to MCP: [https://github.com/modelcontextprotocol/specification/issues/179](https://github.com/modelcontextprotocol/specification/issues/179)  
  * Simplify Streamable HTTP to use Standard HTTP Protocol / Methods: [https://github.com/modelcontextprotocol/specification/issues/236](https://github.com/modelcontextprotocol/specification/issues/236)  
  * Include OpenTelemetry Trace identifiers as part of the MCP client \-\> server protocol: [https://github.com/modelcontextprotocol/specification/issues/246](https://github.com/modelcontextprotocol/specification/issues/246)

* **Multi-tenancy:**  
  * Clearly define multi-tenancy in a hosting perspective.  
  *  Exploring architectural patterns and requirements for multi-tenant MCP deployments.  
  * Defining best practices for isolation, resource management, and security in shared environments.

***Related issues/discussions:***

* Multi-Tenant Client Support (Server-to-Server): [https://github.com/modelcontextprotocol/specification/discussions/193](https://github.com/modelcontextprotocol/specification/discussions/193)  
  * Multi-user Authorization: [https://github.com/modelcontextprotocol/specification/discussions/234](https://github.com/modelcontextprotocol/specification/discussions/234)

* **Standard MCP Packaging & Configuration:**  
  * Defining a standardized format (e.g., using archives or containers) for distributing and deploying MCPs.  
  * Developing specifications for metadata, dependencies, and configuration management.

***Related issues/discussions:***

* MCP Server Registry: [https://github.com/orgs/modelcontextprotocol/discussions/159](https://github.com/orgs/modelcontextprotocol/discussions/159)

* **Runtime Pluggable Transport:**  
  * Designing an architecture that allows for selecting or swapping transport protocols at runtime.  
  * Creating APIs or conventions for managing and registering transport plugins.

***Related issues/discussions:***

* Provide a more flexible transport: [https://github.com/modelcontextprotocol/specification/issues/98](https://github.com/modelcontextprotocol/specification/issues/98)

* **MCP Server Discovery:**  
  * Defining mechanisms for MCP server discovery in various network and hosting environments.  
  * Developing protocols and standards for advertising and locating MCP servers and users securely.

**Related issues/discussions:**

* .well-known/mcp directory: [https://github.com/orgs/modelcontextprotocol/discussions/84](https://github.com/orgs/modelcontextprotocol/discussions/84), also [https://github.com/modelcontextprotocol/specification/discussions/69](https://github.com/modelcontextprotocol/specification/discussions/69) 

* **Feedback Loop with MCP Core:**  
  * Ensuring that findings and developed standards feed back into the broader MCP specification process.  
  * Advocating for hosting-friendly features and improvements in future MCP releases.  
  * Framework: [\[Public\] MCP CWG Discord Charter](https://docs.google.com/document/d/1wwniFi4IfXx0FwOdutbDp1-An7LHSygDHt8vqZHTRgM/edit?usp=sharing).

### Purpose & Vision

#### **Purpose** 

The MCP Hosting WG is envisioned as a collaborative forum where hosting providers, developers, infrastructure operators, and other stakeholders can:

* Identify, discuss, and propose solutions for hosting-specific challenges outlined in the scope.  
* Help standardize protocols, configurations, and tools that facilitate seamless, efficient, and secure MCP hosting.  
* Share insights and best practices for deploying and scaling MCP servers.

#### **Vision** 

We aspire to build a robust, community-driven ecosystem where:

* **Interoperability is Seamless:** Standards ensure that MCP servers work harmoniously across different hosting environments and deployment models.  
* **Scalability is Built-in:** Solutions are designed to meet the growing demands of MCP deployments, ensuring high performance and reliability.  
* **Innovation is Collaborative:** By pooling expertise, the WG will drive continuous improvement and foster innovative solutions for the entire MCP community.

### Objectives

#### Short-term:

* Establish the WG framework, governance model, and invite initial participants.  
* Identify and prioritize key areas from the scope based on community needs.  
* Initiate technical discussions and draft preliminary proposals or best practice documents for high-priority areas.  
* Explore existing solutions and frameworks relevant to packaging, plugin architectures, discovery, and multi-tenancy.  
* Create a shared repository for documentation, discussions, and sample implementations.  
* Identify and specify the available communication channels (e.g., Slack, Discord, Email, etc.).

#### Medium-term:

* Develop reference implementations or prototypes for agreed-upon standards (e.g., regarding transports, packaging).  
* Conduct pilot projects and gather real-world feedback from diverse hosting environments.  
* Organize regular WG meetings and community calls to track progress and align on priorities.

#### Long-term:

* Achieve broad adoption of the developed standards and best practices within the MCP community.  
* Integrate relevant hosting improvements into the official MCP specification where appropriate.  
* Establish ongoing maintenance and evolution of hosting standards to adapt to future technological advancements.

### Membership & Governance

#### **Membership** 

The WG is open to:

* Hosting providers and infrastructure operators with experience related to MCP (e.g., Glama, Blaxel, Smithery, ToolBase, InstantMCP…).  
* Developers and architects building or consuming MCP-based services.  
* Representatives from organizations deploying MCP at scale.  
* Community members interested in contributing to the hosting aspects of MCP.

### Governance

* **Steering Committee:** A small group representing different stakeholder types to oversee WG activities and ensure balanced decision-making.  
* **Workstreams:** Focused efforts on specific topics (e.g., transport protocols, packaging) led by interested members to drive detailed work.  
* **Open Communication:** Regular meetings, public mailing lists, and collaborative tools to maintain transparency and encourage broad community input.

### Roadmap & Next Steps

* **Kickoff Meeting:** Schedule an initial WG meeting to discuss this vision, refine priorities, and establish initial roles/responsibilities.  
* **Define WG Charter:** Formally agree on the scope, objectives, governance model, and communication channels.  
* **Initiate Workstreams:** Begin focused work on priority topics based on initial discussions, potentially starting with requirements gathering or drafting initial proposals.  
* **Regular Updates:** Set up a cadence for reporting progress, gathering feedback, and iterating on the WG's output.

The proposed MCP Hosting WG represents a vital opportunity to collaboratively address the evolving challenges of deploying and scaling MCP servers. By developing shared standards, best practices, and tooling, the group can ensure continued MCP adoption and deliver significant benefits to consumers, authors, and hosting providers alike. We invite all interested parties to join us in this collaborative effort. Come be part of this journey and help shape the future of MCP hosting\!

### Participants

[CONTACT DETAILS REDACTED FOR GH]
