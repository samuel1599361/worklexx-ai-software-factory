# Worklexx AI Software Factory — Repository Structure Specification

## Document Metadata

- **Document ID:** WLX-ARCH-004
- **Status:** Revised Architecture Blueprint (Phase 0 Revision Cycle — Awaiting Final Human Review and Approval)
- **Author:** Principal Software Architect, DevSecOps Architect, Repository Governance Architect
- **Target Repository:** `https://github.com/samuel1599361/worklexx-ai-software-factory`
- **Classification:** Enterprise Technical Specification
- **Document Type:** Repository Organization and Governance Specification
- **Phase:** Phase 0 — Architecture and Design
- **Approval Status:** Pending explicit Project Owner approval

---

## 1. Purpose

This document defines the proposed repository organization, source-control structure, directory responsibilities, development conventions, and repository governance requirements for the Worklexx AI Software Factory.

It establishes a consistent structure for:

- Five frontend applications.
- Six deployable backend service units.
- Twenty-three logical AI agents.
- Shared libraries and contracts.
- Database schemas and migrations.
- Automated testing.
- Security and compliance controls.
- Infrastructure definitions.
- Documentation.
- Generated projects and user-owned artifacts.

The repository structure must preserve clear ownership and prevent accidental coupling between unrelated components.

This document describes the intended structure. It does not authorize implementation, repository restructuring, branch creation, file deletion, or Git operations.

---

## 2. Repository Architecture Principles

The repository architecture follows these principles.

### 2.1 Clear ownership

Every source directory must have an identifiable owner, purpose, and dependency boundary.

### 2.2 Separation of concerns

Frontend applications, backend services, shared libraries, infrastructure, and documentation must remain distinguishable.

### 2.3 Six-service architecture

The repository must represent six deployable backend service units, not 23 independent agent services.

### 2.4 Reusable components

Common contracts and reusable utilities should be maintained in controlled shared locations rather than copied independently into multiple applications.

### 2.5 Independent validation

Each application, service, agent module, and shared package must have appropriate tests and validation requirements.

### 2.6 Tenant isolation

User-generated projects, source code, files, and execution artifacts must be isolated by tenant and project authorization.

### 2.7 Controlled automation

Automated agents and CI/CD workflows must operate with restricted permissions and explicit authorization boundaries.

### 2.8 Reproducible builds

Dependencies, build tools, configuration, and generated artifacts must be traceable and reproducible.

---

## 3. Repository Identity and Current State

### 3.1 Target repository

`https://github.com/samuel1599361/worklexx-ai-software-factory`

### 3.2 Local working directory

`C:\Users\Dell\Projects\worklexx-ai-software-factory`

### 3.3 Existing branch

The repository currently uses the `main` branch.

This existing state must be preserved during Phase 0.

### 3.4 Branch strategy status

A proposed five-tier branch strategy has been discussed but has not received final Project Owner approval.

No new branch structure must be introduced merely because it appears in an architecture document.

The current branch must not be renamed, deleted, or replaced without explicit authorization.

### 3.5 Repository integrity

Original Phase 0 backup files and their SHA-256 baseline must remain unchanged.

Any verification manifest created during the documentation revision process must be preserved separately and must not overwrite the original baseline.

---

## 4. High-Level Repository Structure

The following represents the proposed target structure.

It is an architectural directory blueprint, not a claim that every listed directory currently exists.

