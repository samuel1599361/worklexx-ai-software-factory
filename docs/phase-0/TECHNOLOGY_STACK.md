# Worklexx AI Software Factory — Technology Stack Specification

## Document Metadata

- **Document ID:** WLX-ARCH-003
- **Status:** Revised Architecture Blueprint (Phase 0 Revision Cycle — Awaiting Final Human Review and Approval)
- **Author:** Principal Software Architect, DevSecOps Architect, AI Systems Architect
- **Target Repository:** `https://github.com/samuel1599361/worklexx-ai-software-factory`
- **Classification:** Enterprise Technical Specification
- **Document Type:** Technology Selection and Validation Specification
- **Phase:** Phase 0 — Architecture and Design
- **Approval Status:** Pending explicit Project Owner approval

---

## 1. Purpose

This document defines the proposed technology stack for the Worklexx AI Software Factory.

It identifies the principal technologies, their intended responsibilities, architectural boundaries, selection status, dependencies, security requirements, and validation activities.

The purpose is to establish a coherent, maintainable, secure, scalable, and economically sustainable technical foundation for the platform.

This document distinguishes between:

1. Technologies selected as architectural direction.
2. Technologies proposed as candidates requiring validation.
3. Technologies whose final versions or configurations remain undecided.
4. Technologies that must not become additional deployable services without explicit architecture approval.

A technology appearing in this document does not automatically constitute authorization to purchase a subscription, provision infrastructure, deploy software, or begin Phase 1 implementation.

---

## 2. Technology Selection Principles

Technology selection shall follow these principles:

### 2.1 Security by design

Security controls must be incorporated into architecture, implementation, deployment, and operational processes.

### 2.2 Clear service ownership

Each deployable service must have defined responsibilities, data ownership, interfaces, and security boundaries.

### 2.3 Minimal operational complexity

The platform must avoid unnecessary infrastructure, duplicated services, and excessive technology diversity.

### 2.4 Open standards and portability

Where practical, use established standards and portable interfaces to reduce unnecessary vendor dependency.

### 2.5 Evidence-based selection

Performance, reliability, security, compatibility, and cost claims must be supported by tests or authoritative technical documentation.

### 2.6 Human-controlled execution

AI-generated recommendations must not independently authorize privileged operations, financial transactions, production deployments, or protected repository actions.

### 2.7 Version discipline

Every production dependency must have a documented version policy, compatibility requirements, vulnerability-monitoring process, and upgrade procedure.

---

## 3. Technology Status Classification

The following terminology applies throughout this document.

| Status | Meaning |
|---|---|
| Selected direction | The architectural direction is established, subject to detailed implementation validation. |
| Proposed candidate | A preferred candidate that still requires proof-of-concept or owner approval. |
| Conditional | Suitable only if stated conditions are satisfied. |
| Pending decision | Requires an explicit human decision. |
| Not authorized | Must not be implemented or provisioned under the current Phase 0 authorization. |
| Deprecated | No longer recommended for new implementation. |

A proposed candidate must not be represented as an approved production dependency.

---

## 4. Platform Technology Architecture

The platform is organized around five frontend applications, one separate API Gateway domain, and six deployable backend service units.

### 4.1 Frontend applications

| Application | Domain | Responsibility |
|---|---|---|
| Main website | `worklexx.ai` | Public website, product information, marketing and entry points |
| Main application | `app.worklexx.ai` | Primary authenticated user experience |
| Video application | `video.worklexx.ai` | Video-related user workflows |
| Image application | `images.worklexx.ai` | Image-related user workflows |
| Documentation application | `docs.worklexx.ai` | Documentation, guides and technical resources |

These are five frontend applications.

The API Gateway uses the separate domain:

`api.worklexx.ai`

The API Gateway is not a sixth frontend application.

### 4.2 Six deployable backend service units

The platform architecture defines six deployable backend service units:

1. `api-gateway`
2. `agent-orchestrator`
3. `multimodal-service`
4. `sandbox-runner`
5. `billing-ledger`
6. `adtech-service`

The six-service boundary is an architectural constraint.

AI model routing, AI provider integration, workflow coordination, agent registry, policy evaluation, and related capabilities must be assigned to these services or implemented as internal modules.

They must not silently become additional deployable backend services.

