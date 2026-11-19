# WORKLEXX AI SOFTWARE FACTORY
# DEPLOYMENT ARCHITECTURE

## Document Metadata

| Field | Value |
|---|---|
| Document ID | WLX-ARCH-009 |
| Document Title | Deployment Architecture |
| Platform | Worklexx AI Software Factory |
| Document Version | 1.0 |
| Document Status | Phase 0 Architecture Baseline — Proposed |
| Classification | Internal — Architecture and Engineering |
| Repository | https://github.com/samuel1599361/worklexx-ai-software-factory |
| Repository Branch | main |
| Document Path | docs/phase-0/DEPLOYMENT_ARCHITECTURE.md |
| Architecture Phase | Phase 0 — Architecture and Specification |
| Related Documents | WLX-ARCH-001 through WLX-ARCH-008 |
| Approval Status | Pending formal Project Owner approval |
| Implementation Status | Not implemented or independently verified by this document |

---

## 1. Purpose

This document defines the proposed deployment architecture for the Worklexx AI Software Factory.

It establishes the intended deployment topology, application hosting boundaries, backend runtime architecture, infrastructure responsibilities, environment separation, network security, scaling approach, deployment controls, monitoring, backup, disaster recovery, and operational governance.

The architecture is intended to support a secure, scalable, multi-tenant AI software development platform that uses permission-controlled agents to assist with software planning, development, testing, deployment, maintenance, and related workflows.

This document provides an architectural specification. It does not establish that infrastructure has been provisioned, services deployed, integrations completed, or operational controls tested.

The deployment architecture must remain consistent with:

- The six-deployable-backend-service architecture.
- The five-frontend-application architecture.
- The 23-agent logical ecosystem.
- The central API Gateway and identity-provider separation.
- The deterministic authorization and approval model.
- The PostgreSQL tenant-isolation architecture.
- The security requirements defined in WLX-ARCH-008.
- The Phase 0 restriction against implementation without authorization.

---

## 2. Deployment Architecture Objectives

The deployment architecture has the following objectives:

1. Provide a reliable hosting model for all five frontend applications.
2. Deploy the six defined backend deployable units without introducing undocumented additional deployable services.
3. Support independent scaling of frontend and backend workloads where justified.
4. Enforce separation between development, staging, and production environments.
5. Protect tenant data, source code, uploaded files, credentials, and generated artifacts.
6. Support secure communication between frontend applications, backend services, databases, and external providers.
7. Provide durable workflow execution and recovery mechanisms.
8. Support controlled deployment and rollback procedures.
9. Enforce human approval before production deployment and protected GitHub operations.
10. Provide monitoring, logging, alerting, backup, and disaster recovery capabilities.
11. Support future regional expansion without requiring an uncontrolled redesign.
12. Maintain traceability between source code, build artifacts, approvals, and deployed releases.

---

## 3. Deployment Architecture Principles

The following principles govern the proposed deployment architecture.

### 3.1 Separation of Concerns

Frontend delivery, backend application processing, workflow orchestration, data persistence, sandbox execution, and financial processing must have distinct deployment responsibilities.

### 3.2 Six-Service Deployment Boundary

The proposed backend deployment baseline consists of six deployable service units:

1. `api-gateway`
2. `agent-orchestrator`
3. `multimodal-service`
4. `sandbox-runner`
5. `billing-ledger`
6. `adtech-service`

The 23 AI agents are logical modules managed within the platform's agent architecture. They are not 23 independently deployed microservices.

The AI Gateway and model-routing capability are logical capabilities within the proposed deployment topology. They must not become an undocumented seventh deployable backend service.

Any proposed change to the six-service boundary requires an architecture decision and formal approval.

### 3.3 Environment Isolation

Development, staging, and production must have separate security boundaries and appropriately isolated data, credentials, workloads, and deployment permissions.

### 3.4 Least Privilege

Every service, workload, human operator, and deployment identity must receive only the permissions necessary for its assigned responsibilities.

### 3.5 Infrastructure as Code

Infrastructure configuration should be version-controlled, reviewed, reproducible, and deployed through controlled pipelines.

### 3.6 Immutable Release Artifacts

Production deployments should use identifiable, versioned, immutable build artifacts rather than untracked source changes or mutable deployment packages.

### 3.7 Human-Controlled Sensitive Actions

AI agents may recommend or prepare deployment actions. They must not independently authorize production deployment or protected GitHub operations.

### 3.8 Observable Operations

Deployment, execution, failure, recovery, approval, and security events must be observable and auditable.

### 3.9 No Unverified Availability Claims

High availability, scalability, disaster recovery, and security must be demonstrated through implementation and testing. Architectural descriptions alone do not establish these properties.

---

## 4. Deployment Scope

This architecture covers the proposed deployment of:

- Five frontend applications.
- Six backend service units.
- Identity and authentication integration.
- API Gateway and service-to-service communication.
- AI agent orchestration.
- Multimodal processing.
- Isolated code execution.
- Billing and ledger processing.
- Advertising technology services.
- PostgreSQL and supporting data services.
- Durable workflow infrastructure.
- Object and artifact storage.
- Caching and messaging.
- Observability and security monitoring.
- CI/CD pipelines.
- Backup and disaster recovery.
- External model, payment, and other approved integrations.

This document does not authorize:

- Cloud resource creation.
- DNS changes.
- Domain registration or transfer.
- Production deployment.
- Database provisioning or migrations.
- Git branch creation.
- Git commits or pushes.
- Payment-provider activation.
- Production credentials or secret creation.
- Deployment approval.
- Changes to an existing production environment.

---

## 5. Deployment Topology Overview

The proposed platform uses a distributed application architecture.

The high-level deployment layers are:

1. User access and frontend delivery.
2. Edge protection and application ingress.
3. API Gateway and authentication integration.
4. Backend application services.
5. AI agent and workflow orchestration.
6. Data persistence and supporting infrastructure.
7. External providers and integrations.
8. Monitoring, security, and operational management.

### 5.1 Logical Deployment Flow

```text
USERS
  |
  +--------------------------------------------------+
  |                                                  |
  v                                                  v
FRONTEND APPLICATIONS                         IDENTITY PROVIDER
  |                                                  |
  |                                           Authentication
  |                                           MFA / OIDC
  |                                                  |
  +-------------------------+------------------------+
                            |
                            v
                   EDGE / INGRESS SECURITY
                            |
                            v
                      API GATEWAY
                            |
          +-----------------+------------------+
          |                 |                  |
          v                 v                  v
   AGENT ORCHESTRATOR  MULTIMODAL SERVICE  BILLING-LEDGER
          |                 |                  |
          |                 |                  |
          v                 v                  v
     WORKFLOW ENGINE    OBJECT STORAGE      PAYMENT PROVIDERS
          |
          +--------------------------+
          |                          |
          v                          v
    SANDBOX RUNNER              ADTECH SERVICE
          |
          v
  ISOLATED EXECUTION ENVIRONMENT

          +--------------------------------------+
          | SHARED SUPPORTING INFRASTRUCTURE     |
          |                                      |
          | PostgreSQL / pgvector                |
          | Redis                                |
          | Durable workflow persistence         |
          | Object and artifact storage          |
          | KMS / Secrets Management              |
          | Logs / Metrics / Traces               |
          | Backup / Recovery                     |
          +--------------------------------------+
```

