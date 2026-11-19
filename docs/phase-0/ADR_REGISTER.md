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

The register contains 14 initial ADR identifiers:

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

GATE-05 is intended to govern designated destructive or materially consequential database operations, including destructive schema migrations and incompatible data transformations. GATE-06 is intended to govern designated consequential external integrations and live-account actions with material external, financial, operational, or customer impact. Their complete scope, exceptions, approval authority, enforcement, and evidence requirements remain subject to explicit Project Owner confirmation. GATE-01 and GATE-02 remain pending formal definition.

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

A proposed five-tier branch strategy has been discussed but has not been formally approved or adopted.

### 20.2 Decision Statement

A five-tier Git branching strategy is proposed for evaluation.

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
| HD-03 | Approve primary and disaster-recovery regions | ADR-002, ADR-007, ADR-008, ADR-012 | Pending |
| HD-04 | Confirm the six-deployable backend service topology | ADR-001, ADR-006, ADR-013 | Pending |
| HD-05 | Validate pgvector configuration and the proposed 3072 embedding dimension | ADR-007 | Pending |
| HD-06 | Approve platform RPO and RTO targets | ADR-007, ADR-008, ADR-012 | Pending |
| HD-07 | Designate risk acceptance authority and approval delegation | ADR-011 | Pending |
| HD-08 | Define GATE-01 through GATE-06 and their approval requirements | ADR-011 | Pending |

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

**Human decisions:** HD-01 is approved as the managed identity-provider approach. HD-02 is approved as the conditional preferred initial Temporal Cloud approach. HD-03 through HD-08 remain pending.

**Repository status:** Existing `main` branch remains the baseline. The proposed five-tier branch strategy has not been adopted.

**Approval authority:** Pending explicit confirmation.

**Implementation authority:** This document does not authorise Phase 1 or any implementation, protected GitHub operation, or production deployment.

The ADR Register provides the traceable foundation for recording, reviewing, approving, and maintaining the architectural decisions of the Worklexx AI Software Factory.