# GEXOR

## Non-Functional Requirements Specification

**Document Version:** 1.0-MVP  
**Document Type:** Non-Functional Requirements Specification  
**Product:** Gexor — AI Runtime Platform  
**Product Stage:** Pre-development  
**Status:** Complete — Pending Baseline Approval  
**Source Documents:** `PRD.md`, `FUNCTIONAL-REQUIREMENTS.md`  
**Primary Release:** MVP  

---

# Document Control

| Field | Value |
| --- | --- |
| Document owner | Founder / Product Owner |
| Primary source of truth | Approved PRD and Functional Requirements Specification |
| Intended audience | Product, architecture, engineering, security, QA, operations, and implementation teams |
| Requirement baseline | MVP |
| Change authority | Founder / Product Owner |
| Implementation status | Not started |
| Approval status | Pending Product Owner baseline approval |

---

# Contents

1. Document Purpose  
2. Non-Functional Requirement Conventions  
3. Quality Attribute Model  
4. Performance and Latency Requirements  
5. Availability Requirements  
6. Reliability and Correctness Requirements  
7. Scalability and Capacity Requirements  
8. Security Requirements  
9. Privacy and Data Protection Requirements  
10. Tenant Isolation Requirements  
11. Resilience, Recovery, and Continuity Requirements  
12. Observability and Auditability Requirements  
13. Maintainability and Supportability Requirements  
14. Portability and Provider Independence Requirements  
15. Accessibility and Usability Requirements  
16. Data Integrity, Retention, and Deletion Requirements  
17. Compliance and Governance Requirements  
18. MVP Non-Functional Acceptance Criteria  
19. Traceability and Priority Register  
20. Change History and Baseline Approval  

---

# 1. Document Purpose

## 1.1 Purpose

This Non-Functional Requirements Specification defines the measurable quality attributes, operational constraints, control expectations, and service-level behaviours that the Gexor MVP shall satisfy.

The Functional Requirements Specification defines what the system shall do. This document defines how well, how safely, how consistently, and under what operational constraints those functions shall be delivered.

## 1.2 Scope

This specification covers:

* performance and latency;
* availability;
* reliability and correctness;
* scalability and capacity;
* security;
* privacy and data protection;
* workspace and tenant isolation;
* resilience and recovery;
* observability and auditability;
* maintainability and supportability;
* provider portability;
* accessibility and usability;
* data integrity, retention, backup, and deletion;
* governance and compliance;
* measurable MVP acceptance thresholds.

## 1.3 Out of Scope

This document does not define:

* detailed infrastructure topology;
* specific cloud-vendor services;
* exact database products;
* exact programming languages or frameworks;
* final production pricing;
* contractual enterprise service-level agreements;
* final disaster-recovery regions;
* implementation-specific cryptographic libraries;
* final user-interface design specifications.

## 1.4 Relationship to Functional Requirements

Every non-functional requirement shall support one or more functional domains defined in `FUNCTIONAL-REQUIREMENTS.md`.

Where this document conflicts with an approved higher-authority product requirement, the conflict shall be recorded and resolved before implementation continues.

---

# 2. Non-Functional Requirement Conventions

## 2.1 Normative Language

The terms **shall**, **shall not**, **should**, **should not**, **may**, and **future** shall have the same normative meanings defined in the Functional Requirements Specification.

## 2.2 Identifier Format

Each non-functional requirement shall use the following stable format:

```text
NFR-[DOMAIN]-[NUMBER]
```

Examples:

```text
NFR-PERF-001
NFR-SEC-014
NFR-REL-006
```

Identifiers shall not be reused after retirement.

## 2.3 Requirement Structure

Each requirement shall include:

* a unique identifier;
* a concise title;
* a measurable statement;
* an MVP priority;
* one or more traceability targets;
* verification evidence or a measurable acceptance method.

## 2.4 Priority Classes

| Priority | Meaning |
| --- | --- |
| MVP Critical | Required for safe or viable MVP operation |
| MVP Required | Required before public MVP release |
| MVP Optional | Desirable but not release-blocking |
| Future | Outside the approved MVP baseline |

## 2.5 Measurement Rules

Unless a requirement states otherwise:

* latency shall be measured server-side;
* percentile thresholds shall be calculated over rolling production-like test windows;
* availability shall exclude approved maintenance windows only where explicitly declared;
* error rates shall exclude validated client-originated errors;
* time shall be measured using server-controlled canonical time;
* performance tests shall use representative payloads and concurrency;
* security verification shall include negative-path testing;
* destructive workflows shall include recovery and reconciliation validation;
* all acceptance evidence shall be reproducible.

## 2.6 Permission, Validation, Idempotency, Atomicity, Time, Audit, and Error Conventions

The conventions defined in the Functional Requirements Specification shall apply to all applicable non-functional requirements.

No performance, availability, or usability objective shall weaken:

* authorization;
* validation;
* tenant isolation;
* auditability;
* deletion guarantees;
* security controls;
* data integrity.

---

# 3. Quality Attribute Model

The Gexor MVP shall prioritize the following quality attributes in this order when trade-offs are unavoidable:

1. Security and tenant isolation;
2. data integrity and deletion correctness;
3. runtime correctness and traceability;
4. availability and recoverability;
5. response latency;
6. scalability;
7. maintainability;
8. accessibility and usability;
9. cost efficiency.

A lower-priority attribute shall not override a higher-priority mandatory control without an approved exception.

---

# 4. Performance and Latency Requirements

### NFR-PERF-001 — API Acceptance Latency

**Statement:** For authenticated non-streaming API operations that do not invoke an external AI provider or background job, the system shall complete 95% of valid requests within 500 milliseconds and 99% within 1,500 milliseconds under the approved MVP reference load.

**Priority:** MVP Required  
**Traceability:** FR-AUTH, FR-WORKSPACE, FR-CONVERSATION, FR-MSG, FR-ADMIN  
**Verification:** Load test using representative authenticated operations.

---

### NFR-PERF-002 — Message Acceptance Latency

**Statement:** The system shall acknowledge 95% of valid user-message submissions within 750 milliseconds before external provider response generation begins.

**Priority:** MVP Critical  
**Traceability:** FR-MSG-001 through FR-MSG-010  
**Verification:** End-to-end timing from request receipt to durable acceptance response.

---

### NFR-PERF-003 — Runtime Preparation Latency

**Statement:** Excluding external provider latency, the runtime pipeline from accepted message to provider-request dispatch shall complete within 1,500 milliseconds at the 95th percentile for direct-route executions and within 3,000 milliseconds at the 95th percentile for enhanced-route executions under the MVP reference load.

**Priority:** MVP Critical  
**Traceability:** FR-RUNTIME-001 through FR-RUNTIME-036  
**Verification:** Instrumented pipeline-stage latency test.

---

### NFR-PERF-004 — Streaming First-Event Latency

**Statement:** After the first valid provider response event is received, the system shall emit the corresponding client stream event within 250 milliseconds at the 95th percentile.

**Priority:** MVP Critical  
**Traceability:** FR-STREAM-001 through FR-STREAM-015  
**Verification:** Provider-simulator streaming benchmark.

---

### NFR-PERF-005 — Stream Relay Overhead

**Statement:** The platform-added median latency between receipt of a provider content delta and emission of that delta to an authorized client shall not exceed 100 milliseconds under the MVP reference load.

**Priority:** MVP Required  
**Traceability:** FR-STREAM-004 through FR-STREAM-014  
**Verification:** Controlled provider-stream replay.

---

### NFR-PERF-006 — Memory Retrieval Latency

**Statement:** Memory retrieval for an eligible runtime execution shall complete within 750 milliseconds at the 95th percentile for workspaces containing up to 100,000 active memory records.

**Priority:** MVP Required  
**Traceability:** FR-MEMORY-016 through FR-MEMORY-026  
**Verification:** Retrieval benchmark with representative vector and keyword indexes.