This diagram describes logical relationships. It does not prescribe an already-provisioned network topology or imply that every service shares the same database schema, runtime, or security identity.

---

## 6. Frontend Deployment Architecture

The platform has five frontend applications.

| Application | Proposed Domain | Primary Responsibility |
|---|---|---|
| Marketing Website | worklexx.ai | Public information, product presentation, and acquisition |
| Main Application | app.worklexx.ai | Authenticated user workspace and platform interface |
| Video Application | video.worklexx.ai | Video-related capabilities and workflows |
| Image Application | images.worklexx.ai | Image-related capabilities and workflows |
| Documentation Application | docs.worklexx.ai | Product, technical, and user documentation |

The API Gateway uses a separate domain:

`api.worklexx.ai`

The architecture therefore has five frontend application domains and one API domain.

### 6.1 Frontend Hosting

Vercel is the proposed frontend hosting platform.

The final hosting arrangement must be validated against:

- Framework compatibility.
- Build and runtime requirements.
- Server-side rendering requirements.
- API route requirements.
- Function execution limits.
- Regional availability.
- Environment-variable management.
- Custom-domain configuration.
- Security and deployment controls.
- Hosting plan and cost.

The use of Vercel must not be interpreted as a requirement that every frontend operation executes at the Edge.

CDN delivery, edge caching, server-side rendering, Edge Functions, and Node.js serverless functions are different execution models. Each application must use a runtime appropriate to its actual requirements.

### 6.2 Frontend Deployment Isolation

Each frontend should have:

- Its own application configuration.
- Explicit environment-specific settings.
- Controlled deployment permissions.
- Appropriate domain and routing configuration.
- Independent build and deployment status.
- Security headers and browser policies.
- Error monitoring.
- A documented rollback procedure.

Shared frontend libraries may be used, but one application's deployment must not unintentionally change another application's production behavior.

### 6.3 Frontend Security

Frontend security must include:

- HTTPS.
- Appropriate Content Security Policy.
- Secure cookie handling where applicable.
- Cross-origin restrictions.
- CSRF protection for cookie-authenticated operations.
- Runtime input validation.
- Safe rendering of untrusted content.
- Protection against token leakage.
- Dependency and supply-chain controls.
- No exposure of server-side secrets in browser bundles.

Frontend applications must not be treated as trusted authorization boundaries.

All sensitive authorization decisions must be enforced by trusted backend services.

### 6.4 Frontend-to-Backend Communication

Authenticated application requests should use the approved identity and session architecture.

A Backend-for-Frontend pattern may be adopted where it materially improves token security and session management.

The final decision must be consistent with WLX-ARCH-008.

Frontend applications must not receive unrestricted access to internal services or databases.

---

## 7. Domain and DNS Architecture

The proposed domain structure is:

| Domain | Purpose |
|---|---|
| worklexx.ai | Public marketing website |
| app.worklexx.ai | Main authenticated application |
| video.worklexx.ai | Video application |
| images.worklexx.ai | Image application |
| docs.worklexx.ai | Documentation application |
| api.worklexx.ai | API Gateway |

### 7.1 DNS Responsibilities

DNS configuration must support:

- Domain ownership verification.
- Appropriate application routing.
- TLS certificate validation.
- DNS record integrity.
- Controlled record changes.
- Protection against unauthorized DNS modification.
- Documented recovery procedures.

### 7.2 Domain Separation

The frontend domains and API domain must have clearly defined responsibilities.

CORS must explicitly allow approved origins.

Wildcard CORS permissions must not be used as a substitute for an origin allowlist.

### 7.3 Domain Approval

Domain creation, DNS modification, certificate activation, and production routing changes require authorization from the designated infrastructure owner.

No DNS changes are authorized by this document.

---

## 8. Backend Deployment Architecture

The backend consists of six deployable service units.

| Service | Deployment Responsibility |
|---|---|
| `api-gateway` | Public API ingress, request validation, routing, and gateway-level policy enforcement |
| `agent-orchestrator` | Agent coordination, task lifecycle, and workflow orchestration |
| `multimodal-service` | Image, video, audio, and other multimodal processing |
| `sandbox-runner` | Isolated execution of generated or user-supplied code |
| `billing-ledger` | Financial transactions, credit accounting, reservations, settlement, and reconciliation |
| `adtech-service` | Advertising workflows and approved advertising data processing |

### 8.1 Independent Deployment

Each service should have an independently identifiable build artifact and deployment configuration.

Independent deployment must not create uncontrolled interface incompatibility.

Service contracts must be versioned and tested.

### 8.2 Internal Service Communication

Internal communication must use authenticated service identities and authorized network paths.

Controls should include:

- TLS or an appropriately secured service-mesh transport.
- Workload identity.
- Service-level authorization.
- Request timeouts.
- Bounded retries.
- Circuit breakers where appropriate.
- Request correlation identifiers.
- Idempotency for sensitive operations.
- Rate and resource limits.

Network location alone must not be treated as proof of trust.

### 8.3 Service Discovery

Service discovery should use stable internal service names or an approved service-discovery mechanism.

Internal service addresses must not be exposed unnecessarily to public clients.

### 8.4 Deployment Dependencies

Deployment sequencing must consider:

- Database compatibility.
- Schema version compatibility.
- API contract compatibility.
- Message and event compatibility.
- Workflow compatibility.
- Secret and configuration availability.
- Backward compatibility.
- Rollback feasibility.

A service must not be deployed merely because its build succeeds.

---

## 9. AI Agent and Workflow Deployment

The 23-agent ecosystem is a logical application architecture.

It is coordinated through the `agent-orchestrator` and supporting services.

### 9.1 Agent Deployment Model

Agents should be implemented as controlled logical modules, with explicit:

- Agent identity.
- Responsibilities.
- Tool permissions.
- Input and output contracts.
- Execution limits.
- Tenant context.
- Audit requirements.
- Approval requirements.
- Failure-handling behavior.

Agents must not automatically become independently deployed microservices.

### 9.2 Workflow Orchestration

Temporal is the proposed durable workflow orchestration technology.

A proof of concept must validate:

- Supported deployment model.
- Database and persistence requirements.
- Workflow durability.
- Worker registration.
- Task queue behavior.
- Retry and timeout behavior.
- Workflow versioning.
- Cancellation and compensation.
- Monitoring and alerting.
- Backup and restore.
- Operational cost.

