# GEXOR

## Functional Requirements Specification

**Document Version:** 1.0-MVP
**Document Type:** Functional Requirements Specification
**Product:** Gexor — AI Runtime Platform
**Product Stage:** Pre-development
**Status:** Complete — Pending Baseline Approval
**Source Document:** `PRD.md`
**Primary Release:** MVP

---

# Document Control

| Field                   | Value                                                                                   |
| ----------------------- | --------------------------------------------------------------------------------------- |
| Document owner          | Founder / Product Owner                                                                 |
| Primary source of truth | Gexor Product Requirements Document                                                     |
| Intended audience       | Product, design, engineering, security, QA, operations, and future implementation teams |
| Requirement baseline    | MVP                                                                                     |
| Change authority        | Founder / Product Owner                                                                 |
| Implementation status   | Not started                                                                             |
| Approval status         | Pending Product Owner baseline approval                                                 |

---

# Contents

1. Document Purpose
2. Requirement Conventions
3. Product Actors and Roles
4. Functional Requirement Register Introduction
5. Identity and Authentication Requirements
6. Organization and Workspace Requirements
7. Project and Conversation Requirements
8. Message Requirements
9. Runtime Execution Requirements
10. Context, Memory, and Knowledge Requirements
11. AI Provider Connection and Routing Requirements
12. Streaming, File Processing, and Search Requirements
13. Usage, Billing, Notification, and Administration Requirements
14. Additional MVP Functional Requirements
15. Requirement Register Completion Status
16. MVP Acceptance Criteria
17. Requirement Traceability Matrix
18. Cross-Requirement Dependency Register
19. Functional Error Catalogue
20. Requirement Priority Register
21. Document Change History
22. Approval and Baseline Status

---

# 1. Document Purpose

## 1.1 Purpose

This Functional Requirements Specification defines the observable behaviour that the Gexor system must provide for its MVP release.

The Product Requirements Document defines what the product must achieve and why it must exist. This document converts those product-level expectations into precise, testable, and implementation-independent functional requirements.

This document defines:

* supported users and system actors;
* user-visible system capabilities;
* runtime processing behaviour;
* validation and permission rules;
* state transitions;
* data-management behaviour;
* provider connection behaviour;
* memory and context behaviour;
* error and recovery behaviour;
* administrative controls;
* audit and traceability expectations;
* MVP acceptance conditions.

This document does not prescribe detailed implementation technologies, database schemas, infrastructure topology, internal class structures, or deployment procedures unless a functional constraint requires them.

Those matters shall be defined in their corresponding architecture, domain model, database, API, engine, security, testing, and deployment documents.

## 1.2 Product Context

Gexor is a provider-independent AI runtime and workspace platform positioned between users and supported external AI providers.

Gexor does not provide or train its own foundation model.

The system allows users to connect supported AI-provider accounts or API credentials and interact with those providers through a unified workspace and chat experience.

For each eligible request, Gexor may perform controlled runtime processing that includes:

* intent and task classification;
* prompt enhancement;
* relevant memory retrieval;
* workspace-context retrieval;
* conversation-context retrieval;
* context-budget enforcement;
* provider-ready prompt construction;
* model selection or recommendation;
* provider request execution;
* response streaming;
* token and cost recording;
* background response processing;
* memory-candidate extraction;
* knowledge extraction;
* conflict detection;
* deduplication;
* memory lifecycle management.

The external AI provider remains responsible for generating the underlying model response. Gexor is responsible for orchestrating, controlling, enriching, recording, and processing the interaction.

## 1.3 Functional Objectives

The MVP functional requirements shall support the following objectives:

1. Allow a user to authenticate securely.
2. Provide each user with an isolated personal workspace.
3. Allow supported AI-provider credentials to be connected and managed.
4. Provide a familiar conversational interface.
5. Enhance eligible user prompts without changing the user’s intended objective.
6. Maintain structured long-term memory.
7. Retrieve only relevant and permitted memory.
8. Preserve continuity across conversations and supported providers.
9. Support user-controlled memory inspection and correction.
10. Support basic model selection and recommendation.
11. Record token consumption and estimated provider cost.
12. Stream provider responses with minimal avoidable delay.
13. Process memory and knowledge candidates outside the critical response path where appropriate.
14. Preserve user control over providers, models, memory, context, cost limits, export, and deletion.
15. Prevent data leakage across users and workspaces.
16. Maintain traceability between product requirements, functional requirements, implementation, and tests.

## 1.4 Source-of-Truth Hierarchy

The following authority hierarchy shall apply:

1. Approved Product Requirements Document
2. Approved Functional Requirements Specification
3. Approved Non-Functional Requirements Specification
4. Approved architecture and runtime documents
5. Approved domain, database, and API designs
6. Approved engine-specific specifications
7. Approved security and UX documentation
8. Implementation tasks and source code
9. Test cases and operational procedures

A lower-level artifact shall not contradict a higher-level approved artifact.

Where two documents conflict:

* the higher-authority document shall control;
* the conflict shall be recorded;
* implementation shall pause for the affected behaviour;
* the dependent document shall be corrected;
* approval shall be obtained before development continues.

Developers shall not independently introduce product behaviour that is absent from or inconsistent with the approved requirements.

## 1.5 Scope of This Specification

This specification covers the functional behaviour of the Gexor MVP, including:

* identity;
* authentication;
* workspace isolation;
* provider connections;
* conversations;
* messages;
* runtime execution;
* context retrieval;
* memory management;
* prompt construction;
* provider routing;
* response streaming;
* usage recording;
* background processing;
* user controls;
* export and deletion;
* administrative functions;
* auditability;
* error handling.

This specification may identify future capabilities where necessary to protect architectural compatibility. Such capabilities shall not become MVP commitments unless explicitly marked as MVP requirements.

## 1.6 Out of Scope

The following are outside this document’s primary scope:

* detailed frontend component specifications;
* visual design tokens;
* final page layouts;
* database table definitions;
* endpoint payload schemas;
* infrastructure selection;
* cloud-provider selection;
* detailed encryption implementation;
* internal source-code organization;
* CI/CD implementation;
* detailed observability architecture;
* detailed model-evaluation methodology;
* pricing values and commercial packaging;
* non-MVP autonomous-agent functionality unless explicitly stated.

These areas shall be defined in subsequent specialized documents.

## 1.7 Intended Readers

This document is intended for:

* founder and product owner;
* product manager;
* solution architect;
* system architect;
* UI/UX designer;
* frontend engineer;
* backend engineer;
* AI engineer;
* data engineer;
* database engineer;
* security engineer;
* QA engineer;
* DevOps or platform engineer;
* technical writer;
* future maintainers and reviewers.

## 1.8 Requirement Lifecycle

Every functional requirement shall move through the following lifecycle:

1. Proposed
2. Reviewed
3. Approved
4. Planned
5. Implemented
6. Verified
7. Released
8. Modified, deprecated, or retired

A requirement shall not be considered complete merely because code exists.

A requirement is complete only when:

* its implementation is present;
* applicable automated or manual tests pass;
* permission and failure paths are verified;
* relevant documentation is updated;
* traceability records are complete;
* acceptance criteria are satisfied.

---

# 2. Requirement Conventions

## 2.1 Requirement Language

The following normative terms shall be used:

* **Shall:** Mandatory MVP behaviour.
* **Shall not:** Prohibited behaviour.
* **Should:** Recommended behaviour that may be deferred only with a documented reason.
* **Should not:** Discouraged behaviour that requires justification.
* **May:** Optional or configurable behaviour.
* **Future:** Explicitly outside the MVP baseline.
* **User:** An authenticated human account unless otherwise stated.
* **System:** The complete Gexor platform.
* **Provider:** An external supported AI-provider service.
* **Model:** A provider-hosted AI model available through a connected provider.
* **Workspace:** The primary isolated scope containing a user’s conversations, memories, provider connections, usage records, and related data.
* **Runtime:** The controlled request-processing pipeline between user input and provider output.
* **Memory:** Structured information retained for possible future retrieval.
* **Context:** Information selected for inclusion in a specific runtime execution.
* **Knowledge:** Structured or indexed information derived from approved sources, files, conversations, or explicit user input.
* **Candidate:** Information detected by the system but not necessarily approved for persistent storage.
* **Active memory:** A memory eligible for retrieval.
* **Inactive memory:** A retained memory excluded from normal retrieval.
* **Confirmed memory:** A memory accepted through system policy or explicit user action.
* **Temporary context:** Information usable for a limited scope or period without becoming durable long-term memory.

## 2.2 Requirement Identifiers

Each functional requirement shall use a stable identifier with the following format:

```text
FR-[DOMAIN]-[NUMBER]
```

Examples:

```text
FR-AUTH-001
FR-WORKSPACE-014
FR-CONVERSATION-008
FR-MEMORY-027
FR-RUNTIME-019
FR-PROVIDER-011
```

Identifiers shall not be reused after a requirement is removed.

A retired requirement shall remain in document history with one of these states:

* Deprecated
* Replaced
* Removed
* Deferred

Where a requirement is replaced, the replacement identifier shall be recorded.

## 2.3 Requirement Structure

Each formal requirement should contain:

| Field               | Description                                                      |
| ------------------- | ---------------------------------------------------------------- |
| Requirement ID      | Stable unique identifier                                         |
| Title               | Concise requirement name                                         |
| Statement           | Mandatory system behaviour                                       |
| Priority            | MVP Critical, MVP Required, MVP Optional, or Future              |
| Source              | Related PRD section                                              |
| Actors              | User, administrator, provider, background worker, or other actor |
| Preconditions       | Conditions required before execution                             |
| Trigger             | Event that initiates the behaviour                               |
| Primary flow        | Expected successful behaviour                                    |
| Alternate flow      | Valid alternative behaviour                                      |
| Failure behaviour   | Expected handling when execution fails                           |
| Postconditions      | Expected resulting state                                         |
| Acceptance criteria | Verifiable completion conditions                                 |
| Dependencies        | Related requirements or external dependencies                    |
| Status              | Proposed, approved, implemented, verified, or released           |

Not every short requirement must repeat every field inline. However, the complete specification and traceability register shall preserve this information where necessary.

## 2.4 Priority Classification

Requirements shall use these priorities:

### MVP Critical

The MVP cannot safely or meaningfully operate without the requirement.

Examples include:

* authentication;
* workspace isolation;
* provider credential protection;
* message execution;
* response delivery;
* memory control;
* critical error handling.

### MVP Required

The requirement is part of the approved MVP baseline and must be delivered before general release, but limited internal testing may begin before it is complete.

### MVP Optional

The requirement may be included in the MVP when schedule and quality permit. Its absence shall not invalidate the core product hypothesis.

### Future

The requirement is documented for architectural awareness but shall not be treated as an MVP commitment.

## 2.5 Requirement Quality Rules

Every approved requirement shall be:

* specific;
* testable;
* implementation-independent where practical;
* internally consistent;
* traceable to a product need;
* assigned a priority;
* written in singular behavioural terms;
* clear about scope and actor;
* clear about success and failure outcomes;
* compatible with user-control and data-isolation principles.

Requirements shall avoid ambiguous terms such as:

* fast;
* smart;
* seamless;
* usually;
* normally;
* appropriately;
* user-friendly;
* efficient;
* secure;
* real-time.

Where such terms are necessary, they shall be supported by measurable acceptance criteria in this or a dependent document.

## 2.6 Functional State Terminology

Unless a domain defines additional states, records may use the following general lifecycle:

```text
Created → Active → Updated → Inactive → Archived → Deleted
```

The system shall not assume that all entities support every state.

Deletion shall be classified as:

* **Soft deletion:** The entity is hidden from normal use but remains recoverable for a defined period.
* **Permanent deletion:** The entity is irreversibly removed according to the applicable deletion workflow.
* **Provider-side deletion:** Removal requested from an external provider where supported.
* **Derived-data deletion:** Removal of indexes, embeddings, caches, summaries, or other derived representations associated with deleted source data.

## 2.7 Permission Convention

Every operation involving protected data shall be evaluated against:

1. authenticated identity;
2. workspace membership;
3. assigned role;
4. resource ownership;
5. action-specific permission;
6. resource status;
7. applicable policy restrictions.

The absence of an explicit permission shall be treated as denial.

The system shall not expose whether an inaccessible resource exists when doing so would reveal protected information.

## 2.8 Validation Convention

Input validation shall occur before durable state changes or external provider execution.

Validation may include:

* required-field validation;
* format validation;
* length validation;
* supported-value validation;
* ownership validation;
* permission validation;
* provider-availability validation;
* model-availability validation;
* state-transition validation;
* quota validation;
* cost-limit validation;
* security-policy validation.

Validation failure shall produce a controlled error and shall not leave an unintended partial state.

## 2.9 Idempotency Convention

Operations that may be retried due to network, provider, or client failure should support idempotent behaviour where duplicate execution could cause:

* duplicate messages;
* duplicate provider requests;
* duplicate memories;
* duplicate billing records;
* duplicate files;
* duplicate background jobs;
* duplicate notifications.

Where an operation is not idempotent, the documentation and API design shall state this explicitly.

## 2.10 Atomicity Convention

A multi-step operation shall define which state changes are atomic and which are eventually consistent.

Where a complete atomic transaction is not possible because an external provider is involved, the system shall:

* record the operation state;
* preserve retry information;
* avoid duplicate charging where possible;
* expose a controlled status;
* support recovery or reconciliation;
* maintain an audit trail.

## 2.11 Time Convention

All system-generated timestamps shall be stored in a canonical timezone standard.

User interfaces may display timestamps in the user’s configured timezone.

Time-sensitive requirements shall specify:

* creation time;
* update time;
* expiration time;
* deletion-request time;
* completion time;
* retry time;
* retention deadline where applicable.

## 2.12 Audit Convention

Security-sensitive, billing-sensitive, governance-sensitive, and destructive actions shall generate audit records.

Audit records should identify:

* actor;
* action;
* target resource;
* workspace;
* timestamp;
* result;
* relevant state transition;
* failure category where applicable;
* request or correlation identifier.

Sensitive secrets, complete provider credentials, and unnecessary personal content shall not be written into audit records.

## 2.13 Error Convention

Functional errors shall be classified into stable categories, including:

* authentication error;
* authorization error;
* validation error;
* resource-not-found error;
* resource-conflict error;
* quota error;
* rate-limit error;
* provider error;
* timeout error;
* runtime-processing error;
* storage error;
* background-processing error;
* unsupported-operation error;
* internal system error.

The system shall present user-facing errors without exposing:

* credentials;
* internal stack traces;
* infrastructure details;
* private resource identifiers;
* another user’s information;
* provider secrets.

## 2.14 Traceability Convention

Every MVP functional requirement shall map to one or more of:

* PRD requirement or section;
* user problem;
* user journey;
* MVP capability;
* product principle;
* risk mitigation;
* acceptance criterion.

Every implementation task and test case shall reference the relevant functional requirement identifier.

Traceability shall support both directions:

```text
PRD → Functional Requirement → Design → Implementation → Test
```

and:

```text
Test → Implementation → Design → Functional Requirement → PRD
```

## 2.15 Change-Control Convention

Changes to approved functional requirements shall follow this process:

1. Record the proposed change.
2. Identify the reason and affected user problem.
3. Identify affected requirement identifiers.
4. Evaluate MVP scope and priority impact.
5. Review dependencies.
6. Review architecture, data, API, security, UX, and testing impact.
7. Approve or reject the change.
8. Update the document version and history.
9. Update implementation tasks.
10. Update affected tests.

No silent requirement change shall be introduced through source code alone.

---

# 3. Product Actors and Roles

## 3.1 Actor Overview

The MVP shall recognize the following actors:

1. Visitor
2. Authenticated User
3. Workspace Owner
4. Workspace Member
5. System Administrator
6. External AI Provider
7. Runtime Orchestrator
8. Background Processing Worker
9. Notification Service
10. Scheduled System Process

Not every actor represents a human account. System actors are included because they initiate or participate in functional flows.

## 3.2 Visitor

A Visitor is a person who has not authenticated.

A Visitor may be permitted to:

* access public product pages;
* access sign-up and sign-in flows;
* initiate password recovery;
* review public legal or privacy information.

A Visitor shall not be permitted to:

* access private workspaces;
* view conversations;
* view memories;
* execute provider requests;
* access provider credentials;
* view usage or billing information;
* export private data.

## 3.3 Authenticated User

An Authenticated User is a person with a valid active Gexor account and authenticated session.

An Authenticated User may be permitted to:

* access owned or assigned workspaces;
* manage personal account settings;
* create and manage conversations;
* send messages;
* connect supported providers;
* select available models;
* inspect runtime information where enabled;
* manage memories;
* view usage;
* request export;
* request account deletion.

Access shall remain subject to workspace membership, role, resource ownership, and policy.

## 3.4 Workspace Owner

A Workspace Owner is the principal authority for a workspace.

For a personal MVP workspace, the creating user shall be the Workspace Owner.

The Workspace Owner shall be permitted to:

* view and update workspace settings;
* manage provider connections;
* manage workspace-level memory;
* manage workspace data;
* configure permitted runtime controls;
* export workspace data;
* request workspace deletion;
* review workspace usage;
* manage members where collaboration is supported.

The Workspace Owner shall not be permitted to bypass platform-wide security, retention, legal, or abuse-prevention controls.

## 3.5 Workspace Member

A Workspace Member is a user granted access to a workspace owned or administered by another user or organization.

Workspace membership may be limited or deferred in the initial personal-workspace MVP.

Where membership is supported, the member’s capabilities shall be determined by an explicit role and permission set.

Workspace membership shall never imply access to:

* another workspace;
* another user’s personal memory;
* provider credentials without explicit permission;
* administrative platform data.

## 3.6 System Administrator

A System Administrator is an authorized platform operator.

Administrative access shall be limited to documented operational functions.

A System Administrator may be permitted to:

* investigate platform incidents;
* manage supported provider configurations;
* review system health;
* manage feature availability;
* manage abuse or security restrictions;
* inspect controlled audit data;
* perform approved support operations.

A System Administrator shall not receive unrestricted access to user content by default.

Access to user content, secrets, or workspace data shall require:

* an approved operational purpose;
* appropriate permission;
* auditable access;
* minimum necessary scope;
* compliance with applicable policy.

## 3.7 External AI Provider

An External AI Provider is a supported third-party service that accepts model requests and returns model-generated output.

The provider may:

* authenticate API requests;
* validate provider credentials;
* expose available models;
* accept prompts and context;
* stream or return responses;
* return token usage;
* return provider errors;
* enforce provider quotas and rate limits.

Gexor shall treat provider responses and metadata as external inputs requiring validation and controlled processing.

## 3.8 Runtime Orchestrator

The Runtime Orchestrator is the system actor responsible for coordinating synchronous request execution.

Its responsibilities shall include:

* validating execution eligibility;
* loading permitted runtime settings;
* classifying the request;
* requesting relevant context;
* enforcing context budgets;
* constructing provider-ready input;
* selecting or validating a model;
* initiating the provider request;
* coordinating streaming;
* recording execution state;
* capturing usage metadata;
* scheduling eligible background processing.

The Runtime Orchestrator shall not silently exceed user-defined provider, model, memory, or cost controls.

## 3.9 Background Processing Worker

The Background Processing Worker is a system actor responsible for asynchronous tasks that should not unnecessarily delay the primary response path.

It may perform:

* memory-candidate extraction;
* knowledge extraction;
* classification;
* deduplication;
* conflict detection;
* summarization;
* embedding generation;
* indexing;
* usage reconciliation;
* retry processing;
* cleanup;
* expiration processing.

Background processing shall preserve workspace isolation and shall operate only on authorized data.

## 3.10 Notification Service

The Notification Service is responsible for delivering eligible in-product or external notifications.

Notifications may include:

* provider-connection failures;
* memory-review requests;
* export readiness;
* deletion status;
* usage-limit warnings;
* security events;
* operational notices.

The Notification Service shall respect user preferences and shall not expose sensitive content in insecure notification channels.

## 3.11 Scheduled System Process

A Scheduled System Process initiates time-based maintenance or policy tasks.

Such tasks may include:

* memory expiration;
* temporary-context cleanup;
* export expiration;
* deletion completion;
* retry scheduling;
* usage aggregation;
* stale-job detection;
* retention enforcement.

Scheduled processing shall be idempotent where repeated execution could otherwise create duplicate or destructive results.

## 3.12 Role Assignment Principles

The system shall apply these principles:

* every protected resource shall belong to an explicit scope;
* every human actor shall access resources through an authenticated identity;
* every workspace-scoped operation shall verify workspace access;
* every privileged action shall require explicit permission;
* role changes shall take effect consistently across new requests;
* revoked access shall prevent subsequent protected operations;
* role assignment and removal shall be auditable;
* no role shall implicitly cross workspace boundaries;
* service actors shall use narrowly scoped system permissions.

---

# 4. Functional Requirement Register Introduction

The formal requirement register begins in Section 5.

