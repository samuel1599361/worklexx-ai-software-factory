# WORKLEXX AI SOFTWARE FACTORY
# ARCHITECTURE DECISION RECORD REGISTER

## Document Metadata

| Field | Value |
|---|---|
| Document Title | Architecture Decision Record Register |
| Document ID | WLX-ARCH-012 |
| Version | 1.0 |
| Status | Proposed — Phase 0 |
| Classification | Internal |
| Platform | Worklexx AI Software Factory |
| Repository | https://github.com/samuel1599361/worklexx-ai-software-factory |
| Parent Phase | Phase 0 — Architecture and Planning |
| Document Owner | Project Owner — appointment/confirmation pending |
| Decision Authority | Pending explicit confirmation |
| Review Frequency | At each material architecture change and phase gate |
| Related Documents | Architecture Overview, System Architecture, Technology Stack, Repository Structure, Agent Ecosystem, Service Boundaries, Database Architecture, Security Architecture, Deployment Architecture, Development Roadmap, Risk Register, Phase 0 Inspection Report, Testing Strategy, Monitoring and Observability, Cost and Scalability |
| Approval Status | Not formally approved |

---

## 1. Purpose

This document establishes the Architecture Decision Record (ADR) register for the Worklexx AI Software Factory.

An ADR records a significant architectural decision, including:

- The problem or architectural question.
- The context in which the decision is required.
- The options considered.
- The selected or proposed approach.
- The reasons for the approach.
- The consequences and trade-offs.
- Dependencies and related decisions.
- The person authorised to approve the decision.
- The decision date and supporting evidence.
- The status and any superseding decision.

The register provides a traceable history of architectural reasoning and prevents important decisions from being made informally, inconsistently, or without appropriate approval.

## 2. Scope

This register covers significant architectural decisions affecting:

1. Overall platform architecture.
2. Frontend and backend deployment boundaries.
3. Technology selection and version baselines.
4. Repository and Git branching strategy.
5. API Gateway and AI model-routing architecture.
6. Agent ecosystem and orchestration.
7. Database architecture and tenant isolation.
8. Object storage and file management.
9. Financial ledger integrity.
10. Security and sandbox execution.
11. Human approval gates and protected operations.
12. Messaging and workflow communication.
13. Agent module organisation.
14. Source-code governance and release strategy.

Minor implementation choices that do not materially affect system architecture do not necessarily require an ADR.

## 3. ADR Governance Principles

All ADRs must follow these principles:

- **Explicit decisions:** Significant architectural choices must be documented.
- **Traceability:** Each ADR has a unique identifier that is not reused.
- **Evidence:** Decisions should be supported by relevant technical evidence, testing, or documented reasoning.
- **Human authority:** AI agents may draft, analyse, compare, and recommend decisions but cannot approve them without explicit delegated authority.
- **Consistency:** ADRs must align with the approved architecture and related controlled documents.
- **Change control:** Material changes require a new ADR or a formally recorded revision.
- **Reversibility:** Decisions should identify migration or replacement implications where relevant.
- **Separation of approval and implementation:** An approved ADR does not automatically authorise deployment, spending, or protected GitHub operations.

## 4. ADR Status Definitions

The following status vocabulary applies to every ADR.

| Status | Meaning |
|---|---|
| Proposed | A decision has been documented for review but has not been approved |
| Conditionally Accepted | An authorised decision-maker has approved the approach subject to explicitly recorded conditions |
| Accepted | An authorised decision-maker has formally approved the decision and its evidence is recorded |
| Deprecated | The decision is no longer recommended for new work but may remain relevant to existing components |
| Superseded | A later ADR has replaced the decision |

An ADR must not be marked Accepted merely because it appears in this register, is technically plausible, or has been discussed.

### 4.1 Acceptance Requirements

An ADR may be marked Accepted only when the record includes:

- The authorised decision-maker's identity or role.
- Evidence that the decision-maker holds the required authority.
- The decision date.
- The approved decision and scope.
- Any conditions or limitations.
- Supporting test results or evidence where required.
- Related ADRs and architecture documents affected by the decision.

Where approval authority has not been established, the ADR remains Proposed.

## 5. ADR Identification and Numbering

The register contains 14 initial ADR identifiers. Repository-level decisions HD-REP-01 through HD-REP-11 are maintained as a separate controlled decision series:

- ADR-001
- ADR-002
- ADR-003
- ADR-004
- ADR-005
- ADR-006
- ADR-007
- ADR-008
- ADR-009
- ADR-010
- ADR-011
- ADR-012
- ADR-013
- ADR-014

Identifiers must not be reused, even when an ADR is deprecated or superseded.

Future decisions must receive new sequential identifiers.

## 6. ADR Register Summary

| ADR ID | Decision Area | Current Status |
|---|---|---|
| ADR-001 | Overall Platform Architecture | Proposed |
| ADR-002 | Frontend Hosting and Runtime Architecture | Proposed |
| ADR-003 | Backend Technology and Version Baseline | Proposed |
| ADR-004 | Frontend Application Architecture | Proposed |
| ADR-005 | API Design and Service Communication | Proposed |
| ADR-006 | API Gateway, AI Gateway, and Model Routing | Proposed |
| ADR-007 | Database Architecture and Tenant Isolation | Proposed |
| ADR-008 | Object Storage and File Management | Proposed |
| ADR-009 | Financial Ledger Integrity and Posting Controls | Proposed |
| ADR-010 | Secure Sandbox Execution | Proposed |
| ADR-011 | Human Approval Gates and Protected Operations | Proposed |
| ADR-012 | Messaging and Event Communication | Proposed |
| ADR-013 | Agent Ecosystem and Module Organisation | Proposed |
| ADR-014 | Git Branching and Repository Workflow | Proposed |

**Important:** These statuses represent the Phase 0 register baseline. They do not imply that all underlying technologies or architectural approaches have been approved for implementation.

---

## 7. ADR-001 — Overall Platform Architecture

**Status:** Proposed

**Decision area:** Platform architecture and service organisation.

### 7.1 Context

The Worklexx AI Software Factory requires a scalable architecture capable of supporting multiple frontend applications, backend services, AI agents, multimodal processing, secure code execution, billing, and advertising capabilities.

The architecture must provide clear service ownership, security boundaries, tenant isolation, and independent scaling where justified.

### 7.2 Decision Statement

The proposed architecture consists of five frontend applications and six deployable backend service units.

The five frontend applications are:

1. `worklexx.ai`
2. `app.worklexx.ai`
3. `video.worklexx.ai`
4. `images.worklexx.ai`
5. `docs.worklexx.ai`

The API Gateway uses:

`api.worklexx.ai`

The six deployable backend service units are:

1. `api-gateway`
2. `agent-orchestrator`
3. `multimodal-service`
4. `sandbox-runner`
5. `billing-ledger`
6. `adtech-service`

The API Gateway is a separate deployable from the identity provider.

The AI Gateway and model-routing capability are logical capabilities within the approved deployment architecture, not an additional undocumented seventh deployable service.

### 7.3 Alternatives Considered

- A single monolithic backend.
- A large collection of independently deployed microservices.
- A modular service architecture with a controlled number of deployable units.

### 7.4 Rationale

A controlled service topology provides separation of responsibilities without introducing unnecessary deployment complexity.

It also provides a defined foundation for tenant isolation, security boundaries, service monitoring, and operational ownership.

### 7.5 Consequences

- Each service requires a defined responsibility and interface.
- Cross-service operations require explicit communication and failure-handling policies.
- Additional deployables require architecture review and approval.
- Service ownership and deployment responsibilities must be documented.

### 7.6 Dependencies

- ADR-002
- ADR-005
- ADR-006
- ADR-007
- ADR-013

### 7.7 Acceptance Evidence Required

- Architecture review.
- Service-boundary validation.
- Deployment topology review.
- Confirmation of service ownership.
- Project Owner approval.

---

## 8. ADR-002 — Frontend Hosting and Runtime Architecture

**Status:** Proposed

**Decision area:** Frontend hosting, runtime, and deployment.

### 8.1 Context

The platform requires multiple frontend applications with independent domains, user experiences, and deployment requirements.

The proposed technology baseline includes Vercel for frontend hosting and Google Cloud infrastructure for backend services.

Hosting decisions must distinguish CDN and edge caching from actual application execution.

### 8.2 Decision Statement

Vercel is a proposed frontend hosting option for the five frontend applications.

The platform must not assume that all application logic runs at the Edge.

Runtime selection must be made according to application requirements, including:

- Server-side rendering.
- Static generation.
- Node.js or supported serverless execution.
- Edge middleware and caching where appropriate.
- Long-running background processing.
- Secure access to backend APIs.

Long-running and resource-intensive workflows must be executed in appropriate backend workers rather than relying on frontend hosting runtime limits.

### 8.3 Alternatives Considered

- Vercel for all frontend applications.
- Google Cloud hosting for frontend applications.
- A hybrid hosting architecture.
- Self-hosted frontend infrastructure.

### 8.4 Rationale

A managed frontend platform may simplify deployment and delivery, but its runtime constraints and ingress security responsibilities must be understood.

### 8.5 Consequences

- Runtime limitations must be documented.
- Frontend and API ingress security must be assessed separately.
- Cloud Armor must not be assumed to protect every Vercel-hosted frontend ingress automatically.
- Webhooks, WebSockets, server-sent events, and internal service endpoints require explicit security review.
- Long-running jobs require durable backend execution.

### 8.6 Dependencies

- ADR-001
- ADR-005
- ADR-010

### 8.7 Acceptance Evidence Required

- Hosting and runtime evaluation.
- Deployment proof of concept.
- Security and ingress review.
- Cost and availability assessment.
- Project Owner approval.

---

## 9. ADR-003 — Backend Technology and Version Baseline

**Status:** Proposed

**Decision area:** Backend frameworks, programming language, and dependency versions.

### 9.1 Context

The backend requires a maintainable technology baseline for API development, database access, validation, workflow integration, and service operations.

The current architecture documentation identifies Python and FastAPI as proposed backend technologies.

The version baseline must remain consistent across the Technology Stack, deployment, and implementation documents.

### 9.2 Decision Statement

Python and FastAPI are proposed as the primary backend development technologies.

SQLAlchemy is proposed for database interaction, with Alembic for controlled database schema migration management.

The exact versions must be selected from supported, compatible releases and pinned in the relevant dependency and lock files before implementation.

The following are proposed technology components:

- Python.
- FastAPI.
- SQLAlchemy.
- Alembic.
- PostgreSQL.
- Pydantic.
- Redis where justified.
- Temporal as a workflow-orchestration candidate.

Specific version numbers must be maintained in the Technology Stack document and validated against compatibility, support, and security requirements.

### 9.3 Alternatives Considered

- Python with FastAPI.
- Python with Django.
- TypeScript-based backend frameworks.
- A mixed-language backend.

### 9.4 Rationale

Python and FastAPI provide a suitable candidate foundation for API services and AI-oriented integration.

SQLAlchemy and Alembic provide a structured approach to data access and schema evolution.

### 9.5 Consequences

- Dependencies must be pinned and reproducible.
- Runtime and library compatibility must be tested.
- Security and support status must be monitored.
- Lockfiles must be maintained.
- Type annotations do not replace runtime validation.
- API contracts and generated types must be tested for compatibility.
- Version changes require controlled review.

### 9.6 Dependencies

- ADR-001
- ADR-005
- ADR-007
- ADR-012

### 9.7 Acceptance Evidence Required

- Compatibility matrix.
- Dependency and security review.
- API performance tests.
- Database integration tests.
- Technology Stack consistency review.
- Project Owner approval.

---

## 10. ADR-004 — Frontend Application Architecture

**Status:** Proposed

**Decision area:** Frontend frameworks, state management, and application organisation.

### 10.1 Context

The platform requires multiple frontend applications with a consistent design system and reliable communication with backend services.

The architecture must distinguish transient user-interface state from authoritative server-side business state.

### 10.2 Decision Statement

The proposed frontend baseline uses a modern TypeScript-based web application architecture.

The technology candidates include:

- React.
- Next.js.
- TypeScript.
- Zustand for selected client-side interface state.
- TanStack Query for server-state retrieval and caching.
- A shared design system and reusable component library.

The final versions and application-specific deployment configurations remain subject to compatibility and performance validation.

### 10.3 State Ownership

The architecture must distinguish:

- Local interface state.
- Server-managed application data.
- Durable business records.
- Workflow execution state.
- Authentication and authorisation state.

Zustand must not become the authoritative source of financial, tenant, approval, or workflow state.

TanStack Query caching must not be treated as a substitute for backend authorisation or durable storage.

The backend and workflow engine remain authoritative for business workflow transitions.

### 10.4 Real-Time Communication

Server-sent events or WebSockets may be used where appropriate.

The implementation must support:

- Reconnection.
- Event replay where supported.
- State resynchronisation.
- Authorisation checks.
- Tenant isolation.
- Durable recovery through backend records.

### 10.5 Alternatives Considered

- React and Next.js.
- Other TypeScript frontend frameworks.
- Separate frontend implementations for each application.
- A shared frontend codebase with application-specific deployments.

### 10.6 Consequences

- Shared components require version and compatibility management.
- Frontend state must not bypass backend authorisation.
- Real-time updates require reconnection and recovery handling.
- Accessibility and responsive design must be validated.

### 10.7 Dependencies

- ADR-001
- ADR-002
- ADR-005

### 10.8 Acceptance Evidence Required

- Frontend architecture proof of concept.
- Accessibility testing.
- Performance testing.
- State-management review.
- Project Owner approval.

---

## 11. ADR-005 — API Design and Service Communication

**Status:** Proposed

**Decision area:** API contracts and service-to-service communication.

### 11.1 Context

The platform's frontend applications, backend services, and agents require reliable communication contracts.

Inconsistent interfaces can cause integration failures, security weaknesses, and difficult maintenance.

### 11.2 Decision Statement

The proposed architecture uses versioned API contracts with documented request, response, error, and authorisation behaviour.

HTTP APIs are proposed for synchronous request-response interactions.

Asynchronous messaging and durable workflow orchestration may be used for long-running or event-driven processes.

OpenAPI specifications and generated client types are proposed where appropriate.

### 11.3 Contract Requirements

API contracts should define:

- Endpoint and version.
- Authentication requirements.
- Authorisation requirements.
- Tenant context.
- Request schema.
- Response schema.
- Error model.
- Idempotency requirements.
- Rate limits.
- Timeout expectations.
- Audit requirements.
- Deprecation policy.

Runtime validation must be enforced at service boundaries.

TypeScript types or generated client declarations do not independently guarantee that runtime payloads conform to the expected schema.

### 11.4 Alternatives Considered

- REST-oriented HTTP APIs.
- GraphQL.
- gRPC.
- Event-driven communication.
- A combination of synchronous and asynchronous interfaces.

### 11.5 Rationale

A documented contract approach provides clear integration boundaries while allowing different communication mechanisms to be used where justified.

### 11.6 Consequences

- API changes require version and compatibility review.
- Contract tests must be maintained.
- Authentication and tenant checks must be enforced server-side.
- Service-to-service calls require identity and authorisation.
- Retries and idempotency must be designed explicitly.

### 11.7 Dependencies

- ADR-001
- ADR-003
- ADR-006
- ADR-012

### 11.8 Acceptance Evidence Required

- API contract examples.
- OpenAPI validation.
- Contract-test results.
- Security review.
- Project Owner approval.

---

## 12. ADR-006 — API Gateway, AI Gateway, and Model Routing

**Status:** Proposed

**Decision area:** Request routing, model routing, and gateway responsibility.

### 12.1 Context

The platform requires a public API entry point and a controlled capability for routing AI requests to suitable model providers.

These responsibilities must be distinguished to prevent duplicate infrastructure and unclear service ownership.

### 12.2 Decision Statement

The proposed public API entry point is the independently deployable `api-gateway`.

The proposed AI model-routing capability is a logical capability within the approved architecture and must not automatically create an additional independently deployed service.

The `multimodal-service` remains responsible for multimodal processing capabilities.

The six deployable backend service units remain:

1. `api-gateway`
2. `agent-orchestrator`
3. `multimodal-service`
4. `sandbox-runner`
5. `billing-ledger`
6. `adtech-service`

The identity provider is a separate identity infrastructure component and is not the API Gateway.

### 12.3 Responsibility Boundaries

**API Gateway:**
- Public API entry point.
- Request validation and routing.
- Token validation.
- Rate limiting.
- Request-level policy enforcement.
- Request correlation and observability.

**AI model-routing capability:**
- Model capability selection.
- Provider routing.
- Model configuration.
- Fallback and timeout policies.
- Model-specific telemetry.
- Version and cost tracking.

**Multimodal service:**
- Image, audio, video, and document processing.
- Media-specific validation.
- Multimodal processing workflows.
- Controlled interaction with relevant AI capabilities.

### 12.4 Redis and Semantic Caching

Redis may be evaluated for caching where justified.

A semantic cache must not return data across tenant boundaries or expose sensitive information.

Any semantic caching design must address:

- Tenant-aware access control.
- Data classification.
- Sensitive-content exclusion.
- Cache-key design.
- Invalidation.
- Retention.
- Model and embedding versioning.
- Auditability.
- Leakage testing.