---

### NFR-PERF-007 — Search Latency

**Statement:** Workspace-scoped keyword or vector searches returning no more than 50 results shall complete within 1,000 milliseconds at the 95th percentile for approved MVP dataset sizes.

**Priority:** MVP Required  
**Traceability:** FR-STREAM-039 through FR-STREAM-055  
**Verification:** Search performance test with representative index sizes.

---

### NFR-PERF-008 — Conversation Listing Latency

**Statement:** Paginated conversation-list requests with page sizes up to 100 records shall complete within 500 milliseconds at the 95th percentile under the approved MVP reference load.

**Priority:** MVP Required  
**Traceability:** FR-CONVERSATION-012 through FR-CONVERSATION-014  
**Verification:** API load test.

---

### NFR-PERF-009 — Memory Listing Latency

**Statement:** Paginated memory-list requests with page sizes up to 100 records shall complete within 750 milliseconds at the 95th percentile under the approved MVP reference load.

**Priority:** MVP Required  
**Traceability:** FR-MEMORY-027 through FR-MEMORY-030  
**Verification:** API load test.

---

### NFR-PERF-010 — Administrative Query Latency

**Statement:** Authorized usage, audit, and administrative list queries over a 30-day period shall complete within 2,000 milliseconds at the 95th percentile for approved MVP data volumes.

**Priority:** MVP Required  
**Traceability:** FR-ADMIN-001 through FR-ADMIN-057  
**Verification:** Representative administrative-query benchmark.

---

### NFR-PERF-011 — File Upload Acceptance

**Statement:** The system shall acknowledge successful receipt of a supported file within 2,000 milliseconds after the final upload byte is received, excluding file-parsing time.

**Priority:** MVP Required  
**Traceability:** FR-STREAM-016 through FR-STREAM-023  
**Verification:** Upload benchmark for supported file sizes.

---

### NFR-PERF-012 — TXT Processing Time

**Statement:** Plain-text files up to 10 MB shall reach a terminal parsed or failed state within 60 seconds for 95% of valid files under normal MVP load.

**Priority:** MVP Required  
**Traceability:** FR-STREAM-024, FR-STREAM-027 through FR-STREAM-031  
**Verification:** Batch file-processing test.

---

### NFR-PERF-013 — PDF Processing Time

**Statement:** Machine-readable PDF files up to 100 pages or 25 MB, whichever limit is reached first, shall reach a terminal parsed or failed state within 180 seconds for 95% of valid files under normal MVP load.

**Priority:** MVP Required  
**Traceability:** FR-STREAM-025 through FR-STREAM-031  
**Verification:** Representative PDF processing suite.

---

### NFR-PERF-014 — Export Generation Time

**Statement:** Workspace exports containing up to 5 GB of eligible data shall reach a ready or failed state within 30 minutes for 95% of requests under normal MVP load.

**Priority:** MVP Required  
**Traceability:** FR-ADMIN-047 through FR-ADMIN-057  
**Verification:** Export benchmark using synthetic workspace data.

---

### NFR-PERF-015 — Cancellation Responsiveness

**Statement:** After an authorized cancellation request is accepted, the system shall stop presenting additional normal generation output within 500 milliseconds at the 95th percentile.

**Priority:** MVP Critical  
**Traceability:** FR-MSG-020 through FR-MSG-023, FR-RUNTIME-039  
**Verification:** Active-stream cancellation test.

---

### NFR-PERF-016 — Snapshot-Lock Non-Blocking Behaviour

**Statement:** Active background processing for a preceding message shall add no more than 100 milliseconds of platform latency to acceptance of a subsequent message that uses snapshot-lock behaviour.

**Priority:** MVP Critical  
**Traceability:** FR-RUNTIME-043  
**Verification:** Rapid-fire message concurrency test.

---

### NFR-PERF-017 — Background Queue Dispatch

**Statement:** Eligible background work shall be enqueued within 2 seconds after synchronous runtime finalization for 99% of completed executions.

**Priority:** MVP Required  
**Traceability:** FR-RUNTIME-042, FR-BACKGROUND  
**Verification:** Runtime-to-queue timing test.

---

### NFR-PERF-018 — Token Counting Overhead

**Statement:** Local token estimation and budget calculation shall add no more than 250 milliseconds at the 95th percentile for prompts up to the approved maximum MVP context size.

**Priority:** MVP Required  
**Traceability:** FR-RUNTIME-017 through FR-RUNTIME-023, FR-ADMIN-001 through FR-ADMIN-007  
**Verification:** Tokenization benchmark.

---

### NFR-PERF-019 — Performance Degradation Bound

**Statement:** At 80% of approved MVP capacity, 95th-percentile latency for critical runtime operations shall not exceed twice the corresponding baseline threshold defined in this section.

**Priority:** MVP Required  
**Traceability:** All runtime-critical functional requirements  
**Verification:** Capacity stress test.

---

### NFR-PERF-020 — Performance Test Reproducibility

**Statement:** Every release candidate shall include a reproducible performance-test report identifying dataset size, concurrency, payload profile, environment, and percentile results.

**Priority:** MVP Required  
**Traceability:** Requirement governance and release acceptance  
**Verification:** Release evidence review.

---

# 5. Availability Requirements

### NFR-AVAIL-001 — Monthly Service Availability

**Statement:** The production MVP shall achieve at least 99.5% monthly availability for authenticated workspace and conversation access, excluding approved maintenance windows.

**Priority:** MVP Required  
**Traceability:** FR-AUTH, FR-WORKSPACE, FR-CONVERSATION  
**Verification:** Monthly availability report.

---

### NFR-AVAIL-002 — Runtime Submission Availability

**Statement:** The system shall achieve at least 99.0% monthly availability for accepting valid runtime execution requests, excluding failures caused solely by unavailable external providers.

**Priority:** MVP Critical  
**Traceability:** FR-MSG-001, FR-RUNTIME-001 through FR-RUNTIME-036  
**Verification:** Synthetic transaction monitoring.

---

### NFR-AVAIL-003 — Provider Failure Isolation

**Statement:** Unavailability of one external AI provider shall not make workspace access, conversation access, memory management, export status, or administrative functions unavailable.

**Priority:** MVP Critical  
**Traceability:** FR-PROVIDER-020 through FR-PROVIDER-034  
**Verification:** Provider outage simulation.

---

### NFR-AVAIL-004 — Degraded Mode

**Statement:** When an optional subsystem is unavailable, the system shall continue eligible operations using an explicitly documented degraded mode rather than failing unrelated capabilities.

**Priority:** MVP Required  
**Traceability:** FR-RUNTIME-009, FR-MEMORY-026, FR-STREAM-045  
**Verification:** Dependency-failure test.

---

### NFR-AVAIL-005 — Streaming Service Availability

**Statement:** The streaming service shall achieve at least 99.0% monthly availability for authorized active executions.

**Priority:** MVP Required  
**Traceability:** FR-STREAM-001 through FR-STREAM-015  
**Verification:** Synthetic stream monitoring.

---

### NFR-AVAIL-006 — Administrative Availability

**Statement:** Security-critical administrative actions, including account restriction and session revocation, shall remain available during partial failure whenever the identity and authorization services are operational.

**Priority:** MVP Critical  
**Traceability:** FR-AUTH-008, FR-AUTH-022, FR-ADMIN-030 through FR-ADMIN-037  
**Verification:** Partial-outage operational test.

---

### NFR-AVAIL-007 — Maintenance Declaration

**Statement:** Planned maintenance that affects user-facing availability shall be declared before execution and shall identify expected start time, end time, affected capabilities, and recovery criteria.

**Priority:** MVP Required  
**Traceability:** Operational governance  
**Verification:** Maintenance procedure review.

---

### NFR-AVAIL-008 — Health Check Coverage

**Statement:** Every production service participating in authentication, runtime execution, streaming, storage, retrieval, or background processing shall expose a machine-readable health state.