The requirement domains defined by this specification are consolidated where related behaviours share actors, state, permission boundaries, or execution flows. Consolidation shall not reduce the authority, uniqueness, testability, or traceability of any individual requirement.

| Requirement Group | Section | Status |
| --- | ---: | --- |
| Identity and Authentication | 5 | Complete |
| Organization and Workspace | 6 | Complete |
| Project and Conversation | 7 | Complete |
| Message | 8 | Complete |
| Runtime Execution | 9 | Complete |
| Context, Memory, and Knowledge | 10 and 14.1 | Complete |
| AI Provider Connection and Routing | 11 | Complete |
| Streaming, File Processing, and Search | 12 | Complete |
| Usage, Billing, Notification, and Administration | 13 and 14.2 | Complete |
| Background Processing | 14.3 | Complete |
| Final acceptance and governance registers | 15–22 | Complete |

# 5. Identity and Authentication Requirements

## 5.1 Registration Requirements

### FR-AUTH-001 — User Registration

**Statement:** The system shall allow a Visitor to create a Gexor user account by submitting the mandatory registration attributes defined by the approved identity policy.

**Validation Rules:**

* The system shall validate all mandatory attributes before creating the account.
* The system shall normalize the submitted email address before uniqueness evaluation.
* The system shall reject registration when the normalized email address is already associated with an active account.
* The system shall reject malformed, unsupported, or policy-prohibited registration values.
* The system shall not create a partially initialized account when registration validation fails.

**Postconditions:**

* A unique user identity shall be created.
* The account shall be assigned an explicit lifecycle state.
* A registration audit event shall be recorded.
* Personal workspace provisioning shall be initiated according to Section 6.

---

### FR-AUTH-002 — Registration Email Verification

**Statement:** The system shall require verification of the user-controlled email address before granting full authenticated access where email verification is enabled by platform policy.

**Core Flow:**

1. The system shall generate a single-purpose verification token.
2. The system shall associate the token with the pending user account.
3. The system shall apply an expiration time to the token.
4. The system shall deliver the verification action through the configured notification channel.
5. The system shall activate the verified email state only after successful token validation.

**Failure Behaviour:**

* The system shall reject expired, malformed, revoked, or previously consumed verification tokens.
* The system shall not reveal whether an unrelated email address is registered.
* The system shall allow a replacement verification token to be requested subject to rate limits.
* Issuing a replacement token shall invalidate earlier active verification tokens where required by policy.

---

### FR-AUTH-003 — Registration Abuse Protection

**Statement:** The system shall apply configurable abuse-prevention controls to account-registration attempts.

**Validation Rules:**

* The system shall enforce request-rate limits by relevant client, network, device, or risk signal.
* The system may require additional verification when an attempt exceeds a configured risk threshold.
* The system shall reject automated or policy-prohibited registration attempts.
* The system shall record security-relevant registration failures without recording submitted passwords.

---

### FR-AUTH-004 — Account Initialization Atomicity

**Statement:** The system shall ensure that user identity creation and mandatory account initialization complete as one recoverable operation.

**Atomicity Rules:**

* The system shall not expose an account as fully active until all mandatory identity records have been created.
* If personal workspace provisioning cannot complete synchronously, the account shall remain in a controlled initialization state.
* The system shall support safe retry of incomplete initialization.
* Repeated initialization attempts shall not create duplicate user identities or duplicate personal workspaces.

---

## 5.2 Login Requirements

### FR-AUTH-005 — Credential-Based Login

**Statement:** The system shall allow an eligible registered user to authenticate using an approved login identifier and valid authentication credential.

**Validation Rules:**

* The system shall validate the normalized login identifier.
* The system shall compare the supplied credential using an approved credential-verification mechanism.
* The system shall verify that the account is active and permitted to authenticate.
* The system shall reject authentication when the credential is invalid, the account is disabled, or the authentication method is unavailable.

**Postconditions:**

* A new authenticated session shall be created following successful authentication.
* The successful authentication event shall be recorded.
* The system shall update the applicable last-authentication metadata.

---

### FR-AUTH-006 — Authentication Failure Privacy

**Statement:** The system shall return a generic authentication failure response that does not disclose whether the submitted account identifier exists.

**Error Rules:**

* The response shall not distinguish between an unknown account, an invalid password, an inactive account, or a disabled account unless disclosure is explicitly permitted after an independently authenticated step.
* Internal audit records may preserve the specific failure category.
* User-facing errors shall not expose credential hashes, identity-provider responses, stack traces, or internal account identifiers.

---

### FR-AUTH-007 — Login Attempt Throttling

**Statement:** The system shall throttle repeated failed authentication attempts according to configurable security policy.

**Validation Rules:**

* Throttling may be evaluated by account, network source, device, session, or combined risk signal.
* The system shall apply increasing delay, temporary restriction, additional verification, or account-protection action when configured thresholds are reached.
* Successful authentication shall not automatically erase security audit evidence.
* Throttling controls shall not disclose whether the target account exists.

---

### FR-AUTH-008 — Account Lock and Restriction

**Statement:** The system shall support temporary or administrative restriction of authentication for an account.

**Core Behaviour:**

* A restricted account shall not receive a new authenticated session.
* Existing sessions shall be revoked when required by the restriction policy.
* The restriction shall include a reason category, effective time, actor, and applicable expiration or review state.
* Administrative restriction and restoration shall generate audit records.
* The user-facing response shall not reveal sensitive administrative or security details.

---

### FR-AUTH-009 — Optional Federated Authentication

**Statement:** Where approved federated identity providers are enabled, the system may allow a Visitor to authenticate through a supported external identity provider.

**Validation Rules:**

* The system shall validate the external identity-provider response.
* The system shall bind the external identity to exactly one Gexor account unless an approved account-linking workflow states otherwise.
* The system shall not trust unverified external claims.
* The system shall prevent creation of duplicate accounts caused by repeated federated login attempts.
* External provider failure shall not corrupt existing Gexor account state.

---

## 5.3 Password Requirements

### FR-AUTH-010 — Password Creation

**Statement:** Where password authentication is supported, the system shall require newly created passwords to satisfy the approved password policy.

**Validation Rules:**

* The policy shall define the minimum acceptable length.
* The system shall reject passwords found in a configured prohibited-password set where such checking is enabled.
* The system shall reject passwords that exceed supported processing bounds.
* The system shall not silently truncate passwords.
* The system should permit password-manager-generated values and supported special characters.

---

### FR-AUTH-011 — Password Storage

**Statement:** The system shall store user passwords only as outputs of an approved one-way password-hashing function with unique salts and configured work factors.

**Security Rules:**

* The system shall not store plaintext passwords.
* The system shall not store reversibly encrypted passwords.
* Password values shall not be written to logs, audit events, traces, analytics, or error reports.
* Password verification shall use constant-time comparison where technically applicable.
* Hashing parameters shall be upgradeable without requiring plaintext password recovery.

---

### FR-AUTH-012 — Password Change

**Statement:** The system shall allow an Authenticated User to change the account password after satisfying the applicable re-authentication policy.

**Core Flow:**

1. The user shall provide the current credential or complete an approved re-authentication method.
2. The system shall validate the replacement password.
3. The system shall replace the stored password representation.
4. The system shall record the password-change time.
5. The system shall revoke other sessions where required by policy.

**Failure Behaviour:**

* An invalid current credential shall prevent the change.
* A replacement password that fails policy shall be rejected.
* Failure shall not modify the active password.
* The system shall not include either credential in an audit record.

---

### FR-AUTH-013 — Password-Reuse Control

**Statement:** Where password-history enforcement is enabled, the system shall reject reuse of password values covered by the configured history policy.

**Validation Rules:**

* Password-history comparison shall not require recovery of previous plaintext passwords.
* Password-history records shall receive equivalent protection to the active password representation.
* Failure shall not reveal which historical password matched.

---

## 5.4 Password Recovery Requirements

### FR-AUTH-014 — Password-Recovery Request

**Statement:** The system shall allow a Visitor to request password recovery for an account using an approved account identifier.

**Privacy Rules:**

* The system shall return a neutral response regardless of whether the account exists.
* The system shall rate-limit recovery requests.
* The system shall not send recovery credentials to unverified destinations.
* The system shall record security-relevant request metadata without recording submitted passwords.

---

### FR-AUTH-015 — Password-Recovery Token

**Statement:** The system shall generate a single-purpose, time-limited, cryptographically unpredictable token for an eligible password-recovery request.

**Validation Rules:**

* The token shall be bound to one account and one recovery purpose.
* The token shall expire after the configured recovery period.
* The token shall become unusable after successful consumption.
* Issuing a replacement token shall invalidate earlier active recovery tokens where required by policy.
* The stored token representation shall not expose the usable token value where hashing is technically feasible.

---

### FR-AUTH-016 — Password Reset Completion

**Statement:** The system shall allow the user to establish a replacement password after successful validation of an active password-recovery token.

**Postconditions:**

* The active password representation shall be replaced.
* The recovery token shall be consumed.
* Existing sessions shall be revoked according to security policy.
* A password-reset audit event shall be recorded.
* The user shall receive an applicable security notification.

**Failure Behaviour:**

* Expired, malformed, revoked, or consumed tokens shall be rejected.
* Failure shall not modify the password or session state.
* Repeated completion requests using the same consumed token shall remain unsuccessful.

---

## 5.5 Logout and Session Requirements

### FR-AUTH-017 — Current-Session Logout

**Statement:** The system shall allow an Authenticated User to terminate the current authenticated session.

**Postconditions:**

* The current session shall no longer authorize protected requests.
* Relevant session credentials shall be invalidated or removed.
* The logout operation shall be idempotent.
* Repeating logout for an already terminated session shall not recreate or extend the session.

---

### FR-AUTH-018 — Logout From All Sessions

**Statement:** The system shall allow an Authenticated User to terminate all active sessions associated with the account after satisfying applicable re-authentication controls.

**Core Behaviour:**

* All revocable sessions shall be invalidated.
* The system may preserve the initiating session only where the user explicitly selects that option and policy permits it.
* Session termination shall propagate to protected APIs within the documented consistency boundary.
* The action shall generate an audit event.

---

### FR-AUTH-019 — Session Creation

**Statement:** The system shall create a unique authenticated session after successful authentication.

**Session Data Requirements:**

* Each session shall have a unique identifier.
* Each session shall be associated with exactly one user identity.
* Each session shall record creation time and applicable expiration time.
* Each session shall include the authentication assurance information required by policy.
* Session records shall not contain plaintext passwords or provider API keys.

---

### FR-AUTH-020 — Session Expiration

**Statement:** The system shall enforce configurable session inactivity and absolute-lifetime limits.

**Time Rules:**

* An expired session shall not authorize protected operations.
* Session extension shall not exceed the configured absolute lifetime.
* The system shall use server-evaluated time for authorization decisions.
* Client-side time shall not be trusted for session validity.
* Expiration shall apply consistently across supported clients.

---

### FR-AUTH-021 — Session Renewal

**Statement:** The system may renew an eligible session without requiring full authentication when the renewal request satisfies the approved session-renewal policy.

**Validation Rules:**

* The existing renewal credential shall be valid, unexpired, and unrevoked.
* Renewal shall rotate the renewal credential where token rotation is enabled.
* Reuse of an already rotated credential shall trigger the configured session-protection response.
* Renewal shall not increase the authentication assurance level without additional verification.

---

### FR-AUTH-022 — Session Revocation

**Statement:** The system shall support immediate logical revocation of a specific session.

**Core Behaviour:**

* Revoked sessions shall fail subsequent authorization checks.
* Revocation shall be idempotent.
* Session revocation shall include actor, reason category, and timestamp.
* Security-triggered revocation shall be auditable.
* Revocation failure shall not falsely report successful termination.

---

### FR-AUTH-023 — Concurrent Session Inspection

**Statement:** The system should allow an Authenticated User to inspect active sessions associated with the account.

**Displayed Information:**

* Approximate device or client description;
* session creation time;
* last activity time;
* approximate location where available and permitted;
* current-session indicator;
* session expiration state.

The system shall not display reusable session secrets.

---

### FR-AUTH-024 — Session Credential Protection

**Statement:** The system shall protect session credentials against unauthorized disclosure, replay, and client-side access beyond the requirements of the supported client architecture.

**Security Rules:**

* Session credentials shall be transmitted only through approved encrypted transport.
* Browser session cookies shall use applicable secure, HTTP-only, and same-site controls.
* Session tokens shall not be written to application logs.
* Session credentials shall be invalidated on logout, revocation, or expiration.
* The system shall not place reusable credentials in user-visible URLs.

---

## 5.6 Re-authentication Requirements

### FR-AUTH-025 — Sensitive-Action Re-authentication

**Statement:** The system shall require recent authentication or an approved additional verification step before completing designated sensitive operations.

**Sensitive Operations May Include:**

* password change;
* account deletion;
* provider-key display or replacement;
* complete data export;
* session-wide logout;
* high-impact workspace administration.

**Failure Behaviour:**

* Failure to re-authenticate shall prevent the sensitive action.
* Re-authentication failure shall not invalidate the existing session unless security policy requires it.
* The system shall record repeated suspicious failures.

---

## 5.7 AI Provider Credential Protection Requirements

### FR-AUTH-026 — Provider Credential Submission

**Statement:** The system shall allow an authorized Workspace Owner to submit a supported AI-provider credential through an approved protected interface.

**Validation Rules:**

* The system shall validate the provider type.
* The system shall reject empty, malformed, or unsupported credential values.
* The system shall verify workspace-level permission before accepting the credential.
* The credential shall be transmitted only through encrypted transport.
* The credential shall not be returned in a normal response after submission.

---

### FR-AUTH-027 — Provider Credential Encryption

**Statement:** The system shall encrypt each stored AI-provider credential using an approved secrets-management or encryption mechanism before durable persistence.

**Security Rules:**

* Provider credentials shall not be stored as plaintext.
* Encryption keys shall be logically separated from encrypted credential records.
* Encryption-key access shall be restricted to authorized runtime services.
* Provider credentials shall not be included in database exports intended for normal user portability.
* Credential encryption and decryption operations shall be auditable at the service-action level without recording credential values.

---

### FR-AUTH-028 — Provider Credential Vaulting

**Statement:** The system should store provider credentials in a dedicated secrets vault or equivalent controlled credential store.

**Core Behaviour:**

* Application records shall reference a secret identifier rather than contain the reusable secret where the selected architecture supports vaulting.
* Secret retrieval shall require service identity and workspace authorization context.
* Secret values shall be released only to the minimum runtime component requiring provider authentication.
* Retrieved secret values shall not be cached longer than operationally necessary.

---

### FR-AUTH-029 — Provider Credential Masking

**Statement:** The system shall display stored provider credentials only in masked, non-recoverable form.

**Display Rules:**

* The user interface shall not reveal the complete stored secret.
* Masked display may include a limited provider-approved prefix or suffix.
* Copying a previously stored full credential shall not be supported.
* To replace a credential, the user shall submit a new value.

---

### FR-AUTH-030 — Provider Credential Access Control

**Statement:** The system shall restrict provider-credential creation, replacement, validation, disabling, and deletion to explicitly authorized actors.

**Permission Rules:**

* Workspace ownership alone shall not bypass a stricter organization-level credential policy where applicable.
* Workspace Members shall not access provider credentials unless explicitly permitted.
* System Administrators shall not receive plaintext credential access through ordinary administrative functions.
* Unauthorized attempts shall generate controlled authorization errors.
* Security-relevant access attempts shall be auditable.

---

### FR-AUTH-031 — Provider Credential Replacement

**Statement:** The system shall allow an authorized actor to replace an existing provider credential without exposing the previous credential.

**Atomicity Rules:**

* The replacement credential shall be validated before becoming active where provider validation is available.
* The previous credential shall remain active until the replacement is committed or shall enter a clearly defined disabled state.
* Failure during replacement shall not leave an ambiguous active credential state.
* Successful replacement shall invalidate references to the previous credential according to the credential-storage design.

---

### FR-AUTH-032 — Provider Credential Deletion

**Statement:** The system shall allow an authorized actor to delete or disconnect a stored provider credential.

**Postconditions:**

* The deleted credential shall no longer be available for new provider requests.
* Associated provider connections shall enter a disconnected or unavailable state.
* The secret shall be removed from the credential store according to the applicable deletion guarantee.
* Cached credential material shall be invalidated.
* The action shall generate an audit event.

---

### FR-AUTH-033 — Provider Credential Logging Prohibition

**Statement:** The system shall not write complete provider API keys, access tokens, refresh tokens, client secrets, or equivalent reusable credentials to logs, traces, analytics, audit records, exception messages, or user-visible errors.

---

### FR-AUTH-034 — Credential-Rotation Support

**Statement:** The system shall support replacement and rotation of provider credentials without requiring deletion of the associated workspace, conversations, memories, or usage history.

---

### FR-AUTH-035 — Identity Audit Events

**Statement:** The system shall generate audit events for security-significant identity operations.

**Events Shall Include, Where Applicable:**

* registration;
* verification;
* successful and failed login;
* password change;
* password reset;
* session revocation;
* account restriction;
* provider credential creation;
* provider credential replacement;
* provider credential deletion.

Audit events shall exclude passwords, recovery tokens, session secrets, and provider credential values.

---

# 6. Organization and Workspace Requirements

## 6.1 Organization Scope

### FR-WORKSPACE-001 — Organization Record Support

**Statement:** The system shall support an organization scope capable of containing one or more workspaces, users, roles, provider policies, and governance settings where organization functionality is enabled.

**Scope Rule:** Organization support may remain operationally limited in the personal-workspace MVP, but the system shall not model personal workspace data in a manner that prevents future organization assignment.

---

### FR-WORKSPACE-002 — Personal Organization Context

**Statement:** Where the platform architecture requires an organization boundary for all workspaces, the system shall create or assign a personal organization context for each eligible user without exposing unnecessary organizational complexity in the MVP user experience.

---

### FR-WORKSPACE-003 — Organization Isolation

**Statement:** The system shall prevent a user, service, query, job, cache entry, search result, export, or administrative operation from accessing another organization’s protected data without explicit authorized cross-organization capability.

---

## 6.2 Personal Workspace Provisioning

### FR-WORKSPACE-004 — Personal Workspace Creation

**Statement:** The system shall provision one personal workspace for each newly eligible user account.

**Postconditions:**

* The user shall be assigned as Workspace Owner.
* The workspace shall have a unique identifier.
* The workspace shall have an active lifecycle state.
* Default workspace settings shall be applied.
* Workspace creation shall be auditable.

---

### FR-WORKSPACE-005 — Workspace Provisioning Idempotency

**Statement:** Personal workspace provisioning shall be idempotent for a given user and provisioning purpose.

**Idempotency Rules:**

* Repeated provisioning attempts shall not create duplicate personal workspaces.
* A retried request shall return or reconcile with the existing workspace.
* Conflicting duplicate workspace records shall be detected and isolated for administrative resolution.

---

### FR-WORKSPACE-006 — Workspace Provisioning Recovery

**Statement:** The system shall support recovery from interrupted workspace provisioning.

**Core Behaviour:**

* Incomplete provisioning shall be represented by an explicit state.
* Protected workspace features shall remain unavailable until mandatory initialization completes.
* Recovery shall resume from the last valid state or safely restart initialization.
* Recovery shall not duplicate default records, roles, or settings.

---

### FR-WORKSPACE-007 — Default Workspace Naming

**Statement:** The system shall assign a default display name to a newly provisioned personal workspace and shall allow the Workspace Owner to replace it with a valid name.

**Validation Rules:**

* The name shall satisfy configured length and character bounds.
* The name shall not be interpreted as an authorization boundary.
* Renaming shall not modify the stable workspace identifier.

---

## 6.3 Workspace Lifecycle

### FR-WORKSPACE-008 — Workspace State Model

**Statement:** The system shall maintain an explicit workspace lifecycle state.

**Supported States Shall Include, at Minimum:**

* provisioning;
* active;
* restricted;
* deletion pending;
* deleted.

Additional states may be defined in dependent design documents.

---

### FR-WORKSPACE-009 — Active Workspace Access

**Statement:** The system shall permit normal workspace operations only when the workspace is active and the actor has the required permission.

---

### FR-WORKSPACE-010 — Restricted Workspace Behaviour

**Statement:** The system shall prevent prohibited operations within a restricted workspace while preserving access to any actions explicitly allowed by the restriction policy.

**Examples of Allowed Actions May Include:**

* viewing restriction status;
* exporting permitted data;
* resolving billing or security conditions;
* completing deletion.

---

### FR-WORKSPACE-011 — Workspace Setting Update

**Statement:** The system shall allow an authorized Workspace Owner to update supported workspace settings.

**Validation Rules:**

* The system shall validate each setting independently.
* Unknown settings shall be rejected.
* Invalid combinations shall produce a controlled validation error.
* A failed update shall not partially apply an indivisible setting group.
* Security-significant settings changes shall be audited.

---

### FR-WORKSPACE-012 — Workspace Deactivation

**Statement:** The system may support deactivation of a workspace without immediately deleting its data.

**Postconditions:**

