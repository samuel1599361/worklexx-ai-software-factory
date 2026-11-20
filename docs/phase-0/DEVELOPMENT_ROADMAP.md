# WORKLEXX AI SOFTWARE FACTORY
# DEVELOPMENT ROADMAP

## Document Metadata

| Field | Value |
|---|---|
| Document Title | Development Roadmap |
| Document ID | WLX-ARCH-010 |
| Document Version | 1.0 |
| Document Status | Phase 0 Architecture Baseline — Proposed Roadmap |
| Classification | Internal — Architecture and Planning |
| Repository | https://github.com/samuel1599361/worklexx-ai-software-factory |
| Repository Branch | `main` |
| Document Path | `docs/phase-0/DEVELOPMENT_ROADMAP.md` |
| Related Phase | Phase 0 — Architecture and Planning |
| Planning Horizon | November 2026 – September 2027 |
| Approval Authority | Project Owner or formally delegated authority |
| Implementation Status | Not authorised by this document |

---

## 1. Purpose

This document defines the proposed development roadmap for the Worklexx AI Software Factory.

It translates the approved architectural direction into a phased implementation programme covering:

- Platform foundations and engineering infrastructure.
- Identity, authentication, authorisation, and tenant isolation.
- Backend services and API infrastructure.
- AI orchestration and the 23-agent ecosystem.
- Multimodal processing.
- Secure code generation and sandbox execution.
- Billing, financial controls, and usage metering.
- Advertising technology and data separation.
- Frontend applications and user experience.
- Testing, security validation, deployment, and operational readiness.
- Continuous improvement and future platform expansion.

The roadmap establishes sequencing and dependencies. It does not independently approve implementation, expenditure, infrastructure provisioning, production deployment, or release of any feature.

---

## 2. Roadmap Objectives

The roadmap has the following objectives:

1. Deliver a secure, scalable, multi-tenant AI software development platform.
2. Establish the six deployable backend service units defined in the architecture.
3. Implement the 23 logical agents as governed modules within the agent ecosystem.
4. Provide a consistent user experience across the five frontend applications.
5. Enable users to describe software requirements through text and supported multimodal inputs.
6. Support AI-assisted planning, design, development, testing, debugging, and documentation.
7. Provide controlled execution environments for generated code.
8. Implement durable workflow orchestration and reliable task recovery.
9. Protect customer data, source code, credentials, generated artifacts, and financial records.
10. Establish auditable approval gates for sensitive operations.
11. Support usage metering, billing, and financial reconciliation.
12. Introduce advertising capabilities without exposing confidential customer information.
13. Establish measurable quality, performance, security, and operational standards.
14. Create a foundation for future international scaling.

---

## 3. Roadmap Governance Principles

Development shall follow these principles:

### 3.1 Architecture before implementation

The Phase 0 architecture documents establish the proposed design baseline. Implementation must be checked against the complete architecture set before the relevant work begins.

### 3.2 Incremental delivery

The platform shall be delivered in controlled phases. Each phase must have defined deliverables, dependencies, acceptance criteria, and an accountable owner.

### 3.3 Security by design

Identity, tenant isolation, least privilege, secrets management, auditability, secure execution, and data protection must be designed into each relevant component.

### 3.4 Human-controlled authority

AI agents may analyse, recommend, plan, and coordinate. They must not independently grant themselves privileges or bypass approval requirements.

### 3.5 Deterministic control of critical operations

Deterministic services remain authoritative for:

- Authentication and authorisation decisions.
- Financial calculations and ledger entries.
- Payment state transitions.
- Approval enforcement.
- Tenant access control.
- Workflow state transitions.
- Audit records.
- Production deployment permissions.

### 3.6 Evidence-based completion

A task is not complete merely because code has been generated. Completion requires relevant testing, review, documented evidence, and acceptance.

### 3.7 No implied approval

A roadmap date, proposed milestone, completed document, successful test, or AI-generated recommendation does not constitute approval to proceed to the next phase.

---

## 4. Platform Architecture Baseline

The roadmap follows the architecture defined in the Phase 0 documents.

### 4.1 Frontend applications

The proposed frontend application family comprises:

| Application | Domain | Primary Purpose |
|---|---|---|
| Worklexx Website | `worklexx.ai` | Public website, product information, and marketing |
| Worklexx App | `app.worklexx.ai` | Main customer and developer workspace |
| Worklexx Video | `video.worklexx.ai` | Video-related capabilities |
| Worklexx Images | `images.worklexx.ai` | Image-related capabilities |
| Worklexx Docs | `docs.worklexx.ai` | Documentation and developer resources |

### 4.2 Backend service units

The official deployable backend topology comprises six service units:

1. `api-gateway`
2. `agent-orchestrator`
3. `multimodal-service`
4. `sandbox-runner`
5. `billing-ledger`
6. `adtech-service`

The AI Gateway and model-routing capability is a logical capability, not an additional deployable service in the approved six-service baseline.

### 4.3 Agent ecosystem

The platform contains 23 logical agents.

Agents are implemented as governed modules coordinated through the `agent-orchestrator`. They are not automatically separate microservices.

The implementation must preserve the separation between agent recommendations and deterministic system authority.

In particular:

- Agent21 performs advisory and coordination functions.
- The `billing-ledger` service remains the financial authority.
- Agent22 uses the `multimodal-service`.
- Agent23 uses the `adtech-service`.
- Agent23 must not obtain unauthorised access to private prompts, source code, customer uploads, credentials, or confidential activity.

---

## 5. Development Phases Overview

The proposed programme contains nine phases:

| Phase | Name | Indicative Period |
|---|---|---|
| Phase 0 | Architecture and Planning | November 2026 |
| Phase 1 | Engineering Foundation and Core Infrastructure | December 2026 |
| Phase 2 | Identity, Security, and Multi-Tenant Foundations | January 2027 |
| Phase 3 | Core Backend and Workflow Infrastructure | February 2027 |
| Phase 4 | AI Orchestration and Agent Ecosystem | March 2027 |
| Phase 5 | Multimodal Processing and Secure Sandbox | April 2027 |
| Phase 6 | Billing, Usage Management, and AdTech | May 2027 |
| Phase 7 | Frontend Applications and Integrated User Experience | June–July 2027 |
| Phase 8 | System Validation, Production Readiness, and Controlled Launch | August–September 2027 |

These dates are planning estimates. They may change following technical validation, resource assessment, procurement, security review, and Project Owner approval.

---

## 6. Phase 0 — Architecture and Planning

**Indicative period:** November 2026

### 6.1 Objective

Establish a coherent, reviewed, and governed architecture baseline before implementation begins.

### 6.2 Scope

Phase 0 includes:

- Architecture definition.
- System decomposition.
- Technology selection proposals.
- Repository and source-control planning.
- Agent ecosystem design.
- Service boundary definition.
- Database architecture.
- Security architecture.
- Deployment architecture.
- Development roadmap.
- Risk register.
- Architecture Decision Record register.
- Phase 0 inspection report.

### 6.3 Required documents

The Phase 0 architecture baseline comprises:

1. `ARCHITECTURE_OVERVIEW.md`
2. `SYSTEM_ARCHITECTURE.md`
3. `TECHNOLOGY_STACK.md`
4. `REPOSITORY_STRUCTURE.md`
5. `AGENT_ECOSYSTEM.md`
6. `SERVICE_BOUNDARIES.md`
7. `DATABASE_ARCHITECTURE.md`
8. `SECURITY_ARCHITECTURE.md`
9. `DEPLOYMENT_ARCHITECTURE.md`
10. `DEVELOPMENT_ROADMAP.md`
11. `RISK_REGISTER.md`
12. `ADR_REGISTER.md`
13. `PHASE_0_INSPECTION_REPORT.md`

### 6.4 Deliverables

- Complete Phase 0 document set.
- Cross-document consistency review.
- Document inventory and verification evidence.
- SHA-256 baseline manifest.
- Updated risk register.
- Architecture decision register.
- Human decisions and unresolved assumptions register.
- Phase 0 inspection report.

### 6.5 Acceptance criteria

Phase 0 is eligible for approval when:

- All 16 Phase 0 documents are present.
- Document identifiers and versions are consistent.
- The six-service topology is consistent throughout the architecture.
- The 23-agent model is consistently represented.
- Security and tenant-isolation requirements are documented.
- Approval gates are distinguished correctly.
- Unresolved decisions are clearly identified.
- Risks have owners or explicitly pending ownership.
- The final document inventory and integrity evidence are available.
- The Project Owner has reviewed and formally accepted the Phase 0 baseline.

### 6.6 Implementation boundary

Phase 0 is a documentation and planning phase.

It does not authorise:

- Application implementation.
- Database migrations or SQL execution.
- Cloud infrastructure provisioning.
- Production deployment.
- Creation of new Git branches.
- Repository commits or pushes.
- Paid infrastructure subscriptions.
- External integrations or production credentials.
- Phase 1 commencement.