### 4.3 Logical agents

The platform defines 23 logical agents.

The agents are software modules coordinated through the agent orchestration architecture. They are not 23 independent microservices.

Their implementation must preserve the distinction between:

- Agent responsibilities.
- Backend service responsibilities.
- Deterministic policy enforcement.
- Human authorization.
- External provider operations.

---

## 5. Programming Languages

### 5.1 TypeScript

**Status:** Selected direction for frontend development and suitable backend components.

Intended uses include:

- Frontend applications.
- Shared frontend components.
- Browser-side interaction.
- API clients.
- Typed contracts.
- Suitable backend modules where TypeScript is operationally justified.

TypeScript provides static type checking but does not guarantee that external API responses, database records, uploaded data, or runtime inputs conform to declared types.

Runtime validation remains mandatory at trust boundaries.

### 5.2 Python

**Status:** Selected direction for AI orchestration, machine-learning integration, and suitable backend workloads.

Intended uses include:

- AI agent implementation.
- Model integration.
- Multimodal processing coordination.
- AI-related backend operations.
- Data processing.
- Selected internal services and libraries.

Python package and runtime versions must be pinned and tested against the selected framework and infrastructure versions.

### 5.3 Language boundary

The use of TypeScript and Python must not create duplicated business rules.

Shared business contracts should be expressed through versioned API specifications and event schemas.

Critical authorization, billing, ledger, approval, and workflow-transition rules must remain enforced by authoritative backend components.

---

## 6. Frontend Technology Stack

### 6.1 Frontend framework

**Proposed direction:** React-based frontend applications using a consistent application framework.

Next.js is a preferred candidate, subject to validation of:

- Supported runtime modes.
- Deployment compatibility.
- Authentication and session handling.
- Server-side rendering requirements.
- Static generation requirements.
- API communication.
- Build performance.
- Hosting costs.
- Security and upgrade policy.

The final framework and version must be documented in the implementation dependency baseline.

### 6.2 Frontend state management

Proposed responsibilities:

- **Zustand:** Local application and interface state.
- **TanStack Query:** Server-state retrieval, caching, mutation, and synchronization.

These tools must not become authoritative workflow or financial state stores.

The backend and durable workflow engine remain authoritative for business processes.

### 6.3 Real-time communication

Server-Sent Events (SSE) and WebSockets are possible communication mechanisms.

Selection depends on the workflow:

- SSE for appropriate server-to-client event streams.
- WebSockets for bidirectional real-time communication where justified.
- Standard HTTP APIs for request-response operations.

The implementation must support reconnection, authorization revalidation, event replay where available, and state resynchronization.

A disconnected client must not be assumed to have received every event.

### 6.4 Accessibility and responsiveness

Frontend implementation must support:

- Responsive layouts.
- Keyboard navigation.
- Screen-reader compatibility.
- Accessible form validation.
- Appropriate color contrast.
- Clear error and loading states.
- Mobile-device usability.

Accessibility validation must use defined test criteria rather than visual inspection alone.

---

## 7. Backend Technology Stack

### 7.1 API framework

**Proposed direction:** Python with FastAPI for suitable Python backend APIs.

FastAPI is a candidate for:

- Typed API development.
- Request and response validation.
- OpenAPI documentation.
- Asynchronous request handling.
- Integration with Python-based AI components.

The final framework version must be selected using a supported dependency matrix.

### 7.2 Database access

**Proposed direction:** SQLAlchemy for Python database access.

SQLAlchemy must be used with explicit transaction management, secure query practices, and tenant-aware data access.

ORM-level filtering alone is not an adequate tenant-isolation control.

### 7.3 Database migrations

**Proposed direction:** Alembic for SQLAlchemy-compatible schema migrations.

Migration responsibilities include:

- Version-controlled schema changes.
- Upgrade and downgrade planning.
- Migration testing.
- Backup and recovery considerations.
- Controlled deployment.
- Compatibility with application releases.

Each service must have clearly defined ownership of its database schema and migration responsibilities.

No service may modify another service's owned schema through undocumented direct database access.

### 7.4 API contracts

OpenAPI is the proposed standard for documenting HTTP API contracts.

Generated TypeScript clients and shared schemas may be used where appropriate.

