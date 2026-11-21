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

**Proposed tool direction:** Alembic for SQLAlchemy-compatible schema migrations, subject to per-service compatibility and operational validation.

Under approved HD-REP-06, each of the six deployable backend services maintains its own migration scripts, independent migration history/metadata, immutable migration identifiers and checksums, and migration lifecycle. Each migration identity is restricted to its service-owned schema; runtime credentials have no DDL privileges. A shared PostgreSQL cluster remains possible and does not imply shared migration ownership.

Migration practices must include ordered and reproducible upgrades, expand-and-contract changes where practicable, migration locks and bounded timeouts, transactional execution where supported, compatibility across rolling application versions, integrity checks, and documented rollback or forward-fix/recovery plans. A code rollback does not automatically reverse a schema/data migration.

Cross-service schema changes require explicit coordination of affected services, contracts, consumers, compatibility windows and deployment order. Prefer authorised APIs, events and controlled read models to direct cross-service schema coupling. Destructive migrations are subject to GATE-05; production migration execution also requires applicable GATE-03 authorization. These are architectural requirements only; no migration tool installation, credential creation, pipeline activation or migration execution is authorised.

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

**Approved preferred initial approach:** pgvector within PostgreSQL. A separate vector-database deployment is not proposed at this stage.

This is an architectural direction, not approval of a specific extension version, index configuration, embedding model, or production deployment. POC-05 remains mandatory before implementation relies on a selected configuration.

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

A 3,072-dimensional vector is not a platform-wide requirement. Dimensions must be model- and use-case-specific, with incompatible models or dimensions kept in separate logical indexes unless a compatibility strategy is validated. POC-05 must test 3,072-dimensional workloads where required by a selected model, including relevant full-precision and half-precision options and measured retrieval-quality trade-offs.

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

The approved branching direction under HD-REP-03 is trunk-based development with protected `main` and short-lived branches. GitHub protection configuration and implementation remain unauthorised pending separate approvals.

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

**Approved architectural direction — HD-REP-01 (2026-11-19):** Use pnpm workspaces as the JavaScript/TypeScript package manager and workspace mechanism, with Turborepo for dependency-aware task orchestration and caching in the platform monorepo.

The pnpm lockfile must be committed. Package-manager and build-tool versions must be pinned through repository-controlled configuration. Workspace boundaries, package ownership, dependency policies, build ordering, tests, versioning, and release behavior must be explicit. CI must validate affected workspaces and retain required repository-wide security and compatibility checks.

Turborepo caching must be configured so that secrets, private artifacts, tenant data, and other protected material are not exposed through shared or remote caches. Tool versions, compatibility, licensing, security posture, cache behavior, and CI integration require validation before implementation.

This selection does not collapse independent applications or backend services into one deployment unit. It does not authorise installation, lockfile creation, CI/CD modification, repository restructuring, or Phase 1.

### 19.2 Python

**Approved architectural direction — HD-REP-02 (2026-11-19):** Adopt Astral uv as the preferred Python dependency-management, lockfile, and project-environment tool for Worklexx AI Software Factory.

Python backend services and shared packages remain independently managed projects with explicit dependency ownership. Each independently managed service project must maintain its own `pyproject.toml` and committed `uv.lock`, together with a documented Python-version policy and appropriate dependency groups. Shared Python packages must define their own project metadata and development/test dependencies; a package's development lockfile must not be treated as the dependency lockfile of every consuming service.

Do not require a single Python workspace across all six backend services. Any future workspace grouping requires technical justification and separate approval. Workspace grouping does not provide runtime isolation; runtime isolation remains the responsibility of appropriate processes, containers, service boundaries, and permissions.

CI must use lockfile-enforced installation (for example, `uv sync --locked`) and fail when project metadata and the committed lockfile are inconsistent. Pin the uv tool version and control supported Python runtime versions through repository-managed configuration. Exclude local virtual environments and caches from source control.

Dependency governance must include approved package-source and private-index controls, review of direct URL and Git dependencies, vulnerability scanning, package integrity and provenance review, controlled dependency updates, license review, and SBOM generation for release artifacts. Credentials must be supplied through approved secrets-management mechanisms and must never be embedded in project metadata or lockfiles.

Validate Windows developer workflows, Linux CI, Python 3.12 compatibility, deterministic resolution, service-independent lockfiles, Docker integration, private package sources, security scanning, SBOM generation, upgrades, and rollback before implementation.

### 19.3 Cross-language contracts

Python and TypeScript components must communicate through explicit, versioned API and event contracts. OpenAPI and event-schema definitions should be used where applicable, with generation and compatibility tests where practical.

### 19.4 Dependency policy

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
| HD-03 | Primary and disaster-recovery regions | **Approved — AWS primary Cape Town (`af-south-1`), Ireland DR (`eu-west-1`), and Temporal Cloud Ireland (`aws-eu-west-1`), architectural direction only, subject to validation (2026-11-19)** |
| HD-04 | Final deployment topology for the six backend service units | Pending |
| HD-05 | Initial vector-storage approach and model-specific embedding-dimension policy | **Approved — PostgreSQL/pgvector preferred initially; dimensions model/use-case specific; POC-05 required (2026-11-19)** |
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