### 12.5 Alternatives Considered

- One combined API and AI Gateway.
- Separate API and AI Gateway deployables.
- AI routing embedded within the orchestrator.
- AI routing as a logical capability within an existing approved deployable.

### 12.6 Rationale

Separating responsibilities conceptually while controlling the number of deployables reduces architectural ambiguity and deployment overhead.

### 12.7 Consequences

- The exact internal placement of model-routing logic must be confirmed.
- No seventh deployable service is authorised by this ADR.
- Gateway and identity-provider responsibilities remain distinct.
- AI routing must not bypass service authorisation.
- Model routing must be observable and version-controlled.

### 12.8 Dependencies

- ADR-001
- ADR-003
- ADR-005
- ADR-013

### 12.9 Acceptance Evidence Required

- Service-boundary review.
- Model-routing proof of concept.
- Tenant-aware cache security tests.
- Performance and cost evaluation.
- Project Owner approval.

---

## 13. ADR-007 — Database Architecture and Tenant Isolation

**Status:** Proposed

**Decision area:** Relational database, vector search, and tenant isolation.

### 13.1 Context

The platform requires reliable persistence for users, organisations, projects, workflows, transactions, audit records, and AI-related metadata.

Tenant isolation is a foundational security requirement.

### 13.2 Decision Statement

PostgreSQL is proposed as the primary relational database.

SQLAlchemy and Alembic are proposed for database access and schema migration management.

pgvector is proposed for vector storage and similarity search, subject to a proof of concept.

The proposed embedding dimension of 3072 remains a pending technical decision and must be validated against selected embedding models, index support, performance, and storage requirements.

### 13.3 Tenant Isolation Requirements

The architecture must consider:

- PostgreSQL Row-Level Security.
- Restricted database roles.
- FORCE ROW LEVEL SECURITY where appropriate.
- Transaction-scoped tenant context.
- Tenant-aware foreign keys.
- Connection-pool isolation.
- Background-worker tenant context.
- Privileged-role restrictions.
- Adversarial tenant-isolation testing.

The presence of `app.current_tenant_id` alone does not establish tenant security.

Tenant isolation must also extend to:

- Object storage.
- Git operations.
- Sandbox execution.
- Workflow state.
- Caches.
- Logs and audit records.

### 13.4 Vector Database Requirements

The pgvector proof of concept must evaluate:

- Supported dimensions.
- Exact and approximate search.
- Index selection.
- Recall and retrieval quality.
- Query latency.
- Storage overhead.
- Write performance.
- Concurrent workloads.
- Tenant filtering.
- Re-embedding and model-version migration.

### 13.5 Alternatives Considered

- PostgreSQL with pgvector.
- PostgreSQL with an external vector database.
- A dedicated vector database.
- A managed relational and vector storage combination.

### 13.6 Consequences

- Database schema changes require controlled migrations.
- Tenant context must be securely propagated.
- Vector model changes may require re-embedding.
- Database performance and index behaviour require measurement.
- Financial and audit records need stronger retention and integrity protections.

### 13.7 Dependencies

- ADR-003
- ADR-006
- ADR-008
- ADR-009

### 13.8 Acceptance Evidence Required

- PostgreSQL and RLS proof of concept.
- Adversarial tenant-isolation tests.
- pgvector benchmark results.
- Backup and restoration tests.
- Project Owner approval.

---

## 14. ADR-008 — Object Storage and File Management

**Status:** Proposed

**Decision area:** Storage of uploads, documents, media, and generated assets.

### 14.1 Context

The platform must support potentially large files, including images, audio, video, documents, source assets, and generated outputs.

Storing all large binary assets directly in relational database records may create unnecessary database overhead.

### 14.2 Decision Statement

Object storage is proposed for large binary assets.

PostgreSQL remains responsible for metadata, ownership, references, workflow state, and transactional records.

Git remains responsible for version-controlled source-code history and related repository content.

### 14.3 Storage Requirements

Object storage must support:

- Tenant-aware access control.
- Encryption at rest and in transit.
- Versioning where required.
- Malware quarantine and scanning.
- Signed URL restrictions.
- Retention and deletion policies.
- Backup and recovery.
- Audit logging.
- Access revocation.
- Data lifecycle management.

New uploads must be treated as pending or quarantined until the required validation and security checks are complete.

### 14.4 Alternatives Considered

- Relational database binary storage.
- Object storage.
- Distributed file storage.
- A hybrid database and object-storage model.

### 14.5 Rationale

A hybrid model separates transactional metadata from large binary objects while supporting scalable file handling.

### 14.6 Consequences

- Object references must be protected by tenant-aware authorisation.
- Signed URLs must be short-lived and appropriately scoped.
- Deletion must consider replicas, backups, retention, and legal holds.
- Object storage recovery must be included in platform disaster recovery.

### 14.7 Dependencies

- ADR-001
- ADR-007
- ADR-010

### 14.8 Acceptance Evidence Required

- Storage architecture review.
- Tenant access-control tests.
- Malware quarantine and scanning proof of concept.
- Backup and restoration tests.
- Project Owner approval.

---

## 15. ADR-009 — Financial Ledger Integrity and Posting Controls

**Status:** Proposed

**Decision area:** Financial authority, ledger posting, and transaction integrity.

### 15.1 Context

The platform may process payments, subscriptions, usage charges, credits, refunds, and other financial events.

Financial records must remain consistent, traceable, and protected from unauthorised changes.

AI agents must not independently establish financial truth or modify balances without deterministic controls.

### 15.2 Decision Statement

The `billing-ledger` service is proposed as the deterministic financial authority.

Agent21 may provide advisory, monitoring, and coordination capabilities but must not become the authoritative ledger or independently post financial transactions.

Financial posting must be performed through controlled, deterministic service logic.

### 15.3 Ledger Requirements

The proposed ledger design must support:

- Atomic double-entry accounting.
- Transaction-level currency consistency.
- Controlled draft-to-posted transitions.
- Immutable posted entries.
- Compensating entries for corrections.
- Provider-scoped idempotency.
- Reconciliation against payment providers.
- Authorised adjustments.
- Audit logging.
- Protection against unauthorised balance mutation.

Financial history must not be destroyed through uncontrolled cascading deletes.

### 15.4 Posting Integrity

A financial transaction must not be considered posted merely because an AI agent, frontend application, or external provider reports success.

The authoritative posting process must validate the transaction and record the appropriate balanced entries atomically.

A database trigger, application service, or other enforcement mechanism must be selected only after its behaviour, transaction boundaries, failure handling, and interaction with authorised posting workflows have been clearly defined.

Any proposed database trigger must not contradict the approved application-level posting process or create an uncontrolled second posting authority.

### 15.5 Alternatives Considered

- Agent-controlled financial records.
- Direct balance mutation.
- Deterministic double-entry ledger.
- External financial ledger with internal reconciliation.

### 15.6 Rationale

Financial integrity requires deterministic, auditable controls that do not depend on probabilistic model behaviour.

### 15.7 Consequences

- Agent21 remains advisory and coordinative.
- `billing-ledger` owns authoritative financial state.
- External payment status must be verified.
- Idempotency and reconciliation are mandatory design considerations.
- Posted entries require controlled correction rather than silent modification.
- Financial records require explicit retention and access policies.

### 15.8 Dependencies

- ADR-007
- ADR-011
- ADR-012
- ADR-013

### 15.9 Acceptance Evidence Required

- Ledger data-model review.
- Atomic posting tests.
- Duplicate transaction and idempotency tests.
- Reconciliation proof of concept.
- Authorisation and audit tests.
- Project Owner and designated finance authority approval.

---

## 16. ADR-010 — Secure Sandbox Execution

**Status:** Proposed

**Decision area:** Isolated execution of code and potentially untrusted workloads.

### 16.1 Context

The platform may execute code or other user-controlled workloads through its sandbox capability.

Untrusted execution must be isolated from the platform's infrastructure, other tenants, credentials, and sensitive data.

### 16.2 Decision Statement

A hardened sandbox execution architecture is proposed.

gVisor within an appropriately configured Kubernetes environment is a candidate technology, subject to proof-of-concept evaluation.

MicroVM-based isolation must remain an alternative for comparison.

Neither gVisor nor container isolation should be described as escape-proof.

### 16.3 Security Requirements

The sandbox must address:

- Non-root execution.
- Restricted Linux capabilities.
- Filesystem isolation.
- CPU and memory limits.
- Process and execution-time limits.
- Default-deny network egress.
- DNS and IPv6 controls.
- Cloud metadata access restrictions.
- Short-lived credentials.
- Tenant isolation.
- Secure temporary-file handling.
- Environment cleanup.
- Logging and auditability.
- Escape and adversarial testing.

### 16.4 Alternatives Considered

- Standard containers.
- gVisor.
- MicroVM-based isolation.
- Dedicated virtual machines.
- External isolated execution services.

### 16.5 Rationale

The sandbox requires a deliberate balance of isolation strength, operational complexity, performance, and cost.

### 16.6 Consequences

- A proof of concept is required before selection.
- Security testing must include realistic escape attempts.
- Network and metadata restrictions must be enforced outside agent instructions.
- Sandbox capacity and cleanup require operational monitoring.
- A microVM alternative must be evaluated where the threat model requires stronger isolation.

### 16.7 Dependencies

- ADR-001
- ADR-002
- ADR-008

### 16.8 Acceptance Evidence Required

- Threat model.
- Isolation proof of concept.
- Escape and adversarial test results.
- Network-egress verification.
- Resource-limit testing.
- Cost and performance assessment.
- Project Owner approval.

---

## 17. ADR-011 — Human Approval Gates and Protected Operations

**Status:** Proposed

**Decision area:** Human approvals, production deployment, and protected GitHub operations.

### 17.1 Context

The platform requires controlled approval for sensitive actions.

Approval mechanisms must distinguish production deployment authority from protected source-code and repository operations.

Technical permissions alone must not be treated as proof of human approval.

### 17.2 Decision Statement

GATE-03 and GATE-04 are separate approval requirements.

**GATE-03 — Production Deployment Approval**

Controls authorisation to perform a designated production deployment.

**GATE-04 — Protected GitHub Operations Approval**

Controls authorisation to perform designated protected GitHub operations.

The two gates must remain independent and must not be treated as interchangeable.

HD-08 has approved the six-gate framework. GATE-01 governs material product and architecture changes; GATE-02 governs financial and resource commitments without establishing spending thresholds or delegated limits; GATE-05 governs destructive database operations and migrations; and GATE-06 governs consequential external integrations and live-account actions. The Project Owner is the sole approval authority for all six gates during the initial governance phase. Specialists may assess and advise but do not approve on the Project Owner's behalf. The common enforcement requirements, action/context binding, expiry, revocation, audit evidence, fail-closed behavior and independent-gate rules are recorded in the Security Architecture and Architecture Overview.

### 17.3 Approval-Binding Requirements

Where applicable, an approval must be bound to:

- The specific action.
- The project or tenant.
- The artifact or commit digest.
- The target environment.
- The authorised approver.
- The approval scope.
- The approval time.
- The expiry.
- The revocation state.
- The audit record.

Material changes to the approved artifact or scope must invalidate the approval where the change affects the approved action.

Single-use and replay-resistant approval identifiers should be used where appropriate.

### 17.4 Alternatives Considered

- One universal approval gate.
- Separate deployment and repository-operation gates.
- Role-based permission without explicit approval records.
- Explicit action-bound approval records.

### 17.5 Rationale

Production deployment and protected repository operations create different risks and require distinct authorisation boundaries.

### 17.6 Consequences

- GATE-03 approval does not automatically authorise GATE-04 operations.
- GATE-04 approval does not automatically authorise GATE-03 deployment.
- Owner or Administrator roles do not automatically grant every approval authority.
- Approval evidence must be auditable.
- The final approval-gate framework requires explicit human approval.

### 17.7 Dependencies

- ADR-001
- ADR-009
- ADR-014

### 17.8 Acceptance Evidence Required

- Approval-gate definitions.
- Role and authority matrix.
- Replay-resistance tests.
- Artifact-binding tests.
- Audit and revocation tests.
- Project Owner approval.

---

## 18. ADR-012 — Messaging and Event Communication

**Status:** Proposed

**Decision area:** Event communication, asynchronous messaging, and workflow durability.

### 18.1 Context

The platform requires communication between services and agents for status updates, notifications, asynchronous processing, and workflow coordination.

Not every communication mechanism provides durable business-state storage.

### 18.2 Decision Statement

Redis Pub/Sub may be used as an ephemeral messaging or notification mechanism where appropriate.

It must not be treated as the authoritative durable record of a business event, financial transaction, workflow state, or approval.

Temporal is the selected candidate for durable workflow orchestration, with Temporal Cloud approved as the preferred initial hosting approach subject to POC-06 and due diligence; self-hosted Temporal remains a future alternative.

### 18.3 Messaging Responsibilities

**Redis Pub/Sub:**
- Ephemeral notifications.
- Non-authoritative event distribution.
- Suitable low-latency messaging use cases.

**Durable workflow and business records:**
- Persisted in their authoritative systems.
- Recoverable after process or service failure.
- Auditable where required.
- Reconciled with external side effects.

### 18.4 Reliability Requirements

The architecture must assume at-least-once execution where applicable.

It must not claim exactly-once external side effects merely because a workflow engine or message broker is used.

The design must address:

- Idempotency.
- Durable state.
- Bounded retries.
- Timeouts.
- Cancellation.
- Compensation.
- Dead-letter handling.
- Manual recovery.
- Outbox and inbox patterns where appropriate.
- Reconciliation of external provider state.

### 18.5 Alternatives Considered

- Redis Pub/Sub alone.
- Durable message broker.
- Temporal workflow orchestration.
- Combination of durable workflows and ephemeral notifications.

### 18.6 Rationale

Ephemeral communication and durable workflow execution serve different purposes. Separating them reduces the risk of losing authoritative business state.

### 18.7 Consequences

- Redis Pub/Sub cannot be the sole record of a critical business event.
- Workflow state must be durable and recoverable.
- Temporal Cloud is the approved preferred initial hosting approach, subject to POC-06 and due diligence; self-hosted Temporal remains a future alternative. The approval does not authorise a subscription, contract, production deployment, or region selection.
- Messaging delivery and retry semantics must be documented.
- External side effects require idempotency and reconciliation.

### 18.8 Dependencies

- ADR-003
- ADR-005
- ADR-007
- ADR-009

### 18.9 Acceptance Evidence Required

- Workflow-engine proof of concept.
- Failure and retry tests.
- Duplicate-delivery tests.
- Outbox/inbox evaluation.
- Backup and restoration tests.
- Project Owner approval.

---

## 19. ADR-013 — Agent Ecosystem and Module Organisation

**Status:** Proposed

**Decision area:** AI agent organisation, permissions, and service ownership.

### 19.1 Context

The platform includes a multi-agent ecosystem with specialised responsibilities.

The architecture must distinguish logical agent modules from independently deployable services.

AI agents must operate under permission-controlled boundaries and must not assume deterministic authority over sensitive business functions.

### 19.2 Decision Statement

The platform's 23 agents are logical modules organised into five agent modules or groupings.

They are not 23 independently deployed microservices.

Agent execution and coordination are managed through the approved service architecture, particularly `agent-orchestrator` and relevant capability services.

### 19.3 Agent Responsibility Boundaries

Agents may:

- Interpret requests.
- Analyse information.
- Recommend actions.
- Coordinate permitted workflows.
- Invoke authorised tools.
- Report progress and results.
- Request human approval where required.

Agents must not independently override deterministic controls governing:

- Authentication.
- Authorisation.
- Tenant isolation.
- Financial posting.
- Account balances.
- Approval gates.
- Workflow state transitions.
- Audit integrity.
- Production deployment.
- Protected GitHub operations.

### 19.4 Special Responsibility Boundaries

**Agent21 — Financial Advisory and Coordination**

Agent21 may provide financial monitoring, recommendations, and coordination.

The deterministic `billing-ledger` service remains the authoritative financial system.

**Agent22 — Multimodal Capabilities**

Agent22 uses the `multimodal-service` for authorised multimodal processing.

**Agent23 — Advertising Technology**

Agent23 uses the `adtech-service` and must not access private prompts, source code, uploads, credentials, or confidential user activity.

Advertising access must be limited to explicitly authorised public or appropriately aggregated data.

### 19.5 Alternatives Considered

- Twenty-three independently deployed agent services.
- One unrestricted general-purpose agent.
- Logical agent modules coordinated through controlled services.
- A mixture of dedicated agent services and shared orchestration.

### 19.6 Rationale

Logical modules provide specialisation without unnecessary service proliferation.

Deterministic service enforcement preserves accountability and reduces the risks of unauthorised agent actions.

### 19.7 Consequences

- Agent permissions must be explicitly defined.
- Tool calls require server-side authorisation.
- Agent identity and tenant context must be controlled.
- Agent outputs must not be treated as trusted instructions by default.
- Agent evaluations and audit records must be maintained.
- The five-module mapping must remain consistent with the Agent Ecosystem document.