* New runtime executions shall be blocked.
* Existing data shall remain retained according to policy.
* Background jobs shall be cancelled, suspended, or completed according to their type.
* Reactivation shall require authorized action.

---

## 6.4 Workspace Membership and Ownership

### FR-WORKSPACE-013 — Workspace Ownership Binding

**Statement:** Every workspace shall have at least one valid ownership or administrative authority record unless the workspace is in a terminal deleted state.

---

### FR-WORKSPACE-014 — Workspace Membership Verification

**Statement:** The system shall verify active workspace membership or ownership before authorizing any workspace-scoped operation.

**Permission Rules:**

* A valid user session alone shall not grant workspace access.
* The requested resource’s workspace identifier shall match the authorized workspace context.
* Revoked or expired membership shall not authorize new operations.
* The absence of permission shall result in denial.

---

### FR-WORKSPACE-015 — Workspace Context Selection

**Statement:** The system shall require an explicit workspace context for each workspace-scoped operation.

**Validation Rules:**

* The system shall not infer workspace context solely from untrusted client-supplied resource metadata.
* The context shall be resolved against the authenticated actor’s permissions.
* Ambiguous workspace context shall be rejected.
* Background jobs shall carry an immutable workspace scope.

---

### FR-WORKSPACE-016 — Workspace Ownership Transfer

**Statement:** Where ownership transfer is enabled, the system shall transfer workspace ownership only through an explicit, authorized, and auditable workflow.

**Validation Rules:**

* The receiving identity shall be eligible.
* The workspace shall not be left without an owner.
* The transfer shall not expose provider credentials to the recipient unless credential policy permits continued use.
* Failure shall preserve the prior ownership state.

---

## 6.5 Data Segregation and Multi-Tenant Isolation

### FR-WORKSPACE-017 — Workspace Data Ownership

**Statement:** Every workspace-scoped record shall be associated with a stable workspace identifier.

**Covered Records Shall Include, at Minimum:**

* projects;
* conversations;
* messages;
* runtime executions;
* memories;
* files;
* search indexes;
* embeddings;
* provider connections;
* usage records;
* exports;
* background jobs;
* audit events where applicable.

---

### FR-WORKSPACE-018 — Query Scope Enforcement

**Statement:** Every data-access operation involving workspace-scoped data shall enforce workspace filtering at the trusted application or data-access boundary.

**Security Rules:**

* The system shall not rely only on client-side filtering.
* A resource identifier shall not be sufficient to bypass workspace filtering.
* Bulk operations shall apply the same scope enforcement as single-resource operations.
* Search and analytics queries shall preserve workspace boundaries.

---

### FR-WORKSPACE-019 — Cross-Workspace Leakage Prevention

**Statement:** The system shall not include data from one workspace in another workspace’s prompt, memory retrieval, search result, export, notification, usage report, cache response, or administrative view unless an explicit authorized cross-workspace function requires it.

---

### FR-WORKSPACE-020 — Cache Segregation

**Statement:** Workspace-scoped cached data shall be keyed and validated using the applicable workspace boundary.

**Validation Rules:**

* Cache keys shall prevent collisions between workspaces.
* Cached authorization decisions shall expire or be invalidated after access revocation.
* Shared caches shall not return content without re-establishing the workspace context.
* Cache failure shall not weaken authorization enforcement.

---

### FR-WORKSPACE-021 — Vector Index Segregation

**Statement:** The system shall segregate vector embeddings and vector-search operations by workspace.

**Search Rules:**

* Every indexed vector shall carry an immutable workspace scope.
* Every vector query shall include the authorized workspace scope.
* The system shall reject unscoped vector searches.
* Results failing workspace verification shall be discarded and recorded as a security fault.

---

### FR-WORKSPACE-022 — Keyword Index Segregation

**Statement:** The system shall segregate keyword and full-text search indexes by workspace or apply equivalent mandatory workspace filters during every search.

---

### FR-WORKSPACE-023 — Background Job Segregation

**Statement:** Every Background Processing Worker job shall include the workspace identifier and authorization-relevant processing scope required to prevent cross-workspace data access.

**Validation Rules:**

* Workers shall validate job scope before accessing data.
* Jobs lacking valid workspace scope shall fail closed.
* Retried jobs shall retain the original workspace scope.
* Job reassignment shall not change the workspace boundary.

---

### FR-WORKSPACE-024 — Event Segregation

**Statement:** Workspace-scoped events shall include the stable workspace identifier and shall be consumable only by services authorized for that event scope.

---

### FR-WORKSPACE-025 — File Storage Segregation

**Statement:** Uploaded and derived files shall be stored using a workspace-isolated storage path, namespace, access policy, or equivalent segregation control.

**Security Rules:**

* A file-storage object reference shall not grant access without workspace authorization.
* Temporary download links shall be time limited.
* Derived files shall inherit the source workspace scope.
* Deleted workspace files shall not remain available through previously issued links after their permitted validity period.

---

### FR-WORKSPACE-026 — Provider Connection Segregation

**Statement:** A provider connection created for one workspace shall not be used to execute requests for another workspace unless an explicit organization-level sharing policy authorizes that use.

---

### FR-WORKSPACE-027 — Usage Record Segregation

**Statement:** Token, cost, quota, and billing records shall be attributed to the workspace and user context responsible for the execution.

---

### FR-WORKSPACE-028 — Audit Record Segregation

**Statement:** Workspace-level audit queries shall return only events authorized for the requesting actor’s workspace and administrative scope.

---

### FR-WORKSPACE-029 — Export Segregation

**Statement:** A workspace export shall contain only the selected workspace’s authorized data and shall exclude data belonging to other workspaces, organizations, or users.

**Validation Rules:**

* Export generation shall verify each included record’s workspace scope.
* A failed scope verification shall stop or quarantine the export.
* Export completion shall not be reported until integrity validation succeeds.

---

### FR-WORKSPACE-030 — Workspace Deletion Boundary

**Statement:** Deleting a workspace shall affect only records owned by or explicitly derived from that workspace.

**Safety Rules:**

* Shared platform configuration shall not be deleted.
* Another workspace’s records shall not be modified.
* Provider-side deletion requests shall be limited to data attributable to the deleted workspace where supported.
* Deletion shall preserve legally required minimal audit evidence without preserving prohibited user content.

---

## 6.6 Workspace Environment State

### FR-WORKSPACE-031 — Workspace Runtime Configuration

**Statement:** The system shall maintain workspace-level runtime configuration independently from user-interface state.

**Configuration May Include:**

* default provider;
* default model;
* memory mode;
* prompt-enhancement mode;
* context limits;
* spending limits;
* file-processing settings;
* permitted fallback behaviour.

---

### FR-WORKSPACE-032 — Workspace Configuration Versioning

**Statement:** The system shall identify the effective workspace configuration used for each runtime execution.

**Audit Rules:**

* Runtime records shall preserve either the configuration version or an immutable execution snapshot.
* Later setting changes shall not rewrite the historical configuration used by completed executions.
* Replayed or retried operations shall identify whether the original or current configuration applies.

---

### FR-WORKSPACE-033 — Workspace State Consistency

**Statement:** The system shall prevent operations that are incompatible with the current workspace state.

**Examples:**

* A deletion-pending workspace shall not create new conversations.
* A restricted workspace shall not initiate prohibited provider requests.
* A deleted workspace shall not authorize data retrieval.
* A provisioning workspace shall not execute runtime requests before mandatory initialization completes.

---

### FR-WORKSPACE-034 — Workspace Access Audit

**Statement:** The system shall audit privileged workspace operations, including ownership changes, security-setting changes, provider-connection changes, export requests, restrictions, and deletion actions.

---

# 7. Project and Conversation Requirements

## 7.1 Project Requirements

### FR-CONVERSATION-001 — Project Creation

**Statement:** The system shall allow an authorized Authenticated User to create a project within an active workspace.

**Validation Rules:**

* The project name shall satisfy configured bounds.
* The project shall be assigned to exactly one workspace.
* The creator shall have project-creation permission.
* Failed validation shall not create a project.

---

### FR-CONVERSATION-002 — Project Stable Identifier

**Statement:** Each project shall receive a stable identifier that shall not change when the project is renamed, archived, restored, or moved between permitted lifecycle states.

---

### FR-CONVERSATION-003 — Project Update

**Statement:** The system shall allow an authorized actor to update supported project attributes.

**Updatable Attributes May Include:**

* display name;
* description;
* status;
* default runtime settings;
* project instructions;
* project-level memory settings.

The system shall validate project settings against workspace policy.

---

### FR-CONVERSATION-004 — Project Archive

**Statement:** The system shall allow an authorized actor to archive an active project.

**Postconditions:**

* Archived projects shall be excluded from default active-project views.
* Existing project content shall remain retained.
* New conversations shall be blocked unless policy allows creation in archived projects.
* Archiving shall not delete memories, files, conversations, or usage history.

---

### FR-CONVERSATION-005 — Project Restore

**Statement:** The system shall allow an authorized actor to restore an archived project when the containing workspace is active.

---

### FR-CONVERSATION-006 — Project Deletion

**Statement:** The system shall support soft deletion and controlled permanent deletion of a project.

**Deletion Rules:**

* Soft deletion shall prevent normal project access.
* Permanent deletion shall require explicit authorized confirmation.
* Dependent conversations, files, memories, indexes, and derived records shall be processed according to the approved deletion policy.
* Deletion shall not cross the workspace boundary.

---

## 7.2 Conversation Creation and Identification

### FR-CONVERSATION-007 — Conversation Creation

**Statement:** The system shall allow an authorized Authenticated User to create a conversation within an active workspace and, where applicable, an active project.

**Postconditions:**

* The conversation shall have a unique stable identifier.
* The conversation shall be bound to exactly one workspace.
* The conversation may be bound to one project.
* The creator and creation time shall be recorded.
* The conversation shall enter an active state.

---

### FR-CONVERSATION-008 — Conversation-Creation Idempotency

**Statement:** The conversation-creation operation should support an idempotency key to prevent duplicate conversations caused by retries.

**Idempotency Rules:**

* Repeated requests using the same valid key and equivalent payload shall return the original result.
* Reuse of the same key with a conflicting payload shall produce a conflict error.
* Idempotency records shall expire according to documented policy.

---

### FR-CONVERSATION-009 — Conversation Default Title

**Statement:** The system shall assign a default title when a conversation is created without an explicit valid title.

**Core Behaviour:**

* The default title may be generated from the first eligible user message.
* Title generation shall not delay message submission beyond the defined interaction requirement.
* Title-generation failure shall not fail the conversation or message.
* The user shall remain able to rename the conversation.

---

### FR-CONVERSATION-010 — Conversation Naming

**Statement:** The system shall allow an authorized actor to assign or update the conversation title.

**Validation Rules:**

* The title shall satisfy configured length and character bounds.
* Empty or whitespace-only values shall be rejected unless automatic naming is requested.
* Renaming shall not change the conversation identifier.
* The update time shall be recorded.

---

### FR-CONVERSATION-011 — Conversation Metadata

**Statement:** The system shall maintain metadata for each conversation.

**Metadata Shall Include, at Minimum:**

* conversation identifier;
* workspace identifier;
* optional project identifier;
* title;
* lifecycle state;
* creator identifier;
* creation time;
* update time;
* last-message time where applicable;
* selected provider or model defaults where configured.

---

## 7.3 Conversation Retrieval and Listing

### FR-CONVERSATION-012 — Conversation Retrieval

**Statement:** The system shall allow an authorized actor to retrieve an accessible conversation and its permitted metadata.

**Permission Rules:**

* The system shall verify workspace access.
* The conversation shall belong to the selected workspace.
* Soft-deleted conversations shall not be returned through normal retrieval.
* Unauthorized and non-existent resources shall produce privacy-preserving error behaviour.

---

### FR-CONVERSATION-013 — Conversation Listing

**Statement:** The system shall allow an authorized actor to list conversations within the selected workspace or project.

**List Controls Shall Support:**

* lifecycle-state filtering;
* project filtering;
* creation or update-time sorting;
* pagination;
* title search where enabled.

The system shall apply workspace filtering before returning results.

---

### FR-CONVERSATION-014 — Conversation Pagination

**Statement:** Conversation lists shall use deterministic pagination.

**Validation Rules:**

* Page-size bounds shall be enforced.
* Pagination shall not duplicate or omit records under normal stable ordering.
* Invalid cursors shall produce a controlled validation error.
* Pagination tokens shall not expose sensitive query internals.

---

## 7.4 Conversation Updates

### FR-CONVERSATION-015 — Conversation Attribute Update

**Statement:** The system shall allow an authorized actor to update supported mutable conversation attributes.

**Mutable Attributes May Include:**

* title;
* project assignment;
* archive state;
* runtime preferences;
* memory-exclusion setting;
* provider or model override.

Invalid updates shall not partially modify an indivisible update group.

---

### FR-CONVERSATION-016 — Conversation Project Reassignment

**Statement:** Where project reassignment is supported, the system shall allow an authorized actor to move a conversation between eligible projects within the same workspace.

**Validation Rules:**

* Source and target projects shall belong to the same workspace.
* The target project shall be active or otherwise eligible.
* Reassignment shall not change the conversation’s workspace.
* Project-specific memory and context effects shall be recalculated for future executions.
* Historical execution records shall preserve their original project context.

---

### FR-CONVERSATION-017 — Conversation Runtime Preference

**Statement:** The system may allow conversation-specific runtime settings that override eligible workspace or project defaults.

**Precedence Rule:**

1. Mandatory platform policy;
2. organization policy;
3. workspace policy;
4. project setting;
5. conversation setting;
6. per-message setting.

A lower-level setting shall not override a mandatory higher-level restriction.

---

## 7.5 Archive and Restore

### FR-CONVERSATION-018 — Conversation Archive

**Statement:** The system shall allow an authorized actor to archive an active conversation.

**Postconditions:**

* The conversation shall enter an archived state.
* It shall be excluded from default active-conversation listings.
* Existing messages and metadata shall remain retained.
* New messages shall be blocked unless archived-conversation continuation is explicitly supported.
* Archive time and actor shall be recorded.

---

### FR-CONVERSATION-019 — Conversation Restore

**Statement:** The system shall allow an authorized actor to restore an archived conversation when its workspace and project are eligible.

**Failure Behaviour:**

* Restoration shall fail if the workspace is deleted or deletion pending.
* Restoration shall fail or require reassignment if the associated project is permanently deleted.
* Failure shall preserve the archived state.

---

## 7.6 Soft Deletion

### FR-CONVERSATION-020 — Conversation Soft Delete

**Statement:** The system shall allow an authorized actor to soft-delete a conversation.

**Postconditions:**

* The conversation shall enter a soft-deleted state.
* It shall be excluded from normal listings, search, context retrieval, and runtime execution.
* Messages and dependent records shall remain retained for the configured recovery period.
* Deletion actor and time shall be recorded.
* Active generation shall be cancelled or marked for cancellation.

---

### FR-CONVERSATION-021 — Soft-Delete Idempotency

**Statement:** Repeated soft-delete requests for the same already soft-deleted conversation shall succeed idempotently without creating duplicate deletion records.

---

### FR-CONVERSATION-022 — Conversation Recovery

**Statement:** The system shall allow an authorized actor to restore a soft-deleted conversation during the configured recovery period.

**Validation Rules:**

* The workspace shall remain active.
* The recovery period shall not have expired.
* The conversation shall not have entered permanent-deletion processing.
* Restoration shall reactivate eligible dependent search and retrieval references.

---

## 7.7 Permanent Deletion

### FR-CONVERSATION-023 — Permanent Conversation Deletion Request

**Statement:** The system shall require explicit authorized confirmation before permanently deleting a conversation.

**Validation Rules:**

* The conversation shall belong to the selected workspace.
* The requesting actor shall have permanent-deletion permission.
* Re-authentication may be required.
* The system shall identify affected dependent data before accepting the request.
* The request shall be auditable.

---

### FR-CONVERSATION-024 — Permanent Conversation Deletion Processing

**Statement:** The system shall permanently delete or irreversibly de-identify the conversation and its exclusively owned dependent content according to the approved deletion policy.

**Dependent Content Shall Include, Where Applicable:**

* messages;
* generated responses;
* attachments;
* conversation summaries;
* conversation-scoped memories;
* embeddings;
* keyword indexes;
* caches;
* background jobs;
* temporary processing records.

---

### FR-CONVERSATION-025 — Permanent Deletion Integrity

**Statement:** The system shall verify that permanent conversation deletion does not remove shared records still required by another authorized resource.

**Safety Rules:**

* Shared workspace memory shall not be deleted solely because it was retrieved into the conversation.
* A memory derived exclusively from the deleted conversation shall be deleted or re-evaluated according to provenance policy.
* Shared files shall be deleted only when no retained resource requires them.
* Usage and minimal audit records may be retained only where legally or operationally required.

---

### FR-CONVERSATION-026 — Permanent Deletion State

**Statement:** A conversation accepted for permanent deletion shall enter a deletion-pending state until all required deletion steps complete.

**Core Behaviour:**

* The conversation shall not accept new messages.
* It shall not appear in normal search or retrieval.
* Retried deletion jobs shall be idempotent.
* Completion shall be recorded.
* Partial failure shall remain visible to authorized operational processes until reconciled.

---

## 7.8 Conversation Integrity and Audit

### FR-CONVERSATION-027 — Conversation Ordering

**Statement:** The system shall maintain deterministic message ordering within a conversation using server-controlled sequence or timestamp data.

---

### FR-CONVERSATION-028 — Conversation Activity Time

**Statement:** The system shall update the conversation’s last-activity time after accepted user messages and completed system events that qualify as activity.

**Time Rule:** Background maintenance tasks shall not update user-visible activity time unless explicitly defined as conversation activity.

---

### FR-CONVERSATION-029 — Conversation Exclusion From Memory

**Statement:** The system shall allow an authorized user to mark a conversation as excluded from future memory extraction where the workspace policy permits such control.

**Postconditions:**

* New memory extraction shall not process excluded conversation content.
* Existing memories derived from the conversation shall be reviewed or handled according to explicit user action and provenance policy.
* Exclusion shall not silently delete existing memories.

---

### FR-CONVERSATION-030 — Conversation Audit Events

**Statement:** The system shall audit conversation creation, project reassignment, archive, restore, soft deletion, recovery, permanent-deletion request, and permanent-deletion completion.

---

# 8. Message Requirements

## 8.1 Message Creation

### FR-MSG-001 — User Message Submission

**Statement:** The system shall allow an authorized Authenticated User to submit a message to an eligible active conversation.

**Validation Rules:**

* The conversation shall belong to the selected workspace.
* The actor shall have message-creation permission.
* The conversation and workspace shall permit new messages.
* The message shall satisfy supported type, content, and size bounds.
* Applicable provider, quota, and spending validations shall complete before provider execution.

---

### FR-MSG-002 — Message Stable Identifier

**Statement:** Each accepted message shall receive a unique stable identifier before or at the start of runtime processing.

---

### FR-MSG-003 — Message Workspace Binding

**Statement:** Each message shall be permanently bound to exactly one workspace and one conversation.

**Security Rule:** A message shall not be moved across workspace boundaries.

---

### FR-MSG-004 — Message Project Binding

**Statement:** Each message shall record the effective project context, where applicable, at the time of submission.

**Historical Rule:** Later conversation reassignment shall not rewrite the project context of an already completed runtime execution.

---

### FR-MSG-005 — Message Idempotency

**Statement:** Message submission shall support an idempotency key to prevent duplicate user messages and duplicate provider executions caused by client retries.

**Idempotency Rules:**

* Equivalent retries shall return the original accepted message.
* Conflicting payload reuse shall produce a conflict error.
* A provider request shall not be repeated solely because the client did not receive the original acceptance response.
* Idempotency scope shall include the user, workspace, conversation, and operation.

---

## 8.2 Message Content and Validation

### FR-MSG-006 — Supported Message Content

**Statement:** The system shall accept supported textual message content and approved attachment references.

**Validation Rules:**

* Unsupported content types shall be rejected.
* Empty messages shall be rejected unless a supported attachment-only message is permitted.
* Whitespace normalization shall not alter intentional user formatting beyond documented behaviour.
* Message content exceeding configured bounds shall be rejected before provider execution.

---

### FR-MSG-007 — Message Content Preservation

**Statement:** The system shall preserve the user-submitted message content as the canonical user input, subject only to explicit normalization required for safe storage.

**Transparency Rule:** Prompt enhancement shall not overwrite the canonical user message.

---

### FR-MSG-008 — Message Edit Policy

**Statement:** Where message editing is supported, the system shall preserve the original message version or equivalent audit history.

**Core Behaviour:**

* Editing a message shall not silently rewrite a completed provider execution.
* Re-execution after an edit shall create a new execution record.
* The system shall distinguish edited content from the original submission.
* Editing shall be blocked while an incompatible active generation is in progress.

---

## 8.3 Message State Model

### FR-MSG-009 — Message State Lifecycle

**Statement:** The system shall maintain an explicit state for every user message and generated assistant message.