However, generated types do not eliminate runtime validation requirements.

Contract tests must detect incompatible changes between API providers and consumers.

---

## 8. Database and Data Technologies

### 8.1 PostgreSQL

**Status:** Selected architectural direction for relational persistence.

PostgreSQL is the principal relational database technology.

It is intended to support:

- User and organization records.
- Tenant-owned application data.
- Transactional business records.
- Workflow metadata where appropriate.
- Billing and ledger records.
- Audit metadata.
- Integration records.
- Relational constraints and transactional consistency.

The final PostgreSQL major version must be selected based on supported extensions, hosting compatibility, operational support, backup procedures, and migration testing.

### 8.2 Row-Level Security

PostgreSQL Row-Level Security (RLS) is required for tenant-owned relational data.

Implementation requirements include:

- Appropriate RLS policies.
- Restricted database roles.
- Composite tenant-aware foreign keys.
- `FORCE ROW LEVEL SECURITY` where appropriate.
- Transaction-scoped tenant context.
- Safe connection-pool handling.
- Protection against tenant-context leakage.
- Adversarial cross-tenant isolation tests.

A session variable such as `app.current_tenant_id` is not, by itself, a complete security control.

RLS must be combined with authenticated tenant context, restricted database permissions, and application-level authorization.

### 8.3 Vector database capability

**Proposed candidate:** pgvector within PostgreSQL.

The candidate may support vector storage and similarity search without introducing another database deployment.

The following require proof-of-concept validation:

- Supported vector dimensions.
- Index type and version compatibility.
- Exact and approximate search behavior.
- Recall and ranking quality.
- Query latency.
- Index size and memory requirements.
- Write performance.
- Concurrent workload behavior.
- Tenant filtering.
- Metadata filtering.
- Re-embedding and model migration procedures.

A 3,072-dimensional vector requirement must not be treated as production-approved until the selected PostgreSQL and pgvector versions demonstrate compatibility and acceptable performance.

### 8.4 Object storage

**Status:** Required architectural capability; provider and configuration subject to final selection.

Object storage is intended for:

- Uploaded files.
- Images and videos.
- Large generated artifacts.
- Model-related assets.
- Project files.
- Other large binary objects.

Required controls include:

- Tenant-aware authorization.
- Encryption.
- Versioning where required.
- Retention policies.
- Malware scanning and quarantine.
- Controlled signed URL issuance.
- Multipart upload recovery.
- Backup and restoration.
- Deletion and legal-hold handling.
- Egress monitoring and cost controls.

Object storage must not be assumed to inherit PostgreSQL RLS protections.

---

## 9. AI and Model Integration Technologies

### 9.1 AI model providers

The platform may integrate multiple external AI model providers.

The architecture must avoid hardcoding assumptions that a particular model name, model version, API endpoint, or pricing arrangement will remain available indefinitely.

### 9.2 Model routing

**Architectural direction:** A centralized model-routing capability within `agent-orchestrator`.

Responsibilities include:

- Model capability matching.
- Provider selection.
- Version and availability tracking.
- Policy-controlled fallback.
- Request and response normalization.
- Usage measurement.
- Cost estimation.
- Provider error handling.
- Rate-limit management.
- Audit metadata.

This is a logical capability, not an additional deployable backend service.

### 9.3 Model catalogue

Maintain a versioned model catalogue containing, where available:

- Provider.
- Model identifier.
- Supported modalities.
- Context limits.
- Input and output constraints.
- Tool-calling capabilities.
- Structured-output support.
- Availability status.
- Pricing metadata.
- Data-processing restrictions.
- Evaluation results.
- Approved use cases.

Model identifiers and provider capabilities must be periodically reviewed.

### 9.4 AI safety and authority

AI models and agents must not independently:

- Post financial ledger entries.
- Change account balances.
- Approve their own privileged actions.
- Bypass human approval gates.
- Deploy to production.
- Execute protected GitHub operations.
- Disable security controls.
- Override deterministic authorization policies.

Models may propose actions. Authoritative services and approved human workflows determine whether those actions may proceed.

The platform must not expose private model chain-of-thought as a user-facing feature. It may provide progress indicators, tool activity summaries, execution status, concise explanations, and results.

---

## 10. Workflow Orchestration

### 10.1 Temporal