### 19.8 Dependencies

- ADR-001
- ADR-005
- ADR-006
- ADR-009
- ADR-011
- ADR-012

### 19.9 Acceptance Evidence Required

- Agent-to-module mapping.
- Agent-to-service responsibility matrix.
- Permission and tool-access matrix.
- Prompt-injection and tool-authorisation tests.
- Financial and advertising boundary tests.
- Project Owner approval.

---

## 20. ADR-014 — Git Branching and Repository Workflow

**Status:** Proposed

**Decision area:** Git branch strategy and protected repository operations.

### 20.1 Context

The Worklexx AI Software Factory requires a controlled Git workflow that supports development, review, testing, release management, and protected operations.

The current repository has an existing `main` branch.

HD-REP-03 approved trunk-based development using protected `main` and short-lived branches on 2026-11-20; actual configuration and implementation remain separately controlled.

### 20.2 Decision Statement

Trunk-based development using protected `main` and short-lived branches is the approved architectural direction under HD-REP-03; configuration and implementation are not authorised by that decision.

The strategy must be reviewed against the existing repository structure and actual engineering workflow before adoption.

The existence of the `main` branch must be preserved as the current repository baseline.

No branch creation, deletion, renaming, protection-rule modification, commit, merge, or push is authorised by this ADR.

### 20.3 Proposed Branch Strategy

The proposed five-tier structure is:

1. `main` — protected release and production baseline.
2. `develop` — integration branch for approved development work.
3. Feature branches — isolated implementation work.
4. Release branches — controlled release preparation.
5. Hotfix branches — urgent corrections to protected release versions.

Exact naming conventions, branch protection rules, merge policies, and release procedures remain subject to approval.

### 20.4 Alternatives Considered

- Existing `main`-only workflow.
- GitHub Flow.
- Git Flow.
- A simplified feature-branch workflow.
- The proposed five-tier strategy.

### 20.5 Rationale

A structured branch strategy may improve traceability, review, and release control.

However, additional branch layers create process overhead and should be adopted only when justified by the project's delivery and governance requirements.

### 20.6 Consequences

- The current `main` branch remains unchanged unless explicitly authorised.
- The five-tier strategy is not yet adopted.
- The relationship between `develop`, feature, release, and hotfix branches must be defined.
- Branch protection rules require explicit approval.
- Pull-request and review requirements must be documented.
- Protected GitHub operations remain subject to GATE-04.
- Production deployment remains subject to GATE-03.
- Approval for one gate does not imply approval for the other.

### 20.7 Dependencies

- ADR-001
- ADR-011
- Repository Structure document.
- Development Roadmap document.
- Security Architecture document.

### 20.8 Acceptance Evidence Required

- Review of the current repository state.
- Branch-strategy comparison.
- Branch protection design.
- Pull-request and review policy.
- Release and hotfix workflow.
- Explicit Project Owner approval.

---

## 21. Human Decisions Required

The following decisions require explicit human resolution.

| Decision ID | Decision Required | Related ADRs | Status |
|---|---|---|---|
| HD-01 | Select the managed or internally operated identity-provider approach | ADR-001, ADR-005, ADR-011 | **Approved — managed approach** |
| HD-02 | Select Temporal Cloud or self-hosted deployment | ADR-003, ADR-012 | **Approved — Temporal Cloud preferred initial approach (conditional)** |
| HD-03 | Approve primary and disaster-recovery regions | ADR-002, ADR-007, ADR-008, ADR-012 | **Approved — AWS primary Cape Town (`af-south-1`), Ireland DR (`eu-west-1`), and Temporal Cloud Ireland (`aws-eu-west-1`), architectural direction only, subject to validation (2026-11-19)** |
| HD-04 | Confirm the six-deployable backend service topology | ADR-001, ADR-006, ADR-013 | **Approved — retain six logical deployables, physical topology validation remains pending (2026-11-19)** |
| HD-05 | Confirm the initial vector-storage approach and model-specific embedding-dimension policy | ADR-007 | **Approved — PostgreSQL with pgvector preferred initially; dimensions remain model/use-case specific; POC-05 required (2026-11-19)** |
| HD-06 | Approve platform RPO and RTO targets | ADR-007, ADR-008, ADR-012 | **Approved — tiered architectural recovery objectives; POC-15 and operational validation required (2026-11-19)** |
| HD-07 | Designate risk acceptance authority and approval delegation | ADR-011 | **Approved — Project Owner is sole risk acceptance authority during the initial governance phase; no delegation (2026-11-19)** |
| HD-08 | Define GATE-01 through GATE-06 and their approval requirements | ADR-011 | **Approved — six-gate human approval framework; Project Owner sole approval authority during initial governance phase (2026-11-19)** |
| HD-REP-06 | Service-owned database schema and migration governance | ADR-003, ADR-007 | **Approved — independent schema ownership and migration histories for all six deployable services; implementation and execution remain separately controlled (2026-11-20)** |
| HD-REP-07 | Repository backup, disaster recovery and restoration governance | ADR-014, ADR-011 | **Approved — layered, provider-independent backup and recovery architecture; implementation and recovery execution remain separately controlled (2026-11-20)** |
| HD-REP-08 | Repository automation, build integrity and software supply-chain security governance | ADR-014, ADR-011 | **Approved — least-privilege, verifiable automation and trusted build/release controls; implementation remains separately controlled (2026-11-20)** |

### HD-01 — Managed Identity-Provider Approach

- **Decision:** Approved — use a managed identity-provider approach rather than internally operating identity infrastructure.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-19.
- **Rationale:** Reduce the operational and security-maintenance burden of operating identity infrastructure; use established provider capabilities for authentication, MFA, account recovery, federation, and session security; retain Worklexx ownership of application-level authorisation and tenant isolation.
- **Conditions:** Keep the integration provider-independent; do not infer application permissions from successful authentication; services must enforce resource-level authorisation and tenant boundaries; sensitive operations remain subject to their applicable approval gates.
- **Scope limitation:** This decision does not select a specific identity-provider vendor, contract, hosting region, or deployment configuration. Those details require separate evaluation and approval.

HD-02 — Temporal Cloud Preferred Initial Approach

- **Decision:** Approved — use Temporal Cloud as the preferred initial workflow-orchestration hosting approach.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-19.
- **Rationale:** Prefer a managed workflow service initially to reduce the operational burden of running and maintaining the orchestration control plane, subject to validation that the managed service meets Worklexx requirements.
- **Conditions:** Complete POC-06 and due diligence covering total cost of ownership, operational support, availability and service commitments, data residency, security, network architecture, backup and restoration, upgrades, disaster recovery, and vendor dependency. Record evidence and material limitations before implementation planning relies on this approach.
- **Alternative retained:** Self-hosted Temporal remains a future alternative if validation, commercial terms, regulatory/data-residency constraints, or operational requirements make it preferable.
- **Scope limitation:** This is an architectural preference only. It does not authorise a Temporal Cloud subscription, contract, payment, production deployment, account configuration, region selection, or final production service commitment. Those require separate evaluation and explicit approval.

### HD-06 — Tiered Recovery Point and Recovery Time Objectives

- **Decision:** Approved — adopt the tiered RPO and RTO targets below as platform architectural recovery objectives.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-19.
- **Approved objectives:**

  | Workload / data class | RPO | RTO |
  |---|---:|---:|
  | Financial ledger, payment and credit records | ≤ 5 minutes | ≤ 1 hour |
  | Core platform database and tenant/business records | ≤ 15 minutes | ≤ 2 hours |
  | Durable agent and workflow state | ≤ 5 minutes | ≤ 1 hour |
  | Core API and essential user access | Not applicable to service availability itself; persistent state follows its data-class RPO | ≤ 1 hour |
  | Multimodal processing and sandbox workloads | ≤ 1 hour for recoverable workload state; original uploads and completed customer artifacts require separately classified protection | ≤ 4 hours |
  | Analytics, reporting and non-critical derived data | ≤ 24 hours | ≤ 24 hours |

- **Conditions:** These values are planning objectives, not verified capabilities, contractual service levels, or availability guarantees. POC-15 must measure actual recovery performance and validate full-platform restoration and regional recovery. Recovery scope must include PostgreSQL and pgvector, financial records, Temporal workflow state, object storage, Git repositories and build artifacts, identity-provider configuration, KMS and secrets, DNS, infrastructure configuration, and required external dependencies. Financial recovery must preserve ledger integrity and reconcile against payment-provider and other authoritative records, including idempotency and duplicate-side-effect controls. Backup design must address encryption, restricted access, retention, geographic separation, integrity verification, restoration testing, and immutability where appropriate. Restored data must be reconciled against valid deletion requests, anonymisation, legal holds, revoked credentials, access changes, and tenant deactivation before normal access is restored.
- **Validation:** POC-15 must document test environment, recovery scenarios, dependency ordering, measured data-loss window, measured restoration time, integrity and reconciliation results, limitations, and remediation actions. Targets must be reviewed if evidence shows they cannot be achieved safely or economically.
- **Scope limitation:** This decision records architectural objectives only. It does not approve backup frequency or retention configuration, a replication mechanism, database or storage configuration, infrastructure provisioning, subscriptions, production failover, a production recovery commitment, or Phase 1 implementation. Those require separate validation and authorization.

### HD-08 — Six-Gate Human Approval and Enforcement Framework

- **Decision:** Approved — adopt six independent, human-in-the-loop approval gates covering product/architecture changes (GATE-01), financial/resource commitments (GATE-02), production deployment (GATE-03), protected GitHub operations (GATE-04), destructive database operations and migrations (GATE-05), and consequential external integrations/live-account actions (GATE-06).
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-19.
- **Approval authority:** During the initial governance phase, the Project Owner is the sole approval authority for all six gates. No gate approval authority is delegated. Specialists may provide assessment, evidence review and recommendations but do not approve on the Project Owner's behalf.
- **GATE-01:** Applies to material changes to product scope, platform architecture, service boundaries, security design, technology choices or approved architectural decisions. Material security, legal, privacy or infrastructure changes require relevant specialist assessment.
- **GATE-02:** Applies to cloud/infrastructure commitments, AI model/API commitments, paid licences, vendor contracts/recurring subscriptions and material budget increases. No spending thresholds, currency limits or delegated financial limits are established by this decision.
- **GATE-03:** Applies to deployment of a specific approved artifact to a specific production environment. Bind approval to project, tenant where applicable, environment, target, artifact/commit digest, deployment action, validation evidence and rollback plan.
- **GATE-04:** Applies to designated protected GitHub operations, including protected-branch changes, protected releases/tags and other explicitly restricted repository actions. Bind approval to repository, branch/protected resource, operation and relevant PR/commit/artifact. PR review and approval to execute a protected operation are distinct controls.
- **GATE-05:** Applies to irreversible destruction, invalidation or material transformation of persistent data or database structures, including destructive schema migrations, incompatible data transformations, bulk deletion/irreversible correction and production resets/restores that overwrite existing data. Require verified backups, impact analysis, execution plan and rollback/recovery strategy.
- **GATE-06:** Applies to external integrations or live-account actions with material financial, operational, customer, legal or security consequences, including live payments, production identity-provider activation, live customer notifications and consequential financial, insurance or logistics actions. Require provider due diligence, permission review, test evidence, data-protection assessment and rollback/suspension plan.
- **Common enforcement:** Require authenticated human approval, explicit decision and scope, binding to project/tenant/environment/resource/action and artifact or transaction context as applicable, timestamp, expiry, revocation state, supporting evidence and an auditable execution result. Approvals must be replay-resistant and invalidated or reassessed after material changes. The system must fail closed when approval is absent, invalid, expired, revoked or unverifiable.
- **No implied approval:** Silence, prior approvals, general project approval, technical permissions, administrator status or risk acceptance do not constitute gate approval. Gates are independent and cumulative where applicable. Approval of one gate does not satisfy another.
- **AI boundary:** AI agents may prepare requests and evidence but must not approve, impersonate a human approver or override deterministic enforcement.
- **Emergency handling:** Emergency procedures require separate documentation and approval and must not introduce undocumented bypasses.
- **Scope limitation:** This is an architectural governance decision only. It does not authorise implementation, spending, contracts, account activation, infrastructure provisioning, production deployment, protected operations, destructive database execution or Phase 1. Each applicable gate and separate operational authorization remains required.

### HD-07 — Project Owner-Led Risk Acceptance Authority

- **Decision:** Approved — the Project Owner is the sole risk acceptance authority during the initial Worklexx AI Software Factory governance phase. No delegated risk acceptance authority is introduced at this stage.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-19.
- **Delegation boundary:** Risk assessment, investigation, control ownership, mitigation execution, monitoring, and reporting may be delegated in writing. Such delegation does not confer authority to accept residual risk, approve exceptions, or authorise gated activities.
- **Risk-level treatment:** The Project Owner may accept documented Low (1–5) and Medium (6–11) residual risks subject to recorded controls, rationale, conditions, and review dates. High (12–19) residual-risk acceptance is reserved to the Project Owner and requires written justification and relevant independent specialist review. Critical (20–25) risks are not eligible for routine acceptance under this model; the affected activity must be stopped, suspended, or not started while the risk is escalated and addressed. Any exceptional governance route would require a separate explicit human decision and cannot waive mandatory legal, regulatory, security, or safety obligations.
- **Mandatory escalation:** Relevant specialist review is required regardless of numerical score for matters such as regulatory breach, unlawful processing or cross-border transfer, personal-data exposure, cross-tenant leakage, ledger corruption or unauthorised balance mutation, sandbox escape or production-credential compromise, privileged-access abuse, approval-control circumvention, material customer safety risk, or irreversible data loss.
- **Acceptance record:** Each acceptance must record the risk ID; inherent and residual assessment; implemented controls and evidence; affected stakeholders; alternatives; rationale; accepting person's identity and authority; decision date; expiry/review date; conditions, monitoring, and withdrawal triggers. Acceptance is time-limited and must be reassessed after material incidents, changes, or evidence of ineffective controls.
- **Separation of authority:** Risk acceptance is not activity authorisation or gate approval. It does not authorise or bypass Phase 1, production deployment, protected GitHub operations, database migrations, external integrations, financial commitments, or other controlled activities.
- **AI boundary:** AI agents may support assessment and recommendations but must not accept risk, approve exceptions, or impersonate a human approver.
- **Scope limitation:** This is a governance decision only. It does not establish delegation to any other person, approve an activity, waive a gate, or authorise Phase 1 or production operations.

### HD-05 — PostgreSQL and pgvector Vector-Storage Direction

- **Decision:** Approved — retain PostgreSQL with pgvector as the preferred initial vector-storage and similarity-search approach. Do not introduce a separate vector-database deployment at this stage.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-19.
- **Rationale:** Reuse the approved PostgreSQL platform direction and avoid introducing another independently operated database platform before workload evidence demonstrates a need.
- **Embedding dimensions:** Do not impose 3,072 dimensions as a platform-wide requirement. Select dimensions according to the chosen embedding model and use case. Record model/provider, model version, vector dimension, source version, tenant, access scope, and lifecycle metadata. Incompatible models or dimensions must not be mixed in a logical index without an explicitly validated compatibility strategy.
- **Conditions:** Complete POC-05 before implementation relies on the selected configuration. Evaluate supported PostgreSQL/pgvector versions, full-precision and half-precision options where relevant, exact and approximate search, index compatibility, recall and retrieval quality, query latency, index/storage/memory requirements, writes and deletes, concurrency, tenant and metadata filtering, re-embedding, backup/restore, and recovery. Test 3,072-dimensional workloads where a selected model requires them; do not assume half-precision retrieval is acceptable without quality measurements. Tenant isolation, authorization filtering, and deletion/access-revocation propagation are mandatory acceptance criteria.
- **Alternative retained:** A separately operated vector database may be reconsidered only if measured workload, scale, latency, recall, isolation, or operational requirements show that PostgreSQL/pgvector is insufficient, through a separate documented decision.
- **Scope limitation:** This is an architectural direction only. It does not approve a specific PostgreSQL or pgvector version, embedding provider/model, index configuration, database hosting arrangement, schema, migration, subscription, infrastructure provisioning, or production deployment. POC-05 and subsequent implementation approvals remain required.

All other human decisions remain subject to separate explicit resolution. Decisions must be recorded with the decision-maker, date, rationale, evidence, and any conditions.

## 22. ADR Approval and Change-Control Procedure

A new ADR or material ADR revision should follow this procedure:

1. Identify the architectural question.
2. Record the context and constraints.
3. Identify realistic alternatives.
4. Evaluate security, cost, performance, reliability, and maintainability.
5. Document the proposed decision.
6. Identify related ADRs and affected architecture documents.
7. Obtain the required human review and approval.
8. Record approval evidence and date.
9. Update the ADR status.
10. Update affected architecture documents through controlled change management.
11. Reassess dependent risks.
12. Retain the previous decision history.

A material change must not be silently applied to an Accepted ADR.

Where an earlier decision is replaced, the new ADR must identify the superseded decision and explain the migration implications.

## 23. ADR Relationship to Other Documents

This register must remain consistent with:

- `ARCHITECTURE_OVERVIEW.md`
- `SYSTEM_ARCHITECTURE.md`
- `TECHNOLOGY_STACK.md`
- `REPOSITORY_STRUCTURE.md`
- `AGENT_ECOSYSTEM.md`
- `SERVICE_BOUNDARIES.md`
- `DATABASE_ARCHITECTURE.md`
- `SECURITY_ARCHITECTURE.md`
- `DEPLOYMENT_ARCHITECTURE.md`
- `DEVELOPMENT_ROADMAP.md`
- `RISK_REGISTER.md`
- `PHASE_0_INSPECTION_REPORT.md`
- `TESTING_STRATEGY.md`
- `MONITORING_AND_OBSERVABILITY.md`
- `COST_AND_SCALABILITY.md`

Where an ADR conflicts with another architecture document, the conflict must be recorded and resolved through the authorised change-control process.

A proposed ADR does not override an existing approved decision.

## 24. Phase 0 Governance Limitations

This ADR Register records proposed architectural decisions and identifies decisions requiring formal approval.

It does not authorise:

- Phase 1 implementation.
- Creation or modification of Git branches.
- Commits, merges, or pushes.
- GitHub branch-protection changes.
- Database schema changes or migration execution.
- Cloud resource provisioning.
- External service integration.
- Financial transaction processing.
- Production deployment.
- Spending or contractual commitments.

An Accepted ADR establishes an architectural decision only within its approved scope. Separate operational, financial, security, repository, and deployment approvals may still be required.

## 25. Final Status

**Document ID:** WLX-ARCH-012.

**Version:** 1.0.

**Status:** Proposed — Phase 0.

**ADR coverage:** ADR-001 through ADR-014.

**Decision status:** Proposed pending authorised human review and approval.

**Human decisions:** HD-01 is approved as the managed identity-provider approach. HD-02 is approved as the conditional preferred initial Temporal Cloud approach. HD-03 is approved as the regional architecture direction, subject to legal, security, POC, and operational validations. HD-04 is approved as the six-logical-deployable topology, with physical deployment subject to validation. HD-05 is approved as the initial PostgreSQL/pgvector vector-storage direction with model- and use-case-specific dimensions, subject to POC-05 and the stated validations. HD-06 is approved as the tiered architectural recovery objectives, subject to POC-15 and operational validation. HD-07 is approved: the Project Owner is the sole risk acceptance authority during the initial governance phase, with no delegated risk acceptance authority; assessment and mitigation work may be delegated without transferring acceptance authority. HD-08 is approved as the six-gate human approval and enforcement framework, with the Project Owner as sole gate approval authority during the initial governance phase; specialist review is advisory and does not transfer approval authority.

**Repository status:** Existing `main` branch remains the baseline. HD-REP-03 approves trunk-based development with protected `main` and short-lived branches as architectural direction only; no branch-protection settings have been configured.

**Approval authority:** For risk acceptance, the Project Owner is the sole authority during the initial governance phase under HD-07; no delegation is authorised. The Project Owner is the sole approval authority for GATE-01 through GATE-06 during the initial governance phase under HD-08; no gate approval authority is delegated. Specialist assessment and recommendations do not transfer approval authority.

**Implementation authority:** This document does not authorise Phase 1 or any implementation, protected GitHub operation, or production deployment.

The ADR Register provides the traceable foundation for recording, reviewing, approving, and maintaining the architectural decisions of the Worklexx AI Software Factory.

## HD-03 — Approved Regional Architecture Direction (2026-11-19)

- **Cloud provider:** Amazon Web Services (AWS).
- **Primary hosting region:** South Africa (Cape Town), AWS region `af-south-1`.
- **Disaster-recovery region:** Ireland (Dublin), AWS region `eu-west-1`.
- **Temporal Cloud preferred region:** Ireland, Temporal Cloud region identifier `aws-eu-west-1`, subject to POC-06 and due diligence.
- **Scope:** Architectural direction only. No subscription, contract, payment, account configuration, resource provisioning, or production deployment is authorised.
- **Conditions:** Complete legal and privacy assessment (including Nigerian data-protection and cross-border-transfer requirements), security review, service availability and compatibility validation, POC and operational readiness, cost review, and recovery design/testing. Confirm the required data-residency, backup, retention, encryption, key-management, monitoring and incident-response controls.
- **Lagos Local Zone:** Any use is optional and separately evaluated; it is not treated as an independent AWS Region or as proof of full Nigerian data residency.
- **Reversibility:** Region and provider selection may be revisited based on validation evidence or requirements changes.


## HD-04 — Approved Six-Deployable Backend Topology (2026-11-19)

- **Decision:** Retain six logical backend deployable service units: `api-gateway`, `agent-orchestrator`, `multimodal-service`, `sandbox-runner`, `billing-ledger`, and `adtech-service`.
- **Scope:** These are logical deployable boundaries, not a requirement for six separate physical infrastructures. AI model routing remains a capability within the designated architecture and must not introduce an undocumented seventh deployable service.
- **Conditions:** Physical deployment, resource allocation, infrastructure consolidation or separation, network design and implementation remain subject to validation and approval.
- **Implementation authority:** This decision does not authorise Phase 1, infrastructure provisioning or production deployment.

### HD-REP-01 — Approved Monorepo Tooling and Workspace Strategy

- **Decision:** Approved — adopt a controlled Git monorepo for Worklexx AI Software Factory platform-owned source code. Use pnpm workspaces for JavaScript/TypeScript dependency and package management, with Turborepo for dependency-aware task orchestration and caching. Maintain independently managed Python service and package projects; determine Python dependency and lockfile tooling separately under HD-REP-02.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-19.
- **Rationale:** A controlled monorepo supports coordinated development, shared contract management, consistent validation, and traceability while preserving independently owned application and service boundaries. pnpm and Turborepo provide a focused JavaScript/TypeScript workspace and task-orchestration approach without forcing Python dependency management into the same toolchain.
- **Architecture constraints:** Preserve five frontend applications, six independently buildable/testable/versionable/deployable backend service units, 23 logical agent modules, explicit shared-package ownership, and versioned cross-language API/event contracts. Shared packages must not depend on application-specific or service-specific implementation code. Shared packages, agents, contracts, and build tasks must not create additional backend deployable services.
- **Security and reproducibility conditions:** Commit the pnpm lockfile and pin package-manager and build-tool versions. Validate workspace boundaries, dependency policies, build ordering, tests, versioning, release behavior, tool compatibility, licensing, security posture, CI integration, and cache configuration. Build caches must not expose secrets, private artifacts, or tenant data. CI must validate affected workspaces and required repository-wide security and compatibility checks.
- **Generated-project boundary:** Customer- and tenant-generated projects are not ordinary platform workspace packages. Their repository and artifact isolation model remains subject to HD-REP-05; the platform monorepo must not expose one tenant's generated source or artifacts to another tenant, user, or agent.
- **Alternative retained:** Nx or Bazel may be reconsidered if measured repository scale, polyglot build requirements, performance, or governance needs justify their additional capabilities and complexity. Separate repositories may also be reconsidered if independent ownership or isolation requirements materially outweigh monorepo coordination benefits.
- **Scope limitation:** This is an architectural tooling and workspace decision only. It does not authorise repository restructuring, tool installation, lockfile creation or modification, CI/CD changes, branch changes, infrastructure provisioning, production deployment, or Phase 1 implementation. Applicable approvals and validation remain required.

### HD-REP-02 — Approved Python Dependency and Lockfile Tooling

- **Decision:** Approved — adopt Astral uv as the preferred Python dependency-management, lockfile, and project-environment tool for Worklexx AI Software Factory.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-19.
- **Rationale:** uv provides integrated dependency resolution, lockfile management, project-environment management, and reproducible installation while allowing Python services and packages to remain independently managed projects.
- **Project structure:** Each independently managed Python backend service must maintain its own `pyproject.toml` and committed `uv.lock`, with explicit dependency ownership, appropriate dependency groups, and a documented supported Python-version policy. Shared Python packages must define their own project metadata and development/test dependencies. A shared package's development lockfile is not the dependency lockfile for every consuming service.
- **Workspace boundary:** Do not require a single Python workspace across the six backend services. Any future workspace grouping requires technical justification and separate approval. Workspace grouping does not provide runtime isolation; actual isolation remains the responsibility of appropriate processes, containers, service boundaries, and permissions.
- **Reproducibility and version control:** CI must enforce lockfile consistency and reproducible installation (for example, `uv sync --locked`), pin the uv tool version, and control supported Python runtime versions through repository-managed configuration. CI must fail rather than silently rewrite committed lockfiles. Local virtual environments and caches must be excluded from source control.
- **Security and supply chain:** Apply approved package-source and private-index controls, review direct URL and Git dependencies, assess package integrity and provenance, scan dependencies for vulnerabilities and license obligations, control dependency updates, and generate SBOM evidence for release artifacts. Credentials must be supplied through approved secrets-management mechanisms and must not be embedded in project metadata or lockfiles.
- **Validation conditions:** Validate Windows developer workflows, Linux CI, Python 3.12 compatibility, deterministic resolution, independent service lockfiles, Docker integration, private package sources, vulnerability and license scanning, SBOM generation, dependency upgrades, and rollback before implementation.
- **Alternative retained:** Poetry remains a viable alternative if evidence demonstrates a material advantage for packaging, publishing, or project-management requirements. pip-tools remains suitable for specialised requirements-compilation workflows but is not the preferred complete project-management solution.
- **Architecture constraints:** Preserve the six approved backend deployable service units and independently managed Python service boundaries. This decision does not introduce a seventh deployable service or require a shared Python runtime environment.
- **Scope limitation:** This is an architectural tooling decision only. It does not authorise tool installation, dependency changes, lockfile creation or modification, repository restructuring, CI/CD changes, infrastructure provisioning, production deployment, or Phase 1 implementation. Applicable approvals and validation remain required.



### HD-REP-03 — Approved Branching, Integration and Release Strategy

- **Decision:** Approved — trunk-based development using `main` as the permanent protected integration branch, with short-lived feature, fix, and hotfix branches. Require PRs, automated validation, and independent human review. Prohibit direct pushes, force pushes, and routine bypasses. Prefer squash merging.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-20.
- **Release strategy:** Independently version the six backend deployable services and five frontend applications, with component-specific release tags, release notes, artifact provenance, and compatibility controls. Use Semantic Versioning where applicable.
- **Release branches and hotfixes:** Release branches are temporary and justified only for stabilisation, certification, coordinated releases or maintenance. Hotfixes must be reconciled into `main`.
- **Further validation:** Release automation/tool selection, CI/CD implementation, protection configuration, tagging and release procedures require validation and separate approval.
- **Scope limitation:** Architecture only. No branch protection configuration, implementation, release creation, production deployment, infrastructure provisioning or Phase 1 authorisation.


## HD-REP-04 — Approved Repository Ownership and Governance Direction (2026-11-20)

- **Decision:** Adopt an organisation-owned repository model when the Worklexx GitHub organisation is established and repository transfer is separately authorised. Until then, the repository remains in its current location.
- **Access:** Least-privilege role-based access; minimum necessary human administrators; external collaborators and automation identities are scoped and periodically reviewed. No shared credentials.
- **Protected integration branch:** Protect `main` from direct routine pushes, force pushes and deletion. Require PRs, independent human review, designated CODEOWNERS review for critical paths, and mandatory CI checks when implemented. Prefer squash merging and dismiss stale approvals when material changes occur.
- **AI and automation:** Agents may assist with analysis, tests and PR preparation under scoped permissions, but may not approve their own changes, accept risk, alter governance settings, grant access or bypass protections.
- **Governance:** Project Owner remains sole initial governance approval authority. HD-08 and its approval gates remain authoritative; PR review is not gate approval.
- **Scope:** Architectural direction only. Organisation creation, repository transfer, ruleset/branch protection configuration, invitations, permission changes, CI/CD implementation and other consequential operations require separate authorisation as applicable. No Phase 1 or production implementation authorised.
- **Approval:** Project Owner explicitly approved this decision on 2026-11-20.


### HD-REP-05 — Approved Generated-Project Repository Isolation Model

- **Decision:** Approved — adopt a hybrid, provider-independent repository architecture with one isolated Git repository per generated customer project. Keep the Worklexx AI Software Factory platform-source repository separate from all customer-generated project repositories.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-20.
- **Hosting options:** Support Worklexx-managed private project repositories and customer-managed Git hosting integrations, subject to supported-provider validation. A customer does not need a Git hosting account merely to use the Factory; Worklexx-managed hosting is an intended option.
- **Isolation:** Each generated project must have a unique project identity and repository mapping, private-by-default visibility, tenant- and project-scoped authorization, independent access controls, credential boundaries, audit records, lifecycle controls, retention/deletion procedures, backup/recovery, and export capability. Repository separation alone is insufficient: API authorization, storage, Git credentials, background jobs, caches, and agent execution must all enforce tenant/project boundaries.
- **Agent permissions:** Repository access must be mediated by a permission-controlled layer and granted per task and project. Read-only inspection, branch/code-write operations, pull-request creation, and sandbox testing are distinct permissions. Agents receive only the minimum scope required; no cross-tenant access or implicit secret access. Agents cannot change repository ownership or visibility, delete repositories, or perform other protected operations without the applicable human authorization and approval gate.
- **Customer control and portability:** Customers must be able to export source code and Git history, connect or transfer to supported customer-managed hosting, and disconnect/revoke an integration. Export, transfer, and connection actions must be authenticated, authorized, audited, and designed to avoid unintended disclosure.
- **Ownership boundary:** Generated customer software and artifacts must remain distinguishable from Worklexx proprietary platform source, reusable platform components/templates, and third-party components governed by their applicable licences and terms. Ownership and licence terms must be disclosed and recorded.
- **Alternatives considered:** A single Factory monorepo for all generated projects; one repository per customer; one isolated repository per generated project; and a hybrid model combining project-level isolation with Worklexx-managed and customer-managed hosting. The hybrid model is selected to combine strong project-level separation with customer choice and portability.
- **Validation conditions:** Before implementation, validate provider integration and API scopes, tenant/project authorization, credential isolation, cross-tenant negative tests, background-job and cache isolation, agent permission enforcement, secret handling, audit completeness, backup/restore, deletion/retention, export/import integrity, customer disconnection/revocation, and applicable legal/licensing terms.
- **Scope limitation:** This is an architectural decision only. It does not authorise repository provisioning, customer-account connection, OAuth/app installation, provider subscriptions or spending, migration of existing projects, production implementation, changes to the Factory platform repository, or Phase 1 execution. Each consequential operation remains subject to the applicable approval gate and separate authorization.
- **Approval:** Project Owner explicitly approved this decision on 2026-11-20.


## HD-REP-06 — Approved Service-Owned Database Schema and Migration Governance (2026-11-20)

- **Decision:** Approved — adopt service-owned database schema and migration management across all six independently deployable backend services: `api-gateway`, `agent-orchestrator`, `multimodal-service`, `sandbox-runner`, `billing-ledger`, and `adtech-service`.
- **Ownership:** Each service owns its authoritative schema, migration scripts, migration metadata/version history, and migration lifecycle. A service must not independently modify another service's authoritative schema. No single global migration history or unrestricted central migration runner shall control all service schemas.
- **Physical topology:** This decision does not require six physical databases or database servers. A shared PostgreSQL cluster or database remains possible, provided schema ownership, restricted roles, service boundaries, tenant isolation, and controlled interfaces are enforced. Final physical database topology remains a separate matter.
- **Credentials:** Each service's migration identity must be limited to its owned schema. Runtime application credentials must not have DDL/schema-changing privileges. Migration credentials must be separate, protected, narrowly scoped, and used only through separately authorised procedures.
- **Migration safety:** Use backward-compatible expand-and-contract changes where practicable; sequence schema and application changes to support rolling deployment; use migration locks and controlled timeouts; use transactional migrations where supported; retain immutable migration identifiers/checksums and auditable execution evidence. A code rollback must not be assumed to reverse a schema or data migration.
- **Recovery:** Every migration plan must address integrity checks, backup/PITR readiness, rollback where safe, forward-fix where rollback is unsafe, and recovery of dependent services. Destructive changes require impact analysis and a documented recovery plan.
- **Cross-service data:** Prefer authorised APIs, events, and controlled read models over direct cross-service schema coupling. Coordinated changes must identify affected producers, consumers, compatibility windows, and deployment order.
- **Billing and tenant controls:** `billing-ledger` migrations require additional verification of immutable financial history, double-entry integrity, idempotency, reconciliation, and audit continuity. Tenant relationships, RLS policies, and cross-tenant isolation must remain effective throughout migrations.
- **Validation:** Validate clean installation, upgrade paths, migration ordering, compatibility across rolling versions, concurrent execution/locking, failure injection, recovery/forward-fix, least-privilege credentials, schema-boundary enforcement, tenant/RLS controls, ledger reconciliation, backup/restore, and audit/checksum integrity.
- **Governance:** GATE-05 applies to destructive database operations and migrations within its approved scope. Production migration activity also requires GATE-03. A documentation approval, code review, or migration PR does not itself authorise execution. The Project Owner remains sole initial gate approval authority under HD-08.
- **Scope limitation:** Architectural decision only. No database or schema creation/modification, credential creation, permission changes, migration execution, CI/CD activation, infrastructure provisioning, spending, production deployment, or Phase 1 implementation is authorised.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-20.

