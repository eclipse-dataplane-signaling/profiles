## Transfer Profile Registry

A **Transfer Profile** is the normative specification of a particular kind of data transfer supported by a
[=Data Plane=]. It identifies a wire-protocol endpoint type, the transfer direction (s) it supports (push, pull, or
both), and the message contents required to drive those transfers. Transfer Profiles are advertised by data planes
during [registration](https://eclipse-dataplane-signaling.github.io/dataplane-signaling/HEAD/#data-plane-registration) via the `profiles` property, and referenced from
`DataFlowPrepareMessage` and `DataFlowStartMessage` via the `profile` property.

To ensure interoperability across implementations, every Transfer Profile MUST be published in the
[Endpoint Type Registry](https://github.com/eclipse-dataplane-signaling/endpoint-type-registry). This specification does
not enumerate Transfer Profiles; the registry is the authoritative source.

### Transfer Profile Requirements

Each Transfer Profile MUST:

1. **Be identified by a fully-expanded URL.** Each profile is rooted at a single absolute URL (the **profile URL**)
   under which a human-readable spec document is published.

2. **Declare one or more `profile` values.** A Transfer Profile MUST support at least one of the `push` or `pull`
   directions, and MAY support both. Each supported direction is exposed as a `profile` value formed by appending
   `-push` or `-pull` to the profile URL.

   For example, a profile published at `https://w3id.org/dspace-sig/profile/http` that supports both directions declares
   the values:

    - `https://w3id.org/dspace-sig/profile/http-push`
    - `https://w3id.org/dspace-sig/profile/http-pull`

   A `profile` value MUST be defined by exactly one Transfer Profile. Two Transfer Profiles MUST NOT declare the same
   `profile` value. A Transfer Profile that supports both `push` and `pull` MUST be specified as a single profile; the two
   directions MUST NOT be split across separate profiles.

3. **Define the `endpointType` and its `DataAddress` schema.** The profile MUST specify which `DataAddress`
   `endpointProperties` are mandatory or optional for the `endpointType`, and the semantics of each property. Where push
   and pull differ in the data they convey, the profile MUST specify those differences explicitly.

4. **Specify `metadata` semantics, where applicable.** If the profile relies on `metadata` carried in
   `DataFlowPrepareMessage` or `DataFlowStartMessage` from the [=Control Plane=] to the [=Data Plane=], it MUST define
   the structure and semantics of those entries.

5. **Specify `labels` semantics, where applicable.** If the profile assigns meaning to label values, it MUST define
   them.

6. **Publish JSON Schemas.** All objects defined or extended by the profile (for example, `DataAddress`, `metadata`
   payloads) MUST be published as JSON Schemas that reference the corresponding base schemas in this specification.

7. **Declare its scope.** A profile MUST declare whether it is:
    - a **transport-protocol profile** — bound only to a wire protocol (e.g. HTTP, S3, Kafka), or
    - a **usecase profile** — bound to a dataspace usecase that includes business semantics beyond transport. Usecase
      profiles SHOULD reference an existing transport-protocol profile rather than redefining transport-level concerns,
      to maximize reuse and cross-profile interoperability.

### Relationship to Best Practices

Non-normative guidance for authoring Transfer Profiles — architectural patterns, worked examples, and recommended
conventions — is published in the
[Data Plane Signaling Best Practices](https://github.com/eclipse-dataplane-signaling/best-practices) repository. Profile
authors SHOULD follow that guidance; where it conflicts with this specification, this specification takes precedence.

### Relationship to the Dataspace Protocol

Transfer Profiles defined under this specification provide the `DataAddress` object referenced by DSP
`Data Transfer` profiles. DSP-side JSON Schema definitions SHOULD point to the object definitions governed by the
corresponding DPS Transfer Profile rather than redefining them.