### 6.7 Exit gate

**GATE-P0:** Formal Phase 0 architecture approval.

The gate requires documented Project Owner acceptance. Completion of the documents alone does not satisfy this requirement.

---

## 7. Phase 1 — Engineering Foundation and Core Infrastructure

**Indicative period:** December 2026

### 7.1 Objective

Establish the foundational engineering environment and reusable development infrastructure.

### 7.2 Scope

- Repository governance and branch protection.
- Development environment configuration.
- Backend project scaffolding.
- Frontend project scaffolding.
- Shared configuration and environment management.
- Dependency and package management.
- CI quality checks.
- Automated code formatting and linting.
- Initial build pipelines.
- API contract conventions.
- Logging and tracing foundations.
- Developer documentation infrastructure.

### 7.3 Repository implementation

The repository shall be configured in accordance with the approved repository architecture.

Activities may include:

- Establishing approved repository directories.
- Defining service and package boundaries.
- Configuring protected branches.
- Establishing pull-request requirements.
- Configuring CODEOWNERS where appropriate.
- Defining commit and release conventions.
- Introducing dependency lockfiles.
- Establishing software bill of materials generation.
- Establishing code review and security scanning.

The current repository branch is `main`.

A proposed five-tier branch strategy must not be treated as adopted until explicitly approved. No branch shall be created merely because it appears in a proposed architecture or roadmap.

### 7.4 Engineering foundations

Establish the initial technical foundations for:

- Python backend development.
- TypeScript frontend development.
- API schema validation.
- Database connectivity.
- Automated testing.
- Container image construction.
- Secure configuration management.
- Development and staging environments.

Exact versions must be pinned and validated against the approved technology baseline.

### 7.5 Deliverables

- Approved repository configuration.
- Backend and frontend project scaffolding.
- Development environment instructions.
- CI quality-check pipeline.
- Dependency and package-management policy.
- API contract conventions.
- Initial observability framework.
- Engineering standards and contribution guide.

### 7.6 Acceptance criteria

- Developers can reproduce the development environment.
- Project structure follows the approved architecture.
- CI executes the required checks.
- Secrets are not stored in source code.
- Dependencies are version-controlled.
- Pull-request and review controls are documented and tested.
- Build artifacts can be produced reproducibly.
- No unapproved production infrastructure is provisioned.

### 7.7 Exit gate

**GATE-P1:** Engineering foundation acceptance.

---

## 8. Phase 2 — Identity, Security, and Multi-Tenant Foundations

**Indicative period:** January 2027

### 8.1 Objective

Implement the platform's foundational identity, access-control, tenant-isolation, and security capabilities.

### 8.2 Scope

- Identity-provider integration.
- User registration and authentication.
- Organisation and workspace management.
- Role-based access control.
- Permission enforcement.
- Session management.
- Token validation.
- Tenant context propagation.
- PostgreSQL tenant isolation.
- Audit-event foundations.
- Secrets and encryption management.
- Security testing.

### 8.3 Identity architecture

The selected identity provider shall be determined through the relevant human architecture decision.

Implementation should support:

- OpenID Connect.
- Authorization Code Flow with PKCE.
- Secure session handling.
- Multi-factor authentication where required.
- Token expiry and refresh controls.
- Session revocation.
- Role and permission mapping.
- Organisation membership management.

The identity provider owns credential authentication and its identity sessions. Worklexx owns application-specific organisation membership and authorisation policy.

### 8.4 Multi-tenant isolation

Implement tenant-aware access controls across:

- PostgreSQL records.
- Object storage.
- Git repositories and source assets.
- Generated artifacts.
- Sandbox execution.
- Workflow records.
- Logs and audit events.
- Billing and usage records.

Database isolation must include:

- Row-Level Security on tenant-owned tables.
- Restricted database roles.
- `FORCE ROW LEVEL SECURITY` where appropriate.
- Transaction-scoped tenant context.
- Tenant-aware foreign-key relationships.
- Connection-pool context protection.
- Isolation tests using adversarial cross-tenant scenarios.

A tenant context variable alone is not sufficient protection.

### 8.5 Security controls

Implement and test:

- Least-privilege access.
- Secure cookie and CSRF controls.
- JWT issuer, audience, expiry, and algorithm validation.
- JWKS key handling.
- Refresh-token rotation and reuse detection where applicable.
- Secrets-management integration.
- Encryption at rest and in transit.
- Audit logging.
- Rate limiting.
- Secure error handling.
- Dependency vulnerability scanning.

### 8.6 Deliverables

- Identity-provider integration.
- User and organisation identity model.
- Application authorisation framework.
- Tenant isolation implementation.
- Database security policies.
- Audit-event framework.
- Secrets-management integration.
- Security test suite.
- Threat-model updates.

### 8.7 Acceptance criteria

- Unauthenticated requests cannot access protected resources.
- Users cannot access another tenant's data without explicit authorised sharing.
- Role and permission checks are enforced server-side.
- Tenant isolation tests pass.
- Session and token controls are tested.
- Secrets are not exposed in logs or responses.
- Privileged actions are auditable.
- Security findings are assessed and tracked.

### 8.8 Exit gate

**GATE-P2:** Identity, security, and tenant-isolation acceptance.

---

## 9. Phase 3 — Core Backend and Workflow Infrastructure

**Indicative period:** February 2027

### 9.1 Objective

Implement the core backend service architecture and reliable workflow infrastructure.

### 9.2 Scope

Develop the foundational capabilities of:

1. `api-gateway`
2. `agent-orchestrator`
3. `multimodal-service`
4. `sandbox-runner`
5. `billing-ledger`
6. `adtech-service`

The initial focus is on API Gateway, Agent Orchestrator, service communication, database integration, and workflow persistence.

### 9.3 API Gateway

Implement:

- API routing.
- Authentication integration.
- Authorisation enforcement.
- Request validation.
- Rate limiting.
- Tenant context propagation.
- API versioning.
- Request correlation.
- Error handling.
- External API boundary controls.

The API Gateway must remain distinct from the identity provider.

### 9.4 Agent Orchestrator foundations

Implement:

- Agent registration and configuration.
- Agent capability metadata.
- Task routing.
- Workflow initiation.
- Workflow state management.
- Agent execution policies.
- Tool-permission checks.
- Timeout and cancellation controls.
- Human-approval integration.
- Execution history and audit events.

### 9.5 Workflow engine

Temporal is a proposed workflow-engine candidate, subject to a proof of concept and formal selection.

The proof of concept must evaluate:

- Workflow durability.
- Retry behaviour.
- Activity execution semantics.
- Database compatibility.
- Backup and recovery.
- Schema and version upgrades.
- Operational complexity.
- Cost.
- Monitoring.
- Cloud-hosted versus self-hosted operation.

Redis Pub/Sub may support ephemeral notification and event delivery. It must not become the authoritative durable workflow record.

### 9.6 Workflow lifecycle

The initial lifecycle shall support:

`Created → Validating → Queued → Running → AwaitingApproval → Completed / Failed / Cancelled`

The implementation must also define:

- Retry policies.
- Timeouts.
- Cancellation.
- Compensation.
- Dead-letter handling.
- Manual recovery.
- Idempotency.
- Reconciliation.
- Outbox and inbox patterns where appropriate.

The system must assume at-least-once activity execution. It must not claim exactly-once external side effects without a verifiable mechanism at the external boundary.

### 9.7 Deliverables

- API Gateway foundation.
- Agent Orchestrator foundation.
- Durable workflow integration or approved alternative.
- Service-to-service authentication.
- API contract tests.
- Workflow state model.
- Event and audit framework.
- Initial service health monitoring.

### 9.8 Acceptance criteria

- API requests are authenticated and authorised.
- Tenant context is propagated safely.
- Workflows survive expected service restarts.
- Duplicate activity execution is safely handled.
- Failed workflows can be inspected and recovered.
- Approval-required activities cannot bypass their approval conditions.
- Service communication is authenticated.
- API contracts are validated automatically.

### 9.9 Exit gate

**GATE-P3:** Core backend and workflow acceptance.

---

## 10. Phase 4 — AI Orchestration and Agent Ecosystem

**Indicative period:** March 2027

### 10.1 Objective

Implement the Worklexx agent ecosystem as governed, testable, and observable logical modules.

### 10.2 Scope

- Agent capability registry.
- Agent orchestration.
- Model-routing capability.
- Agent-to-agent task coordination.
- Tool invocation framework.
- Prompt and instruction versioning.
- Context management.
- Memory and retrieval controls.
- Agent evaluation.
- Human approval integration.
- Agent performance monitoring.

### 10.3 Agent implementation model

The 23 agents shall be implemented according to the approved Agent Ecosystem document.

They are logical modules coordinated by the `agent-orchestrator`, not automatically 23 independent deployable services.