## HD-REP-07 — Approved Repository Backup, Disaster Recovery and Restoration Governance (2026-11-20)

- **Decision:** Approved — adopt a layered, provider-independent repository backup, disaster-recovery and restoration architecture. Apply distinct protection classes to (A) Worklexx Factory platform source and governance records, (B) Worklexx-managed customer project repositories, (C) customer-managed repositories, and (D) supporting development records and artifacts.
- **Backup scope:** Protect Git objects, commits, branches, tags, references and Git LFS objects where used. Separately protect supported repository metadata (issues, pull requests, reviews, comments, labels, milestones, releases and settings/ruleset definitions), release/build artifacts and packages, project/repository mappings, access and audit records, and the information needed to re-establish authorised integrations. A Git clone alone is not a complete repository or platform backup. Secrets and credentials must not be copied as ordinary repository metadata; restore them through approved secrets and key-management procedures.
- **Hosting responsibility:** Worklexx is accountable for the defined backup and recovery service for Worklexx-managed private project repositories, subject to customer agreements. For customer-managed hosting, the customer remains responsible for provider-account and provider-side recovery; Worklexx may retain only the information it is authorised and technically able to protect. Provider capabilities and limitations must be disclosed. Customer disconnection or revocation must not delete customer-owned repositories.
- **Backup architecture:** Use multiple independently controlled recovery copies, including an off-site copy and at least one immutable or deletion-resistant copy. Separate backup administration and credentials from ordinary repository administration. Encrypt backups in transit and at rest; protect encryption keys independently; enforce least privilege, audit logging, tenant/project isolation, integrity verification and controlled retention/deletion. Preserve portability to an independent compatible Git hosting environment where practicable.
- **Frequency and retention objectives:** Factory source and governance records: daily full logical backup plus incremental/event-based capture through the day; daily copies retained 90 days and monthly copies 12 months. Worklexx-managed customer repositories: continuous or frequent Git replication plus daily metadata backup; daily copies retained 90 days and monthly copies 12 months. Customer-managed repositories: scheduled synchronisation only within customer-authorised scope and daily metadata capture where supported, with retention agreed contractually. Critical audit and financial-related development records follow approved records-retention and legal requirements. Release/build artifacts are protected at creation/release and retained for the associated supported release period. These are initial architectural objectives, subject to legal, technical, cost and contractual validation.
- **Recovery objectives:** Critical Factory source and release-control records: RPO ≤15 minutes / RTO ≤4 hours. Active customer project source repositories: RPO ≤1 hour / RTO ≤8 hours. Repository metadata and development records: RPO ≤4 hours / RTO ≤24 hours. Historical artifacts and noncritical archives: RPO ≤24 hours / RTO ≤48 hours. These are proposed objectives, not verified SLAs or guarantees; validate feasibility and align with HD-06 classifications and POC-15 without automatically applying financial-ledger targets to every repository.
- **Restoration governance:** Use documented incident declaration, containment, verified recovery-point selection, isolated restoration, integrity/security/tenant-isolation checks, authorised reconnection, reconciliation and evidence capture. Do not silently overwrite newer customer work; use separate repositories/branches and controlled reconciliation where necessary. Restore source, metadata, artifacts and platform dependencies as distinct recovery components.
- **Validation:** Exercise Git history/ref and LFS recovery, metadata recovery, artifact checksums/provenance, tenant-isolation negative tests, credential-compromise and deletion scenarios, ransomware-clean-point selection, provider-outage portability, retention/legal holds, customer export, and measured RPO/RTO. A successful backup job is not proof of recoverability; actual restoration evidence is required.
- **Governance and approval:** Agents may detect backup failures and prepare recovery plans or authorised integrity checks, but may not approve consequential restoration, delete protected copies, change retention, or override controls. GATE-02 applies to financial/resource commitments; GATE-04 to protected GitHub operations; GATE-03 to production deployment/recovery operations where applicable; GATE-06 to consequential external integrations/live-account actions. The Project Owner remains sole initial approval authority under HD-08.
- **Scope limitation:** Architectural decision only. No backup configuration, repository setting or permission change, infrastructure or storage provisioning, subscription/spending, customer-account connection, backup/restore/migration execution, CI/CD activation, production implementation, or Phase 1 work is authorised. Legal, privacy, provider, cost, security, operational and contractual validation and separate approvals remain mandatory.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-20.

## HD-REP-08 — Approved Repository Automation, Build Integrity and Software Supply-Chain Security Governance (2026-11-20)

- **Decision:** Approved — adopt a policy-controlled, least-privilege, verifiable automation architecture for Worklexx Factory source and customer-generated projects. Every trusted build and release must be traceable to its source, dependencies, tools, workflow identity and execution evidence. Validation, build, signing, publication and production deployment are distinct activities with separate permissions and approvals.
- **Repository boundaries:** Protect the Factory platform-source repository, Worklexx-managed customer project repositories, and customer-managed repositories as distinct security boundaries. Customer projects retain the one-repository-per-project model under HD-REP-05. Automation, credentials, storage, background jobs, caches, artifacts and agent execution must remain tenant- and project-scoped. Customer-managed repository access is limited to the permissions expressly granted by the customer.
- **Workflow governance:** Default workflow permissions to read-only and grant narrowly scoped write permissions only to jobs that require them. Prefer short-lived credentials; prohibit shared credentials and unnecessary long-lived personal tokens. Review workflow definitions before activation. Pin third-party workflow actions to immutable commit SHAs, control executable downloads and scripts, protect security-critical workflow files, and prevent untrusted pull-request code from accessing privileged secrets or trusted publishing credentials. Separate source validation, dependency checks, tests, build execution, artifact verification, provenance generation, release approval, publication and deployment.
- **Dependency and supply-chain controls:** Enforce committed lockfiles and pinned package-manager/build-tool versions; verify dependency integrity; assess direct and transitive dependencies; scan vulnerabilities, secrets and licences; use SAST and applicable DAST; review dependency changes; and generate machine-readable SBOMs using a recognised format such as SPDX or CycloneDX. Scanner results require risk-based triage; scanning does not prove absence of vulnerabilities. Existing pnpm/Turborepo and Astral uv decisions remain unchanged.
- **Build isolation:** Run builds in isolated, appropriately resettable environments. Separate untrusted pull-request builds from trusted release builds. Apply least privilege, resource limits, timeouts and justified network restrictions. Do not expose Factory secrets to customer builds or untrusted code. Isolate filesystem, process, credentials, caches and artifacts by trust boundary, tenant and project. Build caches must not leak secrets, private artifacts or tenant data. The sandbox-runner remains within the approved six-deployable architecture and does not gain unrestricted release authority.
- **Artifact integrity and provenance:** Generate and verify cryptographic checksums; protect published artifacts against unauthorised replacement; and preserve source-to-artifact traceability. Trusted releases should carry provenance identifying repository/project, source commit, build/workflow identity, relevant toolchain and dependency/lockfile state, timestamp, artifact checksums, SBOM and signing evidence. Evaluate suitable standards and technologies such as SLSA provenance and Sigstore subject to security, compatibility, operational and cost validation. Protect signing keys through approved key-management procedures; do not store private signing keys in source repositories or ordinary workflow configuration.
- **Release failure policy:** Block trusted publication when mandatory checks fail, including critical/prohibited vulnerabilities, compromised or unverified dependencies, integrity/signature failures, missing required provenance, unauthorised workflow changes, exposed secrets, failed tenant-isolation checks or prohibited licensing. Exceptions require documented scope, rationale, risk assessment, compensating controls, owner, expiry/review date and Project Owner risk acceptance where required by HD-07. Mandatory legal, regulatory and contractual obligations cannot be waived.
- **AI-agent boundaries:** Agents may inspect authorised source, run approved tests, identify vulnerabilities, prepare dependency updates, generate SBOMs/provenance and prepare PRs within scoped permissions. They may not approve their own PRs, approve releases or deployments, grant themselves access, access unrelated customer secrets, change security policy or bypass protected operations.
- **Approval governance:** A successful build is not release approval; a verified artifact is not publication authority; publication is not production deployment authority. Apply HD-08 GATE-01 through GATE-06 according to the action. GATE-02 applies to paid tools/services and resource commitments; GATE-03 to production deployments; GATE-04 to protected GitHub operations; GATE-05 to destructive database migrations; GATE-06 to consequential external integrations/live-account actions. The Project Owner remains sole initial gate approval authority. Risk acceptance remains subject to HD-07.
- **Validation:** Complete POC-REP-08-01 through POC-REP-08-12 covering workflow permissions, untrusted PR isolation, lockfile/dependency integrity, vulnerability/secret/licence scanning, SBOM generation, artifact checksums/signatures/provenance, build/cache isolation, cross-tenant isolation, credential protection/revocation, release/publication separation, compromised dependency/workflow scenarios, and audit/recovery traceability. Record methods, environments, results, limitations, defects and remediation. Do not treat unexecuted POCs as passed.
- **Scope limitation:** Architectural decision only. No CI/CD workflow activation, GitHub ruleset/branch-protection change, GitHub App installation, credential/token/signing-key creation, paid service/subscription, infrastructure provisioning, production build, artifact publication, release creation, deployment, customer Git-account connection, database migration execution or Phase 1 implementation is authorised. Each requires applicable validation and separate HD-08 authorisation.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-20.


## HD-REP-09 — Approved Repository Observability, Audit Logging and Security-Event Monitoring Governance (2026-11-20)

- **Decision:** Approved — adopt a provider-independent, privacy-aware observability and audit architecture for Worklexx Factory source and customer-generated project repositories. Consequential actions must be attributable, auditable and detectable. Monitoring, evidence collection and AI analysis do not confer approval authority.
- **Coverage:** Define auditable events for identity/authentication, access and permission changes, repository lifecycle and Git activity, pull requests/reviews/approvals/merges, workflow execution and permissions, AI-agent actions and human interventions, dependency/security scans, SBOM and artifact/provenance activity, releases/publication/deployment, external integrations, backups/restores/deletion/retention, governance decisions, risk acceptance and approval-gate outcomes. Record provider visibility gaps rather than claiming complete coverage.
- **Event envelope:** Use a versioned common schema with unique event ID, event/schema version, event and ingestion timestamps, time-source metadata, actor identity/type, tenant/project/repository scope, action/resource/outcome, originating service/workflow, correlation/trace identifiers, authorisation and policy/approval references, and relevant commit/artifact/workflow references. Avoid copying sensitive payloads when controlled references suffice.
- **Evidence protection:** Use centrally collected, independently protected audit records with append-only or tamper-evident properties, cryptographic integrity verification, encryption in transit/at rest, least privilege, separation of audit administration from ordinary repository administration, protected time synchronisation, auditing of audit-store access, and backup/recovery under HD-REP-07. No actor or agent may silently erase or rewrite its own consequential activity history.
- **Monitoring:** Define detection and escalation for suspicious authentication, privilege changes, cross-tenant access, unusual exports/downloads/deletion, workflow or protected configuration changes, secret exposure, compromised credentials, untrusted build access to privileged environments, provenance/signature failures, backup/integrity failures, and approval-gate bypass attempts. Specify severity, ownership, investigation, incident closure and evidence preservation.
- **Repository responsibility:** Worklexx controls Factory-source audit collection and platform-side records for Worklexx-managed customer projects, subject to customer agreements. For customer-managed hosting, Worklexx records only events available through authorised integrations; customers remain responsible for provider-side records and controls. Provide appropriately scoped customer inspection/export of their own available project history without exposing internal Worklexx security records or other tenants' data.
- **Privacy and retention:** Minimise collected data; never log passwords, token values, private keys, signing keys or secret values. Redact sensitive prompts, source fragments, personal information and request content unless specifically justified and authorised. Separate operational telemetry from security audit evidence. Establish retention, legal-hold, customer export, controlled disposal and deletion requirements by record class after legal, regulatory and contractual assessment; no universal retention duration is approved by this decision.
- **AI-agent boundaries:** Agents may analyse authorised events, identify anomalies, prepare incident summaries and evidence, and recommend remediation. They may not approve gated actions, accept risks, grant permissions, alter/delete protected evidence, change retention/legal holds, disable monitoring or bypass controls. HD-07 and HD-08 remain authoritative.
- **Validation:** Require POC-REP-09-01 through POC-REP-09-12 covering event completeness; schema/identity/time accuracy; tamper detection; tenant isolation; redaction/privacy; detection accuracy and false negatives/positives; alerting/escalation; retention/legal hold/export/deletion; audit backup/restore; provider coverage; agent boundaries; and end-to-end traceability. Record methods, environments, expected/actual results, evidence, limitations, defects and remediation. Unexecuted POCs are not passed.
- **Risk:** Add RSK-29 — Incomplete, altered, exposed or inadequately monitored audit evidence. Likelihood, impact and residual score require formal assessment; proposed controls do not reduce residual risk until implemented and evidenced.
- **Governance:** Project Owner remains sole initial risk acceptance and approval authority under HD-07/HD-08. Applicable gates include GATE-02 for financial/resource commitments, GATE-03 for production deployments, GATE-04 for protected GitHub operations, and GATE-06 for consequential external integrations/live-account actions.
- **Scope limitation:** Architectural and documentation approval only. No telemetry or webhooks activation, GitHub audit configuration, SIEM/observability subscription, spending, infrastructure/storage provisioning, credentials/tokens/signing keys, customer-account connections, GitHub App installation, repository permission/protection changes, CI/CD activation, production integration, incident-response automation or Phase 1 is authorised. Separate validation and applicable HD-08 approvals remain mandatory.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-20.


## HD-REP-10 — Approved Customer Project Lifecycle, Ownership, Portability and Exit Governance (2026-11-20)

- **Decision:** Approved — adopt a customer-centred, lifecycle-managed project architecture with explicit project identity, ownership/control records, lifecycle states, hosting responsibility, portability, retention, suspension, transfer and exit controls. This decision complements HD-REP-05 (one isolated repository per generated customer project), HD-REP-07 (backup and recovery), HD-REP-08 (automation and supply-chain security), HD-REP-09 (audit and monitoring), and HD-08 (approval gates).
- **Project identity and lifecycle:** Every generated project must have a unique immutable project identifier, customer/tenant association, recorded owner or controlling entity, repository mapping, hosting mode, lifecycle state and auditable transition history. Logical lifecycle states are Created, Provisioning, Active, Suspended, Archived, Exported/Transferred, Disconnected, Deletion Pending and Deleted. State transitions must be authenticated, authorised, validated and recorded. Suspension is not deletion; export is not ownership transfer; disconnection must not delete customer-owned external repositories.
- **Ownership and intellectual property:** Project records and customer agreements must distinguish customer-provided source/content/data, customer-generated project code, Worklexx proprietary platform and reusable components/templates, and third-party licensed components. The Factory must not make blanket legal assumptions about ownership of generated code. Ownership, licence, permitted reuse, access and transfer rights must be disclosed and governed by applicable agreements and law. Hosting administration does not itself confer ownership of customer projects.
- **Hosting responsibility:** Preserve the HD-REP-05 hybrid model: Worklexx-managed private repositories for customers who do not need their own Git hosting account, and customer-managed supported hosting integrations. Worklexx is accountable for its managed repository operations subject to contract; customers remain responsible for provider accounts and provider-side controls for customer-managed hosting. Worklexx access is limited to explicitly authorised scope.
- **Portability and export:** Provide an authenticated, customer-scoped export pathway for source and complete Git history, branches/tags/refs, Git LFS where used, project documentation/specifications, configuration templates without secrets, dependency manifests/lockfiles, and applicable artifacts, SBOM/provenance, metadata and customer-entitled audit records. Export inventories must identify omissions/provider limitations and include format/version information and integrity checksums. Passwords, tokens, private keys, signing keys and other secrets must not be included in ordinary exports; credentials must be re-established through an approved secure process. Validate independent import and usability.
- **Transfer and exit:** Distinguish export, repository transfer, ownership transfer, hosting disconnection and account closure. Verify requester identity/authority, ownership and contractual rights, legal holds and retention constraints; prepare and integrity-check the authorised package/transfer; obtain receipt or completion confirmation where applicable; revoke relevant integration credentials when requested; apply approved retention/archive/deletion policy; and retain auditable completion evidence. Ownership transfer requires explicit approval by the current authorised owner and any other party whose approval is required.
- **Suspension and entitlements:** Subscription or entitlement expiry may restrict premium Factory capabilities under disclosed contractual terms but must not automatically delete customer source or data. Suspension must preserve records under applicable policy. Reasonable notification and opportunity to resolve entitlement issues should be provided subject to contract. Read-only retrieval/export should remain available where contractually and technically feasible. No universal grace period, retention duration or deletion deadline is established by this decision.
- **Retention and deletion:** Define record-class-specific rules for active/suspended/archived projects, exports, artifacts, audit records, backups, provider-side copies and financial/contractual records following legal, regulatory and contractual assessment. Deletion is a controlled workflow requiring verified authority, scoped inventory, legal-hold/retention checks, applicable approvals, execution evidence and verification across primary storage, Git/LFS, object storage, caches, indexes, jobs, artifacts and replicas. Backup expiry and restore controls must prevent deleted data from being silently reintroduced. No immediate alteration of immutable backup copies or universal retention period is assumed.
- **Agent boundaries:** Agents may inspect authorised metadata, prepare exports/inventories and transfer documentation, identify policy conflicts and recommend lifecycle actions. They may not independently transfer ownership, change visibility, disconnect external accounts, revoke customer access, delete projects/repos/data/backups, change retention, override legal holds, alter entitlements or approve customer exits. Human authorisation and applicable HD-08 gates remain mandatory.
- **Validation:** Require POC-REP-10-01 through POC-REP-10-15 covering immutable identity/ownership mapping; tenant/project isolation; hosting responsibility boundaries; lifecycle transitions; ownership/collaborator/transfer authority; source/history/LFS/metadata export completeness; independent import; secret exclusion; suspension/entitlement safeguards; retention/legal hold/deletion; backup expiry and restore protection; integration disconnection/revocation; exit traceability; agent prohibited actions; and end-to-end recovery/audit evidence. Record methods, environment, expected/actual results, evidence, limitations, defects and remediation. Unexecuted POCs are not passed.
- **Risk:** Add RSK-30 — Customer Project Ownership Disputes, Incomplete Portability or Improper Suspension/Transfer/Deletion. Likelihood, impact, inherent and residual scores remain pending formal assessment; proposed controls do not reduce residual risk until implemented and evidenced.
- **Governance:** HD-07 and HD-08 remain authoritative. GATE-02 applies to financial/resource commitments; GATE-03 to production lifecycle changes with deployment consequences; GATE-04 to protected GitHub operations; GATE-05 to destructive database operations; GATE-06 to consequential external integrations and live-account actions. Apply gates according to the actual operation; not every routine state transition automatically requires a separate gate.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-20.
- **Scope limitation:** Architectural and documentation approval only. No customer project provisioning, live repository/account connection, OAuth/app installation, repository or ownership transfer, suspension/archive/deletion of live customer projects, production migration, backup/retention configuration, infrastructure provisioning, paid service/subscription/spending, GitHub permission/settings changes, CI/CD activation, production deployment or Phase 1 implementation is authorised. Separate validation and applicable HD-08 approvals remain mandatory.