```text
worklexx-ai-software-factory/
│
├── apps/
│   ├── website/
│   ├── web-app/
│   ├── video-app/
│   ├── image-app/
│   └── docs-app/
│
├── services/
│   ├── api-gateway/
│   ├── agent-orchestrator/
│   ├── multimodal-service/
│   ├── sandbox-runner/
│   ├── billing-ledger/
│   └── adtech-service/
│
├── agents/
│   ├── agent-01/
│   ├── agent-02/
│   ├── agent-03/
│   ├── agent-04/
│   ├── agent-05/
│   ├── agent-06/
│   ├── agent-07/
│   ├── agent-08/
│   ├── agent-09/
│   ├── agent-10/
│   ├── agent-11/
│   ├── agent-12/
│   ├── agent-13/
│   ├── agent-14/
│   ├── agent-15/
│   ├── agent-16/
│   ├── agent-17/
│   ├── agent-18/
│   ├── agent-19/
│   ├── agent-20/
│   ├── agent-21/
│   ├── agent-22/
│   └── agent-23/
│
├── packages/
│   ├── contracts/
│   ├── shared-types/
│   ├── frontend-ui/
│   ├── frontend-config/
│   ├── observability/
│   ├── security/
│   ├── api-clients/
│   └── developer-tools/
│
├── database/
│   ├── schemas/
│   ├── migrations/
│   ├── seeds/
│   ├── policies/
│   └── tests/
│
├── infrastructure/
│   ├── environments/
│   ├── networking/
│   ├── kubernetes/
│   ├── security/
│   ├── observability/
│   ├── backup-recovery/
│   └── modules/
│
├── workflows/
│   ├── definitions/
│   ├── activities/
│   ├── events/
│   └── policies/
│
├── integrations/
│   ├── ai-providers/
│   ├── payment-providers/
│   ├── identity-providers/
│   ├── storage-providers/
│   └── external-apis/
│
├── testing/
│   ├── integration/
│   ├── end-to-end/
│   ├── security/
│   ├── performance/
│   ├── isolation/
│   └── disaster-recovery/
│
├── docs/
│   ├── phase-0/
│   ├── architecture/
│   ├── security/
│   ├── development/
│   ├── operations/
│   └── user-guides/
│
├── scripts/
│   ├── development/
│   ├── validation/
│   ├── maintenance/
│   └── release/
│
├── .github/
│   ├── workflows/
│   ├── ISSUE_TEMPLATE/
│   └── PULL_REQUEST_TEMPLATE/
│
├── .editorconfig
├── .gitattributes
├── .gitignore
├── README.md
├── SECURITY.md
├── CONTRIBUTING.md
├── CODEOWNERS
└── LICENSE
```

The final structure must be refined during implementation based on actual ownership, package dependencies, deployment requirements, and repository tooling.

---

## 5. Frontend Application Organization

The `apps/` directory contains the five frontend applications.

| Directory | Application | Domain |
|---|---|---|
| `apps/website/` | Public website | `worklexx.ai` |
| `apps/web-app/` | Main authenticated application | `app.worklexx.ai` |
| `apps/video-app/` | Video application | `video.worklexx.ai` |
| `apps/image-app/` | Image application | `images.worklexx.ai` |
| `apps/docs-app/` | Documentation application | `docs.worklexx.ai` |

Each application must have:

- An identifiable application entry point.
- Its own runtime configuration.
- Appropriate environment-variable definitions.
- A defined build process.
- Unit and component tests where applicable.
- Accessibility tests.
- Security validation.
- Deployment configuration.
- Documented ownership.

Shared UI components should be maintained in appropriate packages rather than duplicated across applications.

Frontend applications must not contain backend secrets, private API credentials, or unrestricted privileged access tokens.

---

## 6. Backend Service Organization

The `services/` directory contains exactly six deployable backend service units.

### 6.1 `api-gateway/`

Responsibilities:

- Public API ingress.
- Request validation.
- Access-token validation.
- Request-level authorization enforcement.
- Rate limiting.
- Routing to authorized backend services.
- API version management.
- Security headers and request controls.

The API Gateway is separate from the identity provider.

### 6.2 `agent-orchestrator/`

Responsibilities:

- Agent execution coordination.
- Agent registry and capability resolution.
- AI model-routing capability.
- Provider integration coordination.
- Policy-aware task execution.
- Workflow coordination.
- Agent execution metadata.
- Usage measurement coordination.

AI model routing is an internal capability of this service, not a seventh deployable service.

### 6.3 `multimodal-service/`

Responsibilities:

- Multimodal request coordination.
- Image processing integration.
- Audio processing integration.
- Video processing integration.
- Document processing integration.
- File validation and processing coordination.
- Media-related task orchestration.

### 6.4 `sandbox-runner/`

Responsibilities:

- Controlled code execution.
- Isolated development environments.
- Restricted build and test execution.
- Resource limits.
- Network restrictions.
- Artifact handling.
- Execution audit metadata.
- Sandbox lifecycle management.

### 6.5 `billing-ledger/`

Responsibilities:

- Financial transaction authority.
- Double-entry ledger.
- Credit accounting.
- Usage settlement.
- Payment reconciliation.
- Financial idempotency.
- Invoice and payment records.
- Controlled financial adjustments.

AI agents must not directly modify authoritative financial balances or posted ledger entries.

### 6.6 `adtech-service/`

