# Motivation

Interoperation -> Protocol/Standard -> MCP -> Validation -> Single Source of Truth

Here's one way to think about things. The primary goal of MCP is to facilitate interoperation. Interoperation is good because it enables parties to build systems based around a common "language", or set of conventions. Since I can take it for granted that an MCP server will conform to the MCP protocol, I already know a lot about how to interact with it. This enables more frictionless growth and development, hopefully for the good of society.

A protocol specifies a certain set of rules that parties must obey if they are deemed to be compliant. Generally, the rules are documented somewhere such that anyone can (try to) understand them and comply with them. I think people are probably familiar with the notion of a "single source of truth" - there must be a source of truth with respect to what _deterimines_ whether an actor is in compliance with the protocol - and there had better be a _single_ source of truth, because if there are two documents that constitute the rules of the protocol, then there is the chance that they might be inconsistent with one another. Practically speaking, that means there is no way to resolve a disagreement about an issue about which the protocol says two inconsistent things - so I can't really know what the protocol is telling me to do, or be confident in how the other party will act.

There are different kinds of protocols - some are very formal and legalistic, like e.g. USB-C... others are loose, more like "best practices". I think technical protocols tend to be more like the former, because they pertain to how a machine is supposed to operate such it can interoperate with another machine - and small divergences can break the communication flow. I don't really know what kind of protocol this group is trying to establish, but I have been acting under the belief that it's more like the former - maybe not quite an "RFC" as of yet, but pretty formal and explicit, especially in areas where a lack of precision can cause communication failure. (While also being open to extension.)

Issues, by T-shirt size:

LARGE:

- Single Source of Truth (SST):

[CLAIM] The Specification lacks a SST.

Citing the [README](../../README.md) of this repo:

```
The protocol consists of four main components:

1. The [specification](https://modelcontextprotocol.io/specification), defining the Protocol and Transports.
2. [Reference SDKs](https://modelcontextprotocol.io/sdk) that implement the Protocol and Transports to help developers build interoperable solutions.
3. Supporting resources such as User Guides, Tutorials, Debugging Tools and Reference Applications.
4. Working Group artifacts - implementation patterns, configuration guides, and other community-developed resources.
```

First, on its surface, this appears somewhat incoherent, since it states that "The protocol consists of ... 1. The specification, defining the Protocol and Transports." A formal, technical protocol cannot be a recursively nested entity, so the first usage of "protocol" must be read as something different from the second. After a brief conversation with ChatGPT[^1], it seems fair to say that a protocol has a slightly broader connotation than a specification, the latter being a formal ruleset, and the former permitting implicit norms. This comports with the MCP's statement:

> This specification defines the authoritative protocol requirements, based on the TypeScript schema in schema.ts.

So we have the Specification (Spec), the Protocol, the Schema, Transports, Reference SDKs, Supporting Resources, and WG Artifacts. I suggest that the authoritative, formal definition of MCP (violating this constitutes non-compliance) consists of the Spec, the Schema, and the Transports, which are non-exhaustive, since the Spec says "custom transports" are allowed - however, there is room for debate on the status of Transports - MCP currently defines two transports (stdio and Streamable HTTP), and one deprecated one (SSE). The fact that the Spec permits "custom transports" but also has deprecated the use of SSE, suggests that the Spec imposes constraints on what is a permissible Transport, but does not strictly delimit them. However, I'll suppose that for the Transports that are explicitly declared, the Specification's statements are authoritative, while other Transports must be evaluated in light of the Protocol as a whole. (It is worth thinking about whether the constraints on Transports are adequately inferable from the Protocol documentation.)

So I suggest that the Protocol is a slightly broader and looser term, and the Specification is the formal declaration that has so far materialized. Compliance with the Protocol is inherently looser, and probably formally undecidable, while the Specification is meant to be a formal document, where compliance is much more strictly delineated.[^2] It is worth keeping in mind the relationship between these two entities, which is a little slippery - MCP is a _protocol_, but the Specification is an authoritative definition of at least many aspects of the Protocol. How would one resolve a situation where the Spec says X, but the Protocol (various implementations, user guides, etc.) contradicts X? Do you adjust the Specification, or the Protocol? According to the statement above, the Specification "defines the authoritative protocol requirements." This suggests that the Spec is authoritatively dominant over the Protocol, in the sense that any disagreement is resolved in favor of the Spec - at the same time, the Spec can always change, if people think there is a good reason to do so.

Now, to discuss the main issue, the Specification:

[CLAIM] The Specification lacks a SST.