**Supported States Shall Include, at Minimum:**

* accepted;
* sending;
* streaming;
* complete;
* failed;
* cancelled.

Additional internal states may be defined.

---

### FR-MSG-010 — Accepted State

**Statement:** A user message shall enter the accepted state after validation and durable creation succeed.

**Atomicity Rule:** The system shall not report a message as accepted unless the message record can be subsequently retrieved or reconciled.

---

### FR-MSG-011 — Sending State

**Statement:** A message execution shall enter the sending state when the Runtime Orchestrator begins provider-request preparation or transmission.

---

### FR-MSG-012 — Streaming State

**Statement:** The assistant message shall enter the streaming state when the system receives or emits the first valid response event associated with the provider generation.

---

### FR-MSG-013 — Complete State

**Statement:** The assistant message shall enter the complete state only after the provider response stream or non-streamed response has ended successfully and the final response content has been durably recorded.

---

### FR-MSG-014 — Failed State

**Statement:** A message execution shall enter the failed state when the system cannot complete the provider interaction and no valid fallback completes the request.

**Failure Record Shall Include:**

* stable error category;
* failure time;
* retry eligibility;
* provider or runtime stage where applicable;
* correlation identifier.

Sensitive internal details shall not be exposed to the user.

---

### FR-MSG-015 — Cancelled State

**Statement:** A message execution shall enter the cancelled state when an authorized cancellation request is accepted and no further normal generation output will be processed.

---

### FR-MSG-016 — Terminal State Immutability

**Statement:** Complete, failed, and cancelled message states shall be terminal for the associated execution.

**Rule:** A retry shall create a new runtime execution and shall not rewrite the terminal state of the prior execution.

---

## 8.4 Assistant Message Creation

### FR-MSG-017 — Assistant Message Placeholder

**Statement:** The system shall create or reserve an assistant-message record before streaming response content where required to preserve ordering and recovery.

---

### FR-MSG-018 — Streamed Content Persistence

**Statement:** The system shall persist streamed assistant content using a strategy that supports recovery from service interruption without producing invalid message ordering.

**Atomicity Rules:**

* Partial content shall be identifiable as incomplete.
* The system shall not mark partial content complete.
* Reconnection shall not duplicate already persisted chunks.
* Finalization shall reconcile the persisted content with the terminal stream state.

---

### FR-MSG-019 — Partial Response Visibility

**Statement:** The system may display partial assistant content during streaming.

**Failure Behaviour:**

* If generation fails after partial content is displayed, the system shall identify the message as failed or incomplete.
* The system shall not represent partial output as a successful complete response.
* The user may be allowed to retain, copy, or retry from partial content according to product policy.

---

## 8.5 Cancellation

### FR-MSG-020 — Active Generation Cancellation

**Statement:** The system shall allow an authorized user to request cancellation of an active generation associated with the current conversation.

**Validation Rules:**

* The execution shall be in a cancellable state.
* The actor shall have access to the conversation.
* The cancellation request shall identify the target execution.
* Cancellation shall not affect another workspace’s execution.

---

### FR-MSG-021 — Cancellation Propagation

**Statement:** The Runtime Orchestrator shall attempt to propagate cancellation to the active provider request where the provider supports cancellation.

**Failure Behaviour:**

* Provider cancellation failure shall not cause further output to be presented as normal after local cancellation is accepted.
* Late provider events shall be discarded or quarantined.
* The system shall record whether provider-side cancellation was confirmed, unsupported, or failed.

---

### FR-MSG-022 — Cancellation Idempotency

**Statement:** Repeated cancellation requests for the same execution shall be idempotent.

---

### FR-MSG-023 — Cancellation Billing Metadata

**Statement:** The system shall record any provider usage reported for a cancelled request and shall distinguish estimated cost from confirmed provider-reported cost.

---

## 8.6 Message Metadata

### FR-MSG-024 — Message Actor Metadata

**Statement:** Each message shall identify its role or actor classification.

**Supported Classifications Shall Include, at Minimum:**

* user;
* assistant;
* system-generated operational message where exposed;
* tool or provider event where supported.

---

### FR-MSG-025 — Message Time Metadata

**Statement:** Each message shall record server-controlled creation time and applicable state-transition times.

**Applicable Times May Include:**

* accepted time;
* provider-send time;
* first-stream-event time;
* completion time;
* failure time;
* cancellation time.

---

### FR-MSG-026 — Runtime Execution Binding

**Statement:** Every provider-generated assistant message shall be bound to the runtime execution that produced it.

---

### FR-MSG-027 — Provider Metadata Binding

**Statement:** Each completed or failed provider execution shall record the effective provider and model identifiers used.

**Historical Rule:** Later changes to provider display names or default models shall not alter the recorded execution identity.

---

### FR-MSG-028 — Context Metadata Binding

**Statement:** Each runtime execution shall preserve metadata identifying the context categories used to produce the provider request.

**Metadata May Include:**

* conversation-history range;
* memory identifiers;
* file references;
* project instructions;
* workspace instructions;
* token-budget allocation.

The user-facing interface may expose a controlled subset.

---

### FR-MSG-029 — Usage Metadata Binding

**Statement:** Each runtime execution shall record input-token, output-token, total-token, and estimated-cost information where measurable.

---

### FR-MSG-030 — Error Metadata Binding

**Statement:** Failed messages shall record a stable user-safe error code and an internal correlation identifier.

---

## 8.7 Retry and Regeneration

### FR-MSG-031 — Failed Message Retry

**Statement:** The system shall allow an authorized user to retry an eligible failed execution.

**Core Behaviour:**

* Retry shall create a new execution record.
* The original failed execution shall remain unchanged.
* Current provider, model, context, quota, and cost policies shall be revalidated.
* The user shall be informed when retry conditions differ materially from the original attempt.

---

### FR-MSG-032 — Response Regeneration

**Statement:** The system may allow an authorized user to regenerate an assistant response for an existing user message.

**Core Behaviour:**

* Each regeneration shall create a distinct assistant message or response version.
* Provider and model metadata shall be recorded independently.
* Usage and cost shall be recorded independently.
* Regeneration shall not overwrite earlier responses.

---

## 8.8 Message Deletion and Audit

### FR-MSG-033 — Message Deletion

**Statement:** Where individual message deletion is supported, the system shall process deletion without corrupting conversation ordering, memory provenance, or retained execution records.

**Validation Rules:**

* The actor shall have permission.
* The system shall identify derived memories and indexes.
* Deletion shall follow the applicable soft or permanent deletion policy.
* Shared data shall not be deleted without provenance evaluation.

---

### FR-MSG-034 — Message Audit Events

**Statement:** The system shall audit security-sensitive message actions, including cancellation, administrative deletion, permanent deletion, and policy-driven content restriction.

---

# 9. Runtime Execution Requirements

## 9.1 Runtime Initiation

### FR-RUNTIME-001 — Runtime Execution Creation

**Statement:** The system shall create a unique runtime execution record for each accepted request that may invoke an AI provider.

**Execution Record Shall Include:**

* execution identifier;
* workspace identifier;
* conversation identifier;
* user-message identifier;
* requesting user;
* creation time;
* execution state;
* effective policy context.

---

### FR-RUNTIME-002 — Runtime Eligibility Validation

**Statement:** The Runtime Orchestrator shall validate execution eligibility before sending a request to an AI provider.

**Validation Shall Include, at Minimum:**

* authenticated user;
* workspace access;
* active workspace state;
* active conversation state;
* provider connection availability;
* model availability;
* quota;
* spending controls;
* message bounds;
* policy restrictions.

---

### FR-RUNTIME-003 — Runtime Execution State

**Statement:** The system shall maintain an explicit state for each runtime execution.

**Supported States Shall Include, at Minimum:**

* created;
* validating;
* preparing;
* provider pending;
* streaming;
* completed;
* failed;
* cancelled.

---

## 9.2 Synchronous Orchestration Pipeline

### FR-RUNTIME-004 — Controlled Pipeline Order

**Statement:** The Runtime Orchestrator shall process each eligible request through a controlled pipeline.

**The Pipeline Shall Include, as Applicable:**

1. request validation;
2. policy resolution;
3. intent classification;
4. context retrieval;
5. token-budget allocation;
6. prompt construction;
7. provider and model resolution;
8. cost-ceiling validation;
9. provider execution;
10. streaming coordination;
11. usage capture;
12. execution finalization;
13. background-processing scheduling.

---

### FR-RUNTIME-005 — Pipeline Stage Traceability

**Statement:** The system shall record the status and failure category of each material runtime stage.

**Audit Rule:** The record shall not include plaintext provider credentials or unnecessary complete prompt content in operational logs.

---

### FR-RUNTIME-006 — Pipeline Failure Isolation

**Statement:** Failure in one runtime execution shall not modify or block unrelated executions outside the shared resource limits defined by platform policy.

---

## 9.3 Intent Classification

### FR-RUNTIME-007 — Intent Classification

**Statement:** The Runtime Orchestrator shall classify the user request into an approved intent or task category before provider-ready prompt construction where classification is required.

**Classification May Identify:**

* task type;
* complexity;
* expected output format;
* retrieval requirement;
* file requirement;
* memory relevance;
* model capability requirement;
* safety or policy category.

---

### FR-RUNTIME-008 — Classification Confidence

**Statement:** Where classification produces a confidence score or equivalent certainty state, the system shall apply a configured fallback when confidence is insufficient.

**Fallback May Include:**

* using a general intent;
* disabling optional enhancement;
* asking the user for clarification;
* selecting a general-capability model;
* continuing without classification-dependent optimization.

---

### FR-RUNTIME-009 — Classification Failure

**Statement:** Intent-classification failure shall not automatically fail the request when a safe general execution path is available.

---

### FR-RUNTIME-010 — Classification Preservation

**Statement:** The execution record shall preserve the effective classification used for routing and prompt construction.

---

## 9.4 Dynamic Execution Routing

### FR-RUNTIME-011 — Execution Route Resolution

**Statement:** The Runtime Orchestrator shall select an execution route based on the effective request, policy, provider availability, model capability, context requirement, cost control, and user configuration.

---

### FR-RUNTIME-012 — Direct Route

**Statement:** The system shall support a direct route for eligible requests that do not require memory retrieval, file processing, complex prompt enhancement, or special model capabilities.

---

### FR-RUNTIME-013 — Enhanced Route

**Statement:** The system shall support an enhanced route that may include intent classification, memory retrieval, context assembly, prompt enhancement, and model recommendation.

---

### FR-RUNTIME-014 — Retrieval Route

**Statement:** The system shall support a retrieval-assisted route when the request requires workspace memory, project knowledge, file content, or indexed information.

---

### FR-RUNTIME-015 — Route Policy Enforcement

**Statement:** Dynamic routing shall not bypass user-disabled features or mandatory platform restrictions.

**Examples:**

* Memory-disabled conversations shall not retrieve memory.
* File-disabled workspaces shall not inject file content.
* Cost ceilings shall not be bypassed by route selection.
* A user-selected provider lock shall not be ignored unless explicit fallback permission exists.

---

### FR-RUNTIME-016 — Route Transparency

**Statement:** The system should expose a user-readable summary of the effective route, provider, model, and context categories used for a completed execution.

---

## 9.5 Context and Token Budget

### FR-RUNTIME-017 — Context Token Budget

**Statement:** The Runtime Orchestrator shall calculate an effective context-token budget before constructing the provider request.

**Budget Inputs Shall Include:**

* selected model context limit;
* reserved output tokens;
* system instructions;
* provider formatting overhead;
* user message;
* conversation history;
* workspace or project instructions;
* memories;
* file context;
* safety margin.

---

### FR-RUNTIME-018 — Model Limit Enforcement

**Statement:** The system shall not knowingly submit a provider request that exceeds the selected model’s supported context bound.

---

### FR-RUNTIME-019 — Token Allocation Priority

**Statement:** When available context exceeds the effective budget, the system shall reduce context according to a deterministic priority policy.

**The Policy Shall Protect, at Minimum:**

1. mandatory system and safety instructions;
2. current user message;
3. required output instructions;
4. essential conversation context;
5. highest-relevance approved memories;
6. highest-relevance file or knowledge content;
7. lower-priority historical context.

---

### FR-RUNTIME-020 — Context Truncation Transparency

**Statement:** The system shall record whether context was truncated, omitted, summarized, or compressed to satisfy the token budget.

---

### FR-RUNTIME-021 — Context Deduplication

**Statement:** The Runtime Orchestrator shall remove or reduce materially duplicate context before provider submission where doing so does not alter required meaning.

---

### FR-RUNTIME-022 — Reserved Output Capacity

**Statement:** The system shall reserve sufficient output capacity according to model limits, user settings, and task requirements before finalizing the input context.

---

### FR-RUNTIME-023 — Token Estimation Failure

**Statement:** If exact token estimation is unavailable, the system shall use a documented conservative estimation method.

**Failure Rule:** The system shall fail or reduce context safely rather than knowingly exceed the provider limit.

---

## 9.6 Prompt Construction

### FR-RUNTIME-024 — Provider-Ready Prompt Construction

**Statement:** The Runtime Orchestrator shall construct a provider-ready request from the canonical user message and the approved effective context.

---

### FR-RUNTIME-025 — User Intent Preservation

**Statement:** Prompt enhancement shall preserve the user’s intended task and shall not silently introduce a materially different objective.

---

### FR-RUNTIME-026 — Instruction Precedence

**Statement:** Prompt construction shall apply a deterministic instruction-precedence model.

**Precedence Shall Respect:**

1. mandatory platform policy;
2. system safety instructions;
3. organization policy;
4. workspace instructions;
5. project instructions;
6. conversation instructions;
7. user message;
8. retrieved contextual content.

Retrieved content shall not be treated as higher-authority instruction unless explicitly classified as such.

---

### FR-RUNTIME-027 — Untrusted Context Delimitation

**Statement:** Retrieved memories, files, search results, and provider-returned content shall be identified as contextual data rather than trusted system instructions unless an approved policy states otherwise.

---

### FR-RUNTIME-028 — Prompt Snapshot

**Statement:** The system shall preserve an immutable or reproducible representation of the effective provider request for traceability, subject to security, privacy, and retention policy.

---

## 9.7 Cost Validation and Metrics

### FR-RUNTIME-029 — Pre-Execution Cost Estimate

**Statement:** The system shall calculate a pre-execution estimated provider cost where model pricing and token estimates are available.

**Estimate Inputs Shall Include:**

* estimated input tokens;
* reserved or expected output tokens;
* provider;
* model;
* applicable pricing version;
* currency or billing unit.

---

### FR-RUNTIME-030 — Spending-Ceiling Validation

**Statement:** The Runtime Orchestrator shall validate the estimated request cost against applicable user and workspace spending ceilings before provider execution.

---

### FR-RUNTIME-031 — Cost Estimate Unavailability

**Statement:** Where reliable cost estimation is unavailable, the system shall apply the configured unknown-cost policy.

**The Policy May:**

* allow with warning;
* require confirmation;
* block execution;
* apply a conservative maximum estimate.

---

### FR-RUNTIME-032 — Actual Usage Capture

**Statement:** The system shall capture provider-reported token usage after completion where the provider supplies usage data.

---

### FR-RUNTIME-033 — Usage Reconciliation

**Statement:** The system shall reconcile estimated usage with provider-reported usage and shall preserve both values when they differ.

---

### FR-RUNTIME-034 — Cost Calculation Versioning

**Statement:** Each cost record shall identify the pricing data or calculation version used.

---

### FR-RUNTIME-035 — Failed Execution Cost

**Statement:** The system shall record reported or estimated provider cost for failed and cancelled executions where provider usage may have occurred.

---

## 9.8 Provider Execution

### FR-RUNTIME-036 — Provider Request Dispatch

**Statement:** The Runtime Orchestrator shall dispatch the provider request only after all mandatory validations succeed.

---

### FR-RUNTIME-037 — Execution Correlation

**Statement:** Each provider request shall be associated with the corresponding runtime execution through an internal correlation identifier.

---

### FR-RUNTIME-038 — Provider Timeout

**Statement:** The system shall apply configurable connection, first-response, stream-idle, and total-execution timeouts.

**Failure Behaviour:**

* Timeout shall produce a stable timeout category.
* Eligible fallback may be attempted according to Section 11.
* Late provider output shall not be attached to an unrelated or terminal execution.

---

### FR-RUNTIME-039 — Runtime Cancellation

**Statement:** The Runtime Orchestrator shall stop local processing after cancellation is accepted and shall prevent additional provider output from being presented as active generation.

---

## 9.9 Runtime Finalization

### FR-RUNTIME-040 — Successful Finalization

**Statement:** A runtime execution shall be marked completed only after the final assistant content and required usage metadata have been durably recorded or placed in a recoverable reconciliation state.

---

### FR-RUNTIME-041 — Failure Finalization

**Statement:** A failed runtime execution shall record the terminal stage, error category, retry eligibility, and finalization time.

---

### FR-RUNTIME-042 — Background Work Scheduling

**Statement:** After synchronous response completion or eligible terminal failure, the Runtime Orchestrator shall schedule applicable background processing without blocking normal response delivery.

---

### FR-RUNTIME-043 — Snapshot Lock for Rapid-Fire Messages

**Statement:** If a new user message is accepted while background processing for the immediately preceding message remains active, the Runtime Orchestrator shall not block the new message waiting for that background processing to complete.

**Core Behaviour:**

* The system shall create a context snapshot using memories and workspace state committed at the instant the new execution begins.
* Uncommitted memory candidates from the preceding message shall not be included.
* The new message shall proceed using the snapshot.
* Memories committed after the snapshot shall become eligible for subsequent executions.
* Background completion shall not mutate the already constructed context of the active execution.

---

### FR-RUNTIME-044 — Runtime Idempotent Finalization

**Statement:** Retried completion or failure-finalization operations shall not duplicate assistant messages, usage records, cost records, or background jobs.

---

### FR-RUNTIME-045 — Runtime Audit Record

**Statement:** The system shall retain a traceable runtime record containing the effective provider, model, route, context categories, token metrics, cost metrics, state transitions, and error category.

---

# 10. Context and Memory Requirements

## 10.1 Memory Model

### FR-MEMORY-001 — Structured Memory Record

**Statement:** The system shall represent retained memory as a structured record rather than relying exclusively on raw conversation history.

**Memory Record Shall Include, at Minimum:**

* memory identifier;
* workspace identifier;
* memory category;
* normalized content;
* lifecycle state;
* source provenance;
* creation time;
* update time;
* retrieval eligibility;
* confidence or confirmation state where applicable.

---

### FR-MEMORY-002 — Memory Workspace Binding

**Statement:** Every memory shall be bound to exactly one workspace.

**Security Rule:** A memory shall not be retrieved across workspace boundaries.

---

### FR-MEMORY-003 — Memory Scope

**Statement:** The system shall support memory scope sufficient to distinguish workspace, project, conversation, user-preference, and temporary-context applicability where enabled.

---

### FR-MEMORY-004 — Memory Categories

**Statement:** The system shall classify memories using approved categories.

**Categories May Include:**

* user preference;
* project fact;
* decision;
* instruction;
* constraint;
* entity;
* goal;
* workflow state;
* long-term knowledge;
* temporary context.

Unknown categories shall not be silently stored as confirmed memory.

---

## 10.2 Memory Extraction

### FR-MEMORY-005 — Background Memory Extraction

**Statement:** The Background Processing Worker shall evaluate eligible completed conversations or messages for potential long-term memory after or outside the critical response path.

---

### FR-MEMORY-006 — Extraction Eligibility

**Statement:** The system shall determine memory-extraction eligibility before processing source content.

**Validation Shall Include:**

* workspace memory mode;
* conversation exclusion state;
* source deletion state;
* actor permission;
* content policy;
* supported message type.

---

### FR-MEMORY-007 — Memory Candidate Creation

**Statement:** Extracted information shall first be created as a memory candidate unless policy explicitly permits automatic confirmation.

**Candidate Data Shall Include:**

* proposed content;
* proposed category;
* source provenance;
* extraction time;
* confidence or evidence metadata;
* conflict indicators;
* suggested lifecycle action.

---

### FR-MEMORY-008 — Candidate Deduplication

**Statement:** The system shall compare a memory candidate against existing eligible memories before creating a new active memory.

**Possible Outcomes Shall Include:**

* create new memory;
* merge with existing memory;
* update existing memory;
* reject duplicate;
* flag conflict;
* retain as separate scoped memory.

---

### FR-MEMORY-009 — Candidate Conflict Detection

**Statement:** The system shall detect material conflicts between a candidate and existing active memory where feasible.

**Failure-Safe Behaviour:**

* A conflicting candidate shall not silently overwrite confirmed memory.
* The system shall preserve both source references.
* The candidate shall enter a review, conflict, or inactive state according to policy.
* The user may be asked to resolve the conflict.

---

### FR-MEMORY-010 — Automatic Memory Policy

**Statement:** Automatic memory activation shall occur only for categories, confidence levels, and workspace modes explicitly permitted by policy.

---