Responsibilities:

- Advertising campaign operations.
- Advertising placement coordination.
- Creative and campaign metadata.
- Approved advertising measurement.
- Advertising billing integration where authorized.
- Advertising analytics.

The service must be isolated from private prompts, private source code, confidential uploads, credentials, and sensitive workflow content.

---

## 7. Logical Agent Organization

The `agents/` directory represents 23 logical agents.

Each agent is a controlled software module, not an independent deployable backend service.

A logical agent may be implemented as a package, module, workflow component, or other appropriate internal unit within the service that owns its execution.

The directory structure must not imply that every agent has an independently deployable server, database, container, or public API.

### 7.1 Agent directory requirements

Each agent directory should contain, as appropriate:

```text
agent-XX/
├── README.md
├── manifest.yaml
├── capabilities/
├── prompts/
├── policies/
├── schemas/
├── tests/
└── evaluation/
```

Not every agent requires every subdirectory.

The actual implementation must be determined by the agent's responsibility and security classification.

### 7.2 Agent manifest

Each agent manifest should define:

- Agent identifier.
- Agent name.
- Version.
- Purpose.
- Owning backend service.
- Input schema.
- Output schema.
- Allowed capabilities.
- Tool permissions.
- Data classification.
- Tenant scope.
- Approval requirements.
- Failure behavior.
- Evaluation requirements.
- Version compatibility.

### 7.3 Agent permissions

Agent permissions must follow least privilege.

An agent must not receive broad repository, database, cloud, or payment permissions simply because it participates in a workflow.

Tool permissions must be scoped to the intended operation, resource, tenant, and project.

### 7.4 Special agent boundaries

**Agent21 — Advisory and Coordination**

Agent21 may coordinate or recommend financial and business operations.

It is not the financial authority.

Financial operations must be enforced through deterministic `billing-ledger` interfaces and policies.

Agent21 must not bypass financial authorization or ledger controls.

**Agent22 — Multimodal Coordination**

Agent22 coordinates multimodal workflows through `multimodal-service`.

It does not create an independent multimodal backend deployable.

**Agent23 — Advertising Operations**

Agent23 coordinates advertising-related operations through `adtech-service`.

It must not gain access to private prompts, source code, confidential uploads, credentials, or private workflow content.

---

## 8. Shared Packages

The `packages/` directory contains reusable libraries and contracts.

Potential packages include:

| Package | Responsibility |
|---|---|
| `contracts/` | Versioned API and event contracts |
| `shared-types/` | Shared TypeScript types |
| `frontend-ui/` | Reusable UI components |
| `frontend-config/` | Shared frontend configuration |
| `observability/` | Common instrumentation utilities |
| `security/` | Reusable security-related libraries |
| `api-clients/` | Generated or maintained API clients |
| `developer-tools/` | Internal development utilities |

Shared packages must have explicit ownership and versioning rules.

A shared package must not become a hidden source of duplicated business logic.

Security-sensitive authorization and financial decisions must remain enforced by authoritative services.

### 8.1 Dependency direction

The preferred dependency direction is:

- Applications may consume approved shared packages.
- Services may consume approved contracts and compatible shared libraries.
- Agents may use approved internal service interfaces and shared contracts.
- Shared packages must not depend on application-specific code.
- Contracts must not contain hidden runtime dependencies on unrelated services.

Circular dependencies must be avoided.

---

## 9. API Contracts and Event Schemas

The `packages/contracts/` directory is the proposed home for shared API and event definitions.

Contracts should be:

- Versioned.
- Reviewed.
- Validated.
- Documented.
- Backward-compatible where required.
- Covered by automated contract tests.

OpenAPI specifications should describe HTTP interfaces.

Event schemas should describe event names, payloads, versions, ownership, and compatibility expectations.

A change to a contract must identify affected producers and consumers.

Generated client types do not remove the need for runtime validation.

---

## 10. Database Organization and Migration Ownership

The `database/` directory provides the proposed top-level organization for database-related assets.

It may contain:

- Schema definitions.
- Migration coordination.
- Seed data.
- Database policies.
- Database tests.

### 10.1 Service ownership

Each service must own its data model and migration responsibilities.

The repository must make service ownership explicit.

A central directory does not grant every service permission to modify every schema.

### 10.2 Migration governance

Migrations must be:

- Version-controlled.
- Reviewed.
- Tested.
- Ordered.
- Reproducible.
- Auditable.
- Compatible with the deployment strategy.

Destructive changes require an explicit migration and recovery plan.

### 10.3 Tenant isolation

Database code must support PostgreSQL RLS and the approved tenant-isolation design.

Required controls include:

- Tenant-aware relationships.
- Composite tenant foreign keys.
- Restricted database roles.
- Transaction-scoped tenant context.
- Appropriate `FORCE ROW LEVEL SECURITY`.
- Connection-pool context protection.
- Cross-tenant adversarial tests.

A shared directory or ORM-level filter is not a substitute for database-enforced isolation.

### 10.4 Financial history

Financial and audit history must not be destroyed through indiscriminate cascading deletion.

Deletion, anonymization, retention, and legal-hold procedures must be explicitly governed.

---

## 11. Infrastructure Organization

The `infrastructure/` directory is intended for version-controlled infrastructure definitions.

It may contain:

- Environment definitions.
- Networking.
- Kubernetes resources.
- Security configuration.
- Observability configuration.
- Backup and recovery definitions.
- Reusable infrastructure modules.

Infrastructure files must not contain plaintext secrets.

### 11.1 Environment separation

The eventual implementation should distinguish development, testing, staging, and production configurations.

The actual environment topology remains subject to architecture and Project Owner approval.

### 11.2 Infrastructure permissions

Infrastructure changes must be reviewed and authorized.

A successful infrastructure validation or CI pipeline does not independently authorize production deployment.

GATE-03 remains the production deployment approval control.

---

## 12. Workflow Organization

The `workflows/` directory is intended for workflow-related source definitions and supporting artifacts.

It may contain:

- Workflow definitions.
- Activity implementations.
- Event contracts.
- Workflow policies.

Temporal is a proposed workflow orchestration candidate.

The final directory layout must be aligned with the selected workflow engine.

Workflow source code must not treat Redis Pub/Sub or another ephemeral transport as the authoritative durable workflow record.

### 12.1 Workflow reliability

Workflow implementations must account for:

- At-least-once activity execution.
- Idempotency.
- Bounded retries.
- Timeouts.
- Cancellation.
- Compensation.
- Dead-letter handling.
- Manual recovery.
- Reconciliation.

External side effects must not be assumed to execute exactly once.

---

## 13. External Integration Organization

The `integrations/` directory is intended to contain provider adapters and integration contracts.

Potential categories include:

- AI providers.
- Payment providers.
- Identity providers.
- Storage providers.
- External APIs.

Integration code must isolate provider-specific behavior from internal business rules.

Provider credentials must be obtained through approved secrets-management mechanisms.

Provider webhooks must be verified using the provider's documented security procedure.

A payment success redirect must not be treated as authoritative payment confirmation.

---

## 14. Testing Organization

The `testing/` directory contains cross-service and platform-level test assets.

Potential categories include:

- Integration testing.
- End-to-end testing.
- Security testing.
- Performance testing.
- Tenant-isolation testing.
- Disaster-recovery testing.

Individual applications, services, agents, and packages must also maintain their appropriate local tests.

### 14.1 Required testing categories

The testing strategy must include:

- Unit tests.
- Component tests.
- API contract tests.
- Integration tests.
- End-to-end tests.
- Authorization tests.
- Cross-tenant isolation tests.
- Financial consistency tests.
- Workflow recovery tests.
- Security tests.
- Performance tests.
- Backup and restoration tests.

### 14.2 Test evidence

Test results must record:

- Test identifier.
- Software version.
- Test environment.
- Preconditions.
- Procedure.
- Expected result.
- Actual result.
- Pass/fail status.
- Relevant logs or evidence.

A passing test must not be generalized beyond the environment and conditions actually tested.

---

## 15. Documentation Organization

The `docs/` directory is the central documentation location.

It should distinguish:

- Phase 0 architecture documents.
- Architecture references.
- Security documentation.
- Development guidance.
- Operational procedures.
- User documentation.

The Phase 0 documents must remain identifiable and version-controlled.

Changes to architecture documents must be reviewed for cross-document consistency.

Implementation documentation must not describe proposed technology choices as production-tested facts.

---

## 16. Scripts and Developer Tools

The `scripts/` directory is intended for controlled development, validation, maintenance, and release automation.

Scripts must:

- Have a clearly stated purpose.
- Validate their inputs.
- Avoid exposing secrets.
- Fail safely.
- Avoid unintended destructive actions.
- Provide useful output.
- Be documented.
- Be covered by tests where appropriate.

Scripts that alter repositories, infrastructure, databases, or production systems must require the relevant authorization.

A script's presence in the repository does not constitute permission to execute it.

---

## 17. GitHub Repository Governance

GitHub is the proposed repository hosting and collaboration platform.

Repository governance must include:

- Protected branches where configured.
- Pull-request review.
- Required checks.
- Restricted administrative access.
- CODEOWNERS where appropriate.
- Secret scanning.
- Dependency review.
- Security policy.
- Issue and pull-request templates.
- Auditable changes.

The final protection rules must be explicitly configured and tested.

A `CODEOWNERS` file is a review-routing mechanism; it does not independently enforce every authorization requirement.

### 17.1 GATE-04 — Protected GitHub Operations

GATE-04 controls protected GitHub operations.

The final gate definition must specify:

- Covered operations.
- Authorized approvers.
- Repository and branch scope.
- Relevant commit or artifact identity.
- Approval expiry.
- Revocation.
- Replay protection.
- Audit evidence.

An administrator role does not automatically establish approval authority for every protected operation.

GATE-04 is independent of GATE-03 production deployment approval.

---

## 18. CI/CD Repository Organization

The `.github/workflows/` directory is the proposed home for GitHub Actions workflow definitions.

CI/CD pipelines may perform:

- Dependency validation.
- Formatting and linting.
- Unit tests.
- Integration tests.
- Static analysis.
- Security scanning.
- Build validation.
- Artifact creation.
- Artifact integrity checks.
- Authorized deployment workflows.

### 18.1 Pipeline security

CI/CD must use least-privilege tokens and permissions.

Untrusted pull-request content must not receive privileged deployment credentials.

Secrets must be scoped to the required environment and workflow.

### 18.2 Deployment approval

A passing pipeline is evidence of successful checks, not a substitute for human deployment authorization.

GATE-03 must govern production deployment approval.

The approval must be bound to the intended artifact or commit and relevant environment.

Material changes must invalidate an approval where the approval no longer represents the action being executed.

### 18.3 Artifact integrity

Build artifacts must be traceable to:

- Source commit.
- Build workflow.
- Dependency lockfiles.
- Build environment.
- Relevant test results.
- Artifact digest.

Signed artifacts and provenance should be adopted where supported and operationally justified.

---

## 19. Branching and Release Strategy

A five-tier branching strategy has been proposed for future development.

However, it remains pending explicit Project Owner approval.

The repository currently uses `main`.

This document does not authorize:

- Creation of new branches.
- Renaming `main`.
- Deletion of existing branches.
- Force-pushing.
- Rewriting repository history.
- Changing branch protection.
- Merging unapproved work.

The final branching and release model must define:

- Development integration.
- Feature isolation.
- Release preparation.
- Hotfix handling.
- Production release.
- Versioning.
- Rollback.
- Protected branch rules.

### 19.1 Phase 1 branch proposal

Any proposal to begin Phase 1 from a `develop` branch must first be reconciled with the actual current repository state and the final approved ADR.

The existence of a proposed branch name in a roadmap does not create that branch or authorize its use.

---

## 20. Dependency and Monorepo Governance

**Approved direction — HD-REP-01 (2026-11-19):** Adopt a controlled Git monorepo for Worklexx AI Software Factory platform-owned source code. Use pnpm workspaces for JavaScript/TypeScript dependency and package management, with Turborepo for dependency-aware task orchestration and caching. Maintain independently managed Python service and package projects; the Python dependency and lockfile tool is reserved for HD-REP-02.

The monorepo is a source-control and workspace organisation strategy. It does not collapse the five frontend applications or six backend deployable service units into one runtime or deployment unit. Each backend service must remain independently buildable, testable, versionable, and deployable.

### 20.1 JavaScript and TypeScript

- **Package manager/workspaces:** pnpm workspaces.
- **Task orchestration:** Turborepo.
- Commit the pnpm lockfile and pin the package-manager and build-tool versions through repository-controlled configuration.
- Define package ownership, workspace boundaries, dependency policies, build ordering, test execution, versioning, and release behavior.
- Use dependency-aware task execution and caching; cache access and contents must not expose secrets, private artifacts, or tenant data.
- CI must validate the affected workspaces and run required repository-wide security and compatibility checks.