**Priority:** MVP Required  
**Traceability:** FR-PROVIDER-006 through FR-PROVIDER-009 and operational requirements  
**Verification:** Deployment readiness test.

---

### NFR-AVAIL-009 — Readiness Enforcement

**Statement:** A service instance shall not receive production traffic until all mandatory startup dependencies and configuration validations succeed.

**Priority:** MVP Critical  
**Traceability:** Validation and error conventions  
**Verification:** Deployment failure test.

---

### NFR-AVAIL-010 — Availability Measurement Integrity

**Statement:** Availability calculations shall distinguish platform failure, external provider failure, planned maintenance, and client-originated failure.

**Priority:** MVP Required  
**Traceability:** Audit and observability requirements  
**Verification:** Monitoring data review.

---

# 6. Reliability and Correctness Requirements

### NFR-REL-001 — Durable Message Acceptance

**Statement:** No message shall be reported as accepted unless its canonical content and required identifiers are durably stored or placed in a recoverable write-ahead state.

**Priority:** MVP Critical  
**Traceability:** FR-MSG-001 through FR-MSG-010  
**Verification:** Storage-failure injection test.

---

### NFR-REL-002 — Duplicate Execution Prevention

**Statement:** Under client retry, network retry, and service retry conditions, the system shall not create duplicate provider executions for the same valid idempotency scope.

**Priority:** MVP Critical  
**Traceability:** FR-MSG-005, FR-RUNTIME-044  
**Verification:** Retry and replay test.

---

### NFR-REL-003 — Terminal-State Consistency

**Statement:** Completed, failed, and cancelled execution states shall remain mutually exclusive and shall not transition to another terminal state after finalization.

**Priority:** MVP Critical  
**Traceability:** FR-MSG-016, FR-RUNTIME-040 through FR-RUNTIME-044  
**Verification:** State-machine test.

---

### NFR-REL-004 — Usage Record Consistency

**Statement:** Every accepted provider execution shall have exactly one authoritative usage record or one explicit reconciliation record indicating why final usage is unavailable.

**Priority:** MVP Critical  
**Traceability:** FR-RUNTIME-032 through FR-RUNTIME-035, FR-ADMIN-001 through FR-ADMIN-015  
**Verification:** Execution-to-usage reconciliation test.

---

### NFR-REL-005 — Cost Calculation Reproducibility

**Statement:** Recalculation using the recorded pricing version and usage values shall reproduce the stored provider-cost result within the approved numeric precision.

**Priority:** MVP Required  
**Traceability:** FR-RUNTIME-029 through FR-RUNTIME-035, FR-ADMIN-008 through FR-ADMIN-014  
**Verification:** Cost recomputation test.

---

### NFR-REL-006 — Ordering Consistency

**Statement:** Message, stream-event, audit-event, and job ordering shall remain deterministic within their declared scope.

**Priority:** MVP Critical  
**Traceability:** FR-CONVERSATION-027, FR-STREAM-006, FR-ADMIN-038 through FR-ADMIN-044  
**Verification:** Concurrent ordering test.

---

### NFR-REL-007 — Memory Provenance Integrity

**Statement:** Every active extracted memory shall retain at least one valid provenance reference or an explicit record that the memory was independently confirmed by an authorized user.

**Priority:** MVP Critical  
**Traceability:** FR-MEMORY-007 through FR-MEMORY-015, FR-MEMORY-029  
**Verification:** Memory provenance audit.

---

### NFR-REL-008 — Index Consistency

**Statement:** Canonical records and retrieval indexes shall not remain materially inconsistent for longer than 60 seconds after a successful committed update under normal operating conditions.

**Priority:** MVP Required  
**Traceability:** FR-MEMORY-031 through FR-MEMORY-039, FR-STREAM-029 through FR-STREAM-055  
**Verification:** Index reconciliation test.

---

### NFR-REL-009 — Partial Failure Visibility

**Statement:** A multi-step operation that cannot complete fully shall expose a controlled intermediate, pending, failed, or reconciliation state and shall not report false success.

**Priority:** MVP Critical  
**Traceability:** Atomicity and error conventions; deletion, export, and runtime finalization requirements  
**Verification:** Failure-injection suite.

---

### NFR-REL-010 — Background Job Idempotency

**Statement:** Retrying the same background job identity shall not create duplicate active memories, indexes, notifications, exports, usage records, or deletion actions.

**Priority:** MVP Critical  
**Traceability:** FR-BACKGROUND, FR-MEMORY-011, FR-ADMIN-056, FR-ADMIN-067  
**Verification:** Job replay test.

---

### NFR-REL-011 — Clock Consistency

**Statement:** Security, retention, expiration, billing, and ordering decisions shall use server-controlled time synchronized within 2 seconds across production services.

**Priority:** MVP Required  
**Traceability:** Time convention and all time-sensitive requirements  
**Verification:** Time synchronization monitoring.

---

### NFR-REL-012 — Release Regression Protection

**Statement:** A release candidate shall not be approved when automated regression tests fail for any MVP Critical functional or non-functional requirement.

**Priority:** MVP Critical  
**Traceability:** Entire MVP baseline  
**Verification:** Release gate evidence.

---

# 7. Scalability and Capacity Requirements

### NFR-SCALE-001 — Concurrent User Capacity

**Statement:** The MVP architecture shall support at least 1,000 concurrently authenticated users without violating the critical latency thresholds defined in Section 4.

**Priority:** MVP Required  
**Traceability:** Authentication, workspace, conversation, and runtime requirements  
**Verification:** Concurrent-user load test.

---

### NFR-SCALE-002 — Concurrent Runtime Capacity

**Statement:** The system shall support at least 200 concurrently active provider executions across workspaces without cross-execution data leakage or uncontrolled queue growth.

**Priority:** MVP Required  
**Traceability:** FR-RUNTIME, FR-STREAM, FR-WORKSPACE-019  
**Verification:** Runtime concurrency test.

---

### NFR-SCALE-003 — Workspace Data Capacity

**Statement:** A single workspace shall support at least 1,000,000 messages, 100,000 active memories, 10,000 files, and 10,000 runtime executions per month without requiring a data-model redesign.

**Priority:** MVP Required  
**Traceability:** Workspace, conversation, memory, file, and usage requirements  
**Verification:** Capacity-model review and dataset benchmark.

---

### NFR-SCALE-004 — Horizontal Runtime Scaling

**Statement:** Runtime, streaming, search, and background-processing services shall support horizontal scaling without requiring workspace-specific code changes.

**Priority:** MVP Required  
**Traceability:** FR-RUNTIME, FR-STREAM, FR-BACKGROUND  
**Verification:** Multi-instance deployment test.

---

### NFR-SCALE-005 — Stateless Request Handling

**Statement:** User-facing request services should avoid mandatory instance-local session state unless equivalent shared or recoverable state is available.

**Priority:** MVP Required  
**Traceability:** Session, runtime, and streaming requirements  
**Verification:** Instance-termination continuity test.

---

### NFR-SCALE-006 — Queue Backpressure

**Statement:** Background queues shall apply configurable backpressure before queue depth causes unbounded memory growth, data loss, or synchronous runtime failure.

**Priority:** MVP Critical  
**Traceability:** FR-RUNTIME-042, FR-BACKGROUND  
**Verification:** Queue saturation test.

---

### NFR-SCALE-007 — Per-Workspace Fairness

**Statement:** One workspace shall not consume more than its configured share of shared runtime, search, storage, or background-processing capacity when doing so would starve other workspaces.

**Priority:** MVP Required  
**Traceability:** Quota, rate-limit, and isolation requirements  
**Verification:** Noisy-neighbour test.

---

### NFR-SCALE-008 — Storage Growth Monitoring

**Statement:** The system shall measure storage growth by workspace and data category and shall generate an operational warning before any managed storage reaches 80% of its approved capacity.