**Status:** Proposed candidate; final selection pending proof of concept and human decision.

Temporal is the preferred candidate for durable, long-running workflow orchestration.

Potential responsibilities include:

- Workflow lifecycle management.
- Durable execution state.
- Retries and timeouts.
- Human approval waits.
- Cancellation.
- Compensation.
- Recovery after worker interruption.
- Workflow observability.

### 10.2 Cloud versus self-hosted deployment

Temporal Cloud is approved as the preferred initial hosting approach, subject to POC-06 and due diligence. Self-hosted Temporal remains a future alternative; this approval does not authorise a subscription, contract, production deployment, or region selection.

The decision must consider:

- Total cost of ownership.
- Operational staffing.
- Availability and support.
- Data residency.
- Security requirements.
- Network architecture.
- Backup and restoration.
- Upgrade procedures.
- Disaster recovery.
- Vendor dependency.

The preferred approach has received Project Owner approval dated 2026-11-19. POC-06 and the due-diligence conditions above must be completed and documented before implementation planning treats Temporal Cloud as validated. Any subscription, contract, production deployment, or region selection requires separate approval.

### 10.3 Workflow reliability

The platform must assume that workflow activities may execute more than once.

It must not claim exactly-once execution of external side effects.

Required controls include:

- Idempotency keys.
- Durable execution state.
- Bounded retries.
- Timeouts.
- Cancellation handling.
- Compensation.
- Dead-letter handling.
- Manual recovery procedures.
- Reconciliation.
- Transactional outbox and inbox patterns where appropriate.

A proposed workflow lifecycle is:

`Created → Validating → Queued → Running → AwaitingApproval → Completed / Failed / Cancelled`

Actual state transitions must be validated and enforced by authoritative workflow logic.

---

## 11. Caching and Messaging Technologies

### 11.1 Redis

**Proposed direction:** Redis for suitable caching and ephemeral coordination.

Potential uses include:

- Short-lived caching.
- Rate-limiting support.
- Temporary coordination.
- Ephemeral notifications.
- Non-authoritative session-related support where approved.

Redis must not become the authoritative store for financial balances, durable workflow state, or permanent business records.

### 11.2 Redis Pub/Sub

Redis Pub/Sub may be used for transient message notification and wake-up signals.

It is not a durable message queue and must not be treated as a guaranteed event-delivery mechanism.

Critical events require durable persistence and suitable delivery, retry, deduplication, and reconciliation mechanisms.

### 11.3 Cache isolation

Cache keys and access policies must include appropriate tenant and authorization context.

Sensitive information must not be cached without a documented purpose, security assessment, and retention policy.

Cache invalidation must be defined for permission changes, tenant membership changes, and sensitive data updates.

---

## 12. Sandbox and Code Execution Technologies

### 12.1 Container isolation

**Proposed candidate:** Kubernetes-based execution infrastructure with gVisor isolation.

The candidate must be validated for the actual workload and threat model.

gVisor must not be described as eliminating all container escape or isolation risks.

### 12.2 Sandbox controls

Required controls include:

- Non-root execution.
- Default-deny network egress.
- DNS controls.
- IPv4 and IPv6 policy enforcement.
- Cloud metadata endpoint protection.
- CPU, memory, storage, and process limits.
- Execution time limits.
- Filesystem restrictions.
- Short-lived credentials.
- Restricted capabilities.
- Image scanning.
- Execution audit records.
- Cleanup after execution.
- Escape and isolation testing.

### 12.3 Alternative isolation models

The architecture must retain the ability to evaluate stronger isolation technologies, including microVM-based execution, if the gVisor proof of concept does not satisfy security or workload requirements.

### 12.4 Sandbox deployment boundary

Sandbox execution belongs to `sandbox-runner`.

It must not become an uncontrolled general-purpose execution environment.

The sandbox must not receive unrestricted access to platform credentials, production databases, internal networks, or other tenants' artifacts.

---

## 13. Cloud and Hosting Technologies

### 13.1 Frontend hosting

Vercel is a proposed frontend hosting candidate.

The final hosting configuration must distinguish:

- Static hosting.
- CDN delivery.
- Edge caching.
- Server-side rendering.
- Serverless functions.
- Runtime-specific execution limits.