### 20.2 Python

Python services and packages remain independently managed projects with their own dependency declarations and lockfiles as determined by HD-REP-02.

Python workspace grouping does not automatically provide runtime isolation. Actual runtime isolation must be provided through appropriate processes, containers, service boundaries, and permissions.

### 20.3 Cross-language dependencies

Python and TypeScript components must communicate through explicit, versioned API and event contracts, including OpenAPI and event-schema definitions where applicable.

Duplicated schemas and business rules must be minimized. Contract generation and compatibility tests should be used where practical.

### 20.4 Shared package and service boundaries

Shared packages must have explicit ownership, documented interfaces, compatibility rules, and tests. Shared packages must not depend on application-specific or service-specific implementation code. Service-specific business logic, authorization decisions, financial controls, and database ownership remain within their authoritative service boundaries.

The approved six-service topology remains unchanged. Shared packages, agents, contracts, build tasks, and workspace groupings must not silently create additional backend deployable services.

### 20.5 Generated-project boundary

Customer- or tenant-generated projects and artifacts are not ordinary platform workspace packages. Their repository and artifact isolation model remains subject to HD-REP-05. The platform monorepo must not become a shared location through which one tenant, user, or agent can access another tenant's generated source or artifacts.

### 20.6 Decision scope and implementation boundary

HD-REP-01 records an architectural tooling and workspace direction only. It does not authorise repository restructuring, tool installation, lockfile creation or modification, CI/CD changes, branch changes, infrastructure provisioning, production deployment, or Phase 1 implementation. Tool versions, compatibility, security, licensing, cache configuration, and CI integration must be validated before implementation under the applicable approvals.

---

## 21. Generated Projects and User-Owned Artifacts

The Software Factory may generate project repositories, source code, documentation, and build artifacts for users or organizations.

Generated content must be distinguished from the platform's own source code.

### 21.1 Ownership

The system must record:

- Tenant.
- Organization.
- Project.
- Owner or authorized maintainer.
- Repository identity.
- Artifact identity.
- Creation time.
- Version.
- Access permissions.

### 21.2 Isolation

Generated project repositories and artifacts must have tenant-aware access controls.

A user or agent must not gain access to another tenant's source code or generated artifacts through predictable paths, repository names, shared storage, or reused credentials.

### 21.3 Git isolation

Git repositories must have appropriate repository-level authorization.

PostgreSQL RLS does not automatically protect Git hosting or repository content.

### 21.4 Artifact storage

Large artifacts may be stored in object storage with appropriate tenant isolation, encryption, versioning, retention, and deletion controls.

Artifact download links must be short-lived and authorization-controlled where applicable.

### 21.5 Agent access

Agents may access only repositories and artifacts explicitly authorized for the relevant task.

Repository access must be restricted to the minimum required operation.

---

## 22. Agent-Generated Code and Repository Permissions

Agent-generated code must be treated as untrusted until it has passed the applicable review and validation process.

Required controls include:

- Scoped repository access.
- Restricted branches.
- Pull-request-based changes.
- Automated tests.
- Security scanning.
- Human review where required.
- Protected-operation approval.
- Audit records.

Agents must not bypass branch protection, remove required checks, alter repository security policies, or directly perform protected operations without the required authorization.

A code-generation agent does not automatically have permission to commit, push, merge, or deploy.

---

## 23. Security and Compliance Files

The repository should maintain appropriate governance and security documents.

Potential root-level files include:

| File | Purpose |
|---|---|
| `README.md` | Repository overview and entry point |
| `SECURITY.md` | Security reporting and vulnerability handling |
| `CONTRIBUTING.md` | Contribution requirements |
| `CODEOWNERS` | Review ownership mapping |
| `.gitignore` | Exclusion of local and generated files |
| `.gitattributes` | Consistent Git file handling |
| `.editorconfig` | Editor consistency |
| `LICENSE` | Approved licensing terms |

The final license must be selected and approved by the appropriate owner.

The presence of a security policy or configuration file does not prove that all corresponding controls have been implemented.

---

## 24. Environment and Configuration Management

Configuration must be separated from application source code.

The repository may include safe example configuration files, but must not contain real credentials or production secrets.

Configuration management must distinguish:

- Development.
- Testing.
- Staging.
- Production.
- Tenant-specific settings where applicable.
- Provider-specific configuration.