The choice between Temporal Cloud and self-hosted Temporal remains unresolved.

### 9.3 Workflow Lifecycle

The proposed task lifecycle is:

```text
Created
   |
   v
Validating
   |
   v
Queued
   |
   v
Running
   |
   +----------------------+
   |                      |
   v                      v
AwaitingApproval       Failed
   |
   v
Completed

Other permitted terminal state: Cancelled
```

The actual workflow implementation must define valid transitions, retry behavior, cancellation semantics, and recovery procedures.

### 9.4 Execution Guarantees

The architecture must assume that workflow activities and external operations may execute more than once.

Exactly-once external side effects must not be assumed.

The implementation should use:

- Durable workflow state.
- Idempotency keys.
- Unique event identifiers.
- Bounded retries.
- Timeouts.
- Outbox and inbox patterns where appropriate.
- Compensation.
- Dead-letter handling.
- Manual recovery.
- Reconciliation.

Redis Pub/Sub is an ephemeral messaging mechanism. It must not be used as the sole durable authority for workflow state, approvals, financial records, or business-critical events.

### 9.5 Human Approval Boundaries

The following approval meanings are established:

- GATE-03: Production deployment approval.
- GATE-04: Protected GitHub operations approval.

These approvals must be separate and independently bound to the requested action, project or tenant, relevant artifact or commit digest, environment, authorization context, expiry, and audit record.

Material changes must invalidate an approval where the approved action or artifact has changed.

GATE-05 is intended to govern designated destructive or materially consequential database operations, including destructive schema migrations and incompatible data transformations. GATE-06 is intended to govern designated consequential external integrations and live-account actions with material external, financial, operational, or customer impact. Their complete scope, exceptions, approval authority, enforcement, and evidence requirements remain subject to explicit Project Owner confirmation. GATE-01 and GATE-02 remain pending formal definition.

No AI agent may bypass the required approval process.

---

## 10. Cloud Infrastructure Architecture

Google Cloud Platform is the proposed backend infrastructure provider.

The proposed infrastructure may use:

- Google Kubernetes Engine.
- Cloud SQL for PostgreSQL.
- Cloud Storage.
- Cloud KMS.
- Secret Manager.
- Cloud Logging.
- Cloud Monitoring.
- Artifact Registry.
- Cloud Build or another approved CI/CD platform.
- Cloud Armor where applicable.

These are proposed infrastructure components, not confirmed deployed resources.

### 10.1 Infrastructure Selection

Each infrastructure component must be evaluated against:

- Security.
- Reliability.
- Regional availability.
- Operational complexity.
- Cost.
- Scalability.
- Compliance.
- Recovery capability.
- Integration compatibility.
- Vendor dependency.

### 10.2 Infrastructure Ownership

Every production resource must have:

- An identified owner.
- A documented purpose.
- An environment assignment.
- Access-control policies.
- Cost attribution.
- Monitoring.
- Backup or recovery requirements where applicable.
- Lifecycle and decommissioning procedures.

### 10.3 Infrastructure Changes

Infrastructure changes must be reviewed and approved before application.

Infrastructure as Code should be used where practical.

Manual production changes must be restricted, logged, and reconciled with the approved infrastructure configuration.

---

## 11. Container and Kubernetes Deployment

Google Kubernetes Engine (GKE) is the proposed backend container orchestration platform.

### 11.1 Containerization

Backend services should be packaged as controlled container images.

Images should:

- Use approved base images.
- Be versioned and identifiable.
- Avoid unnecessary packages.
- Run as non-root where possible.
- Use read-only filesystems where appropriate.
- Avoid embedded credentials.
- Be scanned for vulnerabilities.
- Have an associated software bill of materials.
- Be traceable to source revisions and build pipelines.

### 11.2 Kubernetes Workload Separation

Workloads should be separated according to their security and operational requirements.

Potential separation dimensions include:

- Environment.
- Service identity.
- Namespace.
- Workload class.
- Resource requirements.
- Network policy.
- Tenant execution context.

Namespaces alone do not provide complete security isolation.

### 11.3 Kubernetes Security

The implementation should evaluate:

- Kubernetes RBAC.
- Workload identity.
- Pod security controls.
- Network policies.
- Admission policies.
- Image provenance.
- Secret access.
- Node security.
- Cluster upgrade procedures.
- Audit logging.
- Resource quotas.
- Runtime threat detection.

### 11.4 GKE Operational Validation

Before production adoption, validate:

- Cluster configuration.
- Regional and zonal architecture.
- Node-pool design.
- Autoscaling.
- Capacity management.
- Upgrade strategy.
- Workload disruption behavior.
- Network configuration.
- Storage behavior.
- Backup and restore.
- Cost and utilization.
- Security monitoring.

GKE adoption remains subject to an operational proof of concept and formal approval.

---

## 12. Sandbox Deployment Architecture

The `sandbox-runner` is a high-risk deployment component because it executes generated and potentially untrusted code.

### 12.1 Isolation Requirements

Sandbox execution must be isolated from:

- Host operating systems.
- Other tenants.
- Production credentials.
- Internal administrative services.
- Financial services.
- Databases not explicitly required for the task.
- Unrelated application workloads.
- Cloud metadata services.
- Unauthorized network destinations.

### 12.2 Proposed Runtime

gVisor on GKE is a proposed sandbox isolation approach.

Its suitability must be demonstrated through a proof of concept.

The evaluation should include:

- System-call compatibility.
- Workload compatibility.
- Runtime performance.
- Startup latency.
- Resource overhead.
- Filesystem isolation.
- Process isolation.
- Network isolation.
- Security testing.
- Escape testing.
- Operational monitoring.
- Cost.

gVisor must not be described as eliminating all container escape or isolation risks.

MicroVM-based execution may be evaluated as an alternative or additional isolation layer.

### 12.3 Sandbox Network Controls

Sandbox workloads should use default-deny network egress.

Explicit controls must address:

- IPv4.
- IPv6.
- DNS.
- Cloud metadata endpoints.
- Internal service addresses.
- Private network ranges.
- Unapproved external destinations.
- DNS rebinding.
- Proxy bypass.
- Redirect behavior.

### 12.4 Resource Controls

Each execution should have enforceable limits for:

- CPU.
- Memory.
- Storage.
- Process count.
- Execution time.
- Network usage.
- Output size.
- Concurrent tasks.

### 12.5 Credential Controls

Production credentials must never be mounted into general-purpose sandbox workloads.

Any temporary credential required for a task must be narrowly scoped, short-lived, auditable, and revocable.

### 12.6 Sandbox Lifecycle

Sandbox instances should be disposable.

The lifecycle must include:

1. Approved execution request.
2. Isolated environment allocation.
3. Policy and resource configuration.
4. Controlled code and input delivery.
5. Execution monitoring.
6. Output collection and validation.
7. Credential revocation.
8. Environment destruction.
9. Audit recording.

The destruction of a sandbox must not be assumed to delete all artifacts or logs unless the relevant storage and retention controls are independently implemented.

---

## 13. Database Deployment Architecture

PostgreSQL is the primary relational database technology.

pgvector is the proposed vector-search extension.

Cloud SQL for PostgreSQL is a candidate managed database hosting option.

### 13.1 Database Deployment Responsibilities

The database architecture must support:

- Tenant and organization records.
- User and access metadata.
- Project and workspace data.
- Workflow and task metadata.
- Agent configuration and execution records.
- Usage and billing metadata.
- Financial ledger records.
- Audit records.
- Vector embeddings and metadata.
- Other approved application records.

### 13.2 Database Separation

The final database topology must distinguish logical data ownership and security boundaries.

The six deployable services do not automatically require six independent PostgreSQL clusters.

However, shared infrastructure must not imply unrestricted access to shared schemas or tables.

Each service should receive a narrowly scoped database role and access only the data necessary for its responsibilities.

### 13.3 Tenant Isolation

Tenant isolation must be enforced at the data-access layer.

The design should include:

- PostgreSQL Row-Level Security.
- Restricted database roles.
- FORCE ROW LEVEL SECURITY where appropriate.
- Transaction-scoped tenant context.
- Tenant-aware foreign keys.
- Composite keys where required.
- Controlled connection-pool behavior.
- Protection against tenant-context leakage.
- Adversarial cross-tenant isolation testing.

A session variable such as `app.current_tenant_id` is not, by itself, a complete security control.

The implementation must ensure that tenant context cannot be manipulated by an untrusted client or reused incorrectly across pooled connections.

### 13.4 Database Deployment Changes

Database changes must use reviewed, version-controlled migrations.

Production migrations must have:

- An approved migration plan.
- Compatibility analysis.
- Backup or recovery preparation.
- Execution authorization.
- Verification procedures.
- Rollback or forward-recovery strategy.

No database migration is authorized by this Phase 0 document.

### 13.5 Financial Database Protection

The `billing-ledger` is the authoritative financial processing service.

It must enforce:

- Atomic financial transactions.
- Double-entry accounting principles.
- Currency-aware transaction integrity.
- Immutable posted ledger entries.
- Controlled draft-to-posted transitions.
- Compensating entries.
- Provider-scoped idempotency.
- Reconciliation.
- Restricted write permissions.

AI agents must not have direct authority to write, alter, or delete posted financial ledger records.

### 13.6 Vector Database Validation

pgvector adoption must be validated through a proof of concept.

The evaluation must include:

- Extension version.
- Supported embedding dimensions.
- Index types.
- Exact versus approximate search.
- Recall and relevance.
- Query latency.
- Storage requirements.
- Write performance.
- Concurrent workloads.
- Tenant filtering.
- Metadata filtering.
- Re-embedding strategy.

The proposed 3072-dimensional embedding requirement remains subject to confirmation against the selected embedding models and PostgreSQL configuration.

---

## 14. Object and Artifact Storage Deployment

Object storage is required for large and binary assets that should not be stored directly in ordinary relational database records.

Google Cloud Storage is a proposed object-storage option.

### 14.1 Storage Responsibilities

Object storage may contain:

- User-uploaded files.
- Images.
- Video.
- Audio.
- Generated artifacts.
- Build outputs.
- Test reports.
- Software packages.
- Exported documents.
- Other approved binary content.

Git repositories remain the authoritative source for version-controlled source code.

PostgreSQL remains authoritative for transactional and relational records.

Object storage is not a replacement for either.

### 14.2 Storage Security

The implementation must provide:

- Tenant-aware object authorization.
- Encryption at rest.
- Secure transport.
- Access logging.
- Versioning where appropriate.
- Retention controls.
- Controlled deletion.
- Backup or recovery arrangements.
- Egress controls.
- Storage lifecycle policies.

### 14.3 Upload Processing

New uploads must default to a pending or quarantined state.

The processing pipeline should include:

1. Upload authorization.
2. File-type and size validation.
3. Quarantine.
4. Malware scanning.
5. Content inspection where appropriate.
6. Safe processing in an isolated environment.
7. Approval for authorized use.
8. Controlled storage and retrieval.

A signed URL provides time-limited access to an object. It does not replace authorization checks, tenant validation, or content security controls.

### 14.4 Artifact Integrity

Generated artifacts should be traceable to:

- Source revision.
- Build identity.
- Build timestamp.
- Pipeline execution.
- Dependency information.
- Artifact digest.
- Approval record where applicable.

---

## 15. Redis and Caching Deployment

Redis is a proposed supporting infrastructure component.

Potential responsibilities include:

- Short-lived caching.
- Ephemeral messaging.
- Rate-limiting support.
- Temporary coordination.
- Session-related data where approved.
- Performance optimization.

### 15.1 Cache Security

Cache design must account for:

- Tenant separation.
- Key naming and namespace controls.
- Data sensitivity.
- Expiration.
- Invalidation.
- Access control.
- Encryption and transport.
- Cache poisoning.
- Stale data.
- Operational recovery.

Sensitive data must not be cached without an approved purpose, access model, retention period, and protection strategy.

### 15.2 Redis Pub/Sub Limitation

Redis Pub/Sub is not a durable workflow or transaction system.

Messages may be lost when subscribers are unavailable.

Critical business events, financial records, approval decisions, and workflow state must be persisted through an appropriate durable mechanism.

### 15.3 Cache Failure Behavior

The application must define its behavior when Redis is unavailable.

A cache failure must not result in unauthorized access, incorrect financial processing, or loss of authoritative workflow state.

---

## 16. Identity and Authentication Deployment

The platform requires a separately managed identity-provider integration.

The identity provider is responsible for authentication, credential handling, MFA, and its own authentication sessions.

Worklexx is responsible for application-level authorization, tenant membership, project permissions, agent permissions, and workflow access.

### 16.1 Identity Provider

The final identity-provider selection remains a human decision.

The architecture must support an approved OIDC implementation.

### 16.2 Authentication Flow

The proposed browser authentication flow uses:

- OpenID Connect.
- Authorization Code flow.
- PKCE.
- State validation.
- Nonce validation.
- Exact redirect URI validation.
- Secure session handling.
- CSRF protection where applicable.

A Backend-for-Frontend pattern is a candidate for protecting sensitive tokens.

The PKCE verifier must be handled securely by the server-side flow where that pattern is adopted.

### 16.3 Token Validation

The API Gateway and relevant services must validate tokens according to their responsibilities.

Validation must include:

- Approved signing algorithm.
- Signature.
- Issuer.
- Audience.
- Expiration.
- Not-before time.
- Subject.
- Scope and claims.
- Key identification and rotation.
- Revocation strategy where applicable.