## HD-REP-11 — Approved Customer Data Isolation, Privacy Boundaries and Data Governance (2026-11-20)

- **Decision:** Approved by the Project Owner on 2026-11-20. Adopt a privacy-by-design, data-governance and tenant-isolation architecture covering Factory platform data and customer-generated projects. Apply a common classification framework (Public, Internal, Confidential, Restricted), purpose limitation, data minimisation, documented processing purposes and legal/contractual authority, explicit controller/processor role assessment, and customer/project-scoped access.
- **Isolation:** Enforce trusted tenant and project identity across APIs, service-to-service calls, PostgreSQL and RLS, pgvector retrieval, object/file storage, search indexes, embeddings, agent memory/context, workflows, queues, caches, multimodal temporary files, build environments, artifacts, logs, backups, exports and restoration. Client-supplied tenant identifiers are not authority. RLS supplements, but does not replace, service-layer authorisation.
- **Data scope:** Cover prompts, text, documents, images, audio, video, transcripts, embeddings, metadata, generated outputs, source code, business records, audit data and derived copies. Deletion and access controls must consider associated derivatives, caches, indexes and backups.
- **AI and subprocessors:** No unrestricted provider access to customer databases or repository credentials. External providers/subprocessors require documented due diligence, purpose, data scope, location, retention, human access, onward transfer, training-use and deletion terms. Customer data must not be used to train or improve general-purpose external models unless a specific lawful and appropriately authorised arrangement expressly permits it.
- **Agents and untrusted content:** Apply least privilege, task/tenant/project scoping, purpose, limited duration and audit to each invocation. Agents cannot expand permissions, access other tenants, approve access, override retention/legal holds or transfer data to unauthorised providers. Treat uploaded/retrieved content as untrusted; prompt injection cannot override system policy, permissions or approval gates.
- **Security and regions:** Protect confidential/restricted data in transit and at rest; separate keys/secrets from application data; control key lifecycle and access. Preserve HD-03's Cape Town primary/Ireland DR and Temporal Ireland direction, but do not infer transfer legality from region selection. Assess applicable Nigerian and other jurisdictional laws, transfer safeguards, localisation, provider/subprocessor access and backup/support locations before live processing.
- **Rights and lifecycle:** Provide legally applicable access, correction, export, erasure, restriction, objection and consent-withdrawal mechanisms. Apply record-class retention and legal holds; no universal retention or deletion duration is approved. Deletion must account for primary data, Git/LFS, object storage, indexes/embeddings, caches, jobs, derivatives, replicas and backups, aligned with HD-REP-07 and HD-REP-10.
- **Audit and incidents:** Align privacy event coverage and redaction with HD-REP-09. Do not place passwords, tokens, private keys, signing keys, full sensitive prompts or personal content in ordinary telemetry. Define privacy incident severity, containment, investigation, evidence, remediation and legally required notifications.
- **Responsibility:** Distinguish Worklexx-managed and customer-managed hosting, customer-provided information, customer project content, Worklexx proprietary components and third-party licensed material. Determine controller/processor roles per processing activity and document responsibilities contractually.
- **Validation:** Require POC-REP-11-01 through POC-REP-11-15 for classification/inventory; tenant isolation; RLS; vector isolation/deletion; agent least privilege; prompt injection; multimodal data; external provider handling/training restrictions; encryption/key controls; cross-border flows; rights/export; retention/deletion/backup; log redaction/audit; hosting responsibility boundaries; and end-to-end privacy/security assessment. Unexecuted POCs are not passed.
- **Risk:** Add RSK-31 — Customer Data Exposure, Unlawful Processing and Privacy Control Failure. Likelihood, impact, inherent and residual scores remain pending formal assessment; proposed controls do not reduce residual risk until implemented and evidenced.
- **Governance:** HD-07 and HD-08 remain authoritative. Applicable gates include GATE-01 for material architecture/policy changes; GATE-02 for paid services/resources; GATE-03 for production processing/deployment; GATE-04 for protected GitHub operations; GATE-05 for destructive database operations; and GATE-06 for external providers, subprocessors, customer integrations and live-account actions.
- **Scope limitation:** Architectural and documentation approval only. No live customer/personal-data processing, external provider/customer integration, OAuth/app installation, infrastructure/storage/database provisioning or modification, credential/key creation, paid service/subscription, GitHub settings/permissions change, production monitoring or workflow activation, migration/deletion/restoration, production deployment or Phase 1 is authorised. Separate validation and applicable HD-08 approvals remain mandatory.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-20.


## HD-REP-12 — Approved Customer Identity, Authentication, Authorisation and Access Lifecycle Governance (2026-11-20)

- **Decision:** Approved by the Project Owner on 2026-11-20. Adopt a centralised managed-identity integration model with Worklexx-controlled application authorisation and service-enforced tenant, project and resource boundaries. Authentication establishes identity; it does not itself grant application or resource authority. Preserve HD-01 and HD-08.
- **Identity classes:** Distinguish individual users, organisations, organisation memberships, project identities/memberships, AI-agent identities, backend service identities, workload identities and external integration identities. A user may belong to multiple organisations with different permissions. Hosting administration does not confer project ownership; HD-REP-10 remains authoritative for project ownership and transfer.
- **Authentication and federation:** Retain the managed identity-provider direction in HD-01. Support appropriate registration, verification, MFA, phishing-resistant methods/passkeys where supported, enterprise SSO/federation, secure recovery, session lifecycle and revocation. Keep provider-specific identity mapped to Worklexx application identities to preserve portability. No specific provider, MFA method or federation protocol is selected by this decision.
- **Authorisation:** Worklexx owns application-level policy. Use RBAC for understandable role assignments, ABAC for contextual conditions, and resource-level permissions for sensitive operations. Services must enforce authenticated identity, trusted tenant/project context, resource ownership/classification, assigned permissions, delegated scope, expiry/revocation and applicable approval-gate state. Client-supplied tenant/project identifiers are never proof of authority. PostgreSQL RLS supplements, and does not replace, service-layer authorisation under HD-REP-06/11.
- **Roles and memberships:** Define a configurable initial role catalogue covering platform governance/administration, organisation owner/administrator, project owner/administrator, developer, reviewer, viewer, billing administrator, security/audit reviewer and agent/automation. Roles are permission bundles, not blanket privileges. Separate organisation membership, project membership, resource ownership and delegated authority. Project ownership changes remain subject to HD-REP-10 and explicit required-party authorisation.
- **Agent and workload identities:** Give each agent invocation a distinct attributable identity and explicit, task-, tenant-, project-, operation- and time-scoped delegation. Do not inherit a human's full authority. The six approved backend deployables retain distinct service identities; no seventh deployable is introduced. Use least-privilege service-to-service permissions and short-lived workload credentials where practicable. API keys/tokens require owner, purpose, scope, expiry where practicable, rotation, revocation and auditable use; privileged secrets must not be embedded in browser/mobile clients or ordinary logs.
- **Access lifecycle:** Govern registration, verification, organisation onboarding, invitations, acceptance, role/permission assignment, periodic review, suspension, restoration, revocation, deprovisioning and account closure. Invitations must be scoped, expiring and revocable. Distinguish suspension, access revocation, account closure and project deletion. Address employee departure, membership termination, compromised/lost accounts, administrator departure, ownership disputes, identity-provider outage and recovery.
- **Privileged and emergency access:** Separate ordinary and privileged identities; require stronger authentication and narrowly scoped, time-limited access for sensitive administration where practicable. Emergency/break-glass access must be documented, attributable, bounded, reviewed and auditable; it cannot bypass HD-08 or mandatory obligations.
- **Revocation propagation:** Define and validate prompt revocation across sessions/tokens, all six services, database/RLS, pgvector, storage, Git/repository integrations, Temporal workflows/queues, agent contexts, build environments, artifacts, caches and external integrations. Sensitive operations must not rely solely on stale cached decisions. Establish measurable propagation objectives through POC; none is claimed as achieved by this decision.
- **Privacy and audit:** Minimise identity data, separate provider authentication data from application profile data, protect identity attributes and secrets, and define applicable rights, retention and legal-hold handling. Record attributable authentication, membership, permission, delegation, privileged-access, recovery, revocation and denial events under HD-REP-09. Never log passwords, token values, private keys or authentication secrets.
- **Human approval and agent limits:** Agents may prepare access reviews, recommendations, recovery evidence and scoped requests, and execute already-authorised tasks. They may not approve their own access, grant themselves permissions, impersonate an approver, accept risks, override legal holds, disable audit controls or bypass approval gates. HD-07/HD-08 remain authoritative; approval is action-, resource- and time-bound, not blanket authority.
- **Validation:** Require POC-REP-12-01 through POC-REP-12-20 covering provider integration/portability; identity mapping; multi-organisation isolation; RBAC/ABAC; cross-tenant/project denial; ownership boundaries; MFA/passkeys/SSO; session expiry/revocation; recovery/compromise; agent delegation; service/workload identity; API key/token lifecycle; revocation propagation; privileged/emergency access; audit attribution; lifecycle/deprovisioning; privacy; provider outage/recovery; approval-gate fail-closed behaviour; and concurrent role changes/stale caches. Unexecuted POCs are not passed.
- **Risk:** Add RSK-32 — Identity Compromise, Excessive Privilege and Access-Control Failure. Likelihood, impact, inherent and residual scores remain pending formal assessment. Proposed controls do not reduce residual risk until implemented and evidenced.
- **Governance:** Project Owner remains sole initial risk-acceptance and approval authority under HD-07/HD-08. Apply GATE-01 to material architecture/policy changes, GATE-02 to paid identity services/resources, GATE-03 to production rollout, GATE-04 to protected GitHub/identity repository operations, GATE-05 to destructive schema/migration activity and GATE-06 to external identity-provider integrations/live-account actions, according to the actual operation.
- **Scope limitation:** Architectural and documentation approval only. No identity-provider selection/connection, customer or organisation account creation, SSO/federation setup, user/permission changes, OAuth/app installation, live credential/API-key issuance, infrastructure/database provisioning or modification, paid service/subscription, GitHub permission/settings change, production authentication/authorisation activation, migration, production deployment or Phase 1 is authorised. Separate validation and applicable HD-08 approvals remain mandatory.
- **Decision-maker:** Project Owner.
- **Decision date:** 2026-11-20.


## HD-REP-13 — AI Agent Security, Delegation, Execution Boundaries and Human Oversight Governance (Approved 2026-11-20)

Adopt permission-controlled, policy-enforced, sandboxed and auditable agent execution for the 23 logical agent modules. This decision does not add a backend deployable or alter the approved six-deployable architecture. Agent intelligence is not authority: each agent has a distinct identity and bounded task, tenant/project, tool, data and time scope; versioned policies; resource limits; audit attribution; and revocation controls.

Five conceptual permission tiers: Tier 0 Observe; Tier 1 Prepare; Tier 2 Execute within controlled scope; Tier 3 Consequential action subject to independent approval and applicable control; Tier 4 prohibited authority (including self-approval and governance bypass). Tool permissions remain granular: inspect, write, PR creation, review, approval, merge, permission changes, deletion and transfer are separate capabilities. The tool-control boundary validates identity/scope, inputs and destinations, classification, policy and approval, then executes, verifies and audits.

Code execution uses an appropriately isolated sandbox within the approved sandbox-runner boundary: restricted networking, resource/time limits, filesystem/process isolation, credential separation, tenant/project-specific caches and artifact handling, and cleanup. Untrusted documents, source, web content, prompts and tool results are data—not policy or authority—and prompt injection must not override permissions, governance or gates. Delegation is task/time bounded, depth-limited, attributable, revocable and cannot expand the initiating authority.

Agent context and memory are scoped, classified, minimised, governed and tenant/project isolated. Outputs require independent verification appropriate to their risk; verification does not substitute for human approvals required by HD-08. Control retries, loops, concurrency, idempotency, resource/cost limits, cancellation and safe failure. Protected audit and monitoring align with HD-REP-09; privacy and data boundaries with HD-REP-11; identity and delegation with HD-REP-12; execution isolation and supply-chain controls with HD-REP-08; customer lifecycle with HD-REP-10.

Validation requirements: POC-REP-13-01 through POC-REP-13-24 (unexecuted) cover agent identity/scope, least privilege, tool authorization, policy enforcement, tier separation, gate binding, sandbox isolation, network/credential restrictions, resource limits, prompt-injection resistance, untrusted content, tenant/project isolation, delegation depth/authority, context/memory privacy, output verification, human oversight, audit attribution, revocation, concurrent actions/races, loops/retries/cancellation, failure/recovery, cost controls, abuse scenarios and end-to-end governance bypass attempts.

Add RSK-33 — AI Agent Misuse, Unsafe Execution, Privilege Escalation and Governance Bypass. Formal likelihood, impact, inherent and residual scores remain pending assessment; proposed controls do not reduce residual risk until implemented and evidenced.

Project Owner remains sole initial risk acceptance and approval authority under HD-07/HD-08. Applicable gates remain mandatory. This is architecture/documentation approval only: no agent execution in production, sandbox provisioning, external integrations, live customer data, credentials, CI/CD activation, GitHub configuration, database changes, paid services, production deployment or Phase 1 is authorised.



## HD-REP-14 — API Contracts, Inter-Service Communication and Integration Governance (Approved 2026-11-20)

Adopt a contract-first, versioned, service-owned, validated and governance-controlled architecture for synchronous APIs, asynchronous events, Temporal workflow/activity interfaces, agent-tool interfaces, data contracts and external integrations. Every contract must have an accountable owner, machine-readable schema where appropriate, explicit version, documented consumers, security/privacy classification, compatibility policy and traceable change history. No service may independently redefine another service's authoritative contract.

Use OpenAPI 3.1 (or a validated compatible later version) for HTTP APIs, JSON Schema for structured payload validation and AsyncAPI for asynchronous interfaces where appropriate. These are standards directions, not selections of specific tooling, brokers, schema registries or infrastructure. Contract versions are independent of service release versions. Breaking changes require impact analysis, compatibility strategy, consumer/provider validation and applicable approval. Preserve backward compatibility where required and explicitly govern event replay and durable Temporal workflow compatibility.

Synchronous interfaces require defined request/response schemas, authentication and authorisation, trusted tenant/project scope, safe errors, correlation, timeouts, bounded retries, failure containment and idempotency for consequential operations. Events require stable identifiers, producer ownership, schema versions, tenant/project scope, correlation/causation metadata, duplicate/replay handling, retention/privacy controls and attributable audit. Events are not proof of approval or completion. Temporal workflow/activity inputs, outputs, state, replay, signals, cancellation and version evolution require dedicated compatibility validation.