Sensitive values must be obtained through approved secrets-management mechanisms.

Configuration changes affecting security, routing, payments, identity, or production behavior must be reviewed and audited.

---

## 25. Repository Backup and Recovery

Repository recovery must account for:

- Git source history.
- Branches and tags.
- Repository configuration.
- Workflow definitions.
- Release artifacts.
- External dependencies.
- Required secrets and key recovery procedures.

GitHub availability alone is not a complete backup strategy.

Recovery procedures must be tested and documented.

The original Phase 0 backup and SHA-256 baseline are separate from future operational backups and must remain unchanged.

---

## 26. Repository Change Management

Changes to the repository structure must follow controlled review.

A structural change must identify:

- Reason for change.
- Affected directories.
- Service and package ownership.
- Dependency impact.
- Security impact.
- Build and test impact.
- Migration requirements.
- Rollback approach.
- Required approvals.

Material changes must be reflected in the relevant architecture documents and ADRs.

No automated agent may independently redefine the repository architecture.

---

## 27. Repository Validation Requirements

Before implementation, the proposed repository structure must be validated for:

1. Five frontend application boundaries.
2. Six deployable backend service boundaries.
3. Twenty-three logical agent modules.
4. Shared package ownership.
5. Explicit API and event contracts.
6. Service-owned database migrations.
7. Tenant isolation across relational and non-relational storage.
8. Git repository and artifact isolation.
9. Dependency and lockfile reproducibility.
10. CI/CD security and approval enforcement.
11. GATE-03 and GATE-04 separation.
12. Branch and release governance.
13. Documentation completeness.
14. Backup and recovery requirements.
15. Build and test execution boundaries.

Validation must produce recorded evidence.

A directory tree alone does not demonstrate that service boundaries, authorization, or isolation are correctly implemented.

---

## 28. Human Decisions Pending

The following decisions remain pending explicit human review and approval.

| Decision ID | Decision | Status |
|---|---|---|
| HD-REP-01 | Final monorepo tooling and workspace strategy | Approved — architectural direction only (2026-11-19) |
| HD-REP-02 | Final Python dependency and lockfile tooling | Pending |
| HD-REP-03 | Final five-tier branching and release strategy | Pending |
| HD-REP-04 | Final ownership and approval rules for protected repositories | Pending |
| HD-REP-05 | Final generated-project repository isolation model | Pending |
| HD-REP-06 | Final service-owned migration organization | Pending |
| HD-REP-07 | Final repository backup and recovery strategy | Pending |

These repository-specific decisions use the `HD-REP-` prefix to distinguish them from platform-wide `HD-01` through `HD-08`, which are maintained in the architecture documents and ADR register. Platform-wide `HD-08` remains the authoritative decision for final approval-gate definitions and approval authority.

These decisions must be reconciled with the ADR register and the remaining Phase 0 architecture documents.

---

## 29. Phase 0 Execution Boundary

Phase 0 is a documentation and architecture-definition phase.

This document does not authorize:

- Repository restructuring.
- Directory creation or deletion.
- Branch creation or deletion.
- Git commits.
- Git pushes.
- Pull-request creation or merging.
- Branch-protection changes.
- CI/CD activation.
- Infrastructure provisioning.
- Application implementation.
- Database migration execution.
- Production deployment.
- Phase 1 execution.

The user's existing repository state, backup files, and SHA-256 baseline must be preserved.

GATE-03 production deployment approval and GATE-04 protected GitHub operations approval remain separate controls.

---

## 30. Related Documents

This document must be reviewed alongside:

1. `ARCHITECTURE_OVERVIEW.md`
2. `SYSTEM_ARCHITECTURE.md`
3. `TECHNOLOGY_STACK.md`
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

The final review must identify and resolve material inconsistencies across these documents.

---

## 31. Final Status

**Document Status:** Revised Architecture Blueprint — Awaiting Final Human Review and Approval.

This specification defines the proposed repository organization and governance model for the Worklexx AI Software Factory.

It preserves the distinction between five frontend applications, six deployable backend service units, and 23 logical agents.

It also defines repository security, tenant isolation, dependency management, generated-project ownership, CI/CD controls, and unresolved human decisions.

The proposed directory structure is an architectural target, not evidence that the directories have been created or validated.

**Phase 0 remains subject to final document verification and explicit Project Owner approval. Phase 1 is not authorized by this document.**