The system must reject unsupported algorithms and insecure configurations, including the `none` algorithm.

### 16.4 Service Identity

Internal workloads must use managed or otherwise securely controlled service identities.

Human credentials must not be reused as permanent service credentials.

Service identities must be revocable and auditable.

---

## 17. Network and Ingress Architecture

Network security must be applied at every relevant ingress and egress boundary.

### 17.1 Public Ingress

Public application ingress includes:

- Frontend application access.
- API Gateway access.
- Approved webhook endpoints.
- Other explicitly authorized public endpoints.

The API Gateway is the principal backend API ingress point.

Internal services must not be exposed publicly without an approved architectural justification.

### 17.2 Cloud Armor

Cloud Armor is a proposed protection component for supported Google Cloud ingress paths.

It must not be assumed to protect every frontend application hosted on Vercel.

The final ingress architecture must map the actual traffic path for:

- Vercel-hosted frontend applications.
- The API Gateway.
- Webhook endpoints.
- WebSocket connections.
- Server-Sent Events.
- Internal service communication.
- Administrative endpoints.

Protection must be applied at the actual ingress provider or enforcement point.

### 17.3 Network Segmentation

The infrastructure should separate:

- Public ingress.
- Application workloads.
- Data services.
- Sandbox execution.
- Administrative access.
- Monitoring and security services.

### 17.4 Egress Security

Outbound traffic must be controlled according to workload requirements.

Controls should include:

- Default-deny policies for sensitive workloads.
- Explicit destination allowlists where feasible.
- DNS controls.
- Metadata endpoint protection.
- Private network restrictions.
- Logging of relevant egress activity.
- Monitoring for unusual outbound behavior.

### 17.5 Administrative Access

Administrative access must use controlled identities, MFA, least privilege, and audit logging.

Direct public administrative access to databases, clusters, and internal services must be prohibited unless explicitly approved and protected by a documented exception.

---

## 18. Environment Architecture

The platform should use three primary environments.

| Environment | Purpose | Data Classification |
|---|---|---|
| Development | Engineering, local integration, and early testing | Synthetic or appropriately sanitized data |
| Staging | Pre-production validation and release testing | Synthetic or explicitly approved test data |
| Production | Live platform operation | Authorized production data |

### 18.1 Development Environment

Development supports:

- Feature development.
- Local testing.
- Integration development.
- Developer debugging.
- Early workflow validation.

Development must not use unrestricted production credentials or production tenant data.

### 18.2 Staging Environment

Staging should approximate relevant production configurations sufficiently to validate releases.

It should support:

- Integration tests.
- Authentication tests.
- Tenant-isolation tests.
- Deployment verification.
- Security testing.
- Performance testing.
- Workflow validation.
- Release acceptance.

Staging must not automatically inherit production access rights.

### 18.3 Production Environment

Production must have the strongest security, access, monitoring, change-control, and recovery requirements.

Production deployment must require GATE-03 approval.

### 18.4 Environment Isolation

Environment isolation must cover:

- Credentials.
- Databases.
- Storage.
- Service identities.
- Network permissions.
- API keys.
- Logging access.
- CI/CD permissions.
- Workflow infrastructure.
- Encryption keys.

A shared cloud provider does not mean environments are adequately isolated.

---

## 19. CI/CD Deployment Architecture

The deployment pipeline must provide controlled, traceable movement from reviewed source code to deployed artifacts.

### 19.1 Proposed Pipeline

```text
SOURCE CONTROL
      |
      v
PULL REQUEST / CODE REVIEW
      |
      v
AUTOMATED VALIDATION
      |
      v
BUILD
      |
      v
SECURITY AND QUALITY SCANNING
      |
      v
TESTING
      |
      v
ARTIFACT CREATION
      |
      v
ARTIFACT SIGNING / PROVENANCE
      |
      v
STAGING DEPLOYMENT
      |
      v
STAGING VERIFICATION
      |
      v
PRODUCTION APPROVAL (GATE-03)
      |
      v
PRODUCTION DEPLOYMENT
      |
      v
POST-DEPLOYMENT VERIFICATION
      |
      v
MONITORING / ROLLBACK IF REQUIRED
```

This is the proposed release flow. It is not evidence of an existing operational pipeline.

### 19.2 Source Control

GitHub is the authoritative source-control platform for the project.

Production deployment must use an approved source revision.

The current repository branch is `main`.

A five-tier branch strategy has been proposed but is not yet confirmed as the adopted repository policy.

No branch creation or branch-protection change is authorized by this document.

### 19.3 Build Validation

The pipeline should include:

- Formatting.
- Linting.
- Static type checks where applicable.
- Unit tests.
- Integration tests.
- API contract tests.
- Database migration checks.
- Dependency checks.
- Secret scanning.
- Static application security testing.
- Container image scanning.
- Infrastructure configuration scanning.

### 19.4 Software Supply Chain

The release process should maintain:

- Dependency lockfiles.
- Version-pinned dependencies.
- Software bill of materials.
- Build provenance.
- Artifact digests.
- Signed artifacts where supported.
- Vulnerability findings.
- Controlled exceptions.
- Traceability to source revisions.

Security scanners can identify known classes of risk. They cannot guarantee that software is vulnerability-free.

### 19.5 Deployment Identity

CI/CD systems must use narrowly scoped workload identities and deployment permissions.

Long-lived unrestricted credentials should be avoided.

### 19.6 Approval Separation

Production deployment requires GATE-03.

Protected GitHub operations require GATE-04.

The two gates are distinct.

A production deployment approval must not automatically authorize unrelated GitHub operations, and GitHub approval must not automatically authorize production deployment.

### 19.7 Approval Binding

Approvals must be bound to the relevant:

- Action.
- Project or tenant.
- Environment.
- Source revision or artifact digest.
- Authorization context.
- Expiry.
- Approval identity.
- Audit record.

A material change to the approved artifact or action must invalidate the previous approval.

### 19.8 Rollback

The deployment process must define:

- Previous known-good release identification.
- Artifact retrieval.
- Configuration rollback.
- Database compatibility.
- Migration recovery.
- Traffic restoration.
- Verification.
- Incident recording.

Rollback must not be assumed to reverse irreversible database or financial operations.

Where reversal is unsafe, a forward-recovery or compensating procedure must be defined.

---

## 20. Deployment Strategies

The platform may use the following strategies where appropriate.

### 20.1 Rolling Deployment

A rolling deployment gradually replaces existing application instances.

It is suitable when the service supports compatible versions and the infrastructure can maintain adequate capacity during replacement.

### 20.2 Blue-Green Deployment

Blue-green deployment maintains two deployment environments or versions and shifts traffic after verification.

It may be appropriate for services requiring controlled cutover.

### 20.3 Canary Deployment