The use of Vercel does not mean every application runs on an Edge runtime.

Plan-dependent execution limits and pricing must be checked against current vendor documentation before final selection.

### 13.2 Backend hosting

Google Cloud Platform is a proposed backend infrastructure direction.

Google Kubernetes Engine (GKE) is a candidate for container orchestration, subject to operational and cost validation.

The final topology must establish:

- Service deployment boundaries.
- Network segmentation.
- Ingress and egress policies.
- Identity and workload authentication.
- Secrets access.
- Autoscaling.
- Logging and monitoring.
- Backup and recovery.
- Disaster recovery.
- Regional placement.

### 13.3 Cloud ingress protection

Cloud Armor may be evaluated for supported Google Cloud ingress paths.

It must not be assumed to protect Vercel-hosted frontend ingress automatically.

Every public and internal entry point must be mapped, including:

- Frontend applications.
- API Gateway.
- Webhooks.
- WebSocket endpoints.
- SSE endpoints.
- Internal service communication.
- Administrative interfaces.

The selected protection must be appropriate for each actual ingress path.

### 13.4 Cloud database hosting

Cloud SQL for PostgreSQL is a candidate managed database service.

High availability within a managed database configuration is not equivalent to complete disaster recovery.

The platform's recovery plan must also cover:

- Workflow orchestration.
- Object storage.
- Git repositories.
- Financial ledger records.
- Identity provider.
- KMS and secrets.
- Application configuration.
- Infrastructure definitions.
- External integration state.

---

## 14. Identity, Authentication, and Authorization Technologies

### 14.1 OpenID Connect

OpenID Connect (OIDC) is the proposed identity federation and authentication standard.

The final identity provider remains a human decision.

### 14.2 OAuth 2.0 Authorization Code with PKCE

Browser-based authentication must use an appropriate Authorization Code flow with PKCE.

The implementation must include:

- Server-side PKCE verifier handling in the Backend-for-Frontend (BFF), where applicable.
- State validation.
- Nonce validation.
- Exact redirect URI validation.
- Secure session cookies.
- CSRF protections.
- Safe logout and session invalidation.

Cookies using the `__Host-` prefix must satisfy the browser's requirements, including `Secure`, `Path=/`, and no `Domain` attribute.

### 14.3 Token validation

The API Gateway must validate access tokens, including:

- Approved signing algorithm.
- Rejection of `none`.
- Issuer.
- Audience.
- Expiration.
- Not-before time.
- Subject.
- Key identifier and signing-key validity.
- Relevant scopes and authorization context.

Key rotation, revocation, clock-skew handling, and refresh-token controls must be specified and tested.

### 14.4 Identity ownership

The identity provider owns authentication credentials, MFA, and identity-provider sessions.

Worklexx owns application-level organization membership and authorization decisions.

The API Gateway validates access tokens and enforces applicable request policies.

Authentication and application authorization must remain distinct.

---

## 15. Security, Encryption, and Secrets Management

### 15.1 Key Management Service

A managed Key Management Service (KMS) is the proposed direction for cryptographic key management.

The final provider and configuration remain subject to architecture approval.

### 15.2 Key lifecycle

The key-management design must define:

- Key generation.
- Key ownership.
- Key versioning.
- Key access policies.
- Envelope encryption.
- Data Encryption Key (DEK) handling.
- Key Encryption Key (KEK) handling.
- Rotation.
- Re-encryption.
- Revocation.
- Recovery.
- Audit.
- Separation of duties.

Using KMS does not automatically rotate every application secret, token, database password, or encryption key.

### 15.3 Secrets management

Secrets must not be stored in source code, committed configuration files, public logs, or frontend bundles.

The final secrets-management solution must support:

- Restricted access.
- Secret versioning.
- Rotation.
- Revocation.
- Audit.
- Environment separation.
- Controlled delivery to workloads.

### 15.4 Transport and application security

The implementation must enforce appropriate TLS configurations, secure headers, access controls, secure cookie settings, input validation, and safe error handling.

Security testing must include authentication, authorization, tenant isolation, API abuse, and integration boundaries.

---

## 16. Payment and Financial Technologies

### 16.1 Payment providers

Paystack and Stripe are potential payment integrations, subject to business, geographic, regulatory, commercial, and technical validation.