We have clarified that the Specification consists of the texts that are documented on the [Specification website](https://modelcontextprotocol.io/specification), especifically the latest published version, as well as the Schema.

[CLAIM] The relationship between the Specification and the Schema is insufficiently clear.

The Schema is declared in a _very_ precise form, given that it is expressed in code (first, in TypeScript; second, in JSON Schema - since the latter is automatically generated from the former, I won't distinguish them unless the need arises). There is _no_ room for interpretation of a TypeScript interface, e.g. The language itself determines whether some code complies with the schema - for instance, an application that produces a message that does not fit into the type system will simply not compile. That being said, the waters are muddied by the extensive use of supplementary comments in the Schema - interfaces and many parameters have JSDocs, which are not strictly encoded into the type system, yet nevertheless (sometimes) use the authoritative and formal language of MUST/SHOULD/MAY.

To illustrate an extensive commentary, consider the `CallToolResult` interface:

```typescript
/**
   * Whether the tool call ended in an error.
   *
   * If not set, this is assumed to be false (the call was successful).
   *
   * Any errors that originate from the tool SHOULD be reported inside the result
   * object, with `isError` set to true, _not_ as an MCP protocol-level error
   * response. Otherwise, the LLM would not be able to see that an error occurred
   * and self-correct.
   *
   * However, any errors in _finding_ the tool, an error indicating that the
   * server does not support tool calls, or any other exceptional conditions,
   * should be reported as an MCP error response.
   */
  isError?: boolean;
```

This is a lot of wording that exceeds what is expressible in the current type system. It includes a mixture of formal "SHOULD" and informal "should" (which, on its own, is fine); it also mentions something about what is "assumed".

Elsewhere, the Schema points back to the Specification, e.g. in the Tool interface:

```typescript
/**
   * See [specification/2025-06-18/basic/index#general-fields] for notes on _meta usage.
   */
  _meta?: { [key: string]: unknown };
```

One could argue this resembles something like a circular dependency. Regardless, the main issue is:

[QUESTION] What is the status of the comments/descriptions/annotations in the Schema that are expressed in natural language, and have no bearing on things like compilation, e.g.?

The language of MCP suggests that the Schema is considered highly authoritative. If the two disagree, which of the two (between the Specification and the Schema) is supposed to be dominant?

I think this is a concrete schism in the source of truth. The Schema comments are not merely supplementary, because I believe there are cases where the Schema comments impose additional requirements on the Spec;[^4] in other cases, they are merely redundant or repitious of the Specification. Furthermore, one has to consider the relation between the Schema comments and the interfaces themselves. Thus, the truth becomes distributed over the Specification documents, the Schema comments, and the Schema interfaces, all of which are supposed to be formal and authoritative (presumably - I am taking the comments in the Schema to be authoritative).

One or two final sources of truth are the JSON-RPC 2.0 specification, and RFC XXX (regarding the all-caps language). The Spec states that JSON-RPC is _part of the specification_ and that all messages conform to that spec, which thankfully is very brief and pretty easy to evaluate (and for which evaluation tools already exist).[^3]

So, in the end, there are about three or four formal documents that constitute the Spec. I suggest that this presents concrete problems for the Protocol: (i) the hierarchy between these documents is not entirely clear, so conflicts can only be resolved on an _ad hoc_ basis; (ii) developers have to negotiate between the Schema and the Spec, referring back and forth between both documents to see what is prescribed by the Spec, and in addition must "interpret" the Schema interfaces, which are effectively very precise expression of MUST (e.g. a required property) and MAY (e.g. an optional property). The whole category of SHOULDs is _not expressible in TypeScript_. On my reading, it's possible to "factor out" SHOULDs into MUSTs, since it's declared that "SHOULD ..." is equivalent "MUST ..., unless doing so would impede interoperation, or there exist good security reasons not to". Still, this "refactor" to translate "SHOULD" statements into "MUST" statements doesn't help much from the standpoint of interpretation, because assessing compliance with a SHOULD constraint involves a lot of context and a value judgment of whether such-and-such counts as a sufficiently good reason not to do something. In other words, what results is a set of MUST statements that still cannot be expressed in a type system.

One plausible, and compelling interpretation, is that the type system expresses a much clearer formalization of a subset of the requirements of the Specification as a whole - in particular, the message formats, and other data structures. This could then form a piece of the Specification overall, just as JSON-RPC forms a separate piece. The problem, again, is what to make of the extensive documentation/comments that exist in the Schema, but are not expressible in the type system itself.

[PROBLEM STATEMENT] The relationship between the Schema (its interfaces and documentation/comments) and the rest of the Spec is ill-defined. If any conflict or inconsistency is discovered, neither can be said to dominate the other. Both appear to be described as authoritative.

[POSSIBLE RESOLUTIONS]

- Eliminate all comments from the Schema, since these are not evaluable by any existing tools (at least, any that don't involve an LLM, or "interpreter"). The comments are either redundant of the Specification, or the interfaces themselves, or are offered as an independent, additional level of the Specification. Instead, move all comments to the Specification, perhaps provide relevant links to the Specification in the Schema, and don't try to express anything in the Schema which cannot be expressed in the type system.
- Try to move more of the Specification _into_ the type system itself. For instance, declare more abstract interfaces such as "Exchange" or something, which express, as types, what kinds of message-_pairs_ are permissible. Given the introduction of conditional types in both TypeScript and JSON Schema, the type system could actually be more expressive. (Still, there is no proposal for how to express "SHOULD" in any schema language that I know of.)
- Declare the the Schema is _not_ authoritative - express everything in the Specification, and state that the Schema is a formal expression of the Specification, which is added for specific technical purposes, but adds no additional information, and is dominated by the language of the Specification.

Footnotes:
[^1] I questioned ChatGPT about "Specification" vs "Protocol". Its response was effectively that a protocol is a set of behavioral norms, possibly implicit, while a specification is the formal declaration of a protocol. Excerpt:

> The protocol is the ruleset itself. The specification is the document that defines and explains that ruleset.

Link to chat: https://chatgpt.com/share/685560d6-073c-8006-900f-0e1b49987a9f

[^2] Due to the limitations of natural language, even compliance with the Specification is probably to some extent undecidable, but far less so than the Protocol. This is why, e.g., the Specification uses the technical expressions "MUST", "SHOULD", and "MAY", while supporting documents employ the informal "must"/"should"/"may".

[^3] The Spec explicitly identifies one or two additional requirements or extensions that it makes on JSON-RPC, for instance disallowing `null` as an `id` - JSON-RPC allows for extensions, so this is just a slightly stricter requrement than what JSON-RPC states, and is not problematic.

Issues, by T-shirt size:

- Single Source of Truth: A critical for a prescriptive document like a protocol is that there be some "thing" (generally, a document or set of documents) which determines what the protocol actually requires. If a spec says on Page 1 that X MUST do such-and-such, and on page 10 it says that X MUST NOT do such-and-such, that's a big problem when I'm trying to implement an X - I don't know which document is to be taken as authoritative - I don't know how to implement X. So it's critical that there be a _source of truth_ when it comes to something like a protocol, and it's best if there's a _single_ source of truth because if there are two, then they had better not say anything contradictory. Having two sources of truth is at best redundant, and at worst logically destructive of the source of truth _tout court_.

Citing the [README](../../README.md) of this repo:

```
The protocol consists of four main components:

1. The [specification](https://modelcontextprotocol.io/specification), defining the Protocol and Transports.
2. [Reference SDKs](https://modelcontextprotocol.io/sdk) that implement the Protocol and Transports to help developers build interoperable solutions.
3. Supporting resources such as User Guides, Tutorials, Debugging Tools and Reference Applications.
4. Working Group artifacts - implementation patterns, configuration guides, and other community-developed resources.
```

To be charitable, we must not read this statement as saying that the source of truth is distributed across all of these source - for one thing, the list is simply too long to have any hope of being mutuaully consistent. Second, it just seems wrong to think that a tutorial about the Protocol would have the same standing as the Spec, e.g. In that case, these "four main components" do not constitute the source. It must be the Spec, or what's often stated, the schema is authoritative with respect to the interfaces and data structures, and the Spec is authoritative with respect to everything else.

This is reasonably coherent. It's preferable to have a protocol that's written in a single language, but if it's clearest or most convenient to express the interfaces as TypeScript schema, then that's OK. One major dispute I have about this is with respect to the status of the comments in the TS schema - the schema contains its own language about MUST and SHOULD. But the schema cannot express the notion of SHOULD. MUST, MUST NOT, and MAY (e.g. "additional properties") is expressible, but SHOULD is not.

SHOULD is, in general, problematic from a validation point of view. According to the relevant RFC, "SHOULD" means "MUST, unless there are good reasons not to, and those reasons pertain to interoperation or security." Well, without knowing a lot about the context of a particular implementation decision, it's very hard to say whether an implementer has complied with SHOULD - i.e., did they really identify a valid reason not to do something that is otherwise mandatory? And is it really a good reason? These are really hard questions to answer. I would advocate for minimizing the usage of should. Or, rather, when a evaluating an implementation, we can say that it is compliant with respect MUST and MAY, but we can only grade it on a scale with respect to SHOULD, since it inherently involves a value judgment (is such-and-such a sufficiently "good" reason to not implement such-and-such). But in any case, it's perfectly to classify implementations as compliant, non-compliant, and then to a greater-or-lesser degree fully compliant (i.e. all SHOULDs are obeyed).

#### Passive Language

The specification is needlessly vague in many places simply due to a preference for "common" parlance, as opposed to the laborious, explicit way that a standard is generally stated. Concretely speaking, the Spec often uses the modality of: "A server