The implementation sequence shall be derived from the agent dependency map and verified against the approved ecosystem document.

### 10.4 Implementation sequencing

The initial implementation sequence should prioritise:

1. Shared agent execution framework.
2. Agent registration and capability discovery.
3. Planning and requirements-analysis capabilities.
4. Architecture and design capabilities.
5. Development and code-generation capabilities.
6. Testing and debugging capabilities.
7. Documentation and knowledge capabilities.
8. Workflow coordination and advisory capabilities.
9. Multimodal and advertising-related agent integrations.

The exact agent-by-agent order must be recorded in the implementation backlog.

The roadmap does not assume that all 23 agents must be completed in a single development iteration.

### 10.5 Model-routing capability

Implement a model-routing capability within the approved service topology.

It should support:

- Capability-based model selection.
- Provider abstraction.
- Model catalogue and version management.
- Cost and usage tracking.
- Latency and reliability monitoring.
- Fallback policies.
- Provider availability checks.
- Data classification and routing restrictions.
- Model evaluation and regression testing.

Model identifiers must be managed through a maintained catalogue rather than permanently hardcoded assumptions.

### 10.6 Agent governance

Every agent must have:

- Defined purpose.
- Input and output contracts.
- Capability boundaries.
- Permitted tools.
- Permission requirements.
- Execution limits.
- Failure behaviour.
- Audit requirements.
- Evaluation criteria.
- Version history.

Agents must not:

- Grant themselves privileges.
- Override tenant authorisation.
- Bypass approval gates.
- Directly mutate authoritative financial records.
- Execute unrestricted code outside approved environments.
- Expose hidden internal reasoning as a user-facing product feature.

User-facing transparency should instead include progress, task status, tool activity where appropriate, concise explanations, and results.

### 10.7 Agent21 and financial authority

Agent21 may provide advisory and coordination functions relating to financial workflows.

It must not become the authoritative financial ledger.

The `billing-ledger` remains responsible for deterministic financial calculations, transaction state, posting, and reconciliation.

### 10.8 Deliverables

- Agent framework.
- Agent registry.
- Initial agent modules.
- Model-routing capability.
- Tool-permission framework.
- Agent evaluation framework.
- Agent observability.
- Human approval integration.
- Agent security and failure tests.

### 10.9 Acceptance criteria

- Agents operate within defined capability boundaries.
- Tool calls are authorised.
- Agent outputs conform to validated contracts.
- Model selection is configurable and observable.
- Agent failures are recoverable.
- Human approvals are enforced.
- Agent execution is auditable.
- No agent bypasses deterministic security or financial controls.

### 10.10 Exit gate

**GATE-P4:** Agent ecosystem acceptance.

---

## 11. Phase 5 — Multimodal Processing and Secure Sandbox

**Indicative period:** April 2027

### 11.1 Objective

Implement multimodal input processing and secure code execution capabilities.

### 11.2 Multimodal processing

The `multimodal-service` shall support approved combinations of:

- Text.
- Images.
- Documents.
- Audio.
- Speech.
- Video.
- Structured data.
- Code and software project artifacts.

Processing must include:

- File-type validation.
- File-size and duration limits.
- Malware scanning.
- Content extraction.
- Metadata handling.
- Tenant-aware storage.
- Processing-status tracking.
- Data retention and deletion controls.
- Provider and model routing.
- Error and retry handling.

### 11.3 Multimodal agent integration

Agent22 shall use the `multimodal-service` for relevant multimodal capabilities.

The agent must not independently bypass upload validation, storage authorisation, or processing security controls.

### 11.4 Secure sandbox

The `sandbox-runner` shall provide isolated environments for approved code execution and testing.

Candidate technologies include GKE-based sandboxing with gVisor, subject to proof of concept and security validation.

The implementation must address:

- Tenant isolation.
- Container and process isolation.
- Non-root execution.
- CPU, memory, disk, and time limits.
- Filesystem restrictions.
- Network egress restrictions.
- DNS and IPv6 controls.
- Cloud metadata-service protection.
- Short-lived execution credentials.
- Image provenance and scanning.
- Execution logging.
- Resource cleanup.
- Abuse detection.
- Escape testing.

gVisor must not be described as eliminating all sandbox-escape risk. MicroVM-based alternatives should be evaluated where the threat model warrants stronger isolation.

### 11.5 Sandbox execution lifecycle

The proposed lifecycle is:

`Requested → Validated → Authorised → Provisioned → Executing → CollectingResults → Completed / Failed / Terminated → CleanedUp`

Execution must be linked to:

- Tenant.
- User or authorised service identity.
- Project.
- Workflow.
- Artifact or source revision.
- Execution policy.
- Resource allocation.
- Approval record where required.

### 11.6 Deliverables

- Multimodal processing pipelines.
- Secure upload and quarantine workflow.
- File and document extraction.
- Audio and video processing foundations.
- Sandbox execution framework.
- Resource and egress controls.
- Execution audit records.
- Sandbox security test suite.

### 11.7 Acceptance criteria

- Untrusted uploads are quarantined before trusted processing.
- Malicious or unsupported files are handled safely.
- Tenant access controls apply to all artifacts.
- Sandbox workloads cannot access unauthorised tenant data.
- Network egress policies are enforced.
- Resource limits and cleanup are tested.
- Sandbox isolation is independently assessed.
- Multimodal processing failures are recoverable and auditable.

### 11.8 Exit gate

**GATE-P5:** Multimodal and sandbox security acceptance.

---

## 12. Phase 6 — Billing, Usage Management, and AdTech

**Indicative period:** May 2027

### 12.1 Objective

Implement deterministic billing, usage metering, financial controls, and privacy-separated advertising capabilities.

### 12.2 Billing and ledger

The `billing-ledger` shall be the authoritative financial service.

Implementation shall include:

- Account and subscription models.
- Usage measurement.
- Pricing configuration.
- Invoice generation.
- Payment-provider integration.
- Payment status tracking.
- Refund and adjustment workflows.
- Double-entry accounting.
- Reconciliation.
- Financial audit history.

### 12.3 Financial integrity

The ledger must support:

- Atomic double-entry posting.
- Currency-aware accounting.
- Immutable posted entries.
- Controlled draft-to-posted transitions.
- Compensating entries instead of silent modification.
- Provider-scoped idempotency.
- Duplicate payment protection.
- Reconciliation against external payment providers.
- Restricted financial permissions.

Agents may recommend financial actions, but deterministic ledger controls must validate and execute them.

### 12.4 Usage metering

Metering may cover:

- Model usage.
- Token consumption.
- Image processing.
- Audio and video processing.
- Storage.
- Sandbox execution.
- Workflow execution.
- API calls.
- Subscription entitlements.
- Other billable platform activities.

Usage records must be traceable to the relevant tenant, project, service, and billing period.

### 12.5 Advertising technology

The `adtech-service` shall provide the technical foundation for authorised advertising and monetisation.

Agent23 may coordinate approved advertising functions through this service.

Advertising data must remain separated from confidential customer data.

Prohibited advertising inputs include unauthorised access to:

- Private prompts.
- Source code.
- Uploaded customer files.
- Credentials.
- Confidential project activity.
- Private workflow content.
- Other restricted tenant information.

### 12.6 Advertising controls

Implement:

- Advertising eligibility policies.
- Consent and preference handling where required.
- Campaign and creative management.
- Placement management.
- Impression and click measurement.
- Fraud and abuse detection.
- Advertiser access controls.
- Data retention policies.
- Audit records.
- Reporting and reconciliation.

Any use of public, aggregated, or explicitly permitted data must be assessed for privacy, contractual, and regulatory compliance.

### 12.7 Deliverables

- Billing and ledger service.
- Usage metering framework.
- Subscription and entitlement foundations.
- Payment-provider integration.
- Financial reconciliation.
- AdTech service foundation.
- Advertising data separation.
- Advertising audit and reporting.

### 12.8 Acceptance criteria

- Financial entries are atomic and auditable.
- Posted ledger entries cannot be silently modified.
- Duplicate payment events are safely handled.
- Usage records are tenant-aware.
- Billing calculations are deterministic and tested.
- Payment reconciliation is demonstrable.
- AdTech cannot access prohibited confidential data.
- Advertising consent and data-use policies are enforced where applicable.

### 12.9 Exit gate

**GATE-P6:** Financial integrity and advertising data-separation acceptance.

---

## 13. Phase 7 — Frontend Applications and Integrated User Experience

**Indicative period:** June–July 2027

### 13.1 Objective

Deliver the user-facing application family and integrate it with the backend platform.

### 13.2 Main application

`app.worklexx.ai` is the primary customer workspace.

Its proposed capabilities include:

- Account registration and login.
- Organisation and workspace management.
- Project creation.
- Natural-language software requirements.
- Project planning and architecture views.
- AI-assisted development.
- Agent activity and task status.
- Code and artifact management.
- Test and debugging results.
- Approval requests.
- Usage and billing dashboards.
- Notifications.
- Documentation access.