Their security mechanisms and feature sets must not be assumed to be interchangeable.

### 16.2 Webhook verification

Paystack webhook verification must use its provider-specific signature procedure, including HMAC-SHA512 verification against the raw request body.

Stripe webhook verification must use its own provider-specific verification mechanism.

For both providers, the implementation must include:

- Raw request-body preservation.
- Signature verification.
- Secure event persistence.
- Provider event identifiers.
- Duplicate-event protection.
- Idempotent processing.
- Controlled acknowledgement.
- Failure recovery.
- Reconciliation.

A browser redirect or payment-success page is not proof that a payment has been completed.

### 16.3 Financial authority

`billing-ledger` is the authoritative financial service.

It must enforce:

- Double-entry accounting.
- Atomic transaction posting.
- Currency consistency.
- Immutable posted entries.
- Controlled draft-to-posted transitions.
- Compensating entries for reversals.
- Provider-scoped idempotency.
- Reconciliation.

AI agents must not directly write financial balances or ledger entries.

### 16.4 Credit and usage lifecycle

The proposed lifecycle is:

`Estimate → Policy/Balance Check → Atomic Reservation → Task Authorization → Usage Measurement → Settlement → Release or Compensation`

The actual implementation must preserve transactional consistency and prevent duplicate charging or unauthorized credit use.

---

## 17. Monitoring, Logging, and Observability

The platform requires centralized observability across frontend applications, backend services, agents, workflows, integrations, and infrastructure.

The implementation should evaluate established observability standards and compatible tools for:

- Structured logging.
- Metrics.
- Distributed tracing.
- Error reporting.
- Workflow visibility.
- Infrastructure monitoring.
- Security events.
- Audit events.

OpenTelemetry is a proposed instrumentation standard.

Observability must not expose secrets, private prompts, credentials, payment data, or unnecessary personal information.

Audit records must be protected against unauthorized alteration.

Operational logs and legally significant audit records must have distinct retention and access policies.

---

## 18. CI/CD, Source Control, and Software Supply Chain

### 18.1 Git and GitHub

Git is the source-control technology.

GitHub is the proposed repository hosting and collaboration platform.

The repository strategy must be approved before introducing new branches or changing the existing branch structure.

The current repository's `main` branch must not be silently replaced by a proposed branching convention.

### 18.2 CI/CD

GitHub Actions is a candidate CI/CD automation platform.

Pipelines must enforce appropriate controls, including:

- Dependency installation from lockfiles.
- Automated tests.
- Static analysis.
- Security scanning.
- Build validation.
- Artifact generation.
- Artifact integrity checks.
- Deployment authorization.
- Audit logging.

### 18.3 Protected GitHub operations

Protected repository operations must follow the independently defined GATE-04 authorization process.

Production deployment must follow GATE-03.

These are separate approval gates.

Neither a successful CI pipeline nor a repository administrator role automatically authorizes every protected operation.

### 18.4 Software supply-chain security

The platform should implement:

- Dependency pinning.
- Lockfiles.
- Software Bill of Materials (SBOM).
- Vulnerability scanning.
- Artifact provenance.
- Signed artifacts where supported.
- Secret scanning.
- Controlled dependency updates.
- Reviewable exceptions.

Security scanners reduce risk but cannot guarantee that software contains zero vulnerabilities.

---

## 19. Package and Dependency Management

### 19.1 JavaScript and TypeScript

Use a consistent package manager and committed lockfile across the relevant repositories.

The final package manager and version must be documented.

### 19.2 Python

Use a consistent Python dependency-management and lockfile strategy.

The selected tool must support reproducible installation, dependency resolution, environment management, and CI integration.

### 19.3 Dependency policy

All production dependencies must have:

- Documented purpose.
- Supported version.
- License information.
- Security review.
- Upgrade policy.
- Compatibility validation.
- Removal procedure.

A dependency's availability in a public package registry does not automatically make it trustworthy.

Package-age restrictions alone are not sufficient security controls. Package integrity, provenance, version pinning, vulnerability status, and controlled exceptions must also be considered.

---

## 20. File, Media, and Multimodal Technologies

### 20.1 Multimodal processing

The `multimodal-service` owns multimodal processing responsibilities.