### FR-MEMORY-011 — Memory Extraction Failure

**Statement:** Memory-extraction failure shall not change the completed user-visible response state.

**Failure Behaviour:**

* The failed background job shall record a stable error category.
* Eligible jobs may be retried.
* Repeated retries shall not create duplicate candidates.
* Failure shall not make unprocessed content retrievable as memory.

---

## 10.3 Memory Confirmation and Activation

### FR-MEMORY-012 — User Confirmation

**Statement:** The system shall allow an authorized user to confirm an eligible memory candidate.

**Postconditions:**

* The memory shall enter an active or confirmed state.
* Confirmation actor and time shall be recorded.
* Search indexes and embeddings shall be created or activated as required.
* The operation shall be idempotent.

---

### FR-MEMORY-013 — Memory Rejection

**Statement:** The system shall allow an authorized user to reject a memory candidate.

**Postconditions:**

* The candidate shall not be eligible for normal retrieval.
* Rejection reason may be recorded.
* Rejected content shall be retained or deleted according to retention policy.
* Rejection shall not delete the source message.

---

### FR-MEMORY-014 — Memory Activation

**Statement:** The system shall allow an authorized user to activate an inactive memory.

**Validation Rules:**

* The memory shall belong to the selected workspace.
* The memory shall not be permanently deleted.
* The content shall satisfy current policy.
* Required embeddings or indexes shall be available or scheduled.

---

### FR-MEMORY-015 — Memory Deactivation

**Statement:** The system shall allow an authorized user to deactivate an active memory without deleting the memory record.

**Postconditions:**

* The memory shall immediately become ineligible for new retrieval.
* Associated vector and keyword indexes shall be disabled or filtered.
* Historical runtime records shall remain unchanged.
* The action shall be auditable.

---

## 10.4 Memory Retrieval

### FR-MEMORY-016 — Relevant Memory Retrieval

**Statement:** The system shall retrieve only active, permitted, and contextually relevant memories for a runtime execution.

---

### FR-MEMORY-017 — Workspace Scope Enforcement

**Statement:** Every memory-retrieval operation shall include and enforce the authorized workspace scope.

---

### FR-MEMORY-018 — Project Scope Enforcement

**Statement:** Project-scoped memories shall be retrieved only when the active execution is associated with the same project or an explicitly authorized related scope.

---

### FR-MEMORY-019 — Conversation Exclusion Enforcement

**Statement:** The system shall not retrieve memory into a conversation where applicable conversation or workspace settings prohibit memory use.

---

### FR-MEMORY-020 — Memory Relevance Ranking

**Statement:** Eligible memories shall be ranked using approved relevance signals.

**Signals May Include:**

* semantic similarity;
* keyword match;
* scope match;
* recency;
* confirmation level;
* memory priority;
* source reliability;
* conflict state.

---

### FR-MEMORY-021 — Retrieval Threshold

**Statement:** A memory shall not be included in runtime context when its retrieval score or policy eligibility falls below the configured threshold.

---

### FR-MEMORY-022 — Retrieval Limit

**Statement:** The system shall limit retrieved memories by count, token budget, or both.

---

### FR-MEMORY-023 — Retrieval Deduplication

**Statement:** The system shall suppress materially duplicate retrieved memories before context construction.

---

### FR-MEMORY-024 — Conflict-Aware Retrieval

**Statement:** Memories in unresolved conflict shall not be presented as unqualified confirmed facts.

**Core Behaviour:**

* Conflicting memories may be excluded.
* The system may include an explicit uncertainty marker.
* The system may request clarification.
* The selected behaviour shall follow workspace policy.

---

### FR-MEMORY-025 — Memory Retrieval Snapshot

**Statement:** The system shall preserve the identifiers and effective versions of memories selected for each runtime execution.

---

### FR-MEMORY-026 — Memory Retrieval Failure

**Statement:** If memory retrieval fails, the Runtime Orchestrator shall apply the configured failure policy.

**The Policy May:**

* continue without memory;
* retry within a bounded time;
* notify the user;
* fail the request when memory is mandatory.

The system shall not substitute memories from another workspace.

---

## 10.5 User Memory Inspection

### FR-MEMORY-027 — Memory Listing

**Statement:** The system shall allow an authorized user to list memories within the selected workspace.

**List Controls Shall Support:**

* lifecycle state;
* category;
* project scope;
* source type;
* creation or update time;
* search;
* pagination.

---

### FR-MEMORY-028 — Memory Detail Inspection

**Statement:** The system shall allow an authorized user to inspect an individual memory.

**Displayed Information Should Include:**

* content;
* category;
* state;
* scope;
* source provenance;
* creation time;
* update time;
* confirmation state;
* retrieval eligibility;
* conflict status.

Sensitive source content may be restricted according to permission.

---

### FR-MEMORY-029 — Memory Provenance

**Statement:** The system shall preserve the provenance of each extracted memory.

**Provenance May Include:**

* source conversation;
* source message;
* source file;
* explicit user entry;
* extraction job;
* actor;
* extraction time.

---

### FR-MEMORY-030 — Memory Usage Inspection

**Statement:** The system should allow an authorized user to determine whether a memory was used in a specific runtime execution.

---

## 10.6 Memory Update

### FR-MEMORY-031 — Memory Content Update

**Statement:** The system shall allow an authorized user to update the content of an eligible memory.

**Validation Rules:**

* The replacement content shall satisfy supported bounds.
* The memory shall belong to the selected workspace.
* The user shall have update permission.
* The update shall create a new memory version or preserve equivalent change history.
* Search indexes and embeddings shall be regenerated.

---

### FR-MEMORY-032 — Memory Category Update

**Statement:** The system shall allow an authorized user to change the category or scope of an eligible memory.

**Failure Behaviour:**

* Invalid category-scope combinations shall be rejected.
* Failure shall preserve the prior memory state.
* The system shall update retrieval indexes only after the change is committed.

---

### FR-MEMORY-033 — Memory Versioning

**Statement:** Material memory updates shall preserve prior version metadata sufficient for audit and conflict analysis.

---

### FR-MEMORY-034 — Memory Update Atomicity

**Statement:** Memory content, version metadata, and retrieval-index transition shall complete as one recoverable operation.

**Atomicity Rules:**

* The old version shall remain active until the replacement is valid.
* The system shall not expose a new memory version with missing mandatory indexes when those indexes are required for retrieval.
* Failed index generation shall result in a controlled pending-index state or rollback.

---

## 10.7 Memory Deletion

### FR-MEMORY-035 — Memory Soft Delete

**Statement:** The system shall allow an authorized user to soft-delete a memory.

**Postconditions:**

* The memory shall become ineligible for retrieval.
* Vector and keyword search shall exclude it.
* Recovery shall remain possible during the configured period.
* Deletion actor and time shall be recorded.

---

### FR-MEMORY-036 — Memory Restore

**Statement:** The system shall allow an authorized user to restore a soft-deleted memory before permanent deletion begins.

---

### FR-MEMORY-037 — Permanent Memory Deletion

**Statement:** The system shall allow an authorized user to permanently delete an eligible memory after explicit confirmation.

**Deletion Shall Include:**

* canonical memory content;
* memory versions subject to retention policy;
* vector embeddings;
* keyword indexes;
* caches;
* pending candidates derived solely from the memory.

---

### FR-MEMORY-038 — Memory Vector Deletion

**Statement:** Permanent deletion or deactivation of a memory shall remove or disable all vector representations used for retrieval.

**Validation Rule:** A deleted vector shall not remain retrievable through stale index references.

---

### FR-MEMORY-039 — Memory Keyword Index Deletion

**Statement:** Permanent deletion or deactivation of a memory shall remove or disable associated keyword-search entries.

---

### FR-MEMORY-040 — Memory Deletion Idempotency

**Statement:** Repeated deletion processing for the same memory and deletion request shall be idempotent.

---

### FR-MEMORY-041 — Source Deletion Reconciliation

**Statement:** When a source conversation, message, or file is permanently deleted, the system shall evaluate memories derived from that source.

**Possible Outcomes Shall Include:**

* delete memory;
* remove deleted-source provenance;
* retain memory when independently confirmed;
* require user review;
* retain minimal non-content audit metadata.

The selected outcome shall follow provenance and deletion policy.

---

## 10.8 Temporary Context

### FR-MEMORY-042 — Temporary Context Creation

**Statement:** The system may create temporary context records that are eligible for limited use without becoming long-term active memory.

---

### FR-MEMORY-043 — Temporary Context Expiration

**Statement:** Temporary context shall have an explicit expiration condition.

**Expiration May Be Based On:**

* time;
* conversation closure;
* project state;
* execution count;
* explicit user action.

---

### FR-MEMORY-044 — Temporary Context Cleanup

**Statement:** Expired temporary context shall be removed from retrieval and processed for deletion according to retention policy.

---

## 10.9 Memory Audit

### FR-MEMORY-045 — Memory Audit Events

**Statement:** The system shall audit memory confirmation, rejection, activation, deactivation, content update, scope update, conflict resolution, soft deletion, restoration, and permanent deletion.

---

# 11. AI Provider Connection and Routing Requirements

## 11.1 Provider Connection

### FR-PROVIDER-001 — Supported Provider Registry

**Statement:** The system shall maintain a registry of supported AI providers and their applicable capabilities.

**Provider Metadata May Include:**

* provider identifier;
* display name;
* authentication method;
* available regions;
* model catalogue;
* streaming capability;
* tool capability;
* context limits;
* usage-reporting capability;
* current operational state.

---

### FR-PROVIDER-002 — BYOK Connection Creation

**Statement:** The system shall allow an authorized Workspace Owner to create a Bring Your Own Key provider connection for a supported provider.

**Validation Rules:**

* The provider shall be enabled.
* The credential shall satisfy format bounds.
* The workspace shall permit BYOK.
* The credential shall be protected according to Section 5.
* Duplicate connection policy shall be enforced.

---

### FR-PROVIDER-003 — Provider Connection Identifier

**Statement:** Each provider connection shall receive a stable identifier independent of the secret value.

---

### FR-PROVIDER-004 — Provider Connection State

**Statement:** The system shall maintain an explicit state for each provider connection.

**Supported States Shall Include, at Minimum:**

* pending validation;
* active;
* degraded;
* invalid credential;
* rate limited;
* disabled;
* disconnected.

---

### FR-PROVIDER-005 — Provider Credential Validation

**Statement:** The system shall validate a newly submitted provider credential through an approved provider-specific validation mechanism where available.

**Failure Behaviour:**

* Invalid credentials shall not become active.
* The complete provider error shall not be exposed when it contains sensitive information.
* Validation failure shall not reveal the credential.
* Repeated validation shall be rate limited.

---

### FR-PROVIDER-006 — Connection Health Check

**Statement:** The system shall perform health checks for active provider connections according to configurable policy.

**Health Checks May Validate:**

* credential acceptance;
* provider reachability;
* account status;
* model-list access;
* quota status;
* regional availability.

---

### FR-PROVIDER-007 — Health Check Isolation

**Statement:** Provider health checks shall use the target workspace’s connection and shall not reuse another workspace’s credential.

---

### FR-PROVIDER-008 — Health Check Result

**Statement:** The system shall record the latest provider-connection health state and check time.

**User-Facing Information May Include:**

* connected;
* action required;
* temporarily unavailable;
* credential invalid;
* rate limited.

The system shall not display the credential.

---

### FR-PROVIDER-009 — Manual Health Check

**Statement:** The system shall allow an authorized actor to request a provider-connection health check subject to rate limits.

---

### FR-PROVIDER-010 — Connection Disable

**Statement:** The system shall allow an authorized actor to disable a provider connection without deleting its historical usage records.

**Postconditions:**

* New provider executions shall not use the connection.
* Active executions may complete or be cancelled according to policy.
* The disabled connection shall remain inspectable.
* The action shall be audited.

---

### FR-PROVIDER-011 — Provider Disconnection

**Statement:** The system shall allow an authorized actor to disconnect a provider and delete its stored credential.

---

## 11.2 Model Catalogue and Selection

### FR-PROVIDER-012 — Model Catalogue

**Statement:** The system shall maintain a catalogue of models available through each supported provider.

**Model Metadata Shall Include, Where Available:**

* stable internal model identifier;
* provider model identifier;
* display name;
* capability classification;
* context limit;
* output limit;
* streaming support;
* pricing;
* availability state.

---

### FR-PROVIDER-013 — Model Catalogue Refresh

**Statement:** The system shall support refresh of provider model metadata without rewriting historical execution records.

---

### FR-PROVIDER-014 — Workspace Default Provider

**Statement:** The system shall allow an authorized Workspace Owner to select an active provider connection as the workspace default.

---

### FR-PROVIDER-015 — Workspace Default Model

**Statement:** The system shall allow an authorized Workspace Owner to select an eligible model as the workspace default.

**Validation Rules:**

* The model shall belong to an active permitted provider connection.
* The model shall be enabled for the workspace.
* The model shall satisfy organization and spending policy.
* Invalid selection shall preserve the previous default.

---

### FR-PROVIDER-016 — Project Default Model

**Statement:** The system may allow an authorized user to configure a project-level default model that overrides the workspace default when permitted.

---

### FR-PROVIDER-017 — Conversation Model Override

**Statement:** The system shall allow an authorized user to select an eligible provider or model for a conversation or individual execution when permitted by policy.

---

### FR-PROVIDER-018 — Effective Model Resolution

**Statement:** The system shall resolve the effective model using the approved configuration-precedence order.

---

### FR-PROVIDER-019 — Model Capability Validation

**Statement:** Before provider execution, the system shall verify that the selected model supports the required request capabilities.

**Capabilities May Include:**

* context size;
* streaming;
* file or image support;
* structured output;
* tool calling;
* required language or modality;
* expected output bound.

---

### FR-PROVIDER-020 — Model Unavailability

**Statement:** If the selected model is unavailable, the system shall apply the configured unavailability policy.

**The Policy May:**

* use an approved fallback;
* request user selection;
* queue or retry;
* fail with a controlled error.

---

## 11.3 Dynamic Routing

### FR-PROVIDER-021 — Provider Routing Decision

**Statement:** The Runtime Orchestrator shall select a provider connection and model based on explicit user selection or approved dynamic-routing policy.

**Routing Inputs May Include:**

* user choice;
* workspace default;
* project default;
* task capability;
* context size;
* availability;
* latency;
* spending ceiling;
* estimated cost;
* provider health;
* fallback permission.

---

### FR-PROVIDER-022 — User-Selected Provider Priority

**Statement:** An explicit user-selected provider or model shall take precedence over dynamic recommendation unless the selection is invalid, unavailable, prohibited, or exceeds mandatory limits.

---

### FR-PROVIDER-023 — Cost-Aware Routing

**Statement:** Dynamic routing may select a lower-cost eligible model when it satisfies the required capability and quality policy.

**Restriction:** Cost optimization shall not silently select a model known to be incapable of completing the task.

---

### FR-PROVIDER-024 — Capability-Aware Routing

**Statement:** The system shall not route a request to a model that lacks a mandatory task capability.

---

### FR-PROVIDER-025 — Routing Transparency

**Statement:** The execution record shall preserve the routing reason category and selected provider and model.

---

## 11.4 Fallback Routing

### FR-PROVIDER-026 — Fallback Policy

**Statement:** The system shall support configurable fallback routing when the primary provider or model cannot complete an eligible request.

**Fallback Triggers May Include:**

* provider timeout;
* provider unavailability;
* rate limit;
* model unavailability;
* transient provider error;
* context-limit incompatibility.

---

### FR-PROVIDER-027 — Fallback Permission

**Statement:** Fallback shall occur only when permitted by workspace policy and applicable user selection.

**Restriction:** The system shall not switch to another provider using another provider credential without explicit fallback authorization.

---

### FR-PROVIDER-028 — Fallback Model Eligibility

**Statement:** A fallback model shall satisfy the mandatory request capabilities, context requirement, security policy, and spending ceiling.

---

### FR-PROVIDER-029 — Fallback Cost Validation

**Statement:** The system shall re-evaluate estimated cost before dispatching a fallback request.

---

### FR-PROVIDER-030 — Fallback Context Revalidation

**Statement:** The system shall revalidate and, where necessary, reconstruct the provider request for the fallback model’s context and formatting requirements.

---

### FR-PROVIDER-031 — Fallback Attempt Limit

**Statement:** The system shall enforce a configurable maximum number of fallback attempts per runtime execution.

---

### FR-PROVIDER-032 — Duplicate Provider Execution Prevention

**Statement:** The system shall not initiate a fallback while the primary provider may still produce a valid response unless the primary request has been cancelled, timed out, or placed in a state that prevents duplicate response acceptance.

---

### FR-PROVIDER-033 — Fallback Result Attribution

**Statement:** The final assistant message shall identify the provider and model that actually produced the accepted response.

---

### FR-PROVIDER-034 — Fallback Failure

**Statement:** If all eligible fallback attempts fail, the execution shall enter a failed state with a stable aggregated failure category.

---

## 11.5 Provider Errors and Usage

### FR-PROVIDER-035 — Provider Error Normalization

**Statement:** The system shall map provider-specific failures into stable internal error categories.

**Categories Shall Include, at Minimum:**

* invalid credential;
* rate limit;
* quota exhausted;
* model unavailable;
* request invalid;
* context exceeded;
* provider timeout;
* provider unavailable;
* policy rejection;
* unknown provider error.

---

### FR-PROVIDER-036 — Provider Error Privacy

**Statement:** Provider errors exposed to users shall not include stored credentials, request signatures, internal endpoints, or another account’s information.

---

### FR-PROVIDER-037 — Provider Usage Capture

**Statement:** The system shall capture provider-reported usage and request identifiers where available.

---

### FR-PROVIDER-038 — Provider Pricing Association

**Statement:** The system shall associate provider usage with the effective model-pricing version used for cost calculation.

---

### FR-PROVIDER-039 — Provider Audit Events

**Statement:** The system shall audit provider-connection creation, credential validation, default selection, disabling, disconnection, routing fallback, and administrative provider-state changes.

---

# 12. Streaming, File Processing, and Search Requirements

## 12.1 Server-Sent Events Streaming

### FR-STREAM-001 — SSE Response Channel

**Statement:** The system shall support Server-Sent Events for streaming eligible runtime response events to supported clients.

---

### FR-STREAM-002 — SSE Authentication

**Statement:** The system shall authenticate and authorize an SSE connection before transmitting workspace-scoped response data.

**Security Rules:**

* The connection shall be bound to the authenticated user.
* The execution shall belong to an authorized workspace and conversation.
* An execution identifier alone shall not grant stream access.
* Revoked access shall prevent new stream connections.

---

### FR-STREAM-003 — SSE Content Type

**Statement:** The system shall return the applicable SSE media type and shall format each event according to the supported event contract.

---

### FR-STREAM-004 — Stream Event Types

**Statement:** The SSE stream shall support stable event types sufficient to represent runtime progress.

**Event Types Shall Include, at Minimum:**

* stream opened;
* generation started;
* content delta;
* usage update where available;
* generation completed;
* generation failed;
* generation cancelled;
* heartbeat.

---

### FR-STREAM-005 — Stream Correlation

**Statement:** Each SSE event shall identify the applicable runtime execution and message context without exposing secret identifiers.

---

### FR-STREAM-006 — Stream Event Ordering

**Statement:** Events within one execution stream shall be emitted in deterministic sequence order.

**Validation Rules:**

* Content deltas shall not be applied before generation-start acknowledgement.
* Terminal events shall occur after all accepted content deltas.
* Events received after a terminal event shall be discarded or recorded as late events.
* Sequence gaps shall be detectable.

---

### FR-STREAM-007 — Stream Heartbeat

**Statement:** The system shall emit heartbeat events or equivalent keep-alive data at a configured interval during eligible periods of stream inactivity.

---

### FR-STREAM-008 — First-Event Timeout

**Statement:** The system shall apply a configurable maximum time between provider dispatch and the first valid response event.

---

### FR-STREAM-009 — Stream Idle Timeout

**Statement:** The system shall terminate or fail a stream that remains inactive beyond the configured idle limit, subject to provider-specific policy.

---

### FR-STREAM-010 — Client Disconnect

**Statement:** The system shall detect client disconnection where supported.

**Core Behaviour:**

* Client disconnection shall not automatically imply provider cancellation unless policy requires it.
* The system may continue generation for later retrieval.
* The system may cancel generation to control cost.
* The selected behaviour shall be recorded.

---

### FR-STREAM-011 — Stream Reconnection

**Statement:** The system should allow an authorized client to reconnect to an active or recently completed stream.

**Reconnection Rules:**

* The client may provide the last processed event identifier.
* The system shall avoid resending acknowledged events where replay support exists.
* Reconnection shall not create a second provider execution.
* If replay is unavailable, the client shall receive the persisted current message state.

---

### FR-STREAM-012 — Stream Completion

**Statement:** The system shall emit a terminal completion event only after the assistant response has been finalized according to FR-RUNTIME-040.

---

### FR-STREAM-013 — Stream Failure