### 13.3 Public website

`worklexx.ai` shall provide:

- Product overview.
- Platform capabilities.
- Use cases.
- Pricing information.
- Security and trust information.
- Documentation links.
- Contact and support information.
- Registration and onboarding entry points.

### 13.4 Worklexx Video

`video.worklexx.ai` shall provide the approved video-related user experience, subject to the multimodal service capabilities and processing limits.

### 13.5 Worklexx Images

`images.worklexx.ai` shall provide the approved image-related user experience, including image processing and generation workflows where authorised.

### 13.6 Worklexx Docs

`docs.worklexx.ai` shall provide:

- User documentation.
- Developer documentation.
- API references.
- Integration guides.
- Platform policies.
- Troubleshooting resources.
- Release notes.

### 13.7 Frontend architecture

The frontend shall use the approved TypeScript architecture and shared UI conventions.

Implementation must distinguish:

- Client-side interface state.
- Server-authoritative application data.
- Durable workflow state.
- Realtime notification and transport state.

Zustand may be used for appropriate client-side state. TanStack Query may manage server state. SSE or WebSocket connections may provide realtime updates.

The backend and durable workflow system remain authoritative.

### 13.8 User experience requirements

The platform should provide:

- Responsive desktop and mobile layouts.
- Accessible interface components.
- Clear validation and error messages.
- Visible task progress.
- Workflow status and history.
- Approval prompts.
- Secure session handling.
- Appropriate loading and retry states.
- Reconnection and state resynchronisation.
- Clear usage and billing information.

### 13.9 Deliverables

- Main Worklexx application.
- Public website.
- Video application.
- Images application.
- Documentation application.
- Shared UI components.
- API integration.
- Realtime task-status interface.
- Accessibility and responsive-design tests.

### 13.10 Acceptance criteria

- Each application is integrated with its approved backend boundary.
- Authentication and authorisation are enforced.
- Tenant-specific information is correctly isolated.
- Workflow status is accurately represented.
- Realtime reconnection and resynchronisation work.
- Critical user journeys pass end-to-end testing.
- Accessibility and responsive-design requirements are tested.
- No frontend is treated as the authority for sensitive backend decisions.

### 13.11 Exit gate

**GATE-P7:** Integrated frontend and user-experience acceptance.

---

## 14. Phase 8 — System Validation, Production Readiness, and Controlled Launch

**Indicative period:** August–September 2027

### 14.1 Objective

Validate the integrated platform and establish production readiness before any controlled launch.

### 14.2 Scope

- System integration testing.
- End-to-end testing.
- Security testing.
- Tenant-isolation testing.
- Performance and load testing.
- Reliability testing.
- Workflow recovery testing.
- Backup and disaster recovery testing.
- Financial reconciliation testing.
- User acceptance testing.
- Operational readiness.
- Documentation and support readiness.
- Controlled release planning.

### 14.3 Functional validation

Test the full platform lifecycle:

1. User registration and authentication.
2. Organisation and tenant creation.
3. Project creation.
4. Requirements submission.
5. AI planning and architecture generation.
6. Agent orchestration.
7. Code generation.
8. Sandbox execution.
9. Testing and debugging.
10. Human approval where required.
11. Artifact storage and retrieval.
12. Usage measurement.
13. Billing and payment workflows.
14. Audit and reporting.

### 14.4 Security validation

Perform security assessment covering:

- Authentication and session security.
- Authorisation and privilege escalation.
- Tenant isolation.
- API security.
- Prompt injection and tool abuse.
- Sandbox escape and network egress.
- Secrets exposure.
- Dependency and supply-chain risks.
- Object storage access.
- Git and source-code isolation.
- Financial workflow abuse.
- Approval bypass and replay.
- AdTech data separation.
- Logging and sensitive-data exposure.

Security scanning alone does not establish that the platform is secure. Findings must be assessed, prioritised, remediated, and retested.

### 14.5 Performance validation

Performance testing must establish measured baselines for:

- API response times.
- Workflow completion times.
- Agent execution latency.
- Model-routing latency.
- Multimodal processing throughput.
- Sandbox provisioning and execution.
- Database query performance.
- Storage performance.
- Concurrent tenant workloads.
- Frontend loading and responsiveness.

Targets must be distinguished from measured results and tied to documented test conditions, datasets, versions, and environments.

### 14.6 Reliability and recovery validation

Test:

- Service restarts.
- Worker interruptions.
- Workflow recovery.
- Duplicate events.
- Provider outages.
- Database failover.
- Queue and event-delivery failures.
- Storage recovery.
- Backup restoration.
- Ledger reconciliation.
- Secret and encryption-key recovery.
- Full-platform disaster recovery.

Cloud SQL high availability alone does not establish full-platform disaster recovery.

Recovery testing must account for databases, workflow state, object storage, Git, financial records, identity, KMS, secrets, and infrastructure configuration.

RPO and RTO remain pending formal approval and successful recovery testing.

### 14.7 Operational readiness

Establish:

- Monitoring dashboards.
- Alerting rules.
- Incident-response procedures.
- Escalation paths.
- On-call responsibilities.
- Backup and restoration procedures.
- Change-management controls.
- Release and rollback procedures.
- Security incident handling.
- Support and customer communication.
- Cost and capacity monitoring.

### 14.8 Controlled launch

Any launch must be subject to explicit approval.

The release plan may use:

- Internal testing.
- Private preview.
- Limited pilot.
- Controlled beta.
- Gradual expansion.
- General availability.

The launch sequence, customer eligibility, operational capacity, and commercial commitments must be approved separately.

### 14.9 Deliverables

- Integrated test report.
- Security assessment report.
- Performance benchmark report.
- Tenant-isolation test evidence.
- Backup and disaster recovery test report.
- Financial reconciliation evidence.
- User acceptance report.
- Production operations runbooks.
- Release and rollback plan.
- Production readiness assessment.
- Controlled launch approval record.

### 14.10 Acceptance criteria

- Critical user journeys pass.
- No unresolved critical security findings remain.
- High-risk findings have approved remediation or documented risk disposition.
- Tenant isolation is independently tested.
- Financial reconciliation is demonstrated.
- Workflow recovery is tested.
- Backup restoration is demonstrated.
- RPO and RTO are approved and tested against the agreed targets.
- Operational ownership is assigned.
- Support and incident-response processes are ready.
- Production deployment approval is recorded.
- Protected GitHub operations approval is separately recorded where applicable.

### 14.11 Exit gate

**GATE-P8:** Production readiness and controlled launch approval.

Passing technical tests does not automatically authorise production deployment.

---

## 15. Cross-Phase Approval Gate Framework

The roadmap uses phase exit gates and the separately defined platform approval gates.

These are related but not interchangeable.

### 15.1 Platform approval gates

| Gate | Defined Purpose | Roadmap Application |
|---|---|---|
| GATE-01 | Pending formal definition | Must not be assumed |
| GATE-02 | Pending formal definition | Must not be assumed |
| GATE-03 | Production deployment approval | Required before production deployment |
| GATE-04 | Protected GitHub operations approval | Required for operations within its approved scope |
| GATE-05 | Destructive database operations and migrations; detailed scope and enforcement pending owner confirmation | Do not perform designated destructive operations without explicit Project Owner authorization while the full gate policy is being confirmed |
| GATE-06 | Consequential external integrations and live-account actions; detailed scope and enforcement pending owner confirmation | Do not activate designated consequential external actions or live accounts without explicit Project Owner authorization while the full gate policy is being confirmed |

GATE-05 is intended to govern designated destructive or materially consequential database operations, including destructive schema migrations and incompatible data transformations. GATE-06 is intended to govern designated consequential external integrations and live-account actions with material external, financial, operational, or customer impact. Their complete scope, exceptions, approval authority, enforcement, and evidence requirements remain subject to explicit Project Owner confirmation. GATE-01 and GATE-02 remain pending formal definition.

### 15.2 GATE-03 and GATE-04 separation

GATE-03 and GATE-04 must remain independent.

GATE-03 governs production deployment approval.

GATE-04 governs protected GitHub operations approval.

Approval records must be bound to the relevant action, project or tenant, artifact or commit digest, environment, authorisation, expiry or revocation state, and audit record.

Material changes must invalidate the relevant approval where the approved artifact or action has changed.

An approval for one gate must not be treated as approval for the other.

### 15.3 Phase exit gates

Phase exit gates provide evidence that a phase's deliverables meet their acceptance criteria.

They do not automatically confer permission to perform actions governed by platform approval gates.

---

## 16. Dependencies and Critical Path

The development sequence has the following major dependencies:

| Capability | Depends On |
|---|---|
| Repository implementation | Phase 0 approval and repository governance |
| Identity and tenant security | Engineering foundation |
| API Gateway | Engineering foundation and identity integration |
| Agent Orchestrator | API Gateway, identity, workflow infrastructure |
| Agent ecosystem | Orchestrator, model routing, tool governance |
| Multimodal processing | Storage, tenant controls, service infrastructure |
| Secure sandbox | Identity, tenant isolation, infrastructure, security controls |
| Billing and ledger | Identity, database, audit, usage events |
| AdTech | Identity, consent and data policies, service isolation |
| Frontend integration | Stable API contracts and backend capabilities |
| Production deployment | Full validation, operations, security, approvals |

### 16.1 Critical path considerations

The following capabilities are likely to influence the overall schedule:

1. Identity-provider selection.
2. Tenant-isolation implementation.
3. Workflow-engine selection.
4. Secure sandbox proof of concept.
5. Database and vector-search validation.
6. Payment-provider integration.
7. Multimodal provider selection.
8. Production and disaster recovery architecture.
9. Security assessment and remediation.
10. Availability of approved infrastructure and engineering resources.

Delays in these dependencies may affect multiple downstream phases.

---

## 17. Human Decisions Required Before or During Implementation

The following decisions have been recorded. Their architectural approval does not remove implementation validation, separate operational approvals, or phase-gate requirements.

| Decision ID | Decision | Recorded outcome |
|---|---|---|
| HD-01 | Identity provider | Approved — managed identity-provider approach; provider and implementation validation remain required |
| HD-02 | Workflow engine | Approved — Temporal Cloud preferred initially, conditional on POC and due diligence |
| HD-03 | Cloud regions | Approved architectural direction — AWS Cape Town primary and Ireland DR; legal, security, POC and operational validation remain required |
| HD-04 | Backend topology | Approved — six logical deployable backend services; physical topology validation remains required |
| HD-05 | Vector storage | Approved — PostgreSQL with pgvector preferred initially; model/use-case-specific dimensions and POC-05 required |
| HD-06 | Recovery objectives | Approved — tiered RPO/RTO architectural objectives; POC-15 and operational validation required |
| HD-07 | Risk authority | Approved — Project Owner is sole initial risk acceptance authority; no delegation |
| HD-08 | Approval gates | Approved — six independent gates; Project Owner is sole initial approval authority |
| HD-REP-06 | Database schema and migration governance | Approved — service-owned schemas and independent migration histories across all six backend services; implementation and execution remain separately controlled |
| HD-REP-12 | Customer identity, authentication, authorisation and access lifecycle governance | Approved — architectural direction only; identity provider selection, connection and production rollout remain separately controlled |

Additional decisions may be added through the Architecture Decision Record process.

Any remaining decisions, implementation details, or validation conditions must be recorded explicitly; approval of an architectural direction must not be silently converted into implementation or execution authorization.

---

## 18. Non-Functional Requirements and Validation

The platform shall establish measurable non-functional requirements.

These include:

### 18.1 Performance

- API latency.
- Workflow latency.
- Agent response time.
- Database performance.
- Frontend performance.
- Multimodal processing throughput.
- Sandbox startup and execution time.

### 18.2 Availability

- Service availability.
- Workflow recovery.
- Database availability.
- Provider resilience.
- Realtime connection recovery.
- Storage availability.

### 18.3 Scalability

- Concurrent users.
- Concurrent tenants.
- Concurrent workflows.
- Agent execution capacity.
- Sandbox concurrency.
- Multimodal processing capacity.
- Database growth.
- Storage growth.

### 18.4 Security

- Tenant isolation.
- Least privilege.
- Secure authentication.
- Data encryption.
- Secrets protection.
- Sandbox isolation.
- Auditability.
- Supply-chain security.

### 18.5 Maintainability

- Modular code.
- Versioned APIs.
- Automated tests.
- Documentation.
- Dependency management.
- Reproducible builds.
- Change traceability.

### 18.6 Accessibility

- Responsive interface design.
- Keyboard navigation.
- Appropriate contrast.
- Screen-reader compatibility.
- Accessible forms and feedback.
- Usable error and status messages.

### 18.7 Measurement rules

Every performance or quality target must be recorded with:

- Metric definition.
- Target value.
- Measurement method.
- Test environment.
- Dataset or workload.
- Software and model versions.
- Measured result.
- Acceptance threshold.
- Evidence reference.

A target is not a measured result. A benchmark under one environment does not automatically apply to another.

---

## 19. Testing Strategy

Testing shall be continuous throughout development.

### 19.1 Unit testing

Validate individual functions, modules, business rules, and deterministic service behaviour.

### 19.2 Integration testing

Validate interactions between services, databases, workflow systems, external providers, and internal APIs.

### 19.3 Contract testing

Verify that service interfaces and generated client contracts remain compatible.

### 19.4 End-to-end testing

Validate complete user and system workflows across frontend and backend components.

### 19.5 Security testing

Test authentication, authorisation, tenant isolation, sandbox controls, secrets handling, approval enforcement, and data separation.

### 19.6 Agent evaluation

Evaluate agent outputs for correctness, consistency, tool-use safety, instruction compliance, and resilience to adversarial inputs.

### 19.7 Performance testing

Measure throughput, latency, concurrency, resource use, and capacity limits.

### 19.8 Recovery testing

Validate workflow recovery, backup restoration, disaster recovery, and reconciliation.

### 19.9 Regression testing

Re-run relevant tests after changes to services, agents, models, dependencies, policies, and infrastructure.

### 19.10 Evidence management

Test results must be reproducible and traceable to:

- Commit or artifact digest.
- Environment.
- Test suite and version.
- Execution date.
- Test result.
- Relevant defect or exception.
- Reviewer or responsible owner.

---

## 20. Security and Risk Management Across Phases

Security and risk management are continuous activities.

The risk register shall be updated as implementation progresses.

The programme must actively manage, at minimum:

- Cross-tenant data leakage.
- Identity compromise.
- Session abuse.
- Privilege escalation.
- Prompt injection.
- Unauthorised tool execution.
- Sandbox escape.
- Data loss and corruption.
- Backup and disaster recovery failure.
- Approval bypass and replay.
- Privacy and cross-border compliance.
- Ledger inconsistency.
- Payment fraud.
- Insider and privileged-access abuse.
- Supply-chain compromise.
- Provider outages.
- Cost overruns.
- Capacity exhaustion.

A proposed control does not reduce residual risk until it is implemented and supported by evidence of effectiveness.

Risk acceptance must be performed by the formally designated authority. The Project Owner's risk authority must not be assumed without explicit identification or delegation.

---

## 21. Deployment and Environment Progression

The proposed environment progression is:

`Local Development → Automated CI → Development Environment → Staging Environment → Production Environment`

Each environment must have defined:

- Purpose.
- Access permissions.
- Data classification.
- Configuration.
- Secrets.
- Deployment controls.
- Monitoring.
- Backup requirements.
- Retention.
- Approval requirements.

Production credentials and customer data must not be copied into development environments without an explicitly approved, secure, and compliant process.

### 21.1 Deployment strategy

Deployment strategies may include:

- Rolling deployments.
- Blue-green deployments.
- Canary releases.
- Feature flags.
- Controlled rollback.

The strategy must be selected according to service architecture, state compatibility, risk, and operational capability.

### 21.2 Infrastructure

Google Cloud Platform and GKE are proposed backend infrastructure choices, subject to approval and validation.

Vercel is a proposed frontend hosting option.

The final hosting design must account for frontend runtime requirements, serverless limitations, long-running workers, ingress protection, data residency, cost, and operational responsibility.

No cloud provisioning is authorised by this roadmap.

---

## 22. Operational Readiness and Service Ownership

Before production release, every deployable service must have an accountable operational owner.

The ownership model must define:

- Service owner.
- Technical owner.
- Security owner.
- Data owner.
- Operational escalation.
- Incident response.
- Change approval.
- Release responsibility.
- Recovery responsibility.
- Cost accountability.

The six backend service units must have documented service-level operational responsibilities.

The platform must also define ownership for:

- Frontend applications.
- Identity infrastructure.
- Workflow infrastructure.
- Databases.
- Object storage.
- Git and artifact repositories.
- Monitoring and logging.
- Encryption and secrets.
- External integrations.

Unassigned ownership is a production-readiness gap.

---

## 23. Indicative Programme Timeline

The following timeline is a planning estimate, not a contractual delivery schedule.

| Period | Phase | Primary Focus |
|---|---|---|
| November 2026 | Phase 0 | Architecture, documentation, decisions, approval |
| December 2026 | Phase 1 | Engineering and repository foundations |
| January 2027 | Phase 2 | Identity, security, tenant isolation |
| February 2027 | Phase 3 | Backend services and workflows |
| March 2027 | Phase 4 | AI orchestration and agents |
| April 2027 | Phase 5 | Multimodal and sandbox |
| May 2027 | Phase 6 | Billing, metering, and AdTech |
| June 2027 | Phase 7 | Frontend integration |
| July 2027 | Phase 7 | Frontend completion and user acceptance |
| August 2027 | Phase 8 | System validation and operational readiness |
| September 2027 | Phase 8 | Controlled launch decision and approved release |

The schedule may be revised following technical proof of concepts, resource allocation, risk assessment, and formal phase reviews.

---

## 24. Resource and Capability Planning

The roadmap requires a combination of engineering, security, infrastructure, product, and operational capabilities.

Indicative capability areas include:

- Technical architecture.
- Backend engineering.
- Frontend engineering.
- AI and agent engineering.
- Machine learning and model integration.
- Database engineering.
- Cloud and platform engineering.
- Cybersecurity.
- Quality assurance and test automation.
- UX and accessibility.
- DevOps and SRE.
- Financial systems and payment integration.
- Privacy and compliance.
- Product management.
- Technical documentation.
- Customer support and operations.

The final staffing model, team size, procurement requirements, and budget must be separately assessed and approved.

No staffing level, subscription, service contract, or expenditure is authorised by this document.

---

## 25. Cost and Budget Governance

The programme must establish a cost model before significant infrastructure or external-service commitments.

Cost categories include:

- Cloud compute.
- Managed databases.
- Object storage.
- Network traffic and egress.
- Workflow orchestration.
- AI model inference.
- Multimodal processing.
- Sandbox execution.
- Identity services.
- Monitoring and logging.
- Security tooling.
- Payment-provider fees.
- External APIs.
- Software subscriptions.
- Support and operations.

Cost controls should include:

- Budget limits.
- Usage metering.
- Alerts.
- Resource quotas.
- Sandbox limits.
- Model-routing cost policies.
- Storage lifecycle management.
- Idle-resource cleanup.
- Tenant-level usage visibility.
- Periodic cost reviews.

Actual budget and financial authority must be established independently.

---

## 26. Change Management and Roadmap Updates

This roadmap is a controlled planning document.

Changes must be traceable.

A roadmap change should record:

- Change identifier.
- Date.
- Requestor.
- Reason.
- Affected phase.
- Affected architecture documents.
- Dependency impact.
- Risk impact.
- Cost impact.
- Schedule impact.
- Approval status.
- Decision reference.

Material architecture changes must be assessed through the ADR process.

A roadmap revision must not silently override an accepted architecture decision or an existing approval gate.

---

## 27. Phase Completion and Acceptance Records

Each phase must produce a completion record containing:

1. Phase identifier and name.
2. Approved scope.
3. Completed deliverables.
4. Outstanding work.
5. Test evidence.
6. Security findings.
7. Risk updates.
8. Architecture changes.
9. Budget and resource status.
10. Known limitations.
11. Acceptance decision.
12. Approver identity and authority.
13. Approval date.
14. Related commit or artifact references.

A phase must not be marked accepted solely because its scheduled end date has passed.

Incomplete work must be recorded transparently.

---

## 28. Roadmap Risks and Mitigation

| Risk | Potential Impact | Proposed Mitigation |
|---|---|---|
| Unresolved architecture decisions | Rework and delay | Resolve through documented ADRs |
| Identity-provider uncertainty | Authentication redesign | Complete identity proof of concept |
| Tenant-isolation weaknesses | Cross-customer data exposure | Adversarial isolation testing |
| Workflow-engine uncertainty | Reliability and operational risk | Complete workflow proof of concept |
| Sandbox vulnerabilities | Code execution compromise | Threat modelling and isolation testing |
| Model-provider changes | Agent instability | Capability-based model catalogue |
| Multimodal cost escalation | Budget pressure | Quotas, metering, routing, and limits |
| Payment integration issues | Financial errors | Idempotency and reconciliation testing |
| AdTech data leakage | Privacy and trust failure | Enforced service and data separation |
| Resource constraints | Schedule slippage | Resource and dependency planning |
| DR design gaps | Extended service outage or data loss | Full-platform recovery exercises |
| Approval ambiguity | Unauthorised actions | Formal gate definitions and enforcement |

These risks must be integrated into the formal Risk Register.

---

## 29. Future Expansion Beyond the Initial Roadmap

The initial programme establishes the platform foundation.

Future expansion may include:

- Additional AI agent capabilities.
- More model providers.
- Additional multimodal workflows.
- Advanced software development lifecycle automation.
- Enterprise governance features.
- Additional integrations.
- Advanced analytics.
- International data-region support.
- Expanded billing and commercial models.
- Additional developer tools.
- Partner and marketplace ecosystems.
- More sophisticated evaluation and continuous-improvement systems.

Future expansion must preserve the approved service boundaries, security model, tenant isolation, financial controls, and governance framework.

New capabilities must be assessed for whether they belong within existing services or require a formally approved architecture change.

---

## 30. Phase 1 Readiness Conditions

Before Phase 1 begins, the following conditions must be satisfied:

- All 13 Phase 0 documents are available.
- Cross-document consistency review is completed.
- The Phase 0 inspection report is completed.
- The document inventory and SHA-256 baseline are preserved.
- Material architecture contradictions are resolved or formally dispositioned.
- Human decisions required for Phase 1 are identified.
- The Project Owner formally approves the Phase 0 baseline.
- Phase 1 scope and acceptance criteria are approved.
- Engineering resources and budget are authorised.
- Required repository and operational permissions are explicitly granted.

Approval to begin Phase 1 must be recorded separately.

The existence of this roadmap is not Phase 1 authorisation.

---

## 31. Implementation and Repository Boundary

This document defines proposed future work.

It does not authorise:

- Editing application source code.
- Creating database schemas or executing migrations.
- Running SQL against development, staging, or production databases.
- Provisioning cloud resources.
- Purchasing services or subscriptions.
- Creating or modifying production credentials.
- Creating Git branches.
- Committing or pushing repository changes.
- Deploying services.
- Enabling production integrations.
- Launching the platform.
- Beginning Phase 1 without explicit approval.

All future implementation actions must follow the applicable repository, security, review, approval, and change-management procedures.

---

## 32. Related Architecture Documents

This roadmap must be read together with:

| Document | Document ID |
|---|---|
| Architecture Overview | WLX-ARCH-001 |
| System Architecture | WLX-ARCH-002 |
| Technology Stack | WLX-ARCH-003 |
| Repository Structure | WLX-ARCH-004 |
| Agent Ecosystem | WLX-ARCH-005 |
| Service Boundaries | WLX-ARCH-006 |
| Database Architecture | WLX-ARCH-007 |
| Security Architecture | WLX-ARCH-008 |
| Deployment Architecture | WLX-ARCH-009 |
| Risk Register | WLX-ARCH-011 |
| ADR Register | WLX-ARCH-012 |
| Phase 0 Inspection Report | WLX-ARCH-013 |
| Testing Strategy | WLX-ARCH-014 |
| Monitoring and Observability | WLX-ARCH-015 |
| Cost and Scalability | WLX-ARCH-016 |

If a roadmap statement conflicts with an approved architecture decision, the conflict must be reviewed and resolved through the appropriate governance process. This document does not silently supersede other architecture documents.

---

## 33. Document Maintenance

This document shall be reviewed:

- At the completion of Phase 0.
- Before Phase 1 approval.
- At each phase exit review.
- When a material architecture decision changes.
- When a significant risk affects the programme.
- When scope, schedule, cost, or resources change materially.
- Before production-readiness assessment.

All revisions must update the document version, change history, and approval record as appropriate.

---

## 34. Document Status and Limitations

This document represents the proposed development roadmap for the Worklexx AI Software Factory.

Its timeline, technology choices, phase sequencing, and deliverables are planning baselines subject to review and approval.

It does not represent:

- Completed implementation.
- Verified production capability.
- A contractual delivery commitment.
- An approved project budget.
- An approved procurement decision.
- Production-readiness certification.
- Formal security certification.
- Authorisation to begin Phase 1.

The roadmap must be updated when approved decisions or verified implementation evidence materially change the programme.

---

## 35. Final Status

**Document ID:** WLX-ARCH-010  
**Document Title:** Development Roadmap  
**Version:** 1.0  
**Status:** Proposed Phase 0 Architecture Baseline  
**Implementation Status:** Not authorised by this document  
**Next Governance Step:** Complete Phase 0 cross-document review and obtain formal Project Owner approval.

**End of Document — WLX-ARCH-010**

## HD-REP-07 — Approved Repository Backup and Recovery Direction (2026-11-20)

The Project Owner approved layered, provider-independent protection for Factory source, Worklexx-managed customer repositories, customer-managed repositories within authorised scope, and supporting development records/artifacts. Protect Git history/refs/LFS, repository metadata, artifacts, project mappings and audit records as distinct recovery components. Use independent off-site and immutable/deletion-resistant copies, separate backup identities and key custody, encryption, least privilege, audit, tenant isolation, integrity verification, retention and portability. Worklexx-managed and customer-managed backup responsibilities must be contractually distinguished.

Initial objectives include daily full plus incremental/event-based Factory source capture; continuous/frequent Git replication and daily metadata backup for Worklexx-managed projects; and customer-managed synchronisation only within authorised scope. Proposed retention: 90 days daily / 12 months monthly. Proposed RPO/RTO: critical Factory source 15 minutes/4 hours; active customer source 1 hour/8 hours; metadata 4 hours/24 hours; historical/noncritical artifacts 24 hours/48 hours. These objectives are not verified SLAs and require technical, legal, cost, contractual and operational validation, including HD-06/POC-15 alignment. Actual restoration exercises and evidence are mandatory; a successful backup job alone is insufficient.

**Scope limitation:** Architectural direction only. No backup configuration, infrastructure provisioning, subscriptions/spending, repository settings/permission changes, customer account connections, backup/restore/migration execution, CI/CD activation, production implementation or Phase 1 is authorised. Applicable HD-08 gates remain in force.

## HD-REP-08 — Approved Build Integrity and Supply-Chain Security Direction (2026-11-20)

The Project Owner approved a policy-controlled, least-privilege and verifiable automation architecture. Future implementation planning must separate untrusted PR validation from trusted release builds; default workflows to read-only permissions; scope write permissions per job; prefer short-lived credentials; pin third-party actions to immutable commit SHAs; protect workflow definitions; and prevent untrusted code from accessing privileged secrets.

The supply-chain baseline includes lockfile and tool-version enforcement, dependency integrity checks, direct/transitive vulnerability and licence scanning, secret scanning, dependency review, SAST and applicable DAST, and machine-readable SBOM generation. Builds must run in isolated environments, with tenant/project-specific credential, cache, job and artifact boundaries. Trusted release artifacts require checksums, integrity verification, source-to-artifact provenance and protected signing-key management. SLSA and Sigstore are candidates for evaluation, not final product selections.

The Factory platform repository, Worklexx-managed customer projects and customer-managed repositories remain separate trust boundaries. AI agents may assist with authorised validation, tests, scanning and evidence generation but cannot approve their own PRs/releases, grant themselves access or bypass protected operations. Build, verification, release approval, publication and production deployment remain separate activities under HD-08.

**Required POCs:** POC-REP-08-01 through POC-REP-08-12 cover workflow permissions, untrusted PR isolation, dependency integrity, scanning, SBOMs, artifact integrity/provenance, build/cache isolation, tenant isolation, credential protection, release/publication separation, compromised dependency/workflow scenarios and audit traceability.

**Scope limitation:** Architectural direction only. No CI/CD activation, repository configuration, credentials, signing keys, paid services, infrastructure, production builds, artifact publication, releases, deployments or Phase 1 work is authorised. Applicable HD-08 gates remain mandatory.


## HD-REP-09 — Observability and Audit Governance Workstream

**Approved architectural direction (2026-11-20):** establish provider-independent repository and platform audit coverage, protected evidence storage, privacy-aware event handling, security-event monitoring, alert escalation, investigation and customer-scoped audit access. Preserve the distinction between Worklexx-managed and customer-managed repositories. This workstream does not add a seventh backend deployable.

**Prerequisites before operational reliance:** define event schemas and source coverage; assess provider audit APIs and gaps; specify event retention and legal-hold rules; establish privacy/redaction requirements; validate tenant/project isolation; define detection, severity and incident workflows; and complete POC-REP-09-01 through POC-REP-09-12 with retained evidence and remediation. Tool selection and operational design remain subject to separate review.

**Authorisation boundary:** roadmap inclusion is not implementation authority. No telemetry/webhook activation, GitHub audit configuration, SIEM subscription, spending, infrastructure, credentials, customer connections, production integration, automated incident response or Phase 1 activity is authorised. Applicable HD-08 gates and separate Project Owner approvals remain mandatory.


## HD-REP-10 — Customer Project Lifecycle, Portability and Exit Governance Workstream

**Approved architectural direction (2026-11-20):** plan a customer-centred project lifecycle control plane consistent with HD-REP-05, HD-REP-07, HD-REP-08 and HD-REP-09. Each project requires immutable identity, customer/tenant and ownership mapping, hosting mode, repository mapping, lifecycle state and auditable transitions. Lifecycle states include Created, Provisioning, Active, Suspended, Archived, Exported/Transferred, Disconnected, Deletion Pending and Deleted.

The workstream must define and validate the two approved hosting modes (Worklexx-managed and customer-managed), ownership/IP and licence disclosures, collaborator/transfer authority, customer-scoped source/history/LFS/metadata export, independent import, credential re-establishment, customer exit, integration disconnection, entitlement suspension safeguards, retention/legal holds and verified deletion. Export is not ownership transfer; suspension is not deletion; customer-managed disconnection must not delete the customer's repository. No universal grace period or retention duration is established; legal, regulatory, contractual and operational review is required.

**Prerequisites before operational reliance:** complete POC-REP-10-01 through POC-REP-10-15, including negative cross-tenant tests, export/import integrity, secret exclusion, legal-hold/deletion controls, backup expiry/restore safeguards, credential revocation, agent prohibited-action tests and end-to-end audit evidence. Add and formally assess RSK-30. Record provider limitations and customer responsibility boundaries.

**Authorisation boundary:** Roadmap inclusion and architectural approval do not authorise project provisioning, customer integrations, OAuth/app installation, ownership/repository transfer, live suspension/archive/deletion, production migration, retention/backup configuration, infrastructure provisioning, spending, GitHub permission/settings changes, CI/CD activation, production deployment or Phase 1. Applicable HD-08 gates and separate Project Owner approvals remain mandatory.



## HD-REP-11 — Customer Data Isolation, Privacy and Data Governance Workstream

**Approved architectural direction (2026-11-20):** Establish privacy-by-design data governance across Factory platform data and customer-generated projects. Define Public/Internal/Confidential/Restricted classifications; data inventory, purpose limitation and minimisation; lawful/contractual processing authority; ownership and controller/processor responsibilities; and trusted tenant/project-scoped access across APIs, all six services, databases/RLS, pgvector, files, indexes, embeddings, agents, workflows, queues, caches, multimodal temporary data, build environments, artifacts, logs, backups, exports and restoration.

**Prerequisites before operational reliance:** Complete POC-REP-11-01 through POC-REP-11-15. Validate cross-tenant negative cases, RLS and vector filtering/deletion, agent least privilege, prompt-injection resistance, multimodal lifecycle, external provider training/retention/location controls, encryption/key management, cross-border transfer assessments, applicable data-subject rights, deletion across derived and backup data, audit redaction and hosting responsibility boundaries. Add and formally assess RSK-31; scores remain pending until formally assessed. Align with HD-REP-07, HD-REP-09 and HD-REP-10.

**Delivery sequencing:** During Phase 0, complete architecture, data-flow inventories, classification, role/responsibility mapping, provider due-diligence criteria, privacy threat modelling, retention/legal-hold requirements and POC plans. Phase 1 implementation, test environments, data integrations, key-management configuration and privacy tooling require separate authorisation and applicable HD-08 gates. Live customer/personal-data processing must not begin until legal, security, contractual, regional and technical prerequisites are satisfied.

**Authorisation boundary:** Roadmap inclusion and architectural approval do not authorise live data processing, customer or external provider connections, OAuth/app installation, infrastructure/database/storage provisioning or modification, credentials/keys, paid services, GitHub permission/settings changes, production monitoring/workflow activation, migrations, deletion/restoration, production deployment or Phase 1. Applicable HD-07/HD-08 controls and separate Project Owner approvals remain mandatory.


## HD-REP-12 — Customer Identity, Authentication, Authorisation and Access Lifecycle Workstream

**Approved architectural direction (2026-11-20):** plan a centralised managed-identity integration with Worklexx-controlled application authorisation and service-enforced tenant, project and resource boundaries. Preserve HD-01 and HD-08. Authentication establishes identity but does not automatically authorise access. Distinguish human, organisation, membership, project, agent, service, workload and external-integration identities.

**Architecture and planning activities:** define identity mapping and organisation/project membership records; configurable role and permission catalogue; RBAC/ABAC and resource-level policy enforcement; standards-based identity federation/SSO options; MFA/passkey and recovery requirements; service/workload identity; agent delegation; API-key/token lifecycle; privileged and emergency access; session management; access reviews; suspension/deprovisioning; revocation propagation; identity privacy; and audit event coverage. Maintain separation of organisation administration from project ownership under HD-REP-10.

**Prerequisites before operational reliance:** complete POC-REP-12-01 through POC-REP-12-20, including provider portability, multi-organisation and cross-tenant negative tests, service and agent identity boundaries, session/revocation behaviour, recovery, concurrent role changes/cache invalidation, audit attribution, privacy, provider outage and fail-closed approval-gate enforcement. Add RSK-32; formal likelihood, impact and residual scores remain pending.

**Authorisation boundary:** This roadmap entry records an approved architectural workstream only. It does not authorise selecting/connecting an identity provider, creating customer accounts, configuring SSO/OAuth, changing user permissions, issuing live credentials, provisioning infrastructure/databases, purchasing services, changing GitHub permissions, activating production authentication/authorisation, running migrations, deploying production or starting Phase 1. Apply HD-07/HD-08 and obtain separate Project Owner approvals for applicable gates.


## HD-REP-13 — AI Agent Security, Delegation, Execution Boundaries and Human Oversight Governance (Approved 2026-11-20)

Adopt permission-controlled, policy-enforced, sandboxed and auditable agent execution for the 23 logical agent modules. This decision does not add a backend deployable or alter the approved six-deployable architecture. Agent intelligence is not authority: each agent has a distinct identity and bounded task, tenant/project, tool, data and time scope; versioned policies; resource limits; audit attribution; and revocation controls.

Five conceptual permission tiers: Tier 0 Observe; Tier 1 Prepare; Tier 2 Execute within controlled scope; Tier 3 Consequential action subject to independent approval and applicable control; Tier 4 prohibited authority (including self-approval and governance bypass). Tool permissions remain granular: inspect, write, PR creation, review, approval, merge, permission changes, deletion and transfer are separate capabilities. The tool-control boundary validates identity/scope, inputs and destinations, classification, policy and approval, then executes, verifies and audits.

Code execution uses an appropriately isolated sandbox within the approved sandbox-runner boundary: restricted networking, resource/time limits, filesystem/process isolation, credential separation, tenant/project-specific caches and artifact handling, and cleanup. Untrusted documents, source, web content, prompts and tool results are data—not policy or authority—and prompt injection must not override permissions, governance or gates. Delegation is task/time bounded, depth-limited, attributable, revocable and cannot expand the initiating authority.

Agent context and memory are scoped, classified, minimised, governed and tenant/project isolated. Outputs require independent verification appropriate to their risk; verification does not substitute for human approvals required by HD-08. Control retries, loops, concurrency, idempotency, resource/cost limits, cancellation and safe failure. Protected audit and monitoring align with HD-REP-09; privacy and data boundaries with HD-REP-11; identity and delegation with HD-REP-12; execution isolation and supply-chain controls with HD-REP-08; customer lifecycle with HD-REP-10.

Validation requirements: POC-REP-13-01 through POC-REP-13-24 (unexecuted) cover agent identity/scope, least privilege, tool authorization, policy enforcement, tier separation, gate binding, sandbox isolation, network/credential restrictions, resource limits, prompt-injection resistance, untrusted content, tenant/project isolation, delegation depth/authority, context/memory privacy, output verification, human oversight, audit attribution, revocation, concurrent actions/races, loops/retries/cancellation, failure/recovery, cost controls, abuse scenarios and end-to-end governance bypass attempts.

Add RSK-33 — AI Agent Misuse, Unsafe Execution, Privilege Escalation and Governance Bypass. Formal likelihood, impact, inherent and residual scores remain pending assessment; proposed controls do not reduce residual risk until implemented and evidenced.

Project Owner remains sole initial risk acceptance and approval authority under HD-07/HD-08. Applicable gates remain mandatory. This is architecture/documentation approval only: no agent execution in production, sandbox provisioning, external integrations, live customer data, credentials, CI/CD activation, GitHub configuration, database changes, paid services, production deployment or Phase 1 is authorised.

Approved workstream: HD-REP-13 agent governance architecture. Before operational reliance, complete POC-REP-13-01 through -24, formally assess RSK-33 and obtain separate approvals for implementation, integrations, spending, configuration and deployment as applicable. Approval here is not implementation authorisation.


## HD-REP-14 — API Contracts, Inter-Service Communication and Integration Governance (Approved 2026-11-20)

Approved workstream: contract-first, versioned, service-owned and validated interface governance across synchronous APIs, asynchronous events, Temporal workflows/activities, agent-tool interfaces, data schemas and external integrations. Roadmap activities include contract inventory and ownership, machine-readable schema conventions, independent contract versioning, consumer/provider compatibility analysis, standard error and correlation conventions, tenant/project authorization, idempotency/retry/failure policies, event replay and delivery controls, workflow replay compatibility, webhook security, external provider due diligence, contract test strategy and release traceability.

Use OpenAPI, JSON Schema and AsyncAPI standards directions where appropriate, subject to POC validation; no specific tooling, broker, schema registry, gateway configuration or infrastructure is selected. Preserve six backend deployables and existing service-owned schema/migration boundaries. Add RSK-34; formal scoring remains pending. Complete POC-REP-14-01 through POC-REP-14-24 before operational reliance. This workstream approval authorises documentation only, not implementation, integrations, credentials, spending, CI/CD, production deployment or Phase 1.


## HD-REP-15 — API Gateway Workstream (Approved 2026-11-20)

Approved workstream: define the gateway's logical boundary, public route inventory and ownership, identity-context propagation, service-side authorization responsibilities, tenant/project isolation, layered rate-limit and quota policy, edge/WAF/DDoS requirements, TLS/certificate lifecycle, request/upload validation, SSRF and outbound-destination restrictions, CORS, webhook protection, API version/deprecation, timeout/retry/idempotency, backpressure/circuit-breaking, safe errors, observability/audit and regional resilience. Preserve six backend deployables and 23 agent modules; do not select a vendor, product, broker, infrastructure topology or numerical global quota in this decision.

Complete POC-REP-15-01 through -24 before operational reliance and formally assess RSK-35. Gateway controls complement, and do not replace, HD-REP-11/12/13 service-side authorization and tenant isolation or HD-08 approval gates. Approval authorises documentation only, not installation, configuration, external services, credentials, spending, CI/CD, live data processing, production deployment or Phase 1.


## HD-REP-16 — API Security and Cryptographic Controls Workstream (Approved 2026-11-20)

Approved workstream: define controlled secrets and key lifecycle; human/service/agent/integration credential boundaries; short-lived workload identity; token and API-key validation/revocation; purpose-separated encryption, token-signing, artifact-signing, webhook and transport keys; certificate lifecycle; encryption in transit/at rest; secure service-to-service communication; webhook authenticity/replay protection; secret scanning/redaction; key compromise response; agent restrictions; and audit/monitoring.

Do not select a vendor, KMS/HSM, certificate authority, secrets product, cryptographic hardware provider or paid security service in this decision. Require POC-REP-16-01 through -26 and formal RSK-36 assessment before operational reliance. Preserve HD-08 approval gates and all existing deployment/implementation boundaries. This workstream authorises documentation only, not credentials, keys, infrastructure, integrations, spending, CI/CD, production changes or Phase 1.



## HD-REP-17 — Secure SDLC and Vulnerability Management Workstream (Approved 2026-11-20)

Add a Phase 0 architecture and validation workstream for application security across five frontend applications, six backend deployables, shared packages, 23 logical agent modules and generated customer projects. Define security requirements and classification, threat-modelling triggers, secure coding standards, independent review, risk-based SAST/SCA/secret scanning/DAST, API and frontend security testing, authorised penetration-testing criteria, vulnerability triage and remediation verification, customer-project security disclosures and release-security evidence.

Proposed internal vulnerability remediation/mitigation objectives are Critical 24 hours, High 7 calendar days, Medium 30 calendar days and Low 90 calendar days. These are not SLAs; contextual severity, active exploitation and exposure may require faster action. Exceptions require documented compensating controls, owner, expiry/review and Project Owner risk acceptance under HD-07. Critical findings require immediate escalation and assessment of whether affected activity must stop or be suspended.

Track POC-REP-17-01 through POC-REP-17-24 in TESTING_STRATEGY.md. All remain unexecuted and must not be reported as passed. Add RSK-37 to RISK_REGISTER.md; formal scores remain pending. This roadmap entry is documentation/planning only and does not authorise tool installation, CI/CD activation, source changes, external testing, infrastructure, spending, live data processing, production deployment or Phase 1.

---

## HD-REP-18 — Configuration and Environment Governance (Approved 2026-11-21)

Add configuration and environment governance as a Phase 0 architecture validation workstream. The intended logical environments are Development, Testing, Staging and Production, with independent configuration and access boundaries. Before Phase 1, define configuration ownership/contracts, classification, schema validation, secret references, feature-flag controls, deployment provenance, drift detection, rollback/recovery and customer-project isolation. Track POC-REP-18-01 through POC-REP-18-24 as unexecuted acceptance requirements, with owners, scope, preconditions, expected results, evidence, outcomes, defects and retest records. No environment provisioning, configuration application, CI/CD activation, paid service, production deployment or Phase 1 implementation is authorised by this decision.