**Priority:** MVP Required  
**Traceability:** FR-ADMIN-026, file, memory, export, and audit requirements  
**Verification:** Capacity alert test.

---

### NFR-SCALE-009 — Capacity Forecast

**Statement:** Production operations shall maintain a rolling 90-day capacity forecast for request volume, storage, vector index size, and background-job volume.

**Priority:** MVP Optional  
**Traceability:** Operational governance  
**Verification:** Capacity review artifact.

---

### NFR-SCALE-010 — Scaling Without Identifier Change

**Statement:** Scaling, partitioning, reindexing, or migration shall not change stable user-facing resource identifiers.

**Priority:** MVP Critical  
**Traceability:** All stable-identifier functional requirements  
**Verification:** Migration and scale-out test.

---

# 8. Security Requirements

### NFR-SEC-001 — Encrypted Transport

**Statement:** All production client, service, database, queue, object-storage, and provider communications carrying protected data shall use approved encrypted transport.

**Priority:** MVP Critical  
**Traceability:** FR-AUTH-024, FR-AUTH-026 through FR-AUTH-033  
**Verification:** Configuration and penetration test.

---

### NFR-SEC-002 — Encryption at Rest

**Statement:** Provider credentials, authentication secrets, user content, memories, files, exports, and backups shall be encrypted at rest using approved cryptographic controls.

**Priority:** MVP Critical  
**Traceability:** Credential protection, storage, export, and backup requirements  
**Verification:** Security architecture review.

---

### NFR-SEC-003 — Secret Separation

**Statement:** Encryption keys and reusable secrets shall be stored separately from the protected application records they secure.

**Priority:** MVP Critical  
**Traceability:** FR-AUTH-027 through FR-AUTH-033  
**Verification:** Secrets-management review.

---

### NFR-SEC-004 — Least Privilege

**Statement:** Human and service identities shall receive only the minimum permissions required for their documented responsibilities.

**Priority:** MVP Critical  
**Traceability:** Permission convention, FR-ADMIN-030 through FR-ADMIN-037  
**Verification:** Role and service-account review.

---

### NFR-SEC-005 — Default Deny

**Statement:** Access to protected resources and actions shall be denied when an explicit permission cannot be established.

**Priority:** MVP Critical  
**Traceability:** Permission convention and workspace isolation requirements  
**Verification:** Negative authorization test.

---

### NFR-SEC-006 — Administrative Strong Authentication

**Statement:** Production administrative access shall require multi-factor authentication or an equivalent elevated assurance mechanism.

**Priority:** MVP Critical  
**Traceability:** FR-ADMIN-030  
**Verification:** Administrative access test.

---

### NFR-SEC-007 — Sensitive Action Re-authentication

**Statement:** Account deletion, workspace deletion, provider-credential replacement, complete export, and session-wide revocation shall require recent authentication not older than 15 minutes or an approved additional verification step.

**Priority:** MVP Critical  
**Traceability:** FR-AUTH-025, FR-ADMIN-047, FR-ADMIN-058 through FR-ADMIN-061  
**Verification:** Sensitive-action authentication test.

---

### NFR-SEC-008 — Session Protection

**Statement:** Browser session cookies shall use Secure, HttpOnly, and an approved SameSite policy, and reusable session credentials shall never appear in user-visible URLs.

**Priority:** MVP Critical  
**Traceability:** FR-AUTH-019 through FR-AUTH-024  
**Verification:** Browser security test.

---

### NFR-SEC-009 — Session Expiration

**Statement:** The default authenticated session shall expire after no more than 30 days absolute lifetime and no more than 24 hours of inactivity unless a stricter policy applies.

**Priority:** MVP Required  
**Traceability:** FR-AUTH-020 through FR-AUTH-022  
**Verification:** Session lifecycle test.

---

### NFR-SEC-010 — Password Protection

**Statement:** Password-based authentication shall use an approved adaptive one-way hashing function with unique salts and configurable work factors.

**Priority:** MVP Critical  
**Traceability:** FR-AUTH-010 through FR-AUTH-016  
**Verification:** Identity implementation review.

---

### NFR-SEC-011 — Password Minimum Length

**Statement:** Where password authentication is enabled, the minimum password length shall be at least 12 characters.

**Priority:** MVP Required  
**Traceability:** FR-AUTH-010  
**Verification:** Registration and password-change test.

---

### NFR-SEC-012 — Authentication Abuse Protection

**Statement:** Authentication, recovery, verification, provider validation, export, and deletion endpoints shall enforce configurable rate limits and abuse controls.

**Priority:** MVP Critical  
**Traceability:** FR-AUTH-003, FR-AUTH-007, FR-AUTH-014, FR-ADMIN-028  
**Verification:** Abuse simulation test.

---

### NFR-SEC-013 — Credential Logging Prohibition

**Statement:** Plaintext passwords, session secrets, recovery tokens, provider API keys, access tokens, refresh tokens, encryption keys, and complete private credentials shall never be written to application logs, traces, analytics, or user-visible errors.

**Priority:** MVP Critical  
**Traceability:** FR-AUTH-011, FR-AUTH-033, FR-ADMIN-040  
**Verification:** Log-content security test.

---

### NFR-SEC-014 — Input Validation

**Statement:** All externally supplied data shall be validated for type, size, format, ownership, scope, and supported values before durable mutation or provider execution.

**Priority:** MVP Critical  
**Traceability:** Validation convention and all write operations  
**Verification:** Negative input test suite.

---

### NFR-SEC-015 — Untrusted Content Isolation

**Statement:** Retrieved memories, files, provider responses, and search results shall be treated as untrusted content and shall not override higher-authority instructions.

**Priority:** MVP Critical  
**Traceability:** FR-RUNTIME-026, FR-RUNTIME-027, FR-STREAM-038  
**Verification:** Prompt-injection test suite.

---

### NFR-SEC-016 — File Processing Isolation

**Statement:** File parsing shall execute with no direct access to provider credentials, unrelated workspace data, or unrestricted host resources.

**Priority:** MVP Critical  
**Traceability:** FR-STREAM-018, FR-STREAM-027, FR-STREAM-028  
**Verification:** Sandbox escape and permission test.

---

### NFR-SEC-017 — Security Event Detection

**Statement:** Repeated authentication failures, unauthorized access attempts, cross-workspace scope failures, credential misuse, and abnormal administrative actions shall generate security events within 60 seconds.

**Priority:** MVP Critical  
**Traceability:** Audit and security-significant functional requirements  
**Verification:** Security-event simulation.

---

### NFR-SEC-018 — Vulnerability Remediation

**Statement:** Confirmed critical vulnerabilities affecting production shall be mitigated within 24 hours and high-severity vulnerabilities within 7 calendar days, unless an approved risk exception exists.

**Priority:** MVP Critical  
**Traceability:** Security governance  
**Verification:** Vulnerability-management records.

---

### NFR-SEC-019 — Dependency Security Review

**Statement:** Production dependencies shall be scanned for known vulnerabilities before release and at least once every 24 hours thereafter.

**Priority:** MVP Required  
**Traceability:** Security governance  
**Verification:** Dependency-scan evidence.

---

### NFR-SEC-020 — Security Testing Gate

**Statement:** Public MVP release shall require passing authentication, authorization, tenant-isolation, secret-exposure, file-processing, injection-resistance, and destructive-operation security tests.

**Priority:** MVP Critical  
**Traceability:** Entire security baseline  
**Verification:** Release security report.

---

# 9. Privacy and Data Protection Requirements

### NFR-PRIV-001 — Data Minimization

**Statement:** The system shall collect, retain, and process only data required for documented product, security, billing, legal, or operational purposes.

**Priority:** MVP Critical  
**Traceability:** PRD privacy principles; export and deletion requirements  
**Verification:** Data-inventory review.

---

### NFR-PRIV-002 — Purpose Limitation

**Statement:** User content shall not be used for an unrelated purpose without explicit policy authority and applicable user consent.