**Statement:** Stream failure shall emit or persist a stable user-safe error state.

**Failure Behaviour:**

* Partial content shall remain marked incomplete.
* The failure shall not be represented as successful completion.
* The client shall be able to retrieve the terminal execution state.
* Sensitive provider details shall not be emitted.

---

### FR-STREAM-014 — Stream Cancellation

**Statement:** Accepted user cancellation shall result in a terminal cancellation event for connected clients.

---

### FR-STREAM-015 — SSE Cross-Tenant Isolation

**Statement:** The system shall not emit an event from one workspace, conversation, message, or execution to a subscriber authorized only for another scope.

---

## 12.2 File Upload and Storage

### FR-STREAM-016 — File Upload

**Statement:** The system shall allow an authorized user to upload supported files to an active workspace or project.

**Validation Rules:**

* The user shall have file-upload permission.
* The workspace shall permit file processing.
* File size shall not exceed the configured bound.
* File type shall be supported.
* Storage quota shall be available.
* Malicious or prohibited content checks shall be applied where configured.

---

### FR-STREAM-017 — Supported MVP File Types

**Statement:** The MVP shall support text extraction from approved PDF and plain-text file formats.

**Supported Types Shall Include, at Minimum:**

* PDF;
* TXT.

Additional formats may be enabled through separate requirements.

---

### FR-STREAM-018 — File Type Verification

**Statement:** The system shall verify file type using content inspection or equivalent trusted detection and shall not rely solely on the client-provided file extension or media type.

---

### FR-STREAM-019 — File Size Bound

**Statement:** The system shall reject files exceeding the configured maximum size before initiating unbounded parsing.

---

### FR-STREAM-020 — File Stable Identifier

**Statement:** Each accepted file shall receive a stable identifier and shall be bound to exactly one workspace.

---

### FR-STREAM-021 — File Integrity Metadata

**Statement:** The system shall record integrity metadata sufficient to detect accidental duplication or corruption.

**Metadata May Include:**

* checksum;
* original filename;
* detected media type;
* byte size;
* upload time;
* uploader;
* workspace;
* project scope.

---

### FR-STREAM-022 — Duplicate File Handling

**Statement:** The system shall apply a documented duplicate-file policy.

**Possible Outcomes May Include:**

* reuse existing content;
* create a new file record referencing shared storage;
* reject duplicate;
* retain separate versions.

The policy shall not merge files across workspaces.

---

### FR-STREAM-023 — File Upload State

**Statement:** The system shall maintain an explicit file-processing state.

**States Shall Include, at Minimum:**

* uploaded;
* validating;
* parsing;
* indexed;
* failed;
* deleted.

---

## 12.3 PDF and TXT Parsing

### FR-STREAM-024 — TXT Parsing

**Statement:** The system shall extract supported textual content from a valid plain-text file using a supported character encoding.

**Failure Behaviour:**

* Unsupported or undecodable content shall produce a controlled parsing error.
* The original file shall remain identifiable.
* Partial extraction shall be marked as partial.

---

### FR-STREAM-025 — PDF Parsing

**Statement:** The system shall extract machine-readable text from supported PDF files within configured page, size, and processing-time bounds.

---

### FR-STREAM-026 — Scanned PDF Handling

**Statement:** Where OCR is not enabled, the system shall identify PDFs with insufficient extractable text and shall not falsely represent them as fully parsed.

---

### FR-STREAM-027 — Parsing Bounds

**Statement:** File parsing shall enforce configurable resource bounds.

**Bounds Shall Include, as Applicable:**

* maximum bytes;
* maximum pages;
* maximum extracted characters;
* maximum processing time;
* maximum nested objects;
* maximum decompressed size.

---

### FR-STREAM-028 — Parser Isolation

**Statement:** File parsing shall execute in a controlled environment that prevents file content from obtaining unauthorized system or workspace access.

---

### FR-STREAM-029 — File Content Segmentation

**Statement:** Parsed file content shall be segmented into retrieval units suitable for keyword and vector indexing.

**Each Segment Shall Preserve:**

* file identifier;
* workspace identifier;
* segment order;
* source location such as page or character range;
* extracted text;
* processing version.

---

### FR-STREAM-030 — File Parsing Idempotency

**Statement:** Repeated parsing of the same file version using the same parser version shall not create duplicate active segments or duplicate index entries.

---

### FR-STREAM-031 — File Processing Failure

**Statement:** A file-processing failure shall place the file in a failed state with a stable error category.

**Failure Shall Not:**

* expose parser stack traces to the user;
* create retrievable incomplete segments as if complete;
* modify another file;
* block unrelated workspace operations.

---

## 12.4 File Context Injection

### FR-STREAM-032 — File Selection for Runtime

**Statement:** The system shall allow an authorized user or approved retrieval process to select eligible files for runtime context.

---

### FR-STREAM-033 — File Workspace Validation

**Statement:** A selected file shall be injected only when it belongs to the active workspace and the actor has access.

---

### FR-STREAM-034 — File Parsing Requirement

**Statement:** A file shall not be injected as parsed context unless its required processing state is complete or explicitly marked as partial and permitted.

---

### FR-STREAM-035 — File Context Relevance

**Statement:** When a selected file exceeds the available context budget, the system shall select the most relevant eligible segments rather than injecting the entire file by default.

---

### FR-STREAM-036 — File Context Token Bound

**Statement:** File-derived context shall remain within the allocation assigned by the Runtime Orchestrator.

---

### FR-STREAM-037 — File Source Attribution

**Statement:** The runtime record shall preserve the file and segment identifiers used in the provider request.

---

### FR-STREAM-038 — File Instruction Isolation

**Statement:** Parsed file content shall be treated as untrusted contextual data and shall not override higher-priority system, workspace, project, conversation, or user instructions.

---

## 12.5 Vector Search

### FR-STREAM-039 — Vector Index Creation

**Statement:** The system shall create vector embeddings for eligible memory and file segments when vector search is enabled.

---

### FR-STREAM-040 — Embedding Model Version

**Statement:** Each vector record shall identify the embedding model and processing version used.

---

### FR-STREAM-041 — Vector Workspace Scope

**Statement:** Every vector-search query shall enforce the authorized workspace scope.

---

### FR-STREAM-042 — Vector Search Query

**Statement:** The system shall allow an authorized runtime or user search to retrieve semantically relevant eligible records.

**Query Inputs May Include:**

* normalized query text;
* workspace;
* project;
* content type;
* lifecycle state;
* result limit;
* minimum relevance threshold.

---

### FR-STREAM-043 — Vector Result Validation

**Statement:** The system shall validate every returned vector result against workspace, lifecycle, permission, and source-availability rules before use.

---

### FR-STREAM-044 — Deleted Vector Exclusion

**Statement:** Deleted, inactive, expired, or unauthorized vector records shall not be returned as eligible search results.

---

### FR-STREAM-045 — Vector Search Failure

**Statement:** Vector-search failure shall not cause the system to return unscoped or stale results.

**Fallback May Include:**

* keyword search;
* no retrieval;
* bounded retry;
* controlled error.

---

## 12.6 Keyword Search

### FR-STREAM-046 — Keyword Index Creation

**Statement:** The system shall index eligible textual content for keyword or full-text search where keyword search is enabled.

---

### FR-STREAM-047 — Keyword Search Query

**Statement:** The system shall allow an authorized actor to search eligible workspace content using supported keyword criteria.

---

### FR-STREAM-048 — Keyword Scope Filtering

**Statement:** Keyword search shall enforce workspace, project, content-type, lifecycle-state, and permission filters before returning results.

---

### FR-STREAM-049 — Search Result Metadata

**Statement:** Search results shall include sufficient source metadata to identify the matching resource without exposing inaccessible content.

---

### FR-STREAM-050 — Search Pagination

**Statement:** User-facing search results shall support deterministic pagination or bounded top-result retrieval.

---

## 12.7 Hybrid Search

### FR-STREAM-051 — Hybrid Search

**Statement:** The system may combine vector relevance, keyword relevance, recency, scope, and content priority into a hybrid result ranking.

---

### FR-STREAM-052 — Hybrid Search Determinism

**Statement:** The effective search-ranking configuration or version shall be identifiable for traceability.

---

### FR-STREAM-053 — Search Deduplication

**Statement:** The system shall remove materially duplicate search results before runtime context injection.

---

### FR-STREAM-054 — Search Result Limit

**Statement:** The system shall enforce configurable result-count and token limits for all runtime search operations.

---

### FR-STREAM-055 — Search Audit Metadata

**Statement:** The runtime record shall preserve the identifiers of search results selected for context injection.

---

## 12.8 File Deletion

### FR-STREAM-056 — File Soft Delete

**Statement:** The system shall allow an authorized user to soft-delete a file.

**Postconditions:**

* The file shall be excluded from normal access, search, and context injection.
* Segments and indexes shall become inactive.
* Recovery shall remain possible during the configured period.

---

### FR-STREAM-057 — File Permanent Delete

**Statement:** Permanent file deletion shall remove the file content, parsed segments, vector embeddings, keyword indexes, derived caches, and temporary download artifacts.

---

### FR-STREAM-058 — File Deletion Idempotency

**Statement:** Repeated file-deletion processing shall be idempotent.

---

### FR-STREAM-059 — File Audit Events

**Statement:** The system shall audit file upload, parsing failure, indexing, soft deletion, restoration, and permanent deletion where applicable.

---

# 13. Usage, Billing, Notification, and Administration Requirements

## 13.1 Token Counting

### FR-ADMIN-001 — Input Token Count

**Statement:** The system shall record the input-token count for each provider execution where the provider reports or the system can reliably calculate it.

---

### FR-ADMIN-002 — Output Token Count

**Statement:** The system shall record the output-token count for each provider execution where available.

---

### FR-ADMIN-003 — Total Token Count

**Statement:** The system shall calculate and record the total token count as the sum of applicable input and output token usage.

---

### FR-ADMIN-004 — Token Estimate

**Statement:** Where provider-reported token usage is unavailable, the system shall record a clearly identified estimate using the applicable tokenizer or conservative estimation method.

---

### FR-ADMIN-005 — Token Source Classification

**Statement:** Token records shall identify whether values are provider reported, locally calculated, estimated, or reconciled.

---

### FR-ADMIN-006 — Token Attribution

**Statement:** Token usage shall be attributed to the applicable user, workspace, project, conversation, runtime execution, provider, and model where available.

---

### FR-ADMIN-007 — Token Reconciliation

**Statement:** The system shall preserve initial estimates and later provider-reported usage when reconciliation changes the recorded values.

---

## 13.2 Provider Cost Tracking

### FR-ADMIN-008 — Estimated Provider Cost

**Statement:** The system shall calculate estimated provider cost for each eligible execution.

**Calculation Inputs Shall Include:**

* provider;
* model;
* input-token rate;
* output-token rate;
* applicable usage units;
* pricing version;
* currency.

---

### FR-ADMIN-009 — Pricing Version

**Statement:** Each cost calculation shall identify the pricing version or effective pricing timestamp used.

---

### FR-ADMIN-010 — Cost Precision

**Statement:** Cost calculations shall use sufficient numeric precision to avoid material rounding error across aggregated usage.

---

### FR-ADMIN-011 — Display Rounding

**Statement:** User-facing cost displays may round values for readability, but stored accounting values shall preserve the approved precision.

---

### FR-ADMIN-012 — Failed and Cancelled Cost

**Statement:** The system shall record provider cost for failed or cancelled executions when usage was incurred or reported.

---

### FR-ADMIN-013 — Cost Attribution

**Statement:** Cost records shall be attributed to the responsible workspace and user context.

---

### FR-ADMIN-014 — Cost Aggregation

**Statement:** The system shall aggregate usage and estimated cost over supported periods.

**Periods Shall Include, at Minimum:**

* current day;
* current billing or calendar month;
* configurable date range.

---

### FR-ADMIN-015 — Usage Inspection

**Statement:** An authorized user shall be able to inspect workspace usage by provider, model, conversation, project, and time period where the data is available.

---

## 13.3 Spending Ceilings

### FR-ADMIN-016 — Workspace Soft Spending Ceiling

**Statement:** The system shall allow an authorized Workspace Owner to configure a soft spending ceiling for the workspace.

**Core Behaviour:**

* Reaching the soft ceiling shall not automatically block execution unless policy converts it to a hard control.
* The system shall generate an applicable warning.
* Warning state and time shall be recorded.
* Repeated warnings shall follow notification policy.

---

### FR-ADMIN-017 — Workspace Hard Spending Ceiling

**Statement:** The system shall allow an authorized Workspace Owner to configure a hard spending ceiling.

**Enforcement Rules:**

* The Runtime Orchestrator shall block a request whose estimated cost would exceed the remaining permitted amount.
* The system shall not bypass the ceiling through fallback routing.
* Unknown-cost requests shall follow the configured unknown-cost policy.
* Administrative override shall require explicit permission and audit.

---

### FR-ADMIN-018 — User Soft Spending Ceiling

**Statement:** The system shall support a soft spending ceiling attributable to an individual user where multi-user workspaces are enabled.

---

### FR-ADMIN-019 — User Hard Spending Ceiling

**Statement:** The system shall support a hard spending ceiling attributable to an individual user where enabled.

---

### FR-ADMIN-020 — Ceiling Precedence

**Statement:** When multiple spending ceilings apply, the most restrictive effective limit shall control unless an approved policy defines otherwise.

---

### FR-ADMIN-021 — Ceiling Time Window

**Statement:** Each spending ceiling shall define its measurement period.

**Supported Periods May Include:**

* daily;
* weekly;
* monthly;
* fixed date range;
* lifetime workspace budget.

---

### FR-ADMIN-022 — Ceiling Reset

**Statement:** Periodic ceilings shall reset according to server-controlled time and the configured timezone or billing period.

---

### FR-ADMIN-023 — Ceiling Concurrency Control

**Statement:** Spending-ceiling enforcement shall account for concurrent in-flight executions.

**Atomicity Rules:**

* The system shall reserve estimated budget before provider dispatch where necessary.
* Concurrent requests shall not collectively exceed the ceiling solely because each observed the same unreserved balance.
* Unused reservation shall be released after completion, failure, or cancellation.
* Reconciliation shall adjust estimated reservation to actual usage.

---

### FR-ADMIN-024 — Ceiling Validation Failure

**Statement:** If spending-ceiling state cannot be reliably determined, the system shall fail closed for hard-ceiling enforcement or apply an explicitly approved degraded-mode policy.

---

### FR-ADMIN-025 — Spending Warning Notification

**Statement:** The system shall notify eligible users when usage reaches configured warning thresholds.

---

## 13.4 Quotas and Rate Controls

### FR-ADMIN-026 — Usage Quota

**Statement:** The system shall support configurable usage quotas based on request count, token count, cost, file volume, storage, or other approved units.

---

### FR-ADMIN-027 — Quota Enforcement

**Statement:** The system shall validate applicable quota before accepting or executing a controlled operation.

---

### FR-ADMIN-028 — Rate Limit

**Statement:** The system shall apply configurable rate limits to protected or resource-intensive operations.

**Operations May Include:**

* login;
* provider validation;
* runtime execution;
* file upload;
* search;
* export;
* deletion request.

---

### FR-ADMIN-029 — Rate-Limit Error

**Statement:** A rate-limited request shall return a stable error and, where safe, an indication of when retry may be attempted.

---

## 13.5 Administrative Access

### FR-ADMIN-030 — Administrator Authentication

**Statement:** System Administrator access shall require an authenticated administrator identity and the applicable elevated authentication controls.

---

### FR-ADMIN-031 — Administrator Authorization

**Statement:** Every administrative action shall require an explicit administrative permission.

**Restriction:** Administrator status shall not imply unrestricted access to all user content.

---

### FR-ADMIN-032 — Least-Privilege Administration

**Statement:** Administrative roles shall be separable by operational responsibility.

**Responsibilities May Include:**

* provider configuration;
* user-support operations;
* security response;
* billing operations;
* audit review;
* platform configuration.

---

### FR-ADMIN-033 — User Account Administration

**Statement:** An authorized System Administrator may inspect limited account status and perform approved account actions.

**Actions May Include:**

* restrict account;
* restore account;
* revoke sessions;
* initiate support verification;
* inspect non-secret operational metadata.

---

### FR-ADMIN-034 — Workspace Administration

**Statement:** An authorized System Administrator may perform approved workspace operational actions without receiving routine plaintext access to provider credentials or private content.

---

### FR-ADMIN-035 — Provider Administration

**Statement:** An authorized System Administrator shall be able to enable, disable, or mark a provider or model as degraded at the platform level.

**Postconditions:**

* New routing decisions shall respect the changed state.
* Active requests shall follow the configured transition policy.
* The action shall be audited.
* Historical execution records shall remain unchanged.

---

### FR-ADMIN-036 — Feature Administration

**Statement:** The system may allow authorized administrators to control feature availability by approved scope.

---

### FR-ADMIN-037 — Administrative Impersonation Prohibition

**Statement:** The system shall not permit unrestricted administrator impersonation of a user.

**Where Controlled Support Access Is Implemented:**

* the purpose shall be recorded;
* the scope shall be limited;
* the duration shall be limited;
* the action shall be visible in audit records;
* provider credentials shall remain inaccessible;
* sensitive actions may remain prohibited.

---

## 13.6 Audit Logs

### FR-ADMIN-038 — Administrative Audit Log

**Statement:** The system shall maintain an append-oriented audit log for administrative and security-significant actions.

---

### FR-ADMIN-039 — Audit Event Fields

**Statement:** Each audit event shall include, where applicable:

* event identifier;
* actor identifier and actor type;
* action;
* target resource;
* workspace or organization scope;
* event time;
* result;
* reason category;
* correlation identifier;
* source client or network metadata where permitted.

---

### FR-ADMIN-040 — Audit Secret Exclusion

**Statement:** Audit events shall not contain plaintext passwords, session secrets, recovery tokens, provider API keys, access tokens, or complete private prompts unless explicitly required by an approved legal policy.

---

### FR-ADMIN-041 — Audit Immutability

**Statement:** Ordinary users and administrators shall not be able to modify existing audit-event content.

**Correction Rule:** Corrections shall be represented by new linked audit events.

---

### FR-ADMIN-042 — Audit Access Control

**Statement:** Audit-log access shall require explicit permission and shall be filtered by the actor’s authorized scope.

---

### FR-ADMIN-043 — Audit Search

**Statement:** Authorized users shall be able to search audit events by supported criteria.

**Criteria May Include:**

* actor;
* action;
* target;
* result;
* workspace;
* date range;
* correlation identifier.

---

### FR-ADMIN-044 — Audit Pagination

**Statement:** Audit queries shall use deterministic pagination and bounded result sizes.

---

### FR-ADMIN-045 — Audit Retention

**Statement:** Audit events shall be retained according to an approved retention schedule that distinguishes security, billing, operational, and user-content concerns.

---

### FR-ADMIN-046 — Audit Export

**Statement:** Authorized actors may export permitted audit records without exposing inaccessible workspace data or secrets.

---

## 13.7 User and Workspace Data Export

### FR-ADMIN-047 — Data Export Request

**Statement:** The system shall allow an authorized user to request export of eligible account or workspace data.

**Validation Rules:**

* The actor shall have export permission.
* Re-authentication may be required.
* The requested scope shall be explicit.
* The workspace shall be identifiable.
* Rate and abuse controls shall apply.

---

### FR-ADMIN-048 — Export Scope

**Statement:** A workspace export shall include eligible user-owned data within the selected scope.

**Eligible Data May Include:**

* workspace settings;
* projects;
* conversations;
* messages;
* memories;
* file metadata and permitted file content;
* provider-connection metadata excluding secrets;
* usage records;
* applicable audit records;
* deletion and consent metadata where required.

---

### FR-ADMIN-049 — Export Secret Exclusion

**Statement:** Data exports shall not contain plaintext provider credentials, password hashes, session tokens, recovery tokens, encryption keys, or internal service secrets.

---

### FR-ADMIN-050 — Export Data Segregation

**Statement:** Export generation shall verify that every included record belongs to the authorized export scope.

---

### FR-ADMIN-051 — Export State

**Statement:** The system shall maintain an explicit state for each export request.

**States Shall Include, at Minimum:**

* requested;
* validating;
* generating;
* ready;
* failed;
* expired;
* deleted.

---

### FR-ADMIN-052 — Export Generation

**Statement:** Large exports shall be generated asynchronously by an authorized background process.

---

### FR-ADMIN-053 — Export Integrity

**Statement:** The system shall verify export completeness and file integrity before marking the export ready.

---

### FR-ADMIN-054 — Export Download Authorization

**Statement:** Export downloads shall require authorization and shall use time-limited access.

---

### FR-ADMIN-055 — Export Expiration

**Statement:** Ready export artifacts shall expire and be deleted after the configured availability period.

---

### FR-ADMIN-056 — Export Idempotency

**Statement:** Retried processing of the same export request shall not create uncontrolled duplicate export artifacts.

---

### FR-ADMIN-057 — Export Audit