Canary deployment releases a change to a limited portion of traffic before wider rollout.

It may be used where monitoring and traffic-control capabilities are available.

### 20.4 Strategy Selection

The deployment strategy must be selected according to:

- Service criticality.
- Compatibility.
- Traffic patterns.
- Data migration requirements.
- Rollback feasibility.
- Cost.
- Operational complexity.

No single deployment strategy is mandatory for every service.

---

## 21. Configuration and Secrets Deployment

Application configuration and secrets must be managed separately.

### 21.1 Configuration

Configuration may include:

- Environment identifiers.
- Service endpoints.
- Feature flags.
- Runtime limits.
- Timeout values.
- Non-sensitive application settings.

Configuration changes must be versioned and controlled.

### 21.2 Secrets

Secrets may include:

- Database credentials.
- API keys.
- Signing credentials.
- Webhook secrets.
- OAuth client secrets.
- Service credentials.
- Encryption-related secrets.

Secrets must not be committed to Git repositories or embedded in container images.

### 21.3 Secret Management

Google Secret Manager is a proposed secret-management service.

The final implementation must define:

- Secret ownership.
- Access policies.
- Versioning.
- Rotation.
- Revocation.
- Audit.
- Recovery.
- Emergency replacement.

### 21.4 Encryption Key Management

Google Cloud KMS is a proposed key-management service.

The key-management architecture must distinguish:

- Data encryption keys.
- Key-encryption keys.
- Envelope encryption.
- Key versions.
- Rotation.
- Re-encryption.
- Revocation.
- Recovery.
- Audit.

Using KMS does not automatically rotate every application secret or re-encrypt every existing data object.

These lifecycle responsibilities must be explicitly designed and tested.

---

## 22. External Integrations Deployment

The platform may integrate with external services for:

- AI model access.
- Payment processing.
- Authentication.
- Email and notifications.
- File processing.
- Monitoring.
- Security intelligence.
- Other approved business functions.

### 22.1 Integration Boundaries

Each external integration must have:

- A documented business purpose.
- An approved owner.
- Defined data-sharing boundaries.
- Authentication and authorization controls.
- Timeout and retry behavior.
- Rate limits.
- Error handling.
- Monitoring.
- Cost controls.
- Vendor dependency assessment.

### 22.2 AI Model Providers

Model access should be mediated through the approved model-routing capability.

The model-routing capability remains logical functionality within the existing six-service deployment boundary.

Model selection should be capability-based and versioned rather than dependent on hardcoded model identifiers that may become stale.

### 22.3 Payment Providers

Payment processing must be coordinated by `billing-ledger`.

Paystack and Stripe require provider-specific verification procedures.

For Paystack, webhook signature verification must use the provider's documented HMAC-SHA512 procedure and the raw request body.

Stripe must use its own documented signature-verification procedure.

The system must not treat browser redirects or frontend success messages as proof of payment.

Verified payment events should be processed idempotently and reconciled against provider records.

### 22.4 External Provider Failure

The platform must define behavior for:

- Provider unavailability.
- Rate limiting.
- Authentication failure.
- Timeout.
- Invalid response.
- Duplicate webhook delivery.
- Delayed event delivery.
- Provider-side transaction reversal.

Provider failure must not cause unauthorized ledger mutation or duplicate financial settlement.

---

## 23. Multimodal Processing Deployment

The `multimodal-service` handles approved multimodal workloads.

These may include:

- Image processing.
- Audio processing.
- Video processing.
- Document processing.
- Other supported input and output formats.

### 23.1 Processing Isolation

Multimodal workloads must use controlled processing environments.

Untrusted media and documents must be treated as potentially malicious.

### 23.2 Resource Management

Processing must have limits for:

- File size.
- Duration.
- CPU.
- Memory.
- Storage.
- Concurrent jobs.
- Processing time.
- Output size.

### 23.3 Storage and Retention

The service must use approved object storage and tenant-aware authorization.

Temporary files and intermediate artifacts must have documented retention and deletion behavior.

### 23.4 External Processing

Where external AI or media-processing providers are used, the platform must assess:

- Data classification.
- Provider retention.
- Training use.
- Geographic processing.
- Contractual obligations.
- Cross-border transfer.
- Security.
- Cost.

---

## 24. AdTech Deployment and Data Separation

The `adtech-service` is a separate proposed backend deployable unit.

It must not become an unrestricted data-access layer for the rest of the platform.

### 24.1 Data Access Boundaries

AdTech access should be limited to authorized public, aggregated, or explicitly permitted advertising data.

It must not receive unrestricted access to:

- Private user prompts.
- Private source code.
- Uploaded confidential files.
- Credentials.
- Authentication tokens.
- Financial secrets.
- Confidential project activity.
- Private tenant data.

### 24.2 Technical Separation

The implementation should enforce separation through:

- Dedicated service identity.
- Restricted database roles.
- Separate data schemas where appropriate.
- Network policies.
- API authorization.
- Data minimization.
- Auditable data-sharing interfaces.

### 24.3 Advertising Operations

Advertising delivery and measurement must comply with approved privacy, consent, retention, and security requirements.

Advertising activity must not interfere with financial integrity, tenant authorization, or platform security.

### 24.4 Deployment Monitoring

The service should have independent monitoring for:

- Availability.
- Processing errors.
- Data-access violations.
- Campaign execution.
- Provider failures.
- Cost.
- Unusual access patterns.

---

## 25. Scaling and Capacity Architecture

The platform must be designed to scale according to actual workload characteristics.

### 25.1 Frontend Scaling

Frontend scaling should use the capabilities of the selected hosting provider and CDN configuration.

Caching must respect authentication, authorization, and data privacy.

### 25.2 Backend Scaling

Backend services should support appropriate horizontal or vertical scaling.

Scaling policies must consider:

- CPU.
- Memory.
- Request volume.
- Queue depth.
- Concurrent workflows.
- Processing duration.
- Database capacity.
- External provider limits.
- Cost.

### 25.3 Worker Scaling

Workflow workers should scale according to workload and task-queue demand.

Scaling must not violate:

- Tenant isolation.
- Per-tenant quotas.
- Provider rate limits.
- Resource budgets.
- Workflow concurrency constraints.

### 25.4 Sandbox Scaling

Sandbox capacity must account for potentially resource-intensive workloads.

Sandbox scaling must enforce resource limits and prevent one tenant's workload from exhausting shared capacity.

### 25.5 Database Scaling

Database scaling decisions must be based on measured workload.

Potential approaches include:

- Connection pooling.
- Query optimization.
- Indexing.
- Read replicas where appropriate.
- Partitioning where justified.
- Storage scaling.
- Workload separation.

Read replicas must not be treated as substitutes for transactional consistency.

### 25.6 Capacity Testing

Capacity targets remain subject to benchmarking.

Testing must cover:

- Expected concurrency.
- Peak concurrency.
- Workload mix.
- Database load.
- Worker utilization.
- Queue latency.
- External provider throttling.
- Failure and recovery.
- Cost per workload.

No unmeasured throughput or capacity guarantee is established by this document.

---

## 26. Observability and Operational Monitoring

The platform requires centralized observability.

The proposed architecture should support:

- Application logs.
- Infrastructure logs.
- Security audit logs.
- Metrics.
- Distributed traces.
- Workflow execution visibility.
- Deployment events.
- Alerting.
- Operational dashboards.

### 26.1 Logging

Logs should include appropriate correlation identifiers, service identity, environment, timestamps, and relevant task or workflow identifiers.

Logs must not unnecessarily expose:

- Passwords.
- Access tokens.
- API secrets.
- Private user content.
- Confidential source code.
- Sensitive personal data.
- Full payment credentials.

### 26.2 Metrics

Metrics should cover:

- Availability.
- Request latency.
- Error rates.
- Throughput.
- Queue depth.
- Workflow duration.
- Worker utilization.
- Database performance.
- Storage utilization.
- Sandbox capacity.
- Payment processing.
- Cost.

### 26.3 Distributed Tracing

Distributed traces should support investigation across service boundaries.

Trace context must not be trusted as authorization evidence.

### 26.4 Alerting

Alerts should be defined for:

- Service unavailability.
- Elevated error rates.
- Unusual latency.
- Queue backlogs.
- Database resource exhaustion.
- Failed deployments.
- Security incidents.
- Payment reconciliation failures.
- Backup failures.
- Recovery failures.
- Unexpected cost increases.

### 26.5 Monitoring Ownership

Every production-critical alert must have an assigned operational owner and escalation procedure.

Monitoring tools and alert thresholds remain subject to implementation and validation.

---

## 27. Backup and Disaster Recovery Architecture

The platform must have a recovery strategy covering all critical components.

### 27.1 Protected Assets

Recovery planning must include:

- PostgreSQL databases.
- Financial ledger records.
- Workflow persistence.
- Object storage.
- Git repositories.
- Build artifacts.
- Infrastructure configuration.
- Secrets and encryption-key recovery.
- Identity-provider configuration.
- DNS and domain configuration.
- Operational documentation.

### 27.2 Backup Strategy

The final backup design must define:

- Backup frequency.
- Retention.
- Encryption.
- Access controls.
- Geographic separation.
- Immutability where appropriate.
- Integrity verification.
- Restore testing.
- Ownership.

### 27.3 Database Recovery

Cloud SQL high availability, if adopted, must not be treated as a complete disaster recovery strategy.

The design must distinguish:

- High availability.
- Point-in-time recovery.
- Backup restoration.
- Regional recovery.
- Full-platform disaster recovery.

### 27.4 Workflow Recovery

Recovery planning must include workflow persistence, worker availability, task queues, activity retries, and the safe handling of in-flight operations.

Restoring a database without reconciling external side effects may cause duplicate or inconsistent business operations.

### 27.5 Financial Recovery

Financial recovery must preserve ledger integrity.

Recovery must include reconciliation against relevant payment-provider records and other authoritative financial sources.

Posted ledger entries must not be silently altered to make recovered data appear consistent.

### 27.6 Object and Git Recovery

Object storage recovery must address versioning, retention, deletion, and access permissions.

Git recovery must preserve repository history and protected-branch integrity.

### 27.7 Recovery Objectives

The final Recovery Point Objective (RPO) and Recovery Time Objective (RTO) remain pending formal human decisions.

They must be based on business impact analysis and demonstrated recovery testing.

### 27.8 Backup Restoration and Deletion

Restoring a backup must not unintentionally reintroduce data that was validly deleted or anonymized after the backup was created.

The recovery process must reconcile:

- Deletion requests.
- Retention rules.
- Legal holds.
- Revoked credentials.
- Access changes.
- Tenant deactivation.
- Other applicable data-governance events.

### 27.9 Recovery Testing

Backup success messages do not prove that the platform can recover.

Recovery testing must include the dependencies required for a functioning platform, not just an isolated database restore.

---

## 28. Security and Compliance Deployment Controls

Deployment security must implement the requirements defined in WLX-ARCH-008.

### 28.1 Identity and Access

Controls must include:

- MFA for privileged users.
- Least privilege.
- Service identity.
- Role-based authorization.
- Controlled administrative access.
- Credential rotation.
- Access reviews.
- Audit logging.

### 28.2 Network Security

Controls must include:

- HTTPS.
- TLS for internal communications where appropriate.
- Network segmentation.
- Ingress restrictions.
- Egress controls.
- DNS security.
- Webhook protection.
- Administrative access restrictions.

### 28.3 Data Protection

Controls must include:

- Encryption at rest.
- Encryption in transit.
- Tenant isolation.
- Data classification.
- Retention controls.
- Secure deletion.
- Backup protection.
- Key management.

### 28.4 Software Supply Chain

Controls must include:

- Dependency pinning.
- Vulnerability scanning.
- Secret scanning.
- Container scanning.
- Infrastructure scanning.
- Software bill of materials.
- Build provenance.
- Artifact integrity.
- Protected source-control operations.

### 28.5 Privacy and Regulatory Compliance

The implementation must assess applicable data-protection requirements, including the Nigeria Data Protection Act where applicable.

Cross-border processing must be assessed according to the actual data, processing purpose, recipient, destination, and applicable legal requirements.

The presence of cloud infrastructure in a particular region does not automatically establish regulatory compliance.

### 28.6 Compliance Evidence

Compliance claims must be supported by evidence.

Deployment architecture alone does not establish certification, regulatory approval, or compliance.

---

## 29. Cost Management and Resource Governance

Cloud and hosting costs must be controlled as part of deployment governance.

### 29.1 Cost Categories

Cost management should include:

- Frontend hosting.
- Compute.
- Kubernetes.
- Database.
- Storage.
- Network egress.
- AI model usage.
- Multimodal processing.
- Sandbox execution.
- Workflow orchestration.
- Monitoring.
- Security services.
- External provider usage.

### 29.2 Cost Attribution

Resources should have appropriate labels or metadata for:

- Environment.
- Service.
- Project.
- Owner.
- Cost category.
- Tenant allocation where appropriate.

### 29.3 Usage Limits

The platform should support configurable limits for:

- User usage.
- Tenant usage.
- AI model consumption.
- Sandbox execution.
- File storage.
- Video and image processing.
- Concurrent workloads.

### 29.4 Financial Authority

Usage estimation and billing recommendations may be performed by AI agents.

Authoritative credit reservation, settlement, ledger posting, and financial reconciliation remain responsibilities of `billing-ledger`.

### 29.5 Cost Alerts

Cost alerts should identify:

- Unusual increases.
- Unexpected resource growth.
- Idle resources.
- Excessive egress.
- Model usage anomalies.
- Sandbox abuse.
- Uncontrolled background workloads.

Actual budgets and thresholds remain pending approval.

---

## 30. Deployment Failure and Incident Management

The deployment architecture must define procedures for failures and operational incidents.

### 30.1 Deployment Failure

A failed deployment must trigger an appropriate response based on severity and service criticality.

The response may include:

- Halt further rollout.
- Preserve diagnostic evidence.
- Restore the previous known-good artifact.
- Apply an approved forward fix.
- Isolate affected workloads.
- Notify responsible operators.
- Record the incident.

### 30.2 Security Incident

Security incidents must follow the incident-response process defined in WLX-ARCH-008.

Potential incidents include:

- Unauthorized deployment.
- Credential compromise.
- Cross-tenant access.
- Sandbox escape.
- Malicious artifact.
- Database compromise.
- Data exfiltration.
- Approval bypass.
- Payment or ledger inconsistency.

### 30.3 Operational Recovery

Recovery procedures must identify:

- Incident owner.
- Affected services.
- Containment actions.
- Recovery authority.
- Communication requirements.
- Evidence preservation.
- Verification requirements.
- Post-incident review.

### 30.4 AI Agent Restrictions

AI agents may assist with diagnosis, evidence gathering, and proposed remediation.

They must not independently authorize sensitive production changes or bypass required human approval.

---

## 31. Deployment Responsibilities and Governance

Deployment responsibilities must be explicitly assigned.

| Responsibility | Proposed Accountable Function |
|---|---|
| Architecture approval | Project Owner or formally delegated authority |
| Cloud infrastructure | Authorized Infrastructure Owner |
| Frontend deployments | Authorized Frontend/Release Owner |
| Backend deployments | Authorized Backend/Release Owner |
| Database operations | Authorized Database Owner |
| Security controls | Authorized Security Owner |
| CI/CD configuration | Authorized DevOps/Platform Owner |
| Production deployment approval | GATE-03 approver |
| Protected GitHub operations | GATE-04 approver |
| Financial integrity | `billing-ledger` service owner |
| Disaster recovery | Designated Operations/Recovery Owner |
| Incident response | Designated Incident Owner |

These are proposed responsibilities, not confirmation that named individuals or teams have been appointed.

The Project Owner's approval authority and any delegation arrangements must be formally established.

An administrator role does not automatically confer authority to approve every sensitive operation.

---

## 32. Human Decisions Pending

The following decisions remain open and require formal review.

| ID | Decision | Current Status |
|---|---|---|
| HD-01 | Select the managed or internally operated identity provider | Pending |
| HD-02 | Select Temporal Cloud or self-hosted Temporal | Pending |
| HD-03 | Confirm primary and disaster-recovery regions | Pending |
| HD-04 | Approve the six-service deployment topology and hosting boundaries | Pending |
| HD-05 | Confirm embedding dimensions and pgvector configuration, including the proposed 3072-dimensional requirement | Pending |
| HD-06 | Approve platform-wide RPO and RTO | Pending |
| HD-07 | Identify risk-acceptance authority and delegated operational owners | Pending |
| HD-08 | Finalize the definitions and approval authorities for GATE-01 through GATE-06 | Pending |

Additional decisions requiring validation include:

- Final frontend hosting configuration.
- GKE cluster topology.
- gVisor versus alternative sandbox isolation.
- Cloud SQL configuration.
- Object storage configuration.
- Redis deployment model.
- Cloud Armor and actual ingress protection.
- CI/CD provider and deployment identity.
- Monitoring and alerting platform.
- Backup retention and recovery architecture.
- Production capacity and cost limits.

No pending decision should be silently converted into an accepted architecture decision.

---

## 33. Deployment Implementation Boundary

This document is part of Phase 0 architecture documentation.

It does not authorize implementation.

The following activities remain outside the scope of this document:

- Creating cloud projects.
- Provisioning Kubernetes clusters.
- Creating databases.
- Creating storage buckets.
- Configuring production DNS.
- Creating production secrets.
- Deploying frontend applications.
- Deploying backend services.
- Configuring payment providers.
- Creating CI/CD pipelines.
- Creating Git branches.
- Committing or pushing source changes.
- Running database migrations.
- Activating production workloads.
- Approving GATE-03.
- Approving GATE-04.
- Beginning Phase 1.

Any implementation activity requires the appropriate authorization and an approved execution plan.

Phase 0 completion does not automatically authorize Phase 1.

---

## 34. Related Architecture Documents

This document must be interpreted together with the following architecture documents:

| Document ID | Document |
|---|---|
| WLX-ARCH-001 | ARCHITECTURE_OVERVIEW.md |
| WLX-ARCH-002 | SYSTEM_ARCHITECTURE.md |
| WLX-ARCH-003 | TECHNOLOGY_STACK.md |
| WLX-ARCH-004 | REPOSITORY_STRUCTURE.md |
| WLX-ARCH-005 | AGENT_ECOSYSTEM.md |
| WLX-ARCH-006 | SERVICE_BOUNDARIES.md |
| WLX-ARCH-007 | DATABASE_ARCHITECTURE.md |
| WLX-ARCH-008 | SECURITY_ARCHITECTURE.md |
| WLX-ARCH-010 | DEVELOPMENT_ROADMAP.md |
| WLX-ARCH-011 | RISK_REGISTER.md |
| WLX-ARCH-012 | ADR_REGISTER.md |
| WLX-ARCH-013 | PHASE_0_INSPECTION_REPORT.md |

Where a deployment decision conflicts with another architecture document, the conflict must be recorded and resolved through the architecture decision process.

This document does not independently override an approved architecture decision.

---

## 35. Final Status

The Deployment Architecture establishes the proposed hosting and operational model for the Worklexx AI Software Factory.

It defines:

- Five frontend applications and their proposed domains.
- A separate API Gateway domain.
- Six deployable backend service units.
- The logical deployment of the 23-agent ecosystem.
- Proposed frontend and backend hosting arrangements.
- Environment separation.
- Container and Kubernetes deployment principles.
- Sandbox isolation requirements.
- Database and object-storage deployment.
- Workflow and messaging requirements.
- Identity and network security.
- CI/CD and approval controls.
- Scaling and capacity principles.
- Monitoring and operational governance.
- Backup and disaster recovery requirements.
- Cost management.
- Pending human decisions.
- The boundary between Phase 0 documentation and implementation.

The architecture remains subject to formal review, cross-document consistency verification, proof-of-concept testing, human decisions, and approval.

**Document Status:** Phase 0 Architecture Baseline — Proposed.

**Implementation Status:** Not authorized by this document.

**Formal Approval Status:** Pending.

**Phase 1 Authorization:** Not granted.

**End of Document WLX-ARCH-009.**