## HD-03 — Approved Regional Architecture Direction (2026-11-19)

- **Cloud provider:** Amazon Web Services (AWS).
- **Primary hosting region:** South Africa (Cape Town), AWS region `af-south-1`.
- **Disaster-recovery region:** Ireland (Dublin), AWS region `eu-west-1`.
- **Temporal Cloud preferred region:** Ireland, Temporal Cloud region identifier `aws-eu-west-1`, subject to POC-06 and due diligence.
- **Scope:** Architectural direction only. No subscription, contract, payment, account configuration, resource provisioning, or production deployment is authorised.
- **Conditions:** Complete legal and privacy assessment (including Nigerian data-protection and cross-border-transfer requirements), security review, service availability and compatibility validation, POC and operational readiness, cost review, and recovery design/testing. Confirm the required data-residency, backup, retention, encryption, key-management, monitoring and incident-response controls.
- **Lagos Local Zone:** Any use is optional and separately evaluated; it is not treated as an independent AWS Region or as proof of full Nigerian data residency.
- **Reversibility:** Region and provider selection may be revisited based on validation evidence or requirements changes.


## 29. Approved Branching and Release Direction — HD-REP-03

**Approved architectural direction (2026-11-20):** Adopt trunk-based development using `main` as the permanent protected integration branch and short-lived feature, fix, and hotfix branches. Require pull requests, automated validation, and independent human review; prohibit direct pushes, force pushes, and routine protection bypasses. Prefer squash merges. Independently version the six backend deployable services and five frontend applications, with component-specific release tags, release notes, artifact provenance, and compatibility controls. Use Semantic Versioning where applicable. Release branches are temporary and justified only for stabilisation, certification, coordinated releases, or maintenance. Hotfixes must be reconciled into `main`.

Release automation/tool selection, CI/CD implementation, GitHub protection configuration, actual release creation and deployment require further validation and approvals. This decision does not authorise Phase 1, implementation, production deployment, or provisioning.


## HD-REP-04 — Approved Repository Ownership and Governance Direction (2026-11-20)

The Project Owner approved the organisation-owned repository model when Worklexx's GitHub organisation is established and repository transfer is separately authorised. Until then, the repository remains in its current location. Access shall follow least privilege, with minimum necessary administrators, scoped collaborators and automation, no shared credentials, and periodic access review. Protect `main` from direct routine pushes, force pushes and deletion; require PRs, independent human review, designated CODEOWNERS review for critical paths and mandatory CI checks once implemented. Prefer squash merging and dismiss stale approvals after material changes. AI agents cannot approve their own changes, accept risks, modify governance settings, grant access or bypass protections. Project Owner remains sole initial governance approval authority, subject to HD-08. This is architectural approval only and does not authorise organisation creation, repository transfer, settings changes, invitations, CI/CD, production deployment or Phase 1.

## 30. Repository Backup and Recovery Architecture — HD-REP-07

**Approved architectural direction (2026-11-20):** Use layered, provider-independent backups for Factory source, Worklexx-managed customer repositories, customer-managed repositories within authorised scope, and supporting development records. Protect Git objects/history/refs and Git LFS separately from repository metadata, release/build artifacts, project mappings, audit records and integration configuration. Git clone alone is not a complete backup. Secrets and credentials are restored through approved secrets/key-management processes.

Use independently controlled off-site copies and at least one immutable or deletion-resistant copy; separate backup identities and key custody from ordinary repository administration; encrypt in transit and at rest; enforce least privilege, audit, tenant/project isolation, integrity verification and controlled retention. Worklexx-managed repository backup responsibilities are governed by customer agreements. Customer-managed provider-account and provider-side recovery remain the customer's responsibility; Worklexx retains only authorised, technically supported copies.

Initial backup/retention objectives: daily full plus incremental/event-based capture for Factory source; continuous/frequent Git replication and daily metadata backup for Worklexx-managed projects; customer-managed synchronisation only within authorised scope. Proposed retention is 90 days for daily copies and 12 months for monthly copies, subject to legal, contractual and cost review. Proposed RPO/RTO: critical Factory source/release-control records ≤15 minutes/4 hours; active customer source ≤1 hour/8 hours; metadata/development records ≤4 hours/24 hours; historical/noncritical artifacts ≤24 hours/48 hours. These are unverified objectives, not SLAs, and must be validated against HD-06 and POC-15.

Restoration must use incident declaration, containment, verified recovery-point selection, isolated restoration, integrity/security/tenant checks, authorised reconnection, reconciliation and retained evidence. Validate Git/LFS, metadata, artifacts, tenant isolation, deletion/ransomware, provider portability, key recovery, retention/legal holds, export and measured RPO/RTO. No backup configuration, provisioning, spending, repository permission changes, customer connections, restore execution, CI/CD or production implementation is authorised by the decision.

## 20. HD-REP-08 — Build Integrity and Software Supply-Chain Governance

The approved architectural direction is a policy-controlled, least-privilege, verifiable automation architecture. GitHub Actions remains a candidate automation platform; HD-REP-08 does not activate workflows or select a final CI/CD implementation.

Workflow permissions default to read-only. Write permissions must be narrowly scoped to the job that requires them. Prefer short-lived credentials, pin third-party actions to immutable commit SHAs, review workflow definitions before activation, protect workflow files, and isolate untrusted pull-request execution from trusted release workflows and secrets. Validation, build, signing, publication and deployment are separate stages and permissions.

Preserve the approved pnpm/Turborepo and uv decisions. Enforce lockfiles and pinned tooling; verify dependencies; scan direct and transitive dependencies for vulnerabilities and licence issues; scan for secrets; apply SAST and applicable DAST; review dependency changes; and generate machine-readable SBOMs using SPDX or CycloneDX. Build environments and caches must be isolated by trust boundary, tenant and project. Untrusted code must not access Factory secrets, signing credentials or unrelated customer data.

Trusted artifacts require cryptographic checksums, integrity verification and traceable provenance linking repository/project, source commit, dependency/lockfile state, build tools, workflow identity, execution, SBOM and artifact. Evaluate SLSA provenance and Sigstore subject to POC, security, compatibility, operational and cost validation. Signing keys must be held in approved key-management systems, not source repositories or ordinary workflow configuration.

The six deployable backend units remain unchanged. The sandbox-runner does not acquire unrestricted build-release or publication authority. Factory source, Worklexx-managed customer repositories and customer-managed repositories remain distinct security boundaries under HD-REP-05.

**Governance:** A successful CI run is not release approval; artifact verification is not publication authority; publication is not production deployment authority. Apply HD-08 and HD-07. No workflow activation, repository settings change, credentials/signing-key creation, paid service, infrastructure provisioning, production build, publication, release or deployment is authorised by this architectural decision.


## Repository Observability and Audit Technology Requirements — HD-REP-09

The architecture is provider-independent; no specific SIEM, logging vendor, telemetry product or storage service is selected or authorised. Candidate technologies must be evaluated against event ingestion reliability, versioned schema support, identity and tenant context, correlation, query and alert capabilities, tamper-evident/append-only retention, cryptographic integrity, encryption, access separation, legal holds, export/portability, backup/recovery, cost and provider limitations.

The logical capability set comprises event producers, collection/normalisation, privacy/redaction, protected audit storage, security-event correlation/detection, alerting/investigation and governed response. It is a logical architecture, not an additional backend deployable; the six deployable service units remain unchanged. Event schemas and collection interfaces should be provider-independent where practicable. Operational telemetry must remain distinguishable from authoritative security audit evidence.

No product selection, subscription, infrastructure provisioning, telemetry activation, credentials or production integration is authorised by HD-REP-09. Selection and adoption require evaluation, POC-REP-09-01 through POC-REP-09-12, applicable HD-08 approvals and separate implementation authorisation.


## HD-REP-10 — Customer Project Lifecycle, Portability and Exit Architecture

**Approved architectural direction (2026-11-20):** implement a customer-centred lifecycle and portability control plane consistent with HD-REP-05. The logical project lifecycle must represent creation, provisioning, active use, suspension, archival, export/transfer, disconnection, deletion pending and deletion, with authenticated and auditable state transitions. The project identity, customer/tenant mapping, owner/controller, hosting mode and repository mapping must remain explicit and immutable where identity is concerned.

The architecture must support both Worklexx-managed private repositories and customer-managed supported Git hosting integrations. Ownership and hosting administration are separate concepts. Customer project content, generated code, Worklexx proprietary platform/reusable components and third-party licensed materials must be separately identifiable under the applicable customer agreements and licences.

Provide customer-scoped source and history export, including Git refs and Git LFS where used, relevant documentation, non-secret configuration templates, dependency manifests/lockfiles, entitled artifacts, SBOM/provenance, metadata and customer-entitled audit records. Export packages require inventories, format/version metadata and integrity checksums. Exclude secrets and private keys; use secure credential re-establishment. Validate independent import and portability. Transfer, disconnection and deletion require distinct workflows and approvals.

Retention, archival, legal hold and deletion must be policy-driven by record class and validated against applicable legal, regulatory and contractual obligations. Do not assume a universal retention duration or grace period. Backup expiry and restore controls must prevent deleted data from silently returning to active systems. Entitlement expiry may restrict premium features but must not automatically destroy customer assets.

Agents may prepare inventories, exports and recommendations but cannot transfer ownership, alter visibility, disconnect integrations, revoke customer access, delete repositories/data/backups, change retention, override legal holds or approve exit actions. Apply HD-07 and HD-08, including GATE-02/03/04/05/06 where applicable.

**Required validation:** POC-REP-10-01 through POC-REP-10-15. Do not treat any unexecuted validation as passed. RSK-30 covers ownership disputes, incomplete portability and improper suspension, transfer or deletion; formal risk scores remain pending.

**Authorisation boundary:** This is an architectural decision only. No customer provisioning, live account/repository connection, OAuth installation, transfer, live project suspension/deletion, production migration, backup/retention configuration, infrastructure, paid services, GitHub permission/settings changes, CI/CD activation, production deployment or Phase 1 is authorised.



## Customer Data Governance and Privacy Technology Requirements — HD-REP-11

HD-REP-11 was approved as an architectural direction on 2026-11-20. It is provider-independent: no specific privacy platform, data-loss-prevention product, consent-management tool, key-management service, SIEM or external AI provider is selected or authorised by this decision.

Technology candidates and designs must support a common Public/Internal/Confidential/Restricted classification; data inventory and purpose records; tenant/project-scoped authorisation across all six backend deployables; PostgreSQL RLS and pgvector tenant-aware retrieval; encryption in transit/at rest; controlled key and secret lifecycle; privacy-aware audit and redaction; retention/legal holds; customer-scoped export and deletion; and end-to-end traceability of derived multimodal data.

External model providers and subprocessors require due diligence and documented terms for permitted purpose, data categories, processing/storage locations, retention, human access, onward processors, model-training use, deletion and incident notification. Customer data must not be used for general-purpose provider training or improvement unless a specific lawful and authorised arrangement permits it. No provider receives unrestricted database or repository credentials.

The data scope includes prompts, source code, documents, images, audio, video, transcripts, embeddings, metadata, outputs and derived copies. Data residency and cross-border controls must assess applicable jurisdictions and transfer safeguards; the approved HD-03 Cape Town/Ireland and Temporal Ireland architecture is not itself legal transfer approval. No universal retention duration is selected. Privacy rights workflows and deletion must cover indexes, vectors, caches, jobs, replicas and backups, aligned with HD-REP-07/10. Agents must receive task-scoped least privilege and treat external content as untrusted; prompt injection cannot alter policy or access boundaries.

**Required validation:** POC-REP-11-01 through POC-REP-11-15. Add RSK-31 for customer data exposure, unlawful processing and privacy control failure; risk scores remain pending formal assessment. Apply HD-07/HD-08, including GATE-01/02/03/04/05/06 as relevant.

**Authorisation boundary:** No live personal/customer-data processing, external model/subprocessor/customer integration, infrastructure or database provisioning/modification, credentials or keys, paid service, production monitoring/workflow activation, migration, deletion/restoration, deployment or Phase 1 is authorised. Architecture approval and documentation do not constitute implementation approval.


## Identity, Authentication and Authorisation Technology Requirements — HD-REP-12

HD-REP-12 was approved as an architectural direction on 2026-11-20. Retain HD-01's managed identity-provider approach, but do not select or connect a specific provider through this decision. Worklexx retains application-level authorisation and each service enforces its own tenant-, project- and resource-scoped permissions.

The architecture should support standards-based identity integration and federation, including OIDC and appropriate SSO protocols where validated; MFA and phishing-resistant authentication/passkeys where supported; secure session and account-recovery lifecycle; and provider-independent mapping to Worklexx user, organisation and project identities. Protocol and provider choices require compatibility, security, privacy, regional, contractual and commercial due diligence.

Use a policy model combining RBAC for organisation/project role assignments, ABAC for contextual conditions, and explicit resource-level permissions for sensitive operations. Policy enforcement must be server-side. Browser/mobile state, API gateway token validation or a role claim alone is not sufficient authorisation. Services must establish trusted tenant/project context and deny access when current authority cannot be established.

The six approved backend deployables retain distinct service identities. Agent invocations require distinct, scoped, time-limited delegated identities. Prefer short-lived workload credentials and narrowly scoped service-to-service permissions. API keys/tokens, where required, need ownership, purpose, scope, expiry where practicable, rotation, revocation and audit. Do not expose privileged credentials in frontend bundles, customer project source or ordinary logs.

Identity and access technology must integrate with the existing PostgreSQL/pgvector, Temporal, repository, storage, build and audit boundaries without introducing a seventh backend deployable. Revocation and policy changes must propagate to sessions, services, database/RLS, vector retrieval, storage, Git integrations, workflows, agent contexts, build environments, artifacts, caches and external integrations. Define measurable propagation objectives through POC rather than assuming instantaneous invalidation.

No specific IAM product, policy engine, SSO vendor, MFA product, secrets platform or paid service is selected. Evaluate interoperability, provider portability, tenant isolation, policy consistency, auditability, recovery, regional processing, subprocessor terms, cost and operational burden. Align identity telemetry and protected audit records with HD-REP-09 and identity-data minimisation with HD-REP-11.

**Validation:** POC-REP-12-01 through POC-REP-12-20 must be completed before operational reliance. Architectural approval does not authorise provider selection/connection, account creation, OAuth installation, credentials, paid services, infrastructure, schema changes, production identity activation or Phase 1. Applicable HD-08 approvals remain mandatory.


## HD-REP-13 — AI Agent Security, Delegation, Execution Boundaries and Human Oversight Governance (Approved 2026-11-20)

Adopt permission-controlled, policy-enforced, sandboxed and auditable agent execution for the 23 logical agent modules. This decision does not add a backend deployable or alter the approved six-deployable architecture. Agent intelligence is not authority: each agent has a distinct identity and bounded task, tenant/project, tool, data and time scope; versioned policies; resource limits; audit attribution; and revocation controls.

Five conceptual permission tiers: Tier 0 Observe; Tier 1 Prepare; Tier 2 Execute within controlled scope; Tier 3 Consequential action subject to independent approval and applicable control; Tier 4 prohibited authority (including self-approval and governance bypass). Tool permissions remain granular: inspect, write, PR creation, review, approval, merge, permission changes, deletion and transfer are separate capabilities. The tool-control boundary validates identity/scope, inputs and destinations, classification, policy and approval, then executes, verifies and audits.

Code execution uses an appropriately isolated sandbox within the approved sandbox-runner boundary: restricted networking, resource/time limits, filesystem/process isolation, credential separation, tenant/project-specific caches and artifact handling, and cleanup. Untrusted documents, source, web content, prompts and tool results are data—not policy or authority—and prompt injection must not override permissions, governance or gates. Delegation is task/time bounded, depth-limited, attributable, revocable and cannot expand the initiating authority.

Agent context and memory are scoped, classified, minimised, governed and tenant/project isolated. Outputs require independent verification appropriate to their risk; verification does not substitute for human approvals required by HD-08. Control retries, loops, concurrency, idempotency, resource/cost limits, cancellation and safe failure. Protected audit and monitoring align with HD-REP-09; privacy and data boundaries with HD-REP-11; identity and delegation with HD-REP-12; execution isolation and supply-chain controls with HD-REP-08; customer lifecycle with HD-REP-10.

Validation requirements: POC-REP-13-01 through POC-REP-13-24 (unexecuted) cover agent identity/scope, least privilege, tool authorization, policy enforcement, tier separation, gate binding, sandbox isolation, network/credential restrictions, resource limits, prompt-injection resistance, untrusted content, tenant/project isolation, delegation depth/authority, context/memory privacy, output verification, human oversight, audit attribution, revocation, concurrent actions/races, loops/retries/cancellation, failure/recovery, cost controls, abuse scenarios and end-to-end governance bypass attempts.

Add RSK-33 — AI Agent Misuse, Unsafe Execution, Privilege Escalation and Governance Bypass. Formal likelihood, impact, inherent and residual scores remain pending assessment; proposed controls do not reduce residual risk until implemented and evidenced.

Project Owner remains sole initial risk acceptance and approval authority under HD-07/HD-08. Applicable gates remain mandatory. This is architecture/documentation approval only: no agent execution in production, sandbox provisioning, external integrations, live customer data, credentials, CI/CD activation, GitHub configuration, database changes, paid services, production deployment or Phase 1 is authorised.

Agent orchestration, tool policy evaluation, delegation, context/memory control, verification and audit are platform capabilities within existing deployables. Sandbox execution remains within sandbox-runner. No specific agent framework, policy engine, model provider, sandbox technology or new service is selected by this decision; evaluate portability, isolation, latency, cost, observability and integration risk during POCs.


## HD-REP-14 — API Contracts, Inter-Service Communication and Integration Governance (Approved 2026-11-20)

Adopt contract-first, versioned and service-owned interface governance. Standards directions: OpenAPI 3.1 (or validated compatible later version) for HTTP APIs, JSON Schema for structured payloads and AsyncAPI for event-driven interfaces where appropriate. These are standards directions only; no specific contract registry, broker, API gateway, validation product, SDK generator or integration platform is selected.

Contracts must cover synchronous requests/responses, asynchronous events, Temporal workflows/activities, agent-tool calls, data schemas and external APIs/webhooks. Require explicit ownership, versioning, consumer inventory, schema validation, compatibility analysis, safe error semantics, authentication/authorization, tenant/project boundaries, correlation, bounded retry/timeout, idempotency where needed, audit and privacy controls. Preserve independent service release versions and do not equate contract versions with service release versions. Breaking changes require compatibility plans and applicable approval. Durable Temporal workflow replay/state compatibility receives dedicated treatment. External interfaces require provider due diligence, webhook authenticity/replay controls, rate limits, destination restrictions and cross-border/privacy review. No tooling or infrastructure implementation is authorised.


## HD-REP-15 — API Gateway and Edge Security Governance (Approved 2026-11-20)

Adopt a policy-enforced API gateway as the controlled external ingress for approved public interfaces. Responsibilities include route registration and routing to the six approved backend deployables, TLS/edge-security integration, token validation and trusted identity-context propagation, policy checks, layered rate limiting/quotas, request validation, safe errors, correlation/audit, API version routing and bounded failure controls. No seventh deployable, gateway vendor, WAF provider, API management product or infrastructure topology is selected.

The gateway does not replace service-level authorization, tenant/project isolation, agent tool permissions or HD-08 approval gates. Internal service calls independently authenticate and authorize under HD-REP-14. Receiving services remain authoritative for resource access. Do not expose internal administration, database, Temporal or sandbox-management interfaces publicly. Client-supplied tenant/project identifiers are not proof of authority.

Apply layered limits by client, principal, tenant, project, operation, network, concurrency and payload/bandwidth; distinguish request quotas from spending and agent execution budgets. Apply stricter controls to multimodal, sandbox and model-intensive operations. Require secure TLS/certificate lifecycle, WAF/DDoS capability, strict request validation, SSRF/destination controls, secure CORS, webhook authenticity/replay, upload validation and sensitive-data redaction. Use bounded timeouts/retries, idempotency, backpressure and circuit-breaking. API versioning follows HD-REP-14 compatibility/deprecation policy. All gateway changes require attributable review and audit. No tooling or infrastructure implementation is authorised.


## HD-REP-16 — Secrets, Cryptography and API Security Technology Direction (Approved 2026-11-20)

Adopt technology-neutral requirements for controlled secrets management, cryptographic key management, workload identity, certificate lifecycle, API credential protection and secure service communication. Do not select a vendor, KMS/HSM, certificate authority, secrets product or paid security service in this decision.

Require short-lived scoped credentials where practicable; secure token validation and revocation; centralised secret lifecycle management; separate encryption, token-signing, artifact-signing, webhook and transport keys; protected private-key storage; key versioning/rotation/recovery/audit; and no secrets in source, frontend bundles, Git history, ordinary logs or build artifacts. Prefer authenticated encryption for application data and modern TLS (TLS 1.2 minimum compatibility; TLS 1.3 preferred where supported). Algorithm and parameter choices require formal standards review; no custom cryptography.

Services independently authenticate and authorise internal calls. The gateway does not replace receiving-service authorization. Frontend applications contain no privileged backend credentials. Customer project and build credentials remain isolated. Agents cannot retrieve unrelated secret values or change key policy. Integrate secret scanning, redaction, integrity verification and compromise monitoring with HD-REP-08/09/11/12/13/14/15.

Require POC-REP-16-01 through -26 before operational reliance; all remain unexecuted. Add RSK-36; formal risk scoring pending. No provider selection, credential/key provisioning, infrastructure, paid tools, integration or production activation is authorised.



## Application Security and Secure Development Lifecycle — HD-REP-17 (Approved 2026-11-20)

Adopt a vendor-independent application security engineering baseline across all frontend applications, backend deployables, shared packages, agent modules and generated customer projects. Use risk-based threat modelling, secure coding standards, independent code review, SAST, software composition analysis, secret scanning, DAST where appropriate, API/frontend security tests, configuration assessment and manual security review. Independent penetration testing may be required for high-risk releases or integrations, subject to explicit scope and authorisation.

OWASP ASVS and applicable OWASP Top 10 guidance are candidate assessment references; confirm current versions and applicability during implementation planning. Maintain dependency and runtime support review, vulnerability tracking, remediation verification and SBOM/provenance alignment with HD-REP-08. Automated findings require contextual triage; scanner success does not establish security.

No specific security scanner, SAST/DAST platform, penetration-testing provider, commercial product, subscription or vendor is selected by this decision. No tools are installed or activated. Proposed vulnerability remediation objectives and exception rules are recorded in HD-REP-17 in ADR_REGISTER.md. All POC-REP-17 validations remain unexecuted. No CI/CD activation, infrastructure, spending, source changes or production deployment is authorised.

---

## HD-REP-18 — Configuration and Environment Management (Approved 2026-11-21)

Adopt environment-isolated, schema-validated, versioned configuration governance across the five frontend applications, six backend deployables and 23 logical agent modules. Four logical environments are required: Development, Testing, Staging and Production; this is not a physical hosting decision. Configuration is classified Public, Internal, Confidential or Restricted. Non-secret settings should use controlled configuration-as-code with ownership, validation, review, versioning, integrity, drift detection and applied-state traceability. Secrets are managed only through the separately approved HD-REP-16 boundary and referenced, never embedded. Frontend bundles contain no privileged credentials. Feature flags require ownership, environment scope, safe defaults and audit; they cannot grant authority or disable mandatory controls. Deployment configuration is part of the software supply chain and must link to source, artifact, configuration version, deployment identity and approval evidence. Customer-project configuration remains tenant/project isolated and portable within entitlement. No vendor or product is selected. No implementation, environment provisioning, configuration store, credentials, GitHub settings, CI/CD activation or deployment is authorised. Require POC-REP-18-01 through -24; all unexecuted.

## HD-REP-19 — Application Deployment, Release Promotion and Rollback Governance

Technology direction: provider-independent, policy-controlled deployment and release-promotion capabilities; no deployment platform, CI/CD vendor, orchestrator, registry, signing service or commercial product is selected by this decision.

Preserve five frontend applications, six backend deployables and 23 logical agent modules. Each independently deployable component has its own release identity. Generated customer projects retain their separate repository and deployment boundaries.

Use Development, Testing, Staging and Production as logical environments under HD-REP-18. Prefer immutable artifact promotion across environments, with environment-specific configuration references. Trace every release from source commit through build identity, artifact checksum, provenance, SBOM, validation, configuration version, approval and deployment outcome.

Separate build, release, deployment and recovery identities/permissions. Production deployment requires explicit GATE-03 authorization and all other applicable HD-08 gates. Deployment strategies may include blue-green, canary, rolling and maintenance-window deployment, selected according to component state, compatibility, risk and recovery capability.

Post-deployment verification and rollback/forward-fix decisions must preserve database, ledger, workflow, credential-revocation, deletion, tenant-isolation and audit integrity. Code rollback must never be assumed to reverse data/schema changes. Require POC-REP-19-01 through -26; all unexecuted. No tool/vendor selection, CI/CD activation, infrastructure, environment provisioning, artifact publication, release, deployment, credential change or Phase 1 is authorised.



## HD-REP-20 — Production Operations and Reliability Architecture (Approved 2026-11-21)

The technology architecture must support service-specific SLIs/SLOs, operational metrics, structured and privacy-aware logs, distributed traces, security/business-integrity signals, incident evidence, capacity measurements and recovery verification. These are capability requirements, not a selection of a monitoring, SIEM, paging, incident-management or APM vendor.

Proposed planning availability objectives (unverified; not SLAs): core API/essential access and agent orchestration/durable workflows 99.9%; billing/ledger 99.95%; multimodal and sandbox 99.5%; analytics/noncritical derived services 99.0%. Service objectives must also measure correctness and integrity, particularly ledger reconciliation, idempotency, tenant isolation and workflow durability. Error budgets inform reliability prioritisation but do not grant authority to bypass gates.

Operational telemetry must correlate metrics, logs and traces while respecting HD-REP-09 audit integrity and HD-REP-11 minimisation/redaction. Monitor all six backend deployables and critical dependencies, including PostgreSQL/pgvector, Temporal, storage, identity, external providers, backups and regional recovery. Do not log secrets or unnecessary sensitive customer content.

The operational architecture must support incident lifecycle/severity management, role assignment, escalation, authorised containment, post-incident reviews, capacity forecasting, controlled runbooks, dependency records and continuity exercises. Preserve HD-06 recovery objectives and verify them through tests before claiming operational capability. No specific monitoring, alerting, paging, incident-management, SIEM or observability technology is selected by HD-REP-20.

Require POC-REP-20-01 through -28; all unexecuted. This decision does not activate monitoring, select or procure tools, create infrastructure, establish staffing/on-call commitments, establish SLAs, change production configuration, or authorise production deployment or Phase 1.



## HD-REP-21 — Customer Support, Knowledge and Communications Capabilities

The target architecture requires logical capabilities for support request intake and ticket lifecycle, customer identity/authority verification, case classification and routing, support communications, complaints management, governed knowledge-base publishing/search, service-status notices, customer feedback and auditable escalation. Candidate channels include in-app help, customer portal, email, technical documentation and approved urgent escalation routes.

No ticketing/help-desk, CRM, knowledge-base, messaging, email-delivery, translation, status-page or customer-communications vendor/tool is selected. Do not add a seventh backend deployable: support functions must be allocated within existing approved service boundaries through a separately documented design. Any future external provider must undergo HD-REP-11/14/16/18/20 due diligence, data-location and subprocessor review, access-scope assessment, contract review and applicable HD-08 approvals.

AI support may use approved knowledge retrieval, classification, summarisation, response drafting and bounded troubleshooting, subject to HD-REP-13, tenant isolation, human review and auditable tool permissions. Support data must not be placed in unapproved external model contexts. All support and knowledge capabilities remain architectural requirements only; no tooling, accounts, integrations, procurement, production activation or Phase 1 is authorised.



## HD-REP-22 — Onboarding, Organisation and Commercial Entitlement Technology Direction (Approved 2026-11-21)

Add logical platform capabilities for individual and organisation registration, organisation profiles and verification, membership/invitations, personal and organisational workspaces, account lifecycle, subscription records, entitlement evaluation, usage metering, customer consumption visibility and commercial/payment integration boundaries. These are capabilities allocated within the existing six backend deployables; HD-REP-22 adds no seventh service and selects no vendor.

Keep identity authentication under the managed identity direction in HD-01 and Worklexx application authorisation under HD-REP-12. The identity provider authenticates a person; Worklexx remains authoritative for organisation membership, workspace/project permissions, ownership and entitlement policy. A person may belong to multiple organisations without shared data or implicit authority. Role labels are configurable and must resolve to explicit server-side permissions.

Provide an entitlement evaluation capability that can be called by relevant services. Entitlement records should be versioned, scoped to an individual/organisation/workspace/project as appropriate, time-bounded and auditable. They may describe features, agent permissions/allowances, project/member capacity, API requests, model/agent consumption, multimodal processing, storage, sandbox resources and support. Subscription status and entitlement state are separate. Do not treat frontend feature flags, gateway rate limits or payment-provider redirects as authoritative entitlement/payment evidence.

Usage metering should use unique, attributable, idempotent events with customer scope, feature/service, unit/quantity, timestamp and entitlement/pricing-version references. Separate usage metering from invoices, provider payment events and the billing-ledger system. Maintain customer-facing consumption and allowance visibility. Financial posting, reconciliation, refunds and adjustments remain within the existing billing-ledger boundary and HD-08 controls.

Payment/subscription integration remains provider-independent. No identity, payment gateway, subscription-management, tax, invoicing, CRM, email, messaging or verification vendor is selected. Any future provider requires security, privacy, data-location, subprocessor, contractual, operational, financial and exit assessment under HD-REP-11/14/16/18/20 and applicable gates.

Do not introduce a seventh backend deployable. Logical capabilities must be allocated to the six approved deployables through a separately validated service ownership design; the billing-ledger remains authoritative for financial records. Require POC-REP-22-01 through -30; all remain unexecuted. No technology procurement, provider connection, schema change, credential, production activation, commercial plan/pricing commitment or Phase 1 is authorised.


## HD-REP-23 — Customer project technology and development-environment governance

The Factory must support project-specific, compatibility-validated technology choices rather than impose one universal customer stack. Candidate catalogue entries may include React/Next.js, Vue, Angular, React Native, Flutter, Python/FastAPI, Node.js, Java/Spring, PostgreSQL, MySQL, pgvector-enabled PostgreSQL, Redis-compatible systems, Pytest, Playwright and Vitest. These are illustrative candidates only: this decision does not mandate or select a new customer technology, provider, editor, hosting platform, container runtime or infrastructure service.

Technology recommendations should consider project requirements, runtime/framework compatibility, developer skills, ecosystem maturity, security maintenance, licensing, portability, performance, scalability, hosting constraints and operating cost. Before initialisation, validate language/runtime, framework and package compatibility; database and API compatibility; OS/build/test requirements; licence constraints; known vulnerabilities; and resource constraints. Unsupported or incompatible combinations must be surfaced before project initialisation.

Template catalogue metadata must identify template owner, provenance, version, supported languages/frameworks/runtimes, dependencies, licence, compatibility, security review state, tests, documentation, known limitations and retirement status. Distinguish Worklexx Verified, Worklexx Experimental, Customer Managed and Third Party. Verification is not a guarantee of generated-project security or production readiness. Template updates must not silently modify customer projects.

Generated projects should use appropriate language-specific package tools, pinned dependencies and lockfiles where supported. Record package sources, direct/transitive dependency information where available, licence and vulnerability results, and SBOM/provenance where appropriate. Do not force Factory monorepo tooling decisions onto every customer project; existing Factory-specific uv/pnpm decisions remain unchanged.

Development environments align with HD-REP-18's four logical environments: Development, Testing, Staging and Production. Future environment modes may include browser-based, local, containerised, approved remote, CI-based and controlled sandbox. No product/provider is selected. Environment definitions identify project, type, runtime, dependencies, resource limits, network policy, storage and secret references, configuration version, access policy and lifecycle. Production secrets/data must not be inherited by lower environments by default. Isolate filesystem, processes, network, credentials, caches, temporary data and artifacts by tenant/project/trust boundary. The sandbox-runner remains within the six approved deployables.

Project configuration is versioned and schema-validated, classified Public/Internal/Confidential/Restricted and linked to approved secret references rather than secret values. No secrets in source, frontend bundles, Git history, images, ordinary logs or customer repositories. Project readiness evidence distinguishes generation, dependency resolution, build, tests, security checks, deployment readiness and production approval.

Require POC-REP-23-01 through -32; all unexecuted. No technology procurement, provider selection/connection, editor subscription, environment provisioning, customer source processing, credential creation, CI/CD activation, production build/deployment or Phase 1 is authorised.


## HD-REP-24 — Governed AI Development and Validation Requirements

The Factory development capability must support specification-driven code generation and modification, project-specific toolchains, reproducible dependency resolution, automated quality checks, test execution, security analysis, artifact integrity and provenance. Technology choices must remain compatible with each customer project's approved stack; no universal language, framework, editor, model provider, code-generation framework or commercial scanning product is selected by this decision.

Execute untrusted or customer-project code only in isolated, policy-controlled workspaces associated with sandbox-runner and bounded by tenant/project/task identity, filesystem/process/network controls, resource/time limits and task-scoped credentials. Preserve the six-deployable topology. Use project-appropriate formatters, linters, type checkers, unit/integration/contract/end-to-end tests and applicable SAST/SCA/secret/licence checks. Record tool versions, dependency lockfiles, test outcomes, SBOM and provenance where applicable. No tool installation, environment provisioning, CI/CD activation, provider connection or expenditure is authorised.