Agent-tool contracts must define tool identity/owner, permitted agent scope and tier, input/output schemas, data classification, destination restrictions, side effects, limits, approval requirements, idempotency, failure behaviour and audit. External API/webhook contracts require provider due diligence, scope control, authenticity/integrity verification, replay protection where supported, rate-limit/failure handling, SSRF/destination restrictions, privacy and cross-border review, and revocation. Contract validation complements HD-REP-08 through HD-REP-13; it does not replace service authorization, tenant isolation, human approvals or HD-08 gates.

Require POC-REP-14-01 through POC-REP-14-24 (unexecuted): OpenAPI validation; JSON Schema evolution; AsyncAPI validation; consumer/provider testing; backward compatibility; breaking-change detection; ownership/traceability; service-boundary enforcement; authentication/authorization; tenant/project isolation; safe error/redaction; idempotency; event duplication/order/replay; retry/timeout/failure containment; dead-letter/recovery; Temporal replay compatibility; workflow cancellation/signals; agent-tool permissions; human approval/gate binding; external schema drift/provider failure; webhook authenticity/replay; SSRF/destination/payload security; billing/ledger integrity/reconciliation; and end-to-end audit/release traceability.

Add RSK-34 — Contract Failure, Interface Drift, Integration Abuse and Communication Integrity. Likelihood, impact, inherent and residual scores remain pending formal assessment; unimplemented controls do not reduce residual risk. Project Owner remains sole initial risk-acceptance and approval authority under HD-07/HD-08. This is architectural/documentation approval only: no API/event infrastructure, broker/schema registry, gateway configuration, external provider connection, webhook activation, credentials, live customer data processing, CI/CD activation, GitHub configuration, database changes, spending, production deployment or Phase 1 is authorised.


## HD-REP-15 — API Gateway Architecture, Routing, Rate Limiting and Edge Security Governance (Approved 2026-11-20)

Adopt a policy-enforced API gateway architecture as the controlled external ingress for Worklexx AI Software Factory. The gateway provides routing to the six approved backend deployables; identity-token validation and trusted request-context propagation; request-level policy checks; rate limiting and quota enforcement; request size/content-type controls; TLS and edge-security integration; correlation, tracing and security audit; public API version routing; safe errors and sensitive-data redaction; and bounded timeout, concurrency, backpressure and circuit-breaking controls. This does not create a seventh deployable service.

The gateway is not a substitute for receiving-service authorization, tenant/project isolation, agent permissions or human approval gates. Internal service-to-service communication may use authorised HD-REP-14 interfaces and must independently authenticate and authorize callers. Services must not trust a request solely because it came through the gateway. Client-supplied tenant/project identifiers are not proof of authority. The gateway must not manufacture approval evidence or elevate agent permissions. Public routing must not expose internal administration, database, Temporal, sandbox-management or privileged service interfaces.

Apply layered, configurable limits by client/API key, principal, tenant/organisation, project, endpoint/operation, IP/network, concurrency, payload size and bandwidth. Align quotas with entitlements while distinguishing request limits from financial spending and agent execution budgets. Prevent API-key multiplication from evading tenant limits. Expensive multimodal, sandbox and model-intensive operations require stricter controls, bounded queues and backpressure. Preserve idempotency and safe retry rules; quota/rate-limit dependency failure must have explicitly tested safe behaviour. No numerical global limits, subscription prices or commercial entitlements are selected.

Adopt defence-in-depth edge controls: modern TLS and certificate lifecycle; WAF and denial-of-service protection capability; strict host/path/method/content-type/header validation; request/header size limits; malformed-request, injection, path-traversal and request-smuggling protection; SSRF and outbound-destination restrictions; webhook authenticity/replay protection; secure CORS; and no disclosure of internal topology. Multimodal uploads require type validation, size limits, malware/content scanning where appropriate, safe temporary storage and controlled hand-off to multimodal-service; extension or client MIME declaration alone is not proof of safety.

Route only to explicitly registered authorised interfaces. Public API versions follow HD-REP-14 contract compatibility and deprecation governance, independent of internal service release versions. Use bounded timeouts, retry budgets, circuit-breaking and failure containment; never blindly retry non-idempotent operations. Fail closed for authentication, authorization and approval checks. Return consistent non-sensitive errors with correlation identifiers and avoid confirming another tenant's resource existence. Gateway failure must not silently enable alternate insecure public paths.

Gateway ownership must cover route lifecycle, policy/configuration changes, certificates, quotas, API version publication/retirement, security incident evidence and capacity/performance monitoring. Consequential changes are attributable, reviewed and auditable. Agents may inspect and prepare proposals but cannot independently expose routes, weaken controls, grant access, bypass gates or alter protected production settings. Align HD-REP-08/09/11/12/13/14 and HD-08 gates.

Require POC-REP-15-01 through -24 as documented in TESTING_STRATEGY.md; all remain unexecuted. Add RSK-35 — API Gateway Compromise, Misconfiguration, Abuse and Unauthorised Exposure; likelihood, impact, inherent and residual scores remain pending formal assessment. This is architectural/documentation approval only: no gateway installation/configuration/activation, WAF or DDoS service activation, infrastructure, DNS/certificates/credentials/secrets, external provider connections, subscriptions/spending, rate-limit implementation, GitHub configuration, CI/CD, live customer-data processing, production deployment or Phase 1 is authorised.


## HD-REP-16 — API Security Architecture, Threat Protection, Secrets Management and Cryptographic Controls Governance (Approved 2026-11-20)

Adopt a provider-independent, zero-trust-oriented API security and cryptographic-control architecture for the Factory platform, six backend deployables, five frontend applications, 23 logical agent modules and customer-generated projects. Protect human, organisation, service, workload, agent and external-integration identities; API keys, tokens, sessions, secrets, encryption keys, signing keys and certificates; internal/external API communications; webhooks; software artifacts and provenance; customer data and source code.

Require centralised controlled secrets and key management; least privilege; short-lived, scoped credentials where practicable; purpose-separated cryptographic keys; attributable lifecycle events; independent verification; and fail-closed behaviour when identity, authorisation, cryptographic integrity or approval verification fails. No specific secrets-management vendor, KMS, HSM, certificate authority, cryptographic hardware provider or commercial security product is selected.

Credentials must not be embedded in source code, frontend bundles, Git history, container images, ordinary logs or generated customer repositories. Use dedicated workload identities for services; unique bounded agent identities; scoped, attributable and revocable customer/integration API credentials; secure token validation, refresh-token rotation and revocation; and service-side resource authorisation. Authentication alone does not grant resource access. Password-equivalent secrets require appropriate one-way password hashing rather than reversible encryption.

Manage secrets through controlled generation, storage, runtime distribution, scoped use, rotation, revocation and destruction. Rotation must account for dependent services, overlap/compatibility and recovery; do not silently interrupt production workloads. Separate data-encryption, key-encryption, token-signing, artifact-signing, webhook and transport keys by purpose and permissions. Protect private/signing keys from source repositories, ordinary workflow configuration and agent contexts. Apply established, independently reviewed cryptographic standards; authenticated encryption for application data; modern TLS with TLS 1.2 minimum compatibility and TLS 1.3 preferred where supported; strong key generation; key versioning, audit, recovery and compromise procedures. Confirm algorithm/parameter choices through formal standards review; prohibit custom cryptography.

Protect browser-to-gateway, gateway-to-service, service-to-service, service-to-database, external API/webhook, backup, export and artifact communications in transit. Encrypt PostgreSQL/pgvector, object and multimodal storage, repositories/LFS, sensitive workflow state, audit evidence, backups and confidential artifacts at rest. Encryption does not replace tenant isolation, data minimisation or authorisation.

The API gateway remains the controlled public ingress under HD-REP-15. Internal services independently authenticate and authorise one another; receiving services enforce resource-level authorisation. Restrict outbound destinations and internal interfaces. Webhooks require authenticity/integrity verification, timestamp and replay controls, secure key rotation, idempotency, bounded retries, tenant attribution and audit. Signature verification is not approval for a consequential operation.

Frontend applications must not contain privileged backend credentials. Treat public client credentials as public. Customer projects retain HD-REP-05 isolation; customer secrets must not cross tenant/project boundaries. Build workloads receive only task-scoped credentials. Secret scanning covers source, Git history where available, PRs, artifacts, configuration and generated projects.

Agents may detect exposures, inspect authorised security metadata and prepare remediation/rotation plans, but cannot grant themselves credentials, read unrelated secrets, export private/signing keys, weaken cryptographic policy, disable encryption/authentication, approve their own changes or bypass HD-08. Prefer tool-mediated secret operations without exposing secret values to agent context or memory.

Integrate credential/key events with HD-REP-09 audit and monitoring. Detect secret leakage, anomalous access, invalid tokens/certificates, signing-key misuse, webhook verification failures, unexpected outbound destinations, cross-tenant credential use, incomplete rotations and encryption/integrity failures. Compromise response includes containment, authorised revocation, rotation, artifact/data integrity checks, investigation, controlled recovery and recorded evidence. Emergency containment does not authorise permanent privilege changes or governance bypass.

Require POC-REP-16-01 through -26 in TESTING_STRATEGY.md; all remain unexecuted. Add RSK-36 — Credential Exposure, Cryptographic Compromise and Unauthorised API Access; likelihood, impact, inherent and residual scores remain pending formal assessment. Align HD-01/03/06/07/08 and HD-REP-05/07/08/09/11/12/13/14/15.

This is architectural/documentation approval only. No provider selection/connection, live credential/key/certificate creation or distribution, GitHub permission/configuration changes, CI/CD activation, infrastructure or paid-service provisioning, external integration, live customer-data processing, database modification/migration, production security configuration, production deployment or Phase 1 is authorised.



## HD-REP-17 — Application Security Architecture, Secure Development Lifecycle and Vulnerability Management Governance (Approved 2026-11-20)

**Decision:** Adopt a security-by-design, secure-by-default application engineering framework for Worklexx-owned applications, six backend deployables, five frontend applications, shared packages, 23 logical agent modules and generated customer projects. Security requirements must be considered throughout requirements, architecture, threat modelling, coding, review, testing, dependency management, release, operation, maintenance and retirement. This is an architectural governance decision; it does not approve implementation or deployment.

**Secure SDLC:** Classify changes by data sensitivity, business criticality, exposure, privilege, tenant/project impact and applicable legal/contractual obligations. Maintain traceability from security requirements through design, implementation, testing, findings, remediation and release evidence. Threat-model new applications, significant changes, high-risk features and material external integrations. Consider trust boundaries, authentication/authorisation, tenant isolation, injection, data leakage, secrets, multimodal uploads, agent/tool abuse, supply-chain compromise, denial of service and financial integrity.

**Secure engineering:** Apply language/framework-appropriate secure coding standards, server-side input validation, context-aware output encoding, parameterised queries, safe file handling, explicit resource authorisation, secure sessions, safe errors, restrictive defaults and protections against applicable injection, XSS, CSRF, SSRF, path traversal, unsafe deserialisation and request manipulation. OWASP ASVS and relevant OWASP Top 10 guidance are assessment references subject to version/applicability review; no commercial tool or vendor is selected.

**Security testing:** Adopt risk-proportionate SAST, software composition analysis, secret scanning, DAST where appropriate, API and frontend security testing, configuration assessment, manual review and independently scoped penetration testing where warranted. Automated scanner output is not proof of security. Testing requires appropriate authorisation and scope.

**Vulnerability lifecycle:** Discover, record, classify, prioritise, remediate/mitigate, independently verify, close and retain evidence. Assess severity alongside exploitability, active exploitation, exposure, business impact, data sensitivity and affected assets. Proposed internal remediation/mitigation objectives (not SLAs): Critical 24 hours; High 7 calendar days; Medium 30 calendar days; Low 90 calendar days. Where targets cannot be met, document reason, exposure, compensating controls, accountable owner, target date, review/expiry and residual risk; apply HD-07 acceptance. Critical issues require immediate escalation and consideration of stopping/suspending affected activity. Do not downgrade severity to meet targets.

**Customer-generated projects:** Provide proportionate project security requirements, threat-model summaries where warranted, dependency/vulnerability reports, test reports, SBOM, findings/remediation records and release-security summaries. Generation does not guarantee security. Disclose material known limitations, unresolved vulnerabilities, dependencies and customer responsibilities; evidence is not a security certification or guarantee.

**AI and authority:** Treat prompts, uploads, retrieved documents and tool outputs as untrusted. Prompt injection cannot override policy, permissions or approval gates. Validate generated code and commands before execution. Agents may discover/analyse findings and prepare remediation PRs within scope but cannot approve their own changes, accept risk, waive mandatory obligations, authorise external testing or deploy production fixes. HD-07/HD-08 and HD-REP-08 through -16 remain authoritative.

**Evidence and records:** Maintain security requirements, coding standards, threat models, test strategy/results, vulnerability register, remediation/verification evidence, exception/risk acceptance, security reviews, testing authorisations and release-security evidence. Protect records under HD-REP-09.

**Validation:** Require POC-REP-17-01 through POC-REP-17-24 as recorded in TESTING_STRATEGY.md. All remain unexecuted; no control effectiveness or risk reduction is claimed.

**Risk:** Add RSK-37 — Application Vulnerabilities, Insecure Development and Delayed Remediation. Likelihood, impact, inherent and residual scores remain pending formal assessment.

**Boundary:** Project Owner approval under HD-07/HD-08. Documentation and architecture only. No source-code/dependency changes, security-tool installation or activation, subscriptions, external service connections, CI/CD activation, GitHub settings, live penetration testing, live customer data processing, infrastructure, credentials, database changes, production deployment or Phase 1 is authorised.

---

## HD-REP-18 — Application Configuration, Environment Management and Deployment Configuration Security Governance (Approved 2026-11-21)

The Project Owner approved HD-REP-18 on 2026-11-21, subject to its validation requirements, governance controls and implementation/authorisation boundaries. Adopt a centralised-governance, environment-isolated, configuration-as-code architecture for application and deployment configuration across the five frontend applications, six approved backend deployables, 23 logical agent modules and generated customer projects. This decision adds no deployable service and does not select a configuration-management, secrets-management, feature-flag or deployment vendor.

Establish four logical environments: Development, Testing, Staging and Production. Each must have independently governed configuration, access permissions, secret references, endpoints, storage/database references, integration destinations, feature flags, logging and operational policies. This is a logical isolation requirement, not an instruction to provision separate cloud accounts or infrastructure. Production credentials, data and privileges must not be inherited by lower environments. Production data must not be copied to lower environments by default; any exception requires documented lawful purpose, minimisation, protection and explicit authorisation.

Classify configuration as Public, Internal, Confidential or Restricted according to sensitivity and legal/contractual obligations. Configuration contracts should document setting name, owner, type, required/optional status, permitted values/ranges, default and failure behaviour, environment applicability, classification, dependencies and validation/deprecation rules. Invalid, missing or incompatible security-critical configuration must fail safely; insecure silent defaults are prohibited. Environment variables are not inherently secure.

Use version-controlled configuration-as-code for appropriate non-secret settings, with ownership, review, schema/policy validation, environment association, version history, integrity verification, approval reference, application evidence and drift detection. Protect configuration repositories and workflow files consistently with HD-REP-04 and HD-REP-08. Runtime-applied configuration must be traceable to its inputs and policy version.

Secrets remain under HD-REP-16: configuration may hold authorised references, never secret values. No credentials in source, Git history, frontend bundles, images, ordinary logs or generated customer repositories. No privileged backend credentials in frontend applications. Apply environment-specific, least-privilege access, runtime retrieval where appropriate, rotation, revocation, expiry, audit and recovery. No secrets provider is selected.

Feature flags require named ownership, purpose, environment scope, permitted values, default/failure behaviour, change history and review/expiry where appropriate. Flags must not grant privileges, weaken security, bypass tenant isolation, alter financial integrity, elevate agent authority or replace human approval. Flags are operational controls, not authorisation.

Deployment configuration is part of the software supply chain. Trace the applied configuration to source commit, release/artifact identity, configuration version, deployment identity, approval reference and result. Detect drift from approved baselines; investigate and contain harmful changes; restore or correct only through authorised processes. Rollback must respect database/workflow compatibility, revoked credentials, deletion and recovery constraints under HD-REP-06/07/10.

Factory, Worklexx-managed customer project, customer-managed project and third-party configuration are distinct scopes. Every generated project has independent tenant/project-scoped configuration ownership and access. Customer export/portability must not expose Factory secrets or other customers' configuration. Agent permissions are limited to authorised inspection, analysis and preparation; consequential application requires independent approval. Agents cannot retrieve unrelated secrets, disable controls, alter governance or bypass HD-08.

Integrate configuration creation, review, approval, application, feature-flag changes, secret-reference changes (never values), validation failures, drift, rollback and deployment events with HD-REP-09 protected audit. Redact sensitive values and minimise telemetry.

Require POC-REP-18-01 through POC-REP-18-24, all unexecuted: environment isolation; environment access boundaries; classification; schema validation; safe failure; secret-reference protection; production/lower-environment credential separation; configuration-as-code review/integrity; versioning/attribution; environment compatibility; feature-flag authorisation/defaults; prevention of flag-based bypass; deployment provenance; drift detection; rollback/recovery integrity; database/workflow compatibility; six-service isolation; frontend secret exposure; agent permissions; customer project isolation; export/portability; audit/redaction; regional/service recovery; independent adversarial review.

