## Introduction

This document defines a set of **profiles** for the [[[dps-base]]] specification. Profiles specify interoperable
behaviours — transfer protocols, authorization mechanisms, and related concerns — that a [=Data Plane=] or
[=Control Plane=] may implement on top of the base signaling protocol.

The profiles are maintained separately from the base specification so that a dataspace may reference a Data Plane
Signaling profile as the foundation for a Dataspace Protocol profile without mandating adoption of Data Plane
Signaling itself.

This document defines:

- The [Transfer Profile Registry](#transfer-profile-registry) — the normative requirements every Transfer Profile
  MUST satisfy.
- The [HTTP Transfer Profile](#http-transfer-profile) — a transport-protocol profile for transferring data over HTTP.
- The [Token Renewal](#token-renewal) profile — an OAuth 2.0 refresh-token mechanism for pull transfers.
- [Authorization Profiles](#authorization-profiles) — profiles for authorizing data plane and control plane
  registration.

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “NOT
RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in
[RFC 8174](https://datatracker.ietf.org/doc/html/rfc8174).

## Terminology

The following terms are used to describe concepts in this specification.

- <dfn>Connector</dfn>: Software services that manage the exchange of data between a provider and consumer as defined by
  the DSP Specification.
- <dfn>Control Plane</dfn>: The [=Connector=] services that implement the DSP protocol.
- <dfn>Data Flow</dfn>: The exchange of data belonging to a [=Dataset=] between a provider and consumer [=Data Plane=].
- <dfn>Data Plane</dfn>: The [=Connector=] services that implement a [=Data Flow=] using a [=Wire Protocol=].
- <dfn>Dataset</dfn>: Data or a technical service that can be shared as defined by the DSP Specification.
- <dfn>Participant</dfn>: A dataspace member as defined by the DSP Specification.
- <dfn>Transfer Process</dfn>: A set of interactions between two connectors that provide access to a dataset as defined
  by the DSP Specification.
- <dfn>Wire Protocol</dfn>: A protocol such as MQTT, AMQP, or an HTTP REST API that governs the exchange of data.
