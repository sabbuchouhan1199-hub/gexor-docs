# GEXOR

## API Design Specification

**Version:** 1.0-MVP

**Status:** Complete — Pending Baseline Approval
**Scope:** Public/client API, streaming, administration, and internal integration contracts

---

# 1. Contract Principles

Gexor exposes a versioned, resource-oriented HTTPS API and Server-Sent Events (SSE) stream. Contracts are provider-neutral, workspace-scoped, least-privilege, idempotent for retriable mutations, cursor-paginated, observable, and backward compatible within a major version.

Base path: `/api/v1`. JSON uses `camelCase`, opaque string IDs, RFC 3339 UTC timestamps, integer token counts, and monetary `{amountMinor, currency}` values. Unknown response fields must be ignored by clients. Provider-native request/response shapes never become public domain contracts.

# 2. Authentication, Scope, and Headers

Bearer sessions or approved service credentials authenticate requests. The server derives the actor and verifies membership; a supplied workspace ID never grants access.

| Header | Use |
| --- | --- |
| `Authorization` | Required authentication credential |
| `X-Workspace-Id` | Explicit active workspace; server-authorized |
| `Idempotency-Key` | Required for create/send/retry/export/delete operations |
| `If-Match` | Aggregate version for conflict-safe updates |
| `X-Request-Id` | Optional client correlation; sanitized or replaced |
| `traceparent` | Standards-based distributed trace correlation |

Responses return `X-Request-Id`, rate-limit metadata where safe, and `ETag` on versioned resources. Credentials, prompts, memory content, file bodies, and provider secrets must not appear in headers or URLs.

# 3. Resource Surface

| Area | Representative endpoints |
| --- | --- |
| Identity | `POST /auth/register`, `/auth/login`, `/auth/logout`, `/auth/recovery`; `GET /me` |
| Workspaces | `GET/POST /workspaces`; `GET/PATCH /workspaces/{id}`; memberships and roles subresources |
| Projects | `GET/POST /workspaces/{wid}/projects`; `GET/PATCH/DELETE /projects/{id}` |
| Conversations | list/create/get/update/archive/restore/delete; messages subresource |
| Runtime | `POST /conversations/{id}/messages`; `GET /executions/{id}`; cancel, retry, regenerate, stream |
| Memory | list/get/create/update/confirm/reject/delete; candidate review endpoints |
| Knowledge/files | upload, processing status, list, search, download authorization, delete |
| Providers | provider/model catalogue; workspace connections; test, revoke, select |
| Usage | workspace usage, costs, quotas, spending controls |
| Notifications | list/read/preferences |
| Lifecycle | exports, deletion requests, retention status, recovery status |
| Administration | dedicated `/admin` resources with elevated authorization and audit |

Nested routes express ownership during creation/listing; canonical resource URLs are used for get/update. All workspace-owned lookup queries enforce both resource ID and authorized workspace.

# 4. Runtime Request and Response

`POST /api/v1/conversations/{conversationId}/messages` accepts content, authorized file references, optional provider/model preference, and client metadata. It atomically creates the user message and execution, returning `202 Accepted` with message/execution IDs, state, stream URL, and correlation ID. Duplicate idempotency keys with identical bodies return the original result; mismatched bodies return conflict.

```json
{
  "content": [{"type": "text", "text": "Summarize the project risks"}],
  "fileIds": ["file_01..."],
  "providerPreference": {"providerId": "provider_openai", "modelId": "model_..."}
}
```

Execution responses expose normalized state, timestamps, chosen provider/model labels, usage/cost visibility, recoverable error category, and links. They do not expose credentials, internal policy text, hidden chain-of-thought, raw provider errors, or unauthorized context.

# 5. SSE Streaming Contract

`GET /api/v1/executions/{id}/events` uses `text/event-stream`. Authorization is revalidated on connection and reconnect. `Last-Event-ID` supports bounded replay from a persisted cursor.

Normalized events: `execution.accepted`, `execution.started`, `response.delta`, `response.completed`, `usage.updated`, `execution.failed`, `execution.cancelled`, and `heartbeat`. Each event carries `id`, `type`, `executionId`, monotonic `sequence`, `occurredAt`, and a versioned `data` object. Terminal events are emitted once; late provider output cannot reactivate a terminal execution.

# 6. Upload and Search Contracts

Uploads use a server-authorized multipart flow or short-lived signed object upload followed by completion. The API validates file identity, declared/actual type, size, checksum, quota, malware status, and workspace ownership. Status progresses through accepted, scanning, parsing, chunking, indexing, ready, failed, or deleted.

Search accepts bounded query text, source filters, project/file scope, modes (`keyword`, `vector`, `hybrid`), and cursor. Results include source ID/version, citation location, relevance metadata, and eligibility state. Search never returns cross-workspace or deleted-source projections.

# 7. Pagination, Filtering, and Versioning

Collections use opaque cursor pagination: `?limit=50&cursor=...`; maximum limits are server-controlled. Sort and filter fields are allow-listed. Offset pagination is not used for mutable high-volume resources. Breaking changes require `/api/v2`; additive optional fields and new enum values are nonbreaking when clients follow compatibility rules. Deprecations publish dates, telemetry, migration guidance, and a supported overlap window.

# 8. Errors

Errors use `application/problem+json`:

```json
{
  "type": "https://docs.gexor/errors/quota-exceeded",
  "title": "Quota exceeded",
  "status": 429,
  "code": "QUOTA_EXCEEDED",
  "detail": "The workspace token quota is exhausted.",
  "requestId": "req_01...",
  "retryable": false
}
```

Categories include validation, unauthenticated, forbidden, not found, conflict, quota/rate limit, provider unavailable, timeout, cancelled, unsafe content, and internal error. Enumeration resistance may intentionally return not found. Field errors identify safe JSON pointers. Raw stack traces and provider payloads are prohibited.

# 9. Idempotency, Concurrency, and Rate Control

Idempotency records bind actor, workspace, route, normalized body hash, key, and retention window. Optimistic updates require `If-Match`; stale versions return `409` or `412`. Cancellation and finalization are conditional terminal transitions. Rate limits apply per identity, workspace, IP/risk signal, endpoint, provider connection, and cost budget; `Retry-After` is returned where appropriate.

# 10. Internal Events and Webhooks

Internal event envelopes contain event ID/type/version, workspace, aggregate ID/version, correlation/causation IDs, canonical time, and minimized payload. Consumers validate schema/scope and record inbox receipts. Customer webhooks, if enabled, are signed, timestamped, replay-protected, retried with backoff, and disableable; delivery never includes secrets or unrestricted content.

# 11. Security and Quality Gates

OpenAPI is the executable contract. CI performs schema linting, breaking-change detection, generated examples, authorization matrix tests, tenant-isolation tests, fuzz/property tests, idempotency and concurrency tests, SSE ordering/reconnect tests, and sensitive-data checks. API logs record identifiers, outcomes, latency, and correlation—not bearer tokens, provider keys, full prompts, or file contents.

# 12. Traceability and Approval

Endpoints map to FRS domains and `DOMAIN-MODEL.md` bounded contexts; runtime semantics map to `RUNTIME-PIPELINE.md`; performance/security/error behavior maps to NFRS. Owners: API Architecture, Security, Engineering, QA, Product, and Operations. Approval pending.

---

# End of Document