**Priority:** MVP Critical  
**Traceability:** User-control principles  
**Verification:** Privacy policy and processing review.

---

### NFR-PRIV-003 — Provider Data Disclosure Transparency

**Statement:** Before transmitting user content to an external AI provider, the system shall make the applicable provider identity and execution context discoverable to the user.

**Priority:** MVP Required  
**Traceability:** FR-RUNTIME-016, FR-PROVIDER-025, FR-PROVIDER-033  
**Verification:** User-interface and runtime-record review.

---

### NFR-PRIV-004 — Export Completeness

**Statement:** A user export shall include all eligible user-controlled data within the requested scope and shall exclude secrets and inaccessible data.

**Priority:** MVP Critical  
**Traceability:** FR-ADMIN-047 through FR-ADMIN-057  
**Verification:** Export-content audit.

---

### NFR-PRIV-005 — Deletion Effectiveness

**Statement:** Permanently deleted content shall become inaccessible through normal APIs, search, retrieval, runtime context, exports, and administrative views immediately after deletion completion.

**Priority:** MVP Critical  
**Traceability:** FR-CONVERSATION-024 through FR-CONVERSATION-026, FR-MEMORY-037 through FR-MEMORY-041, FR-ADMIN-062 through FR-ADMIN-070  
**Verification:** Post-deletion retrieval test.

---

### NFR-PRIV-006 — Derived Data Deletion

**Statement:** Deletion workflows shall remove or invalidate derived embeddings, indexes, caches, summaries, and temporary artifacts associated exclusively with deleted source data.

**Priority:** MVP Critical  
**Traceability:** FR-ADMIN-064, FR-MEMORY-038, FR-MEMORY-039, FR-STREAM-057  
**Verification:** Derived-data deletion test.

---

### NFR-PRIV-007 — Notification Privacy

**Statement:** External notifications shall not include message content, memory content, provider credentials, export contents, or other sensitive workspace data.

**Priority:** MVP Critical  
**Traceability:** FR-NOTIFY, FR-AUTH-002, FR-AUTH-016, FR-ADMIN-070, FR-ADMIN-075  
**Verification:** Notification content test.

---

### NFR-PRIV-008 — Support Access Limitation

**Statement:** Support access to private user content shall require explicit operational purpose, minimum necessary scope, time limitation, and audit recording.

**Priority:** MVP Critical  
**Traceability:** FR-ADMIN-037  
**Verification:** Support-access workflow review.

---

### NFR-PRIV-009 — Data Location Recording

**Statement:** The system shall maintain an inventory of production systems and external providers that store or process protected user data.

**Priority:** MVP Required  
**Traceability:** Governance and provider requirements  
**Verification:** Data-flow inventory.

---

### NFR-PRIV-010 — Privacy Incident Traceability

**Statement:** A privacy-relevant incident shall be traceable to affected workspaces, data categories, processing systems, and time ranges without exposing unrelated user data.

**Priority:** MVP Critical  
**Traceability:** Audit, isolation, and incident-response requirements  
**Verification:** Incident simulation.

---

# 10. Tenant Isolation Requirements

### NFR-ISOL-001 — Workspace Scope Enforcement

**Statement:** Every protected data operation shall enforce workspace scope at a trusted server or data-access boundary.

**Priority:** MVP Critical  
**Traceability:** FR-WORKSPACE-014 through FR-WORKSPACE-030  
**Verification:** Cross-workspace access test.

---

### NFR-ISOL-002 — Cross-Workspace Leakage Prohibition

**Statement:** The tolerated cross-workspace data leakage rate shall be zero.

**Priority:** MVP Critical  
**Traceability:** FR-WORKSPACE-019  
**Verification:** Automated tenant-isolation test suite.

---

### NFR-ISOL-003 — Identifier Non-Authority

**Statement:** Possession of a resource identifier shall not grant access without an independently validated authorized workspace context.

**Priority:** MVP Critical  
**Traceability:** FR-WORKSPACE-014, FR-WORKSPACE-018  
**Verification:** Direct-object-reference test.

---

### NFR-ISOL-004 — Cache Isolation

**Statement:** Shared caches shall include immutable tenant scope in cache keys and shall not return protected data without authorization revalidation where required.

**Priority:** MVP Critical  
**Traceability:** FR-WORKSPACE-020  
**Verification:** Cache-collision test.

---

### NFR-ISOL-005 — Search Isolation

**Statement:** Vector, keyword, hybrid, and administrative searches shall enforce tenant scope before results are returned or injected into runtime context.

**Priority:** MVP Critical  
**Traceability:** FR-WORKSPACE-021, FR-WORKSPACE-022, FR-STREAM-041 through FR-STREAM-055  
**Verification:** Search-scope penetration test.

---

### NFR-ISOL-006 — Queue Isolation

**Statement:** Every workspace-scoped background job shall retain an immutable workspace identifier from creation through retry, reassignment, and completion.

**Priority:** MVP Critical  
**Traceability:** FR-WORKSPACE-023, FR-BACKGROUND  
**Verification:** Queue replay and reassignment test.

---

### NFR-ISOL-007 — File Isolation

**Statement:** File object references and temporary download links shall not authorize access outside the selected workspace.

**Priority:** MVP Critical  
**Traceability:** FR-WORKSPACE-025, FR-STREAM-016 through FR-STREAM-038  
**Verification:** File-access isolation test.

---

### NFR-ISOL-008 — Provider Credential Isolation

**Statement:** A provider credential associated with one workspace shall never authenticate a request for another workspace unless an explicit organization-level sharing policy authorizes it.

**Priority:** MVP Critical  
**Traceability:** FR-WORKSPACE-026, FR-PROVIDER-002 through FR-PROVIDER-011  
**Verification:** Provider-credential scope test.

---

### NFR-ISOL-009 — Export Isolation

**Statement:** Export integrity validation shall fail the export when any included record cannot be proven to belong to the authorized export scope.

**Priority:** MVP Critical  
**Traceability:** FR-WORKSPACE-029, FR-ADMIN-050  
**Verification:** Mixed-tenant export test.

---

### NFR-ISOL-010 — Isolation Regression Gate

**Statement:** No release shall be approved when any automated tenant-isolation regression test fails.

**Priority:** MVP Critical  
**Traceability:** Entire workspace isolation baseline  
**Verification:** Release gate evidence.

---

# 11. Resilience, Recovery, and Continuity Requirements

### NFR-REC-001 — Recovery Point Objective

**Statement:** The production MVP shall maintain a recovery point objective of no more than 15 minutes for canonical workspace, conversation, message, memory, provider-connection metadata, usage, and configuration data.

**Priority:** MVP Critical  
**Traceability:** All durable data requirements  
**Verification:** Backup and recovery test.

---

### NFR-REC-002 — Recovery Time Objective

**Statement:** The production MVP shall maintain a recovery time objective of no more than 4 hours for restoration of core authenticated workspace and conversation capabilities after a recoverable platform-wide failure.

**Priority:** MVP Critical  
**Traceability:** Availability and continuity requirements  
**Verification:** Disaster-recovery exercise.

---

### NFR-REC-003 — Backup Frequency

**Statement:** Canonical production data shall be backed up or continuously replicated at a frequency sufficient to satisfy NFR-REC-001.

**Priority:** MVP Critical  
**Traceability:** FR-ADMIN-065  
**Verification:** Backup schedule review.

---

### NFR-REC-004 — Backup Encryption

**Statement:** Backups containing protected data shall be encrypted in transit and at rest and shall use access controls separate from ordinary application access.

**Priority:** MVP Critical  
**Traceability:** Security and backup requirements  
**Verification:** Backup-security review.

---

### NFR-REC-005 — Backup Restoration Test

**Statement:** A representative production backup restoration shall be tested at least once every 90 days.

**Priority:** MVP Required  
**Traceability:** FR-ADMIN-065  
**Verification:** Restoration evidence.

---