**Statement:** Export request, generation, download, expiration, and deletion shall generate applicable audit events.

---

## 13.8 Account and Workspace Deletion

### FR-ADMIN-058 — Account Deletion Request

**Statement:** The system shall allow an eligible Authenticated User to request deletion of the user account.

**Validation Rules:**

* Re-authentication shall be required.
* The system shall identify owned workspaces and blocking obligations.
* The user shall receive a clear description of the deletion effect.
* The request shall require explicit confirmation.

---

### FR-ADMIN-059 — Workspace Deletion Request

**Statement:** The system shall allow an authorized Workspace Owner to request permanent deletion of an eligible workspace.

---

### FR-ADMIN-060 — Deletion Cooling-Off Period

**Statement:** The system may apply a configurable recovery or cooling-off period before irreversible deletion begins.

**Core Behaviour:**

* The workspace or account shall enter deletion pending.
* New prohibited operations shall be blocked.
* The authorized user may cancel the request during the permitted period.
* The scheduled irreversible-deletion time shall be recorded.

---

### FR-ADMIN-061 — Deletion Cancellation

**Statement:** The system shall allow an authorized user to cancel a deletion request before irreversible deletion begins.

**Postconditions:**

* The resource shall return to the appropriate active or restricted state.
* Scheduled deletion jobs shall be cancelled or invalidated.
* Cancellation shall be audited.

---

### FR-ADMIN-062 — Complete Erasure Processing

**Statement:** Once irreversible deletion begins, the system shall delete or irreversibly de-identify all user or workspace data not subject to an approved legal or security retention obligation.

**Data Shall Include, Where Applicable:**

* account profile;
* workspaces;
* projects;
* conversations;
* messages;
* memories;
* files;
* embeddings;
* search indexes;
* provider credentials;
* provider-connection metadata;
* exports;
* notifications;
* background jobs;
* caches;
* derived summaries;
* temporary context;
* analytics identifiers where applicable.

---

### FR-ADMIN-063 — Provider Credential Erasure

**Statement:** Complete workspace or account deletion shall remove stored provider credentials from the credential vault and invalidate cached credential material.

---

### FR-ADMIN-064 — Derived Data Erasure

**Statement:** Complete deletion shall remove embeddings, search indexes, cached context, generated summaries, and other derived data associated exclusively with the deleted source.

---

### FR-ADMIN-065 — Backup Deletion Handling

**Statement:** Data present in controlled backups shall become inaccessible to normal production use and shall expire according to the approved backup-retention schedule.

**Restoration Rule:** If a backup containing deleted data is restored, the system shall reapply valid deletion records before returning the restored environment to normal service.

---

### FR-ADMIN-066 — Legal Retention Exception

**Statement:** Where data cannot be immediately deleted because of a valid legal, fraud-prevention, security, or financial-retention obligation, the system shall restrict the retained data to the minimum required scope.

**Restriction Rules:**

* Retained data shall not be used for normal product functionality.
* The retention reason and expiration condition shall be recorded.
* User content shall be minimized or de-identified where possible.
* Provider credentials shall not be retained under ordinary audit-retention requirements.

---

### FR-ADMIN-067 — Deletion Job Idempotency

**Statement:** Account and workspace deletion jobs shall be idempotent.

**Idempotency Rules:**

* Retrying deletion shall not recreate resources.
* Already deleted records shall be treated as successfully processed.
* Shared records shall be deleted only after ownership and reference validation.
* Completion shall not be reported until required deletion stages reconcile.

---

### FR-ADMIN-068 — Deletion Failure Reconciliation

**Statement:** Partial deletion failure shall place the request in a controlled reconciliation state.

**Failure Behaviour:**

* The affected resource shall remain inaccessible to normal use.
* Failed deletion stages shall be retried according to policy.
* Operational alerts shall be generated where required.
* The system shall not falsely report complete erasure.

---

### FR-ADMIN-069 — Deletion Completion Record

**Statement:** The system shall retain a minimal deletion-completion record containing no prohibited user content.

**The Record May Include:**

* deletion-request identifier;
* anonymized or irreversible subject reference;
* completion time;
* deletion scope;
* processing result;
* legally required retention category.

---

### FR-ADMIN-070 — Deletion Confirmation

**Statement:** The system shall notify the eligible user when deletion completes or when a material deletion failure requires action.

---

## 13.9 Administrative Error and Recovery

### FR-ADMIN-071 — Administrative Error Normalization

**Statement:** Administrative operations shall return stable error categories consistent with the document-wide Error Convention.

---

### FR-ADMIN-072 — Administrative Atomicity

**Statement:** Administrative operations affecting security, provider state, spending limits, or deletion shall define and enforce atomic or recoverable state transitions.

---

### FR-ADMIN-073 — Administrative Idempotency

**Statement:** Administrative write operations that may be retried shall support idempotency where duplicate action could cause repeated restriction, duplicate export, duplicate deletion, or inconsistent configuration.

---

### FR-ADMIN-074 — Administrative Time Recording

**Statement:** Administrative state changes shall record effective time, actor, and applicable expiration time.

---

### FR-ADMIN-075 — Administrative Notification

**Statement:** The system shall notify affected users of material administrative actions where notification is permitted and does not compromise security.

**Actions May Include:**

* account restriction;
* workspace restriction;
* provider disconnection;
* spending-limit block;
* export readiness;
* deletion scheduling;
* deletion completion.

---

---

# 14. Additional MVP Functional Requirements

## 14.1 Knowledge Requirements

### FR-KNOWLEDGE-001 — Knowledge Record

**Statement:** The system shall represent retained knowledge as a structured or indexed record associated with an authorized workspace and an identifiable source.

**Required Metadata Shall Include, at Minimum:**

* knowledge identifier;
* workspace identifier;
* source identifier and source type;
* content or indexed-content reference;
* lifecycle state;
* processing version;
* creation time;
* update time;
* retrieval eligibility.

---

### FR-KNOWLEDGE-002 — Knowledge Source Eligibility

**Statement:** The system shall create knowledge records only from eligible user input, conversations, files, or other sources authorized by workspace policy.

**Validation Rules:**

* The source shall belong to the active workspace.
* The source shall not be permanently deleted.
* The actor or system process shall have processing permission.
* Conversation memory-exclusion and file-processing restrictions shall be respected.
* Ineligible source content shall not become retrievable knowledge.

---

### FR-KNOWLEDGE-003 — Knowledge Extraction

**Statement:** The Background Processing Worker shall extract eligible knowledge outside the critical response path where synchronous extraction is not required.

**Core Behaviour:**

* Extraction shall preserve source provenance.
* Extracted content shall remain scoped to the source workspace.
* Processing shall identify the extractor or processing version.
* Partial extraction shall be explicitly identified.
* Extraction failure shall not change the completed user-visible response state.

---

### FR-KNOWLEDGE-004 — Knowledge Deduplication

**Statement:** Before activating newly extracted knowledge, the system shall evaluate materially equivalent active knowledge within the authorized scope.

**Possible Outcomes Shall Include:**

* create a new record;
* update or version an existing record;
* link an additional source;
* reject a duplicate;
* retain separate records where scope or meaning differs;
* place the candidate into review when equivalence is uncertain.

---

### FR-KNOWLEDGE-005 — Knowledge Retrieval

**Statement:** Runtime knowledge retrieval shall return only active, permitted, source-valid, and contextually relevant knowledge records.

**Retrieval Rules:**

* Workspace scope shall be mandatory.
* Project and conversation scope shall be applied where relevant.
* Deleted, expired, inactive, or unauthorized sources shall be excluded.
* Result count and token limits shall be enforced.
* Retrieved records shall be deduplicated before prompt construction.
* Selected identifiers shall be preserved in the runtime execution record.

---

### FR-KNOWLEDGE-006 — Knowledge Provenance

**Statement:** Each knowledge record shall preserve sufficient provenance to identify the source material and processing activity from which it was derived.

**Provenance May Include:**

* source conversation;
* source message;
* source file and segment;
* explicit user entry;
* extraction job;
* processing version;
* extraction actor;
* extraction time.

---

### FR-KNOWLEDGE-007 — Knowledge Update and Reprocessing

**Statement:** A material source update shall cause affected knowledge to be invalidated, versioned, or scheduled for reprocessing according to the approved source-change policy.

**Atomicity Rules:**

* The prior active representation shall remain identifiable.
* A replacement shall not become active before mandatory validation completes.
* Search and vector indexes shall correspond to the effective knowledge version.
* Failed reprocessing shall result in a controlled pending, failed, or rollback state.

---

### FR-KNOWLEDGE-008 — Knowledge Deletion Reconciliation

**Statement:** When a knowledge source is permanently deleted, the system shall delete, de-identify, invalidate, or re-evaluate knowledge derived from that source according to provenance and retention policy.

**Restriction:** Deleted-source content shall not remain retrievable through stale keyword indexes, vector indexes, caches, summaries, or runtime snapshots created after deletion becomes effective.

---

### FR-KNOWLEDGE-009 — Knowledge Processing Idempotency

**Statement:** Repeated processing of the same source version under the same processing purpose shall not create duplicate active knowledge, segments, embeddings, or index entries.

---

### FR-KNOWLEDGE-010 — Knowledge Audit Events

**Statement:** The system shall audit security-significant knowledge activation, reprocessing, invalidation, restoration, and permanent deletion.

---

## 14.2 Notification Requirements

### FR-NOTIFY-001 — Notification Creation

**Statement:** The system shall create a notification only when an approved functional event and notification policy require or permit delivery.

**Notification Metadata Shall Include, at Minimum:**

* notification identifier;
* recipient identity or authorized recipient scope;
* event category;
* delivery channel;
* creation time;
* delivery state;
* related resource reference where permitted.

---

### FR-NOTIFY-002 — Notification Authorization

**Statement:** Before delivery, the Notification Service shall verify that the intended recipient remains authorized to receive information about the related resource or event.

**Restriction:** A notification shall not reveal the existence or content of an inaccessible workspace, conversation, memory, file, export, provider connection, or administrative record.

---

### FR-NOTIFY-003 — Notification Preference Enforcement

**Statement:** The Notification Service shall apply effective user and workspace notification preferences except where a mandatory security, legal, billing, or destructive-action notice cannot be disabled.

---

### FR-NOTIFY-004 — Sensitive Content Minimization

**Statement:** Notifications delivered through channels not approved for sensitive content shall contain only the minimum information necessary to communicate the event and a protected path to further details.

**Notifications Shall Not Contain:**

* passwords;
* recovery tokens;
* session credentials;
* provider credentials;
* complete private prompts;
* complete memory content;
* unrestricted export links;
* another user’s protected information.

---

### FR-NOTIFY-005 — Notification Delivery State

**Statement:** The system shall maintain an explicit delivery state for each notification attempt.

**States Shall Include, at Minimum:**

* pending;
* sent;
* delivered where confirmation is available;
* failed;
* suppressed;
* expired.

---

### FR-NOTIFY-006 — Notification Retry

**Statement:** Eligible transient notification failures shall be retried according to a bounded retry policy.

**Retry Rules:**

* Retries shall preserve the original recipient and authorization scope.
* Permanent failures shall not be retried indefinitely.
* Retry processing shall not create uncontrolled duplicate user-visible notifications.
* A material delivery failure shall remain inspectable by authorized operational processes.

---

### FR-NOTIFY-007 — Notification Idempotency

**Statement:** Notification creation and delivery shall support idempotency where repeated event processing could otherwise deliver duplicate security, billing, export, or deletion notices.

---

### FR-NOTIFY-008 — Notification Audit

**Statement:** The system shall record delivery metadata for security-significant, billing-significant, export, restriction, and deletion notifications without recording prohibited secret content.

---

## 14.3 Background Processing Requirements

### FR-BACKGROUND-001 — Background Job Creation

**Statement:** The system shall create an explicit background-job record for each asynchronous processing activity that can affect persistent state, retrieval eligibility, usage reconciliation, notification delivery, export, or deletion.

**Job Metadata Shall Include, at Minimum:**

* job identifier;
* job type;
* workspace scope;
* source or target reference;
* creation time;
* current state;
* attempt count;
* idempotency or deduplication reference where required;
* correlation identifier.

---

### FR-BACKGROUND-002 — Background Job State Model

**Statement:** The system shall maintain an explicit lifecycle state for every background job.

**States Shall Include, at Minimum:**

* queued;
* running;
* succeeded;
* failed;
* retry scheduled;
* cancelled;
* dead-lettered or equivalent terminal reconciliation state.

---

### FR-BACKGROUND-003 — Workspace Scope Validation

**Statement:** A Background Processing Worker shall validate the immutable workspace scope and target eligibility before reading or modifying protected data.

**Failure Behaviour:** A job with absent, invalid, conflicting, or unauthorized scope shall fail closed and shall not be reassigned to another workspace.

---

### FR-BACKGROUND-004 — Background Job Idempotency

**Statement:** A retried or redelivered background job shall not create duplicate active memories, knowledge records, file segments, embeddings, usage records, exports, notifications, or deletion effects.

---

### FR-BACKGROUND-005 — Background Job Claiming

**Statement:** The system shall prevent two workers from concurrently applying the same indivisible job effect unless the job type explicitly supports coordinated parallel processing.

---

### FR-BACKGROUND-006 — Retry Classification

**Statement:** Background-processing failures shall be classified as retryable, non-retryable, cancelled, or requiring reconciliation.

**Retry Rules:**

* Retry delay and maximum attempts shall be bounded.
* Non-retryable validation and permission failures shall not be retried automatically.
* Retried jobs shall retain the original workspace and processing purpose.
* Exhausted retries shall enter a controlled terminal state.

---

### FR-BACKGROUND-007 — Stale Job Detection

**Statement:** A Scheduled System Process shall identify jobs that remain running or claimed beyond the configured processing lease or timeout.

**Core Behaviour:**

* The system shall determine whether the job can be safely retried.
* An active valid worker lease shall not be overwritten.
* Recovery shall not duplicate already committed effects.
* Unrecoverable jobs shall be escalated to reconciliation.

---

### FR-BACKGROUND-008 — Job Cancellation

**Statement:** The system shall support cancellation or invalidation of eligible queued or running background jobs when their source is deleted, their workspace becomes ineligible, or an authorized operation requires cancellation.

**Restriction:** Cancellation shall not roll back a committed effect unless the applicable domain defines a compensating action.

---

### FR-BACKGROUND-009 — Source Snapshot

**Statement:** Each background job shall process an identifiable source version or immutable source snapshot sufficient to prevent an older job from overwriting a newer committed state.

---

### FR-BACKGROUND-010 — Late Result Rejection

**Statement:** The system shall reject or quarantine a background result when its source, workspace, target version, deletion state, or authorization condition no longer permits application.

---

### FR-BACKGROUND-011 — Background Failure Isolation

**Statement:** Failure or backlog in one background-job type or workspace shall not block unrelated synchronous chat execution except where a mandatory safety, deletion, quota, or integrity dependency requires blocking.

---

### FR-BACKGROUND-012 — Background Processing Audit

**Statement:** The system shall retain operationally sufficient job history for security-significant, billing-significant, export, deletion, memory, and knowledge processing.

**Audit Metadata Shall Exclude:** provider credentials, authentication secrets, and unnecessary complete user content.

---

# 15. Requirement Register Completion Status

| Requirement Domain | Identifier Range | Requirement Count | Status |
| --- | ---: | ---: | --- |
| Identity and Authentication | FR-AUTH-001 through FR-AUTH-035 | 35 | Complete |
| Organization and Workspace | FR-WORKSPACE-001 through FR-WORKSPACE-034 | 34 | Complete |
| Project and Conversation | FR-CONVERSATION-001 through FR-CONVERSATION-030 | 30 | Complete |
| Message | FR-MSG-001 through FR-MSG-034 | 34 | Complete |
| Runtime Execution | FR-RUNTIME-001 through FR-RUNTIME-045 | 45 | Complete |
| Context and Memory | FR-MEMORY-001 through FR-MEMORY-045 | 45 | Complete |
| AI Provider Connection and Routing | FR-PROVIDER-001 through FR-PROVIDER-039 | 39 | Complete |
| Streaming, File Processing, and Search | FR-STREAM-001 through FR-STREAM-059 | 59 | Complete |
| Usage, Billing, and Administration | FR-ADMIN-001 through FR-ADMIN-075 | 75 | Complete |
| Knowledge | FR-KNOWLEDGE-001 through FR-KNOWLEDGE-010 | 10 | Complete |
| Notification | FR-NOTIFY-001 through FR-NOTIFY-008 | 8 | Complete |
| Background Processing | FR-BACKGROUND-001 through FR-BACKGROUND-012 | 12 | Complete |
| **Total** |  | **426** | **Complete** |

No requirement identifier shall be reused. Any future requirement shall continue from the next sequential identifier in its domain.

---

# 16. MVP Acceptance Criteria

## 16.1 Baseline Acceptance Rule

The Gexor MVP shall not be accepted for general release unless every **MVP Critical** requirement is verified and every **MVP Required** requirement is either verified or covered by a formally approved release exception.

## 16.2 Functional Acceptance Criteria

### AC-MVP-001 — Account and Workspace Readiness

The MVP shall demonstrate that an eligible Visitor can create an account, complete required verification, authenticate, receive exactly one personal workspace, and retrieve that workspace without duplicate provisioning.

**Mapped Requirements:** FR-AUTH-001 through FR-AUTH-025; FR-WORKSPACE-004 through FR-WORKSPACE-015.

### AC-MVP-002 — Workspace Isolation

The MVP shall demonstrate that users, queries, caches, jobs, files, indexes, exports, provider connections, and runtime executions cannot access another workspace’s protected data without explicit authorization.

**Mapped Requirements:** FR-WORKSPACE-003; FR-WORKSPACE-014 through FR-WORKSPACE-030; FR-MEMORY-002; FR-MEMORY-017; FR-STREAM-002; FR-STREAM-015; FR-STREAM-033; FR-STREAM-041; FR-STREAM-048; FR-BACKGROUND-003.

### AC-MVP-003 — Provider Connection

The MVP shall demonstrate protected provider-credential submission, validation, masked display, replacement, disabling, disconnection, and deletion without plaintext credential exposure.

**Mapped Requirements:** FR-AUTH-026 through FR-AUTH-034; FR-PROVIDER-001 through FR-PROVIDER-011.

### AC-MVP-004 — Conversational Execution

The MVP shall demonstrate conversation creation, idempotent message acceptance, runtime execution, provider dispatch, streamed response delivery, durable assistant-message finalization, cancellation, retry, and stable failure reporting.

**Mapped Requirements:** FR-CONVERSATION-007 through FR-CONVERSATION-030; FR-MSG-001 through FR-MSG-034; FR-RUNTIME-001 through FR-RUNTIME-045; FR-STREAM-001 through FR-STREAM-015.

### AC-MVP-005 — Context and Prompt Control

The MVP shall demonstrate deterministic instruction precedence, context-budget enforcement, context deduplication, user-intent preservation, provider-limit compliance, and traceability of selected context.

**Mapped Requirements:** FR-RUNTIME-017 through FR-RUNTIME-028; FR-MSG-028; FR-MEMORY-016 through FR-MEMORY-026; FR-KNOWLEDGE-005.

### AC-MVP-006 — Structured Memory

The MVP shall demonstrate candidate extraction, confirmation, rejection, activation, deactivation, retrieval, inspection, update, conflict handling, soft deletion, restoration, permanent deletion, and provenance reconciliation.

**Mapped Requirements:** FR-MEMORY-001 through FR-MEMORY-045.

### AC-MVP-007 — Rapid-Fire Message Responsiveness

The MVP shall demonstrate that Message B is not blocked by unfinished memory or knowledge processing for Message A, that Message B uses the committed context snapshot available when its execution begins, and that later committed memory becomes eligible only for subsequent executions.

**Mapped Requirements:** FR-RUNTIME-042 through FR-RUNTIME-044; FR-BACKGROUND-009; FR-BACKGROUND-010.

### AC-MVP-008 — File Processing and Retrieval

The MVP shall demonstrate authorized PDF and TXT upload, trusted type detection, bounded parsing, segmentation, indexing, search, runtime injection, provenance recording, and complete deletion of derived representations.

**Mapped Requirements:** FR-STREAM-016 through FR-STREAM-059.

### AC-MVP-009 — Knowledge Lifecycle

The MVP shall demonstrate source-authorized knowledge extraction, deduplication, retrieval, provenance, reprocessing, source-deletion reconciliation, and idempotent processing.

**Mapped Requirements:** FR-KNOWLEDGE-001 through FR-KNOWLEDGE-010.

### AC-MVP-010 — Usage and Cost Visibility

The MVP shall demonstrate input, output, and total-token recording; cost estimation; pricing-version association; failed and cancelled usage recording; aggregation; and authorized inspection.

**Mapped Requirements:** FR-RUNTIME-029 through FR-RUNTIME-035; FR-ADMIN-001 through FR-ADMIN-015.

### AC-MVP-011 — Spending and Quota Enforcement