Add RSK-38 — Configuration Exposure, Environment Contamination and Deployment Misconfiguration. Formal likelihood, impact, inherent and residual scores remain pending; no risk reduction is claimed before implementation and evidence.

Project Owner remains sole initial risk-acceptance and approval authority under HD-07/HD-08. This is an architectural/documentation decision only. It authorises no environment provisioning, configuration store, application/deployment setting change, credentials/keys, provider connection, GitHub settings/permissions, CI/CD activation, live feature-flag change, database modification/migration, paid service, live customer-data processing, production deployment or Phase 1.

## HD-REP-19 — Application Deployment, Release Promotion and Rollback Governance

**Status:** Approved architectural decision; documentation-only. Approval does not authorise implementation, CI/CD activation, environment provisioning, release publication, deployment, rollback execution or Phase 1.

**Decision:** Adopt a controlled, evidence-based, environment-aware release-promotion and deployment architecture. Keep build, validation, artifact verification, release approval, deployment approval, production deployment and recovery as distinct activities. A successful build or workflow is not release or deployment approval.

**Scope:** Five frontend applications, six approved backend deployables (`api-gateway`, `agent-orchestrator`, `multimodal-service`, `sandbox-runner`, `billing-ledger`, `adtech-service`), shared packages, 23 logical agent modules and customer-generated projects. No seventh deployable is introduced. Preserve independent component release identities and HD-REP-05 customer repository isolation.

**Environments and promotion:** Retain the four logical environments defined by HD-REP-18: Development, Testing, Staging and Production. Promotion is explicit and evidence-based; success in one environment does not automatically approve the next. Prefer promotion of the same verified immutable artifact across environments. Environment configuration remains separately governed. A rebuild creates a new artifact identity and requires applicable revalidation.

**Release evidence:** Record release/component identity and version, source repository and commit, PR/review evidence, build identity, immutable artifact identifier and checksum, signature verification where supported, dependency lockfiles, SBOM, provenance, test/security results, known defects and vulnerabilities, API/event/workflow compatibility, database migration compatibility, configuration version, deployment/recovery plan, exceptions and approval references. Block promotion on failed mandatory checks, unverified integrity/provenance, unauthorised workflow/source changes, exposed secrets, failed tenant isolation, incompatible contracts/workflows/migrations, missing/expired/revoked approval or mandatory legal/regulatory/contractual prohibition.

**Authorization separation:** Build permission, release approval, environment deployment approval, production deployment approval and rollback/recovery approval are distinct. Approval binds the approving person, exact action, component, release/artifact checksum, target environment, deployment plan, configuration/migration versions, risk/exception references, timestamp and expiry/revocation state. An approval for one artifact or scope cannot authorise a materially different one.

**HD-08 gates:** Apply GATE-01 through GATE-06 as relevant. Production deployment requires GATE-03. Protected GitHub operations, destructive database migrations, financial/resource commitments and live external integrations require their respective gates. Project Owner remains the sole initial approval authority under HD-07/HD-08. Agents and automation cannot self-approve or infer approval from successful checks.

**Execution and strategies:** Deployment identities are distinct from build identities and least-privileged. Execution verifies identity, artifact, provenance, approval scope, target environment, configuration and compatibility before applying a change, then records results and performs health/integrity checks. Blue-green, canary, rolling and controlled maintenance strategies may be selected case by case; none is mandated universally. Internal service authorization remains authoritative.

**Verification and recovery:** Post-deployment verification covers health/readiness, critical functionality, authentication/authorization, tenant isolation, databases, ledger reconciliation, durable workflows, multimodal processing, agent boundaries, integrations, errors/latency, resource consumption and security monitoring. Before deployment, define failure triggers, known-good artifact, configuration reference, data/schema/workflow compatibility, safe rollback or forward-fix, approvals and communications. Never assume code rollback reverses schema/data changes. Preserve financial history, workflow state, revoked credentials, deletion controls and audit evidence. Prefer a verified forward-fix where rollback is unsafe.

**Emergency releases:** Emergency response is documented, scoped, risk-assessed, minimally changed, independently authorised under a separately approved route consistent with HD-08, verified proportionately and reviewed afterward. No new emergency approval authority or agent bypass is created by this decision.

**Customer projects:** Distinguish Factory, Worklexx-managed and customer-managed deployments. Require project-specific entitlement, permissions, customer authorisation and isolated release evidence. Do not silently deploy to an external customer account. Customer-managed hosting remains under customer control except where a separately authorised supported integration agreement applies.

**Agent boundary:** Agents may prepare release evidence, notes, readiness assessments, deployment plans, monitoring summaries and recovery recommendations. They may not approve releases/deployments, grant permissions, override blockers, select unauthorised artifacts, execute unauthorised recovery or bypass HD-08.

**Audit:** Record source/artifact/provenance, validation, SBOM, configuration/migration references, target environment, deployment identity, human approval, strategy, timestamps, outcome, health checks, exceptions, incident and recovery evidence under HD-REP-09 and HD-REP-11.

**Validation:** Require POC-REP-19-01 through POC-REP-19-26 as recorded in TESTING_STRATEGY.md. All remain unexecuted. No control effectiveness or risk reduction is claimed before implementation and evidence.

**Risk:** Add RSK-39 — Unauthorised Deployment, Release Integrity Failure and Unsafe Recovery. Formal likelihood, impact, inherent and residual scores remain pending. Proposed controls do not reduce residual risk.

**Authority and boundaries:** Project Owner remains sole initial risk-acceptance and approval authority. This is documentation-only. No CI/CD activation, environment provisioning, artifact publication, release tagging, deployment, credential/permission change, infrastructure, paid service, customer hosting connection, database migration, traffic/DNS change, rollback/recovery execution or Phase 1 is authorised.



## HD-REP-20 — Production Operations, Service Reliability, Incident Management and Business Continuity Governance (Approved 2026-11-21)

Adopt a reliability-oriented, security-conscious, auditable and human-governed production operations architecture for the five frontend applications, six approved backend deployables, 23 logical agent modules, shared platform capabilities and customer-generated projects within authorised scope. This decision adds no backend deployable and does not authorise production activation.

Every production component must have an accountable service owner and documented operational responsibilities. Operational roles may include service owner, technical operations, security lead, database owner, incident commander, communications owner and business owner. Assignment of operational work does not delegate HD-07 risk acceptance or HD-08 approval authority.

Measure reliability through availability, correctness and integrity. Define service-specific SLIs and proposed SLOs, distinguishing internal objectives from contractual SLAs. Planning availability objectives are 99.9% for core API/essential access and agent orchestration/durable workflows; 99.95% for billing/ledger processing; 99.5% for multimodal processing and sandbox execution; and 99.0% for analytics/noncritical derived services. These are unverified planning targets, not guarantees or SLAs. Billing/ledger reliability also requires transaction integrity, idempotency, durable acknowledgement and reconciliation. Error budgets may guide investigation and reliability prioritisation but cannot bypass approval gates or legal obligations.

Operational observability combines metrics, logs, distributed traces and business-integrity signals. Monitor frontend journeys, API gateway and services, PostgreSQL/pgvector, Temporal workflows, object storage, multimodal processing, sandbox execution, billing/ledger reconciliation, agent policy boundaries, external dependencies, backup/recovery readiness and identity/security events. Apply HD-REP-09 audit integrity and HD-REP-11 privacy minimisation/redaction; never expose passwords, token values, private keys or unnecessary sensitive customer content in ordinary telemetry.

Adopt a consistent incident lifecycle: detection; triage/classification; declaration; containment; investigation; recovery; verification; closure and learning. Use SEV-1 Critical, SEV-2 High, SEV-3 Moderate, SEV-4 Low and SEV-5 Informational classifications based on actual and foreseeable impact, including data sensitivity and financial integrity. Incident roles coordinate work but do not confer authority for gated deployments, destructive migrations, external account actions or risk acceptance. Proposed internal acknowledgement/assessment targets are SEV-1 15/30 minutes, SEV-2 30 minutes/1 hour, SEV-3 4 business hours/1 business day, SEV-4 1/3 business days and SEV-5 3 business days/when scheduled. These are planning targets only, subject to staffing, coverage and operational feasibility; they are not SLAs.

Security/privacy incident response integrates HD-REP-09, -11, -12, -13 and -16: contain, preserve evidence, identify affected identities/tenants/data, perform authorised credential revocation/rotation, assess integrity and customer impact, evaluate applicable notification obligations, recover safely and document corrective action. Notification deadlines depend on applicable law, jurisdiction and processing context; no universal deadline is established.

Business continuity and disaster recovery must address regional, database, Temporal, identity, object-storage, API gateway, GitHub, external model, payment, critical personnel and ransomware/destructive-administration disruptions. Retain the existing HD-06 RPO/RTO targets without silently changing them: ledger/payment/credit RPO <=5 minutes/RTO <=1 hour; core platform database and tenant records <=15 minutes/<=2 hours; durable agent/workflow state <=5 minutes/<=1 hour; core API/essential access RTO <=1 hour with state-specific RPO; multimodal/sandbox recoverable state <=1 hour/<=4 hours; analytics/noncritical derived data <=24 hours/<=24 hours. These remain unverified architectural objectives, not SLAs. Validate recovery points, isolated restoration, tenant boundaries, revocation, financial reconciliation, workflow/event consistency, deletion/retention and key availability before reconnection.

Capacity management covers compute, memory, storage, database connections/locks, pgvector, workflow queues, API traffic, multimodal processing, sandbox resources, model/provider consumption, ledger throughput, bandwidth and regional capacity. Plan for normal/peak workloads, growth, abuse, dependency failure and recovery/backfill. Resource automation cannot bypass financial commitments or production change approvals.

Material operational changes require an owner, scope, reason, risk/dependency assessment, test and recovery plan, applicable approvals, execution evidence and verification. Maintain controlled service runbooks for outages, databases, gateway, Temporal, billing discrepancies, credential compromise, data exposure, multimodal failures, sandbox incidents and regional recovery. Maintain a dependency register with owner, data/access scope, failure impact, recovery, contractual/regulatory constraints, monitoring and exit considerations.

Production agents may correlate alerts, analyse authorised telemetry, prepare incident timelines, retrieve runbooks, propose root causes, assess capacity and draft recovery/post-incident reports. They cannot accept risk, approve or execute unauthorised production changes, alter/delete audit evidence, grant access, perform destructive database operations, make unapproved financial corrections or declare an incident resolved solely on their own assessment. Automated containment/remediation requires separate scope, validation and authorisation.

SEV-1 and SEV-2 incidents require formal post-incident reviews; review SEV-3 where recurring, security-related or materially customer-impacting. Record timeline, scope, affected customers/data, detection, response, root/contributing causes, control effectiveness, notification assessment, recovery objective results, corrective actions, owners and verification. Feed lessons into architecture, risk, testing, runbooks and roadmap.

Require POC-REP-20-01 through POC-REP-20-28 as recorded in TESTING_STRATEGY.md. All remain unexecuted; no operational capability or recovery objective is claimed validated. Add RSK-40 — Production Operational Failure, Inadequate Incident Response and Business Continuity Failure; formal likelihood, impact, inherent and residual scores remain pending.

Project Owner remains sole initial risk-acceptance and approval authority under HD-07/HD-08. This is documentation-only: no production activation, monitoring/SIEM activation, staffing/on-call commitment, SLA, infrastructure, subscription/spend, database/configuration change, traffic/DNS change, automated remediation, external integration, live customer-data processing, backup/restore execution or Phase 1 is authorised.



## HD-REP-21 — Customer Support, Service Desk, Customer Communications and Service Escalation Governance

**Status:** Approved architectural decision; documentation-only. **Scope:** Five frontend applications, six approved backend deployables, 23 logical agent modules, shared platform capabilities, Worklexx-managed customer projects and authorised customer-managed integrations. No additional backend deployable is introduced.

Adopt a customer-centred, secure, auditable and accessible support architecture with unified logical service-desk capabilities for intake, identity/authority verification, classification, ticket lifecycle, assignment, investigation, escalation, resolution, communication, complaints, knowledge management and feedback. Channels may include in-app support, a customer portal, email, governed knowledge base, technical documentation, service-status communications and approved urgent escalation routes. No help-desk, CRM, messaging, status-page or ticketing vendor is selected.

Support categories include account/identity, onboarding, project creation, development, repository, AI/agent, multimodal, billing/subscription, deployment, security/privacy, complaints/feedback and feature requests. Each request has a unique identifier, primary category, accountable owner, priority, auditable state transitions and preserved evidence. Lifecycle: submitted, acknowledged, verified/classified, assigned, investigated, escalated where necessary, resolved, customer-confirmed/closed and reviewed. Additional states include waiting for customer, reopened, duplicate, withdrawn, rejected with explanation and pending external provider. Automated response alone does not establish resolution.

Support must verify customer identity, organisation membership, project ownership/authority and request-specific permissions under HD-REP-12. Apply minimum necessary access, tenant/project isolation, purpose limitation and time-bound/revocable support access. Prefer metadata and customer-provided diagnostics over customer content. Restricted source, prompts, documents, media or records require documented purpose and appropriate lawful/contractual authority. Never request passwords, private keys or authentication tokens. Record access identity, scope, reason, duration and activity; revoke when no longer needed.

Support entitlements may be configurable by approved commercial arrangements (e.g. standard, professional, business, enterprise or contractual support); these are logical categories, not approved packages or prices. Proposed unverified planning targets: Urgent acknowledgement 30 minutes/initial assessment 1 hour; High 2 business hours/4 business hours; Normal 1 business day/2 business days; Low 2 business days/5 business days. They are not SLAs or commitments and require validation of staffing, operating hours, coverage, customer distribution and entitlement. Keep support priority separate from HD-REP-20 SEV-1 through SEV-5 incident severity.

Escalation functions: Level 1 customer support; Level 2 specialist support; Level 3 engineering/service owner; Level 4 security/privacy/financial specialist; Level 5 management/governance. Preserve ticket identity/history/evidence and re-check receiving-team authority. Suspected cross-tenant exposure, account compromise, credential/key leakage, unsafe agent action, sandbox isolation failure, ledger/financial corruption, deletion/recovery failure, unauthorised production change, material privacy concern or widespread outage requires immediate specialist assessment and entry into the HD-REP-20 incident process where applicable. A support ticket alone is not an incident record.

Adopt formal complaint intake, acknowledgement, independent classification/ownership, investigation, evidence, customer communication, documented outcome, review/escalation and controlled closure. Complaints about the original handler should receive independent review where practicable; good-faith complainants must not be disadvantaged. Legal, regulatory and financial disputes go to authorised specialists.

Customer communications must be accurate, clear, attributable and retained appropriately. Distinguish verified facts from hypotheses; state known impact, next steps and limitations; avoid speculation, promises and disclosure of other customers' data or sensitive infrastructure. Planned maintenance and unplanned disruption notices align with HD-REP-20. Restoration is communicated only after verification. No unsupported recovery-time promises.

AI-assisted support may classify, summarise, search approved knowledge, guide validated routine troubleshooting, draft responses, detect duplicates, translate and analyse trends within bounded permissions. Restricted record access requires explicit scope and authorisation. Agents cannot change permissions, accounts, billing/ledger, subscriptions, delete/transfer projects, approve refunds, deploy production changes, accept risk or bypass HD-08. Human review is required according to action risk. AI must not invent capabilities or claim unperformed actions. Retrieved/uploaded content is untrusted; prompt injection cannot alter policy or permissions.

Govern a versioned knowledge base covering onboarding, accounts, projects, repositories, agents, multimodal, APIs, billing, security/privacy, deployment, troubleshooting and exit. Articles require owner, review/version dates, product scope, instructions, warnings and retirement process. Clearly distinguish available, experimental, proposed and unavailable capabilities. Provide mobile-friendly, accessible, low-bandwidth and multilingual support; machine translation of legal, financial, security or contractual meaning requires appropriate human review.

Support data is classified and governed under HD-REP-11. Enforce tenant/project isolation, minimisation, safe attachment handling, malware scanning where appropriate, audit, retention/deletion, legal holds and backup/export controls. Tickets must not become an uncontrolled secondary repository for source code, credentials or sensitive records. Feedback analytics should be minimised/aggregated; no general-purpose external-model training on private support conversations without lawful and explicitly authorised arrangements.

Require POC-REP-21-01 through POC-REP-21-28 in TESTING_STRATEGY.md; all remain unexecuted. Add RSK-41 — Customer Support Failure, Unauthorised Support Access and Inaccurate Customer Communications. Formal likelihood, impact, inherent and residual scores remain pending; unimplemented controls do not reduce residual risk. Align HD-REP-05 and HD-REP-07 through HD-REP-20. Project Owner remains sole initial risk-acceptance and approval authority under HD-07/HD-08.

This decision authorises documentation and future validation planning only. It does not authorise service-desk activation, vendor selection/procurement, staffing commitments, contractual SLAs, subscription/pricing changes, live customer-data processing, restricted customer access, external integrations, account/project changes, refunds or financial commitments, automated administration, production configuration/monitoring changes, infrastructure/spend, deployment or Phase 1.