### NFR-REC-006 — Deletion Reapplication After Restore

**Statement:** Restored environments shall reapply valid deletion records before normal user access is enabled.

**Priority:** MVP Critical  
**Traceability:** FR-ADMIN-065  
**Verification:** Restore-with-deletion test.

---

### NFR-REC-007 — Retry Bound

**Statement:** Automated retries shall use bounded attempt counts, backoff, and terminal failure handling and shall not retry indefinitely.

**Priority:** MVP Critical  
**Traceability:** Error, idempotency, provider fallback, and background requirements  
**Verification:** Retry-policy test.

---

### NFR-REC-008 — Circuit Breaking

**Statement:** Repeated dependency failure shall trigger a controlled circuit-break or equivalent protection before cascading failure affects unrelated operations.

**Priority:** MVP Required  
**Traceability:** Provider, search, queue, and storage failure behaviour  
**Verification:** Dependency-outage test.

---

### NFR-REC-009 — Stale Job Recovery

**Statement:** Background jobs with no progress for longer than their configured execution timeout shall be detected and moved to retry, failure, or reconciliation within 5 minutes.

**Priority:** MVP Required  
**Traceability:** FR-BACKGROUND  
**Verification:** Stale-job simulation.

---

### NFR-REC-010 — Partial Stream Recovery

**Statement:** After service interruption, persisted partial response content shall remain distinguishable from completed content and shall not be duplicated during reconnection.

**Priority:** MVP Critical  
**Traceability:** FR-MSG-018, FR-MSG-019, FR-STREAM-011 through FR-STREAM-014  
**Verification:** Mid-stream failure test.

---

### NFR-REC-011 — Region Failure Readiness

**Statement:** The architecture shall not permanently bind user data or stable identifiers to one compute instance or one non-recoverable runtime node.

**Priority:** MVP Required  
**Traceability:** Portability and recovery requirements  
**Verification:** Architecture review.

---

### NFR-REC-012 — Recovery Audit

**Statement:** Backup restoration, replay, failover, deletion reapplication, and reconciliation actions shall generate audit evidence.

**Priority:** MVP Required  
**Traceability:** Audit convention and recovery requirements  
**Verification:** Recovery audit review.

---

# 12. Observability and Auditability Requirements

### NFR-OBS-001 — Correlation Identifier

**Statement:** Every authenticated request, runtime execution, provider request, stream, background job, export, and deletion workflow shall have a traceable correlation identifier.

**Priority:** MVP Critical  
**Traceability:** FR-RUNTIME-037, FR-MSG-030, FR-ADMIN-039  
**Verification:** Trace-correlation test.

---

### NFR-OBS-002 — Structured Logging

**Statement:** Production services shall emit structured machine-readable logs containing service, environment, severity, event category, timestamp, and correlation context.

**Priority:** MVP Required  
**Traceability:** Audit and error conventions  
**Verification:** Log-schema validation.

---

### NFR-OBS-003 — Secret-Free Telemetry

**Statement:** Logs, metrics, traces, and alerts shall exclude reusable secrets and unnecessary complete user content.

**Priority:** MVP Critical  
**Traceability:** FR-AUTH-033, FR-ADMIN-040  
**Verification:** Telemetry content scan.

---

### NFR-OBS-004 — Runtime Stage Metrics

**Statement:** The system shall measure request count, success rate, error rate, and latency for each material runtime stage.

**Priority:** MVP Required  
**Traceability:** FR-RUNTIME-004, FR-RUNTIME-005  
**Verification:** Metrics coverage review.

---

### NFR-OBS-005 — Provider Metrics

**Statement:** The system shall measure provider availability, timeout rate, rate-limit rate, fallback rate, and usage volume by provider and model.

**Priority:** MVP Required  
**Traceability:** FR-PROVIDER-021 through FR-PROVIDER-039  
**Verification:** Provider dashboard review.

---

### NFR-OBS-006 — Queue Metrics

**Statement:** Background-processing observability shall include queue depth, oldest-job age, processing rate, retry count, dead-letter count, and failure rate.

**Priority:** MVP Required  
**Traceability:** FR-BACKGROUND  
**Verification:** Queue dashboard review.

---

### NFR-OBS-007 — Data-Layer Metrics

**Statement:** The system shall monitor database error rate, connection saturation, query latency, storage utilization, index health, and replication or backup health.

**Priority:** MVP Required  
**Traceability:** Data integrity and availability requirements  
**Verification:** Infrastructure monitoring review.

---

### NFR-OBS-008 — Alerting Time

**Statement:** Critical security, availability, data-loss, cross-workspace isolation, and deletion-integrity events shall generate an operational alert within 5 minutes of detection.

**Priority:** MVP Critical  
**Traceability:** Security, isolation, recovery, and deletion requirements  
**Verification:** Alert-delivery test.

---

### NFR-OBS-009 — Audit Event Durability

**Statement:** Security-significant and destructive audit events shall be durably recorded before the corresponding operation is reported complete where technically feasible.

**Priority:** MVP Critical  
**Traceability:** FR-ADMIN-038 through FR-ADMIN-046  
**Verification:** Audit-write failure test.

---

### NFR-OBS-010 — Audit Immutability

**Statement:** Ordinary application and administrative workflows shall not modify existing audit-event content.

**Priority:** MVP Critical  
**Traceability:** FR-ADMIN-041  
**Verification:** Audit mutation test.

---

### NFR-OBS-011 — Audit Search Performance

**Statement:** Authorized audit searches over 90 days of MVP-scale data shall complete within 5 seconds at the 95th percentile.

**Priority:** MVP Required  
**Traceability:** FR-ADMIN-043, FR-ADMIN-044  
**Verification:** Audit-search benchmark.

---

### NFR-OBS-012 — Monitoring Retention

**Statement:** Operational metrics shall be retained for at least 90 days and security-relevant audit events for at least 365 days unless a stricter approved policy applies.

**Priority:** MVP Required  
**Traceability:** FR-ADMIN-045  
**Verification:** Retention-policy review.

---

# 13. Maintainability and Supportability Requirements

### NFR-MAINT-001 — Modular Service Boundaries

**Statement:** Identity, workspace, runtime, memory, provider routing, streaming, search, usage, notification, and background-processing responsibilities shall have explicit module or service boundaries.

**Priority:** MVP Required  
**Traceability:** Functional domain model  
**Verification:** Architecture review.

---

### NFR-MAINT-002 — Configuration Externalization

**Statement:** Environment-specific endpoints, credentials, timeouts, limits, pricing data, and feature controls shall not require source-code modification.

**Priority:** MVP Required  
**Traceability:** Provider, runtime, quota, and administrative requirements  
**Verification:** Configuration-management review.

---

### NFR-MAINT-003 — Schema Migration Safety

**Statement:** Production data migrations shall be versioned, reversible where practical, and validated against rollback or forward-recovery procedures.

**Priority:** MVP Critical  
**Traceability:** Data integrity requirements  
**Verification:** Migration rehearsal.

---

### NFR-MAINT-004 — Backward Compatibility

**Statement:** An API change that breaks an approved client contract shall require a new version or an explicitly approved migration window.

**Priority:** MVP Required  
**Traceability:** API design dependencies  
**Verification:** Contract-test review.

---

### NFR-MAINT-005 — Automated Test Coverage

**Statement:** MVP Critical requirements shall have automated verification where technically feasible, and any manual-only verification shall have documented justification.

**Priority:** MVP Critical  
**Traceability:** Entire MVP baseline  
**Verification:** Traceability matrix review.

---

### NFR-MAINT-006 — Code Quality Gate

**Statement:** Release candidates shall pass approved static analysis, formatting, type checking where supported, dependency scanning, and automated test suites.

**Priority:** MVP Required  
**Traceability:** Release governance  
**Verification:** CI evidence.

---

### NFR-MAINT-007 — Operational Runbooks

**Statement:** Authentication failure, provider outage, queue backlog, data restoration, tenant-isolation incident, export failure, and deletion failure shall each have an approved operational runbook before public MVP release.

**Priority:** MVP Required  
**Traceability:** Error and recovery requirements  
**Verification:** Runbook review.

---

### NFR-MAINT-008 — Support Diagnostics

**Statement:** Authorized support personnel shall be able to inspect non-secret operational status using correlation identifiers without requiring direct database access.

**Priority:** MVP Required  
**Traceability:** FR-ADMIN-033, FR-ADMIN-034  
**Verification:** Support workflow test.

---

### NFR-MAINT-009 — Documentation Currency

**Statement:** A release shall not be approved when implemented behaviour materially differs from the approved PRD, FRS, NFRS, API, or security documentation.

**Priority:** MVP Critical  
**Traceability:** Source-of-truth hierarchy  
**Verification:** Release documentation review.

---

### NFR-MAINT-010 — Change Traceability

**Statement:** Every implementation task, code change, and test case affecting MVP behaviour shall reference at least one approved requirement identifier.

**Priority:** MVP Required  
**Traceability:** Traceability convention  
**Verification:** Repository and work-item audit.

---

# 14. Portability and Provider Independence Requirements

### NFR-PORT-001 — Provider-Neutral Domain Model

**Statement:** Canonical conversations, messages, memories, usage records, and runtime executions shall not require one provider’s proprietary identifier as their primary identity.

**Priority:** MVP Critical  
**Traceability:** Provider independence product principle  
**Verification:** Domain-model review.

---

### NFR-PORT-002 — Provider Adapter Boundary

**Statement:** Provider-specific authentication, request formatting, streaming events, errors, usage reporting, and model metadata shall be isolated behind an explicit provider integration boundary.

**Priority:** MVP Required  
**Traceability:** FR-PROVIDER-001 through FR-PROVIDER-039  
**Verification:** Architecture review.

---

### NFR-PORT-003 — Provider Replacement

**Statement:** Adding or replacing a supported provider shall not require modification of canonical workspace, conversation, message, or memory records.

**Priority:** MVP Required  
**Traceability:** Provider routing and canonical data requirements  
**Verification:** Provider-adapter test.

---

### NFR-PORT-004 — Error Normalization

**Statement:** Provider-specific failures shall be normalized into stable internal categories before they are consumed by user-facing or orchestration logic.

**Priority:** MVP Critical  
**Traceability:** FR-PROVIDER-035, FR-PROVIDER-036  
**Verification:** Provider error mapping test.

---

### NFR-PORT-005 — Pricing Version Independence

**Statement:** Provider pricing updates shall be deployable as versioned configuration without rewriting historical usage records.

**Priority:** MVP Required  
**Traceability:** FR-RUNTIME-034, FR-ADMIN-009  
**Verification:** Pricing update test.

---

### NFR-PORT-006 — Model Catalogue Refresh

**Statement:** Provider model catalogues shall be refreshable without application redeployment where the selected architecture supports dynamic metadata refresh.

**Priority:** MVP Optional  
**Traceability:** FR-PROVIDER-012, FR-PROVIDER-013  
**Verification:** Catalogue refresh test.

---

### NFR-PORT-007 — Data Export Portability

**Statement:** User exports shall use documented, machine-readable formats for structured data and shall preserve stable identifiers and provenance where permitted.

**Priority:** MVP Required  
**Traceability:** FR-ADMIN-047 through FR-ADMIN-057  
**Verification:** Export-schema review.

---

### NFR-PORT-008 — Infrastructure Portability

**Statement:** Core business rules shall not depend directly on one cloud vendor’s proprietary runtime semantics without an explicit abstraction or approved exception.

**Priority:** MVP Required  
**Traceability:** Architecture principles  
**Verification:** Architecture dependency review.

---

# 15. Accessibility and Usability Requirements

### NFR-UX-001 — Accessibility Standard

**Statement:** User-facing MVP web interfaces shall conform to WCAG 2.2 Level AA for supported workflows, excluding documented third-party limitations outside platform control.

**Priority:** MVP Required  
**Traceability:** Authentication, conversation, memory, usage, export, and deletion workflows  
**Verification:** Accessibility audit.

---

### NFR-UX-002 — Keyboard Operation

**Statement:** Core authentication, conversation, message, memory, provider, export, and deletion workflows shall be operable using a keyboard alone.

**Priority:** MVP Required  
**Traceability:** Core user workflows  
**Verification:** Keyboard accessibility test.

---

### NFR-UX-003 — Error Comprehension

**Statement:** User-facing errors shall state the failed action, a stable error category, and an actionable next step where one exists, without exposing sensitive internals.

**Priority:** MVP Required  
**Traceability:** Error convention  
**Verification:** Error-message review.

---

### NFR-UX-004 — Destructive Action Confirmation

**Statement:** Permanent deletion and credential-removal actions shall require explicit confirmation that clearly identifies the affected scope and reversibility.

**Priority:** MVP Critical  
**Traceability:** Deletion and credential requirements  
**Verification:** UX workflow test.

---

### NFR-UX-005 — Streaming State Visibility

**Statement:** The interface shall distinguish sending, streaming, complete, failed, incomplete, and cancelled message states.

**Priority:** MVP Critical  
**Traceability:** FR-MSG-009 through FR-MSG-019  
**Verification:** UI state test.

---

### NFR-UX-006 — Provider and Model Visibility

**Statement:** The effective provider and model used for a completed execution shall be discoverable by the user.

**Priority:** MVP Required  
**Traceability:** FR-RUNTIME-016, FR-PROVIDER-025, FR-PROVIDER-033  
**Verification:** UI and execution-detail review.

---

### NFR-UX-007 — Long-Running Operation Visibility

**Statement:** File processing, export generation, deletion, and background-review workflows shall expose a current state and terminal success or failure state.

**Priority:** MVP Required  
**Traceability:** File, export, deletion, and background requirements  
**Verification:** UI state-transition test.

---

### NFR-UX-008 — Timezone Display

**Statement:** User-facing timestamps shall be displayed in the configured user timezone while preserving canonical server time internally.

**Priority:** MVP Required  
**Traceability:** Time convention  
**Verification:** Timezone display test.

---

# 16. Data Integrity, Retention, and Deletion Requirements

### NFR-DATA-001 — Canonical Identifier Stability

**Statement:** Stable identifiers shall remain unchanged across rename, archive, restore, scaling, migration, and retry operations.

**Priority:** MVP Critical  
**Traceability:** All stable-identifier functional requirements  
**Verification:** Lifecycle test.

---

### NFR-DATA-002 — Referential Integrity

**Statement:** The system shall prevent creation of orphaned workspace-scoped records unless an explicit temporary reconciliation state is defined.

**Priority:** MVP Critical  
**Traceability:** Workspace, conversation, message, memory, file, usage, and export requirements  
**Verification:** Integrity constraint test.

---

### NFR-DATA-003 — Write Atomicity

**Statement:** Multi-record state transitions shall either complete atomically or enter a recoverable state with sufficient metadata for reconciliation.

**Priority:** MVP Critical  
**Traceability:** Atomicity convention  
**Verification:** Failure-injection test.

---

### NFR-DATA-004 — Data Corruption Detection

**Statement:** Files, exports, and backups shall use integrity metadata sufficient to detect accidental corruption.

**Priority:** MVP Required  
**Traceability:** FR-STREAM-021, FR-ADMIN-053, backup requirements  
**Verification:** Corruption simulation.

---

### NFR-DATA-005 — Retention Policy Definition

**Statement:** Every persistent data category shall have a documented retention rule identifying minimum retention, maximum retention, deletion trigger, and legal exception behaviour.

**Priority:** MVP Critical  
**Traceability:** FR-ADMIN-045, FR-ADMIN-055, FR-ADMIN-062 through FR-ADMIN-066  
**Verification:** Retention register review.

---