The MVP shall demonstrate soft-warning behaviour, hard-ceiling blocking, concurrent budget reservation, quota validation, rate limiting, and stable user-safe errors.

**Mapped Requirements:** FR-ADMIN-016 through FR-ADMIN-029.

### AC-MVP-012 — Export and Deletion

The MVP shall demonstrate authorized export generation, scope integrity, secret exclusion, time-limited download, expiration, account and workspace deletion, derived-data deletion, backup-restoration deletion replay, idempotency, and failure reconciliation.

**Mapped Requirements:** FR-ADMIN-047 through FR-ADMIN-070.

### AC-MVP-013 — Administrative Control

The MVP shall demonstrate elevated administrator authentication, least-privilege authorization, restricted support access, immutable audit records, provider-state administration, and privacy-preserving administrative operations.

**Mapped Requirements:** FR-ADMIN-030 through FR-ADMIN-046; FR-ADMIN-071 through FR-ADMIN-075.

### AC-MVP-014 — Notification Delivery

The MVP shall demonstrate authorized, preference-aware, privacy-minimized, idempotent notification delivery for security, usage, export, restriction, and deletion events.

**Mapped Requirements:** FR-NOTIFY-001 through FR-NOTIFY-008; FR-ADMIN-025; FR-ADMIN-070; FR-ADMIN-075.

### AC-MVP-015 — Background Processing Recovery

The MVP shall demonstrate explicit job states, workspace-scope validation, deduplication, bounded retries, stale-job recovery, cancellation, late-result rejection, and failure isolation.

**Mapped Requirements:** FR-BACKGROUND-001 through FR-BACKGROUND-012.

### AC-MVP-016 — Audit and Error Safety

The MVP shall demonstrate stable error categories, privacy-preserving user messages, correlation identifiers, secret exclusion, and auditable security-significant and destructive actions.

**Mapped Requirements:** Section 2.12; Section 2.13; FR-AUTH-035; FR-CONVERSATION-030; FR-MSG-030; FR-MSG-034; FR-RUNTIME-005; FR-RUNTIME-045; FR-PROVIDER-035 through FR-PROVIDER-039; FR-STREAM-059; FR-ADMIN-038 through FR-ADMIN-046; FR-ADMIN-071 through FR-ADMIN-075.

---

# 17. Requirement Traceability Matrix

## 17.1 Domain-to-PRD Traceability

| Functional Domain | Functional Requirement Range | Relevant PRD Areas | Product Intent |
| --- | --- | --- | --- |
| Identity and Authentication | FR-AUTH-001–035 | Section 1 Product Foundation; Section 3 MVP Scope; Section 4 Product Experience; Section 6 Constraints and Risks; Section 8 Governance | Secure account access, session control, provider-secret protection |
| Organization and Workspace | FR-WORKSPACE-001–034 | Sections 1, 2, 3, 4, 6, and 8 | Personal workspace provisioning, ownership, isolation, portability |
| Project and Conversation | FR-CONVERSATION-001–030 | Sections 2, 3, and 4 | Persistent project organization and conversation continuity |
| Message | FR-MSG-001–034 | Sections 3 and 4 | Familiar chat, durable messages, streaming states, retry and cancellation |
| Runtime Execution | FR-RUNTIME-001–045 | Sections 1, 3, 4, and 6 | Controlled runtime pipeline, prompt construction, token optimization, responsiveness |
| Context and Memory | FR-MEMORY-001–045 | Sections 1, 2, 3, 4, and 6 | Structured, relevant, inspectable, user-controlled memory |
| Provider Connection and Routing | FR-PROVIDER-001–039 | Sections 1, 3, 4, 5, and 6 | BYOK, provider independence, model selection, fallback, cost-aware routing |
| Streaming, Files, and Search | FR-STREAM-001–059 | Sections 3 and 4; Section 6 constraints | Immediate response delivery, supported file context, scoped retrieval |
| Usage, Billing, and Administration | FR-ADMIN-001–075 | Sections 3, 4, 5, 6, 7, and 8 | Cost visibility, usage limits, operational control, export, deletion, governance |
| Knowledge | FR-KNOWLEDGE-001–010 | Sections 1, 3, and 4 | Knowledge extraction, indexing, retrieval, provenance, source reconciliation |
| Notification | FR-NOTIFY-001–008 | Sections 4, 6, and 7 | Security, usage, export, deletion, and operational communication |
| Background Processing | FR-BACKGROUND-001–012 | Sections 1, 3, 4, and 6 | Non-blocking extraction, reconciliation, retry, cleanup, lifecycle enforcement |

## 17.2 Traceability Rules

1. Every implementation task shall reference at least one functional requirement identifier.
2. Every test case shall reference each requirement behaviour it verifies.
3. Every requirement shall map to at least one PRD area and one acceptance criterion.
4. A requirement without a valid PRD or approved governance source shall remain unapproved.
5. A PRD capability without functional coverage shall be recorded as a functional gap before baseline approval.
6. Traceability shall be maintained bidirectionally from PRD to test and from test to PRD.

---

# 18. Cross-Requirement Dependency Register

| Dependency ID | Source Requirement or Domain | Depends On | Dependency Rule |
| --- | --- | --- | --- |
| DEP-001 | FR-AUTH-001–004 | FR-WORKSPACE-004–006 | Account activation and personal-workspace provisioning shall form one recoverable initialization flow. |
| DEP-002 | All workspace-scoped requirements | FR-AUTH-019–024; FR-WORKSPACE-014–019 | Protected operations require a valid session and authorized workspace scope. |
| DEP-003 | FR-MSG-001–005 | FR-CONVERSATION-007–019; FR-RUNTIME-001–003 | Message acceptance requires an eligible conversation and creation of a traceable runtime execution. |
| DEP-004 | FR-RUNTIME-004–028 | FR-MEMORY-016–026; FR-KNOWLEDGE-005; FR-STREAM-032–055 | Prompt construction depends on authorized, bounded, and provenance-preserving context retrieval. |
| DEP-005 | FR-RUNTIME-029–036 | FR-PROVIDER-012–025; FR-ADMIN-001–024 | Provider dispatch depends on model metadata, pricing, quota, and spending validation. |
| DEP-006 | FR-RUNTIME-036–045 | FR-PROVIDER-026–039; FR-STREAM-001–015 | Execution completion depends on provider error normalization and valid stream finalization. |
| DEP-007 | FR-RUNTIME-043 | FR-MEMORY-005–011; FR-KNOWLEDGE-003; FR-BACKGROUND-009–010 | Snapshot Lock requires exclusion of uncommitted background results from the active execution. |
| DEP-008 | FR-MEMORY-005–011 | FR-BACKGROUND-001–012 | Memory extraction requires scoped, idempotent, recoverable background processing. |
| DEP-009 | FR-KNOWLEDGE-003–009 | FR-STREAM-024–055; FR-BACKGROUND-001–012 | Knowledge processing depends on valid source parsing, indexing, and background-job controls. |
| DEP-010 | FR-STREAM-016–038 | FR-WORKSPACE-025; FR-ADMIN-026–029 | File processing depends on isolated storage, quota, and rate controls. |
| DEP-011 | FR-STREAM-039–055 | FR-WORKSPACE-021–022; FR-MEMORY-038–039; FR-KNOWLEDGE-008 | Search depends on workspace-scoped indexes and timely deletion or invalidation. |
| DEP-012 | FR-ADMIN-016–024 | FR-RUNTIME-029–035 | Spending enforcement depends on reliable cost estimation, reservation, and reconciliation. |
| DEP-013 | FR-ADMIN-047–057 | FR-WORKSPACE-029; FR-BACKGROUND-001–012; FR-NOTIFY-001–008 | Export requires scope integrity, asynchronous generation, and controlled readiness notification. |
| DEP-014 | FR-ADMIN-058–070 | All deletion-bearing domains; FR-BACKGROUND-001–012 | Account and workspace deletion depends on domain-specific deletion and reconciliation. |
| DEP-015 | FR-NOTIFY-001–008 | FR-AUTH-019–024; FR-WORKSPACE-014–019 | Notification delivery depends on current recipient authorization and privacy controls. |
| DEP-016 | FR-ADMIN-038–046 | Section 2.12 and all audit-bearing requirements | Audit completeness depends on consistent event generation and secret exclusion. |

---

# 19. Functional Error Catalogue

| Error Code | Category | Trigger | Required System Behaviour | Retry Classification |
| --- | --- | --- | --- | --- |
| ERR-AUTH-001 | Authentication | Invalid, expired, revoked, or absent authentication | Deny protected operation without revealing account existence or secret details | Retry after valid authentication |
| ERR-AUTHZ-001 | Authorization | Actor lacks required role, membership, ownership, or permission | Deny; do not expose inaccessible resource existence where privacy requires | Non-retryable until authorization changes |
| ERR-VALIDATION-001 | Validation | Required, format, size, state, or supported-value validation fails | Reject before durable mutation or provider execution | Retry after corrected input |
| ERR-NOTFOUND-001 | Resource not found | Authorized lookup finds no eligible resource | Return privacy-preserving not-found response | Non-retryable unless identifier changes |
| ERR-CONFLICT-001 | Resource conflict | Idempotency-key conflict, duplicate state, version conflict, or invalid transition | Preserve existing valid state and return stable conflict response | Retry only after reconciliation or new key/version |
| ERR-QUOTA-001 | Quota | Applicable request, token, storage, or processing quota exhausted | Block controlled operation and expose permitted quota guidance | Retry after reset or quota change |
| ERR-RATE-001 | Rate limit | Configured request-rate threshold exceeded | Reject with stable category and safe retry time where available | Retry after indicated interval |
| ERR-COST-001 | Spending limit | Estimated or reserved cost exceeds a hard ceiling | Block provider dispatch; do not bypass via fallback | Retry after budget or policy change |
| ERR-PROVIDER-001 | Invalid provider credential | Provider rejects workspace credential | Mark connection invalid or action required; protect credential value | Retry after credential replacement |
| ERR-PROVIDER-002 | Provider rate limit | Provider returns rate-limit response | Normalize error; apply bounded retry or permitted fallback | Conditionally retryable |
| ERR-PROVIDER-003 | Provider unavailable | Provider or model is unavailable | Apply approved fallback or fail safely | Conditionally retryable |
| ERR-PROVIDER-004 | Provider request rejected | Provider rejects request format, context, policy, or capability | Normalize; do not expose unsafe provider details | Retry after request or model correction |
| ERR-TIMEOUT-001 | Connection timeout | Provider connection not established in time | Fail or fallback according to policy | Conditionally retryable |
| ERR-TIMEOUT-002 | First-event timeout | No valid first stream event within bound | Cancel or isolate late output; fail or fallback | Conditionally retryable |
| ERR-TIMEOUT-003 | Stream-idle timeout | Active stream exceeds inactivity bound | Finalize as failed or incomplete; reject late events | Conditionally retryable |
| ERR-RUNTIME-001 | Runtime processing | Classification, retrieval, budgeting, or prompt construction fails | Apply safe degraded path where permitted; otherwise fail before dispatch | Depends on failed stage |
| ERR-CONTEXT-001 | Context limit | Effective input exceeds model context bound | Reduce context deterministically or reject before provider submission | Retry after context or model change |
| ERR-MEMORY-001 | Memory processing | Extraction, confirmation, index, retrieval, or deletion fails | Preserve source and valid prior state; isolate failed candidate or job | Conditionally retryable |
| ERR-KNOWLEDGE-001 | Knowledge processing | Extraction, indexing, retrieval, or reconciliation fails | Prevent incomplete or stale knowledge from normal retrieval | Conditionally retryable |
| ERR-FILE-001 | File validation | Unsupported, oversized, unsafe, or invalid file | Reject before unbounded parsing | Retry with valid file |
| ERR-FILE-002 | File parsing | Supported file cannot be completely parsed | Mark failed or partial; do not expose incomplete content as complete | Conditionally retryable |
| ERR-SEARCH-001 | Search | Vector, keyword, or hybrid search fails | Do not return unscoped or stale results; use approved fallback | Conditionally retryable |
| ERR-STREAM-001 | Streaming | Stream connection, ordering, replay, or persistence fails | Preserve terminal state and mark partial content incomplete | Conditionally retryable |
| ERR-STORAGE-001 | Storage | Durable write, read, or integrity validation fails | Do not report success; preserve recoverable operation state | Conditionally retryable |
| ERR-BACKGROUND-001 | Background processing | Background job fails transiently | Record failure and schedule bounded retry | Retryable |
| ERR-BACKGROUND-002 | Background terminal | Job exhausts retries or fails validation/permission | Dead-letter or reconcile; do not apply partial unauthorized effect | Non-retryable automatically |
| ERR-NOTIFY-001 | Notification | Delivery channel fails | Record failure; retry only under bounded policy | Conditionally retryable |
| ERR-EXPORT-001 | Export | Export validation, generation, integrity, or authorization fails | Do not mark ready; prevent download of invalid artifact | Conditionally retryable |
| ERR-DELETION-001 | Deletion | One or more deletion stages fail | Keep resource inaccessible; enter reconciliation; do not report completion | Retryable through controlled reconciliation |
| ERR-UNSUPPORTED-001 | Unsupported operation | Capability, provider, model, file type, or state is not supported | Reject without mutation | Retry only after supported selection |
| ERR-INTERNAL-001 | Internal system | Unclassified internal failure | Return user-safe error and correlation identifier; protect internals | Determined operationally |

---

# 20. Requirement Priority Register

## 20.1 Priority Assignment Rule

Unless a requirement is explicitly classified below as **MVP Optional** or **Future**, every requirement containing **shall** or **shall not** is **MVP Required**. Requirements necessary to protect identity, workspace isolation, provider credentials, execution integrity, deletion, billing limits, or user-visible response delivery are **MVP Critical**.

## 20.2 MVP Critical Requirements

| Domain | Critical Range or Requirement |
| --- | --- |
| Authentication | FR-AUTH-001–008, FR-AUTH-010–012, FR-AUTH-014–022, FR-AUTH-024–027, FR-AUTH-029–033, FR-AUTH-035 |
| Workspace | FR-WORKSPACE-003–006, FR-WORKSPACE-008–010, FR-WORKSPACE-013–030, FR-WORKSPACE-033–034 |
| Conversation | FR-CONVERSATION-007, FR-CONVERSATION-012–014, FR-CONVERSATION-020–026, FR-CONVERSATION-027, FR-CONVERSATION-030 |
| Message | FR-MSG-001–007, FR-MSG-009–018, FR-MSG-020–031, FR-MSG-034 |
| Runtime | FR-RUNTIME-001–006, FR-RUNTIME-015, FR-RUNTIME-017–028, FR-RUNTIME-030, FR-RUNTIME-036–045 |
| Memory | FR-MEMORY-001–002, FR-MEMORY-005–012, FR-MEMORY-015–026, FR-MEMORY-029, FR-MEMORY-034–041, FR-MEMORY-045 |
| Provider | FR-PROVIDER-001–011, FR-PROVIDER-019–022, FR-PROVIDER-024–039 |
| Streaming/File/Search | FR-STREAM-001–015, FR-STREAM-016, FR-STREAM-018–020, FR-STREAM-023–045, FR-STREAM-048, FR-STREAM-054, FR-STREAM-056–059 |
| Administration | FR-ADMIN-001–010, FR-ADMIN-012–017, FR-ADMIN-020–024, FR-ADMIN-027–035, FR-ADMIN-037–045, FR-ADMIN-047–075 |
| Knowledge | FR-KNOWLEDGE-001–010 |
| Notification | FR-NOTIFY-001–002, FR-NOTIFY-004–008 |
| Background | FR-BACKGROUND-001–012 |

## 20.3 MVP Required Requirements

All remaining mandatory requirements not classified as MVP Critical are **MVP Required**.

## 20.4 MVP Optional Requirements

The following requirements are **MVP Optional** because their statements use optional or recommended behaviour and their absence does not invalidate the central MVP hypothesis:

* FR-AUTH-009;
* FR-AUTH-013;
* FR-AUTH-021;
* FR-AUTH-023;
* FR-AUTH-028;
* FR-WORKSPACE-001–002 where organization functionality is not exposed in the personal-workspace MVP;
* FR-WORKSPACE-012;
* FR-WORKSPACE-016;
* FR-CONVERSATION-008;
* FR-CONVERSATION-017;
* FR-MSG-008;
* FR-MSG-019;
* FR-MSG-032–033;
* FR-RUNTIME-008;
* FR-RUNTIME-012–014 where route eligibility does not require each route;
* FR-RUNTIME-016;
* FR-RUNTIME-031 where unknown-cost requests are otherwise blocked;
* FR-MEMORY-003–004 category or scope extensions beyond the MVP-approved set;
* FR-MEMORY-010;
* FR-MEMORY-020 ranking signals beyond the approved minimum;
* FR-MEMORY-024 alternate conflict behaviours;
* FR-MEMORY-028 displayed optional metadata;
* FR-MEMORY-030;
* FR-MEMORY-042;
* FR-PROVIDER-016;
* FR-PROVIDER-023;
* FR-STREAM-011;
* FR-STREAM-022;
* FR-STREAM-026 where OCR is not enabled;
* FR-STREAM-039–045 only if vector search is formally deferred and keyword retrieval satisfies the approved MVP retrieval acceptance criteria;
* FR-STREAM-046–055 ranking enhancements beyond the approved minimum;
* FR-ADMIN-018–019 while multi-user workspaces remain deferred;
* FR-ADMIN-021 period types beyond the approved MVP period;
* FR-ADMIN-036;
* FR-ADMIN-060 where no cooling-off period is adopted.

## 20.5 Future Capabilities

The following capabilities are not part of the locked MVP unless separately approved:

* autonomous agent execution;
* general-purpose tool orchestration;
* third-party integration marketplace;
* organization collaboration beyond the approved personal-workspace compatibility model;
* file formats beyond the approved MVP set;
* OCR unless separately approved;
* provider-managed billing resale;
* proprietary foundation-model training.

---

# 21. Document Change History

| Version | Date | Author / Authority | Change |
| --- | --- | --- | --- |
| 0.1 | 2026-07-11 | Founder / Product Owner and documentation process | Initial baseline sections and requirement conventions drafted. |
| 0.2 | 2026-07-11 | Founder / Product Owner and documentation process | FR-AUTH-001 through FR-ADMIN-075 consolidated. |
| 0.3 | 2026-07-11 | FRS finalization review | Section numbering and contents reconciled; terminology rules clarified; requirement ranges verified; final governance registers added. |
| 0.4 | 2026-07-11 | FRS finalization review | Knowledge, notification, and background-processing functional gaps closed through FR-KNOWLEDGE-001–010, FR-NOTIFY-001–008, and FR-BACKGROUND-001–012. |
| 1.0-MVP | Pending approval | Founder / Product Owner | Reserved for approved and baseline-locked Functional Requirements Specification. |

---

# 22. Approval and Baseline Status

## 22.1 Review Result

The functional requirement registers have been reviewed for:

* requirement-identifier continuity;
* duplicate identifiers;
* consolidated section numbering;
* actor terminology;
* workspace-scope consistency;
* provider terminology;
* state-transition consistency;
* permission behaviour;
* validation behaviour;
* idempotency;
* atomicity and reconciliation;
* time handling;
* audit behaviour;
* error handling;
* PRD capability coverage;
* MVP acceptance coverage;
* cross-domain dependencies.

## 22.2 Finalization Result

The finalization review found:

1. No duplicate requirement identifiers within the original nine domains.
2. No missing identifiers inside the stated original ranges.
3. A mismatch between the original Contents and the actual consolidated section structure.
4. An obsolete draft-status section before the requirement registers.
5. Missing final acceptance, traceability, dependency, error, priority, history, and approval registers.
6. Missing dedicated functional coverage for knowledge lifecycle, notification delivery, and background-job control.
7. No basis for adding autonomous-agent or third-party-integration requirements to the MVP baseline.

## 22.3 Current Status

**Document 2 — Functional Requirements is complete but under review.**

The document shall become **fully completed and baseline locked** only when:

1. the Product Owner approves this finalization patch;
2. the consolidated file is generated from the approved repository source;
3. the resulting document is checked for Markdown integrity and exact requirement counts;
4. the document version is set to `1.0-MVP`;
5. the status is set to `Approved — Baseline Locked`;
6. the approval record is completed;
7. the approved file is committed to the repository.

## 22.4 Approval Record

| Approval Field | Status |
| --- | --- |
| Product Owner review | Pending |
| Architecture review | Not required for FRS baseline approval; downstream review pending |
| Security review | Downstream review pending |
| QA review | Acceptance and traceability review pending |
| Baseline decision | Pending Product Owner approval |
| Implementation authorization | Not granted |
| GitHub update | Not performed |

## 22.5 Baseline Lock Statement

After Product Owner approval, replace the document header status with:

```markdown
**Status:** Approved — Baseline Locked
```

and update Document Control as follows:

```markdown
| Approval status         | Approved — Baseline Locked                                                       |
```

No architecture, API, database, engine, security, UX, testing, deployment, or implementation artifact shall contradict the approved functional baseline.