It may coordinate supported text, image, audio, video, and document-processing workflows through approved provider integrations and internal modules.

### 20.2 File lifecycle

Uploaded content must enter a pending or quarantined state until applicable validation and malware-scanning requirements have been satisfied.

A successful upload must not automatically mean the file is safe for processing or sharing.

### 20.3 Media processing controls

Required controls include:

- File-type validation.
- MIME-type verification.
- File-size limits.
- Malware scanning.
- Safe parsing.
- Content-specific validation.
- Access control.
- Tenant isolation.
- Retention and deletion.
- Processing limits.
- Audit records.

### 20.4 Storage separation

Use PostgreSQL for structured metadata and transactional records.

Use object storage for large binary content and generated artifacts.

Use Git for version-controlled source code and appropriate text-based project assets.

These storage systems must have separate access controls and retention rules.

---

## 21. Advertising Technology

### 21.1 AdTech service

`adtech-service` is the dedicated backend service for advertising operations.

Advertising functions must not be mixed indiscriminately with confidential AI execution and project data.

### 21.2 Data separation

The advertising system must not access:

- Private prompts.
- Private source code.
- Uploaded confidential documents.
- Credentials.
- Private workflow content.
- Confidential user activity.

Any approved advertising measurement must use explicitly authorized data with documented purpose, access control, and retention.

### 21.3 Enforcement

Advertising data separation must be enforced through suitable:

- Service identities.
- Database schemas and roles.
- Network boundaries.
- API permissions.
- Data minimization.
- Auditing.
- Privacy controls.

A written policy alone is insufficient.

---

## 22. Performance, Reliability, and Cost Validation

Technology performance claims must be supported by reproducible measurements.

The validation process must distinguish:

- Target performance.
- Measured performance.
- Test environment.
- Workload.
- Concurrency.
- Data volume.
- Test duration.
- Observed limitations.

### 22.1 Required performance tests

The platform should test:

- API response latency.
- Database query performance.
- Tenant-filtered vector search.
- Workflow execution throughput.
- Model-provider latency.
- Media-processing throughput.
- Sandbox startup and execution time.
- Concurrent user workloads.
- Real-time event delivery.
- Recovery and reconciliation performance.

### 22.2 Cost validation

Cost modelling must include:

- Frontend hosting.
- Compute.
- Database.
- Storage.
- Network egress.
- AI model usage.
- Workflow orchestration.
- Observability.
- Security tooling.
- Backup and disaster recovery.
- Support and operational staffing.

Vendor prices, service limits, and commercial terms must be checked against current authoritative documentation before procurement or final approval.

### 22.3 No unsupported guarantees

The architecture must not promise:

- Zero cold starts.
- Zero downtime.
- Exactly-once external side effects.
- Unlimited scalability.
- Complete sandbox escape prevention.
- Zero vulnerabilities.
- Guaranteed model availability.
- Fixed latency without workload evidence.

---

## 23. Technology Validation and Proof-of-Concept Requirements

The following validation activities are required before the corresponding production technology decisions are finalized.

| ID | Technology or capability | Required validation |
|---|---|---|
| POC-01 | Frontend framework and hosting | Runtime compatibility, authentication, deployment, limits and cost |
| POC-02 | FastAPI and backend runtime | Version compatibility, concurrency, API performance and security |
| POC-03 | PostgreSQL and SQLAlchemy | Transactions, migrations, connection pooling and operational behavior |
| POC-04 | PostgreSQL RLS | Adversarial tenant-isolation and privilege-escalation tests |
| POC-05 | pgvector | Dimensions, indexes, recall, latency, storage and tenant filtering |
| POC-06 | Temporal | Workflow durability, retries, recovery, upgrades, backup and restore |
| POC-07 | Redis | Cache isolation, failure behavior, invalidation and ephemeral messaging |
| POC-08 | GKE and gVisor | Isolation, egress, metadata protection, scaling, startup, cleanup and cost |
| POC-09 | Object storage | Tenant isolation, encryption, scanning, versioning, retention and recovery |
| POC-10 | KMS and secrets | Key lifecycle, rotation, revocation, recovery and audit |
| POC-11 | AI model routing | Provider compatibility, capability selection, fallback, cost and observability |
| POC-12 | Payment integrations | Webhook verification, idempotency, failure recovery and reconciliation |
| POC-13 | Observability | Trace correlation, sensitive-data exclusion, alerting and retention |
| POC-14 | CI/CD | Reproducible builds, artifact integrity, scanning and approval enforcement |
| POC-15 | Disaster recovery | Full-platform restoration and measured RPO/RTO |