### NFR-DATA-006 — Temporary Artifact Expiration

**Statement:** Temporary upload artifacts, stream buffers, processing files, and export download artifacts shall expire automatically within their documented validity period.

**Priority:** MVP Required  
**Traceability:** Temporary context, file, streaming, and export requirements  
**Verification:** Expiration test.

---

### NFR-DATA-007 — Deleted Data Non-Retrievability

**Statement:** Deleted or inactive memories, files, vectors, indexes, and conversations shall not appear in normal retrieval within 60 seconds of the committed state change.

**Priority:** MVP Critical  
**Traceability:** Memory, file, conversation, and search deletion requirements  
**Verification:** Post-deletion retrieval benchmark.

---

### NFR-DATA-008 — Deletion Completion Evidence

**Statement:** Permanent deletion shall produce a minimal completion record containing no prohibited user content.

**Priority:** MVP Critical  
**Traceability:** FR-ADMIN-069  
**Verification:** Deletion record review.

---

### NFR-DATA-009 — Backup Retention Bound

**Statement:** Backups containing deleted data shall expire according to a documented retention period not exceeding 35 days for the MVP unless an approved legal exception applies.

**Priority:** MVP Required  
**Traceability:** FR-ADMIN-065, FR-ADMIN-066  
**Verification:** Backup-retention configuration review.

---

### NFR-DATA-010 — Data Migration Verification

**Statement:** Data migrations shall verify record counts, integrity constraints, identifier preservation, and tenant scope before completion is accepted.

**Priority:** MVP Critical  
**Traceability:** Data integrity and isolation requirements  
**Verification:** Migration validation report.

---

# 17. Compliance and Governance Requirements

### NFR-GOV-001 — Requirement Traceability

**Statement:** Every MVP Critical and MVP Required non-functional requirement shall map to at least one product principle, functional domain, risk, design control, or acceptance test.

**Priority:** MVP Required  
**Traceability:** Entire baseline  
**Verification:** Traceability matrix review.

---

### NFR-GOV-002 — Change Control

**Statement:** Changes to approved non-functional thresholds, priorities, or scope shall require documented impact analysis and Product Owner approval.

**Priority:** MVP Critical  
**Traceability:** Change-control convention  
**Verification:** Change record review.

---

### NFR-GOV-003 — Exception Approval

**Statement:** A temporary exception to an MVP Critical requirement shall identify scope, reason, risk owner, mitigation, expiration date, and approval authority.

**Priority:** MVP Critical  
**Traceability:** Governance model  
**Verification:** Exception register review.

---

### NFR-GOV-004 — Release Evidence

**Statement:** Public MVP release shall require an evidence package covering performance, availability, security, isolation, recovery, accessibility, and deletion verification.

**Priority:** MVP Critical  
**Traceability:** Sections 4 through 16  
**Verification:** Release readiness review.

---

### NFR-GOV-005 — Incident Classification

**Statement:** Operational incidents shall be classified by severity, affected scope, data impact, user impact, and recovery status.

**Priority:** MVP Required  
**Traceability:** Observability, security, privacy, and recovery requirements  
**Verification:** Incident process review.

---

### NFR-GOV-006 — Post-Incident Review

**Statement:** Critical incidents shall receive a documented post-incident review within 5 business days after service restoration.

**Priority:** MVP Required  
**Traceability:** Operational governance  
**Verification:** Incident-review evidence.

---

### NFR-GOV-007 — Data Processing Inventory

**Statement:** The system owner shall maintain a current inventory of personal data categories, processing purposes, storage locations, external providers, retention rules, and deletion mechanisms.

**Priority:** MVP Required  
**Traceability:** Privacy and provider requirements  
**Verification:** Data-processing register review.

---

### NFR-GOV-008 — Baseline Approval

**Statement:** This specification shall not become the implementation baseline until approved by the Product Owner.

**Priority:** MVP Critical  
**Traceability:** Document governance  
**Verification:** Approval record.

---

# 18. MVP Non-Functional Acceptance Criteria

The MVP non-functional baseline shall be accepted only when all of the following conditions are satisfied:

1. All MVP Critical requirements have passing verification evidence.
2. No unresolved cross-workspace isolation defect exists.
3. No plaintext credential or secret is present in logs, exports, or user-visible errors.
4. Message acceptance, runtime preparation, and streaming thresholds satisfy Section 4.
5. Recovery-point and recovery-time objectives have been tested.
6. Backup restoration and deletion reapplication have been demonstrated.
7. Provider outage does not prevent unrelated workspace operations.
8. Background retries do not create duplicate durable records.
9. Export and deletion scope integrity tests pass.
10. Accessibility testing confirms supported MVP workflows meet the declared standard.
11. Audit and correlation records support reconstruction of critical operational flows.
12. All requirement identifiers are unique and sequential within their domains.
13. Every MVP Critical and MVP Required requirement has an assigned verification method.
14. All approved exceptions are unexpired and documented.
15. Product Owner baseline approval is recorded.

---

# 19. Traceability and Priority Register

| Domain | Identifier Range | Count | Default Priority |
| --- | ---: | ---: | --- |
| Performance and Latency | NFR-PERF-001 through NFR-PERF-020 | 20 | MVP Required |
| Availability | NFR-AVAIL-001 through NFR-AVAIL-010 | 10 | MVP Required |
| Reliability and Correctness | NFR-REL-001 through NFR-REL-012 | 12 | MVP Critical |
| Scalability and Capacity | NFR-SCALE-001 through NFR-SCALE-010 | 10 | MVP Required |
| Security | NFR-SEC-001 through NFR-SEC-020 | 20 | MVP Critical |
| Privacy and Data Protection | NFR-PRIV-001 through NFR-PRIV-010 | 10 | MVP Critical |
| Tenant Isolation | NFR-ISOL-001 through NFR-ISOL-010 | 10 | MVP Critical |
| Resilience and Recovery | NFR-REC-001 through NFR-REC-012 | 12 | MVP Critical |
| Observability and Auditability | NFR-OBS-001 through NFR-OBS-012 | 12 | MVP Required |
| Maintainability and Supportability | NFR-MAINT-001 through NFR-MAINT-010 | 10 | MVP Required |
| Portability and Provider Independence | NFR-PORT-001 through NFR-PORT-008 | 8 | MVP Required |
| Accessibility and Usability | NFR-UX-001 through NFR-UX-008 | 8 | MVP Required |
| Data Integrity, Retention, and Deletion | NFR-DATA-001 through NFR-DATA-010 | 10 | MVP Critical |
| Compliance and Governance | NFR-GOV-001 through NFR-GOV-008 | 8 | MVP Required |
| **Total** |  | **160** |  |

## 19.1 Traceability Rule

Implementation tasks, architecture decisions, operational controls, and test cases shall reference the applicable NFR identifier.

## 19.2 Conflict Rule

When two approved non-functional requirements conflict:

1. Security and isolation shall take precedence.
2. Data integrity and deletion correctness shall take precedence over latency.
3. Explicit legal or regulatory obligations shall take precedence over product convenience.
4. The conflict shall be recorded and approved before implementation.

---

# 20. Change History and Baseline Approval

## 20.1 Change History

| Version | Date | Change | Status |
| --- | --- | --- | --- |
| 1.0-MVP | 2026-07-11 | Initial complete MVP non-functional baseline | Pending approval |

## 20.2 Approval Record

| Role | Name | Decision | Date |
| --- | --- | --- | --- |
| Product Owner | Pending | Pending | Pending |
| Architecture Review | Pending | Pending | Pending |
| Security Review | Pending | Pending | Pending |
| QA Review | Pending | Pending | Pending |

## 20.3 Baseline Rule

After approval:

* requirement identifiers shall remain stable;
* threshold changes shall follow change control;
* implementation and tests shall reference approved identifiers;
* no silent requirement change shall be introduced through source code alone;
* future requirements shall be added through a new approved document version.