A proof of concept must produce recorded evidence, including the test environment, procedure, results, limitations, and recommendation.

Passing one proof of concept does not automatically approve unrelated architecture decisions.

---

## 24. Technology Decisions Pending

The following decisions require explicit human review and approval.

| Decision ID | Decision | Current status |
|---|---|---|
| HD-01 | Managed external identity provider versus internally operated identity platform | **Approved — managed approach (2026-11-19)** |
| HD-02 | Temporal Cloud versus self-hosted Temporal | **Approved — Temporal Cloud preferred initial approach, conditional on POC-06 and due diligence (2026-11-19)** |
| HD-03 | Primary and disaster-recovery regions | Pending |
| HD-04 | Final deployment topology for the six backend service units | Pending |
| HD-05 | Confirmation of PostgreSQL and pgvector support for the required 3,072-dimensional vector workload | Pending POC |
| HD-06 | Final platform RPO and RTO targets | Pending |
| HD-07 | Risk acceptance authority and delegated responsibilities | Pending |
| HD-08 | Final definitions and approval authority for GATE-01 through GATE-06 | Pending |

Additional technology decisions must be documented through the Architecture Decision Record (ADR) process.

No proposed technology in this document may be treated as finally approved merely because it appears in a technology table.

---

## 25. Technology Governance and Change Management

Technology changes must follow a controlled review process.

Any proposed change affecting a technology's:

- Security properties.
- Service boundary.
- Data ownership.
- Deployment topology.
- Tenant isolation.
- Financial authority.
- Approval workflow.
- External dependency.
- Operational cost.
- Recovery capability.

must undergo architecture review.

Material changes must be reflected in relevant architecture documents and ADRs.

Dependency upgrades must be evaluated for compatibility, vulnerabilities, licensing, performance, and migration impact.

Technology substitutions must not silently create additional backend deployables or weaken the six-service architecture.

---

## 26. Phase 0 Execution Boundary

Phase 0 is a documentation and architecture-definition phase.

The work covered by this document does not authorize:

- Application implementation.
- Database schema creation.
- Database migrations.
- Infrastructure provisioning.
- Cloud deployment.
- Payment-provider activation.
- Production identity configuration.
- Sandbox deployment.
- Production AI model activation.
- Protected GitHub operations.
- Phase 1 execution.

Any implementation work requires the appropriate separate authorization.

GATE-03 production deployment approval and GATE-04 protected GitHub operations approval remain independent controls.

---

## 27. Related Documents

This document must be reviewed alongside:

1. `ARCHITECTURE_OVERVIEW.md`
2. `SYSTEM_ARCHITECTURE.md`
3. `REPOSITORY_STRUCTURE.md`
4. `AGENT_ECOSYSTEM.md`
5. `SERVICE_BOUNDARIES.md`
6. `DATABASE_ARCHITECTURE.md`
7. `SECURITY_ARCHITECTURE.md`
8. `DEPLOYMENT_ARCHITECTURE.md`
9. `DEVELOPMENT_ROADMAP.md`
10. `RISK_REGISTER.md`
11. `ADR_REGISTER.md`
12. `PHASE_0_INSPECTION_REPORT.md`
13. `TESTING_STRATEGY.md`
14. `MONITORING_AND_OBSERVABILITY.md`
15. `COST_AND_SCALABILITY.md`

The final review must identify and resolve material inconsistencies between these documents.

---

## 28. Final Status

**Document Status:** Revised Architecture Blueprint — Awaiting Final Human Review and Approval.

The technology architecture establishes a proposed and controlled technical direction for the Worklexx AI Software Factory.

It defines the technology responsibilities, six backend deployable boundaries, technology validation requirements, security expectations, and unresolved decisions.

It does not claim that every proposed technology has passed a proof of concept or received final procurement and implementation approval.

**Phase 0 remains subject to final document verification and explicit Project Owner approval. Phase 1 is not authorized by this document.**