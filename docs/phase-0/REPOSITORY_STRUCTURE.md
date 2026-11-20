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

Each of the six deployable backend services must own its authoritative schema, migration scripts, migration metadata/version history, and migration lifecycle:

- `api-gateway`
- `agent-orchestrator`
- `multimodal-service`
- `sandbox-runner`
- `billing-ledger`
- `adtech-service`

A service must not independently modify another service's authoritative schema. The repository must make ownership explicit. A shared PostgreSQL cluster or database remains possible; service ownership does not require six physical database servers. A central coordination mechanism, if later introduced, must not have unrestricted authority over every schema.

### 10.2 Migration governance

Each service maintains an independent, ordered and auditable migration history with immutable migration identifiers and checksums. Migrations must be version-controlled, reviewed, reproducible, tested against supported application versions, and compatible with rolling deployment.

Use expand-and-contract changes where practicable. Use migration locks, bounded timeouts, and transactional execution where supported. Separate migration identities from runtime credentials; each migration identity is restricted to its owned schema, and runtime credentials have no DDL privileges. A code rollback must not be assumed to reverse a schema or data migration.

Cross-service changes must identify affected services, API/event consumers, compatibility windows, and deployment sequence. Prefer authorised APIs, events, or controlled read models over direct cross-service schema coupling.

Destructive changes require impact analysis, explicit authorization under GATE-05, and a documented backup/recovery or forward-fix plan. Production execution additionally requires applicable GATE-03 authorization. Approval of a migration design or PR is not execution authorization.

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

**Approved direction — HD-REP-02 (2026-11-19):** Use Astral uv as the preferred Python dependency-management, lockfile, and project-environment tool.

Python backend services and shared packages remain independently managed projects. Each independently managed service project must maintain its own `pyproject.toml` and committed `uv.lock`, with explicit dependency ownership, dependency groups, and a documented supported Python-version policy. Shared Python packages must define their own project metadata and development/test dependencies; their development lockfiles do not replace the lockfiles of consuming services.

Do not require a single Python workspace across the six backend services. Any future workspace grouping requires technical justification and separate approval. Python workspace grouping does not provide runtime isolation. Actual runtime isolation must be provided through appropriate processes, containers, service boundaries, and permissions.

CI must enforce lockfile consistency and reproducible installation (for example, `uv sync --locked`), pin the uv tool version, and fail rather than silently rewrite committed lockfiles. Exclude local virtual environments and caches from source control. Apply approved package-source controls, private-index credential handling, dependency integrity/provenance review, vulnerability and license scanning, controlled updates, and SBOM generation. Validate Windows development, Linux CI, Python 3.12, Docker integration, independent service lockfiles, private package sources, upgrades, and rollback before implementation.

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

## 28. Human Repository Decisions and Status

The following table records the approval status of repository architecture decisions. Items marked Pending remain subject to explicit human review and approval.

| Decision ID | Decision | Status |
|---|---|---|
| HD-REP-01 | Final monorepo tooling and workspace strategy | Approved — architectural direction only (2026-11-19) |
| HD-REP-02 | Final Python dependency and lockfile tooling | Approved — architectural direction only (2026-11-19) |
| HD-REP-03 | Branching, integration and release strategy | Approved — architectural direction only (2026-11-20) |
| HD-REP-04 | Final ownership and approval rules for protected repositories | Approved — architectural direction only (2026-11-20) |
| HD-REP-05 | Final generated-project repository isolation model | Approved — architectural direction only (2026-11-20) |
| HD-REP-06 | Service-owned schema and migration governance across six deployable services | Approved — architectural direction only (2026-11-20) |
| HD-REP-07 | Final repository backup and recovery strategy | Approved — architectural direction only (2026-11-20) |
| HD-REP-08 | Repository automation, build integrity and software supply-chain security governance | Approved — architectural direction only (2026-11-20) |
| HD-REP-09 | Repository observability, audit logging and security-event monitoring governance | Approved — architectural direction only (2026-11-20) |
| HD-REP-10 | Customer project lifecycle, ownership, portability and exit governance | Approved — architectural direction only (2026-11-20) |
| HD-REP-11 | Customer data isolation, privacy boundaries and data governance | Approved — architectural direction only (2026-11-20) |
| HD-REP-12 | Customer identity, authentication, authorisation and access lifecycle governance | Approved — architectural direction only (2026-11-20) |

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

### HD-REP-03 — Approved Branching and Release Direction (2026-11-20)

- **Decision:** Adopt trunk-based development using `main` as the permanent protected integration branch and short-lived feature, fix, and hotfix branches. Require PRs, automated validation and independent human review. Prohibit direct pushes, force pushes and routine bypasses. Prefer squash merging.
- **Release strategy:** Independently version the six backend deployable services and five frontend applications. Use component-specific release tags, release notes, artifact provenance and compatibility controls. Apply Semantic Versioning where applicable.
- **Release branches:** Temporary only, justified by stabilisation, certification, coordinated releases or maintenance. Hotfixes must be reconciled back into `main`.
- **Scope limitation:** This architectural direction does not authorise GitHub branch-protection configuration, CI/CD implementation, release automation/tool selection, release creation, deployment, infrastructure provisioning or Phase 1. These require validation and separate approval.


## HD-REP-04 — Approved Repository Ownership and Governance Direction (2026-11-20)

The Project Owner approved the organisation-owned repository model when Worklexx's GitHub organisation is established and repository transfer is separately authorised. Until then, the repository remains in its current location. Access shall follow least privilege, with minimum necessary administrators, scoped collaborators and automation, no shared credentials, and periodic access review. Protect `main` from direct routine pushes, force pushes and deletion; require PRs, independent human review, designated CODEOWNERS review for critical paths and mandatory CI checks once implemented. Prefer squash merging and dismiss stale approvals after material changes. AI agents cannot approve their own changes, accept risks, modify governance settings, grant access or bypass protections. Project Owner remains sole initial governance approval authority, subject to HD-08. This is architectural approval only and does not authorise organisation creation, repository transfer, settings changes, invitations, CI/CD, production deployment or Phase 1.


## HD-REP-05 — Approved Generated-Project Repository Isolation Model (2026-11-20)

The Project Owner approved a hybrid, provider-independent architecture using one isolated Git repository per generated customer project. The Factory platform-source repository remains separate from all customer-generated project repositories. Support Worklexx-managed private hosting and customer-managed hosting integrations; a customer need not have a Git hosting account merely to use the Factory.

Each project must have a unique project identity and repository mapping, private-by-default visibility, tenant- and project-scoped authorization, independent credentials and access controls, audit records, lifecycle and retention/deletion controls, backup/recovery, and customer export/portability. Isolation must also be enforced across API authorization, storage, Git credentials, background jobs, caches, agent execution, and artifact delivery; repository separation alone is insufficient.

Repository access is mediated by a permission-controlled layer. Agents receive only task- and project-scoped minimum permissions for inspection, code changes, pull requests, and approved sandbox testing. No cross-tenant access or implicit secret access is permitted. Agents cannot alter ownership or visibility, delete repositories, or perform protected operations without applicable human authorization and approval.

Generated customer software must be distinguished from Worklexx proprietary platform source, reusable platform components/templates, and third-party licensed components. Customer export, hosting connection/transfer, disconnection, and revocation must be authenticated, authorized, audited, and validated.

**Scope limitation:** Architectural approval only. No repository provisioning, customer-account connection, OAuth/app installation, subscription/spending, migration, production implementation, Factory repository change beyond this controlled documentation update, or Phase 1 execution is authorized. Provider integration, isolation, permissions, security, portability, legal/licensing, backup and recovery controls require validation and applicable separate approvals.


## HD-REP-06 — Approved Service-Owned Schema and Migration Direction (2026-11-20)

The Project Owner approved independent schema ownership and migration histories for all six deployable backend services. Each service owns its authoritative schema, migration scripts, migration metadata and lifecycle. Runtime credentials must not have DDL privileges; migration identities must be separately scoped to the service-owned schema. Expand-and-contract changes, compatibility across rolling releases, migration locks, immutable identifiers/checksums, audit evidence, backup/recovery and forward-fix planning are required architectural controls. A shared PostgreSQL cluster remains possible; six physical databases are not mandated. Cross-service changes must be coordinated through explicit compatibility and deployment planning, with APIs/events/read models preferred over direct schema coupling. `billing-ledger` requires additional financial-integrity and reconciliation validation. GATE-05 governs destructive migrations and GATE-03 applies to production deployment; neither documentation approval nor PR review authorises execution. This decision does not authorise schema changes, credential or permission changes, migration execution, CI/CD activation, infrastructure provisioning, production deployment or Phase 1.

## HD-REP-07 — Approved Repository Backup, Disaster Recovery and Restoration Governance (2026-11-20)

The Project Owner approved a layered, provider-independent backup and recovery architecture with separate protection classes for Factory platform source, Worklexx-managed customer projects, customer-managed repositories, and supporting development records/artifacts. Backups must protect Git objects, branches, tags, refs and Git LFS where used, while separately protecting supported repository metadata, release/build artifacts, project mappings, access/audit records and integration configuration. A Git clone alone is not a complete backup. Secrets and credentials must be restored through approved secrets/key-management procedures, not copied as ordinary metadata.

Use multiple independently controlled recovery copies, including off-site and immutable or deletion-resistant protection. Separate backup identities from ordinary repository administration; encrypt data in transit and at rest; protect keys independently; enforce least privilege, auditability, tenant/project isolation, integrity checks, retention/deletion controls and portability. Worklexx is accountable for Worklexx-managed repositories subject to customer agreements. Customers remain responsible for provider-account and provider-side recovery of customer-managed repositories; Worklexx protects only authorised and technically supported data. Customer disconnection must not delete customer-owned repositories.

Initial objectives: daily full plus incremental/event-based capture for Factory source, with 90-day daily and 12-month monthly retention; continuous/frequent Git replication and daily metadata backup for Worklexx-managed customer repositories with the same proposed retention; customer-managed synchronisation only within authorised scope and agreed retention. Proposed RPO/RTO: critical Factory source/release-control records ≤15 minutes/4 hours; active customer source repositories ≤1 hour/8 hours; metadata/development records ≤4 hours/24 hours; historical/noncritical artifacts ≤24 hours/48 hours. These are unverified objectives, not SLAs, and require technical, legal, cost, contractual and operational validation aligned with HD-06 and POC-15.

Restoration requires incident declaration, containment, verified recovery-point selection, isolated restore, integrity/security/tenant checks, authorised reconnection, reconciliation and retained evidence. Newer customer work must not be silently overwritten. Test Git/LFS, metadata, artifact, tenant-isolation, deletion, ransomware, provider-outage portability, legal-hold, export and measured RPO/RTO scenarios. A successful backup job alone does not demonstrate recoverability.

Agents may detect failures and prepare recovery plans but cannot approve consequential restores, delete protected copies or alter retention. GATE-02, GATE-03, GATE-04 and GATE-06 apply according to the action; HD-08 remains authoritative. **Architectural approval only:** no configuration, provisioning, subscription/spending, repository settings or permission changes, customer connections, backup/restore/migration execution, CI/CD activation, production implementation or Phase 1 is authorised.

## HD-REP-08 — Approved Repository Automation, Build Integrity and Software Supply-Chain Security Governance (2026-11-20)

The Project Owner approved a policy-controlled, least-privilege, verifiable automation architecture for Factory source and customer-generated projects. Factory, Worklexx-managed customer projects and customer-managed repositories remain distinct trust boundaries. Customer projects retain one isolated repository per project under HD-REP-05; automation, credentials, jobs, caches, artifacts and agent execution must be tenant/project-scoped. Customer-managed access is limited to expressly granted permissions.

Workflows default to read-only permissions and receive narrowly scoped write access only when necessary. Prefer short-lived credentials. Review workflow definitions before activation; pin third-party actions to immutable commit SHAs; protect workflow files; and prevent untrusted pull-request code from accessing privileged secrets or trusted publishing credentials. Separate validation, build, artifact verification, provenance, release approval, publication and deployment.

Enforce lockfiles, pinned tools, dependency integrity, vulnerability/secret/licence scanning, dependency review, SAST and applicable DAST, and machine-readable SBOMs (SPDX or CycloneDX). Build in isolated environments; separate untrusted PR builds from trusted release builds; isolate caches, credentials, jobs and artifacts by trust boundary, tenant and project. Generate cryptographic artifact checksums and preserve source-to-artifact provenance. Evaluate SLSA and Sigstore subject to validation; protect signing keys through approved key management.

Agents may perform authorised inspection, tests, scanning, SBOM/provenance preparation and PR preparation. They may not approve their own PRs or releases, grant themselves access, access unrelated customer secrets, change security policy or bypass protected operations. A successful build, verified artifact or publication does not authorise production deployment. HD-08 gates and HD-07 risk acceptance authority remain controlling.

**Required validation:** POC-REP-08-01 through POC-REP-08-12 must test workflow least privilege, untrusted PR isolation, lockfile integrity, security scanning, SBOMs, checksums/signatures/provenance, build/cache isolation, tenant isolation, credential protection, release/publication separation, compromised dependency/workflow scenarios and audit/recovery traceability.

**Scope limitation:** Architectural approval only. No workflow activation, GitHub settings change, app installation, credential/signing-key creation, paid service, infrastructure provisioning, production build, artifact publication, release, deployment, customer Git-account connection, migration execution or Phase 1 is authorised. Applicable validation and separate HD-08 approvals remain mandatory.


## HD-REP-09 — Repository Observability, Audit Logging and Security-Event Monitoring Governance

The Project Owner approved a provider-independent, privacy-aware observability and audit architecture on 2026-11-20. It covers Factory source and customer-generated repositories, with distinct responsibility for Worklexx-managed and customer-managed hosting. Required event domains include identity/access, repository and Git activity, pull requests and reviews, workflows, AI-agent actions, supply-chain and artifact events, releases, integrations, backup/recovery, deletion/retention and governance decisions.

Use a versioned event envelope with actor, tenant/project/repository scope, action/resource/outcome, timestamps and time-source metadata, originating service/workflow, correlation identifiers, authorisation/approval references and relevant commit/artifact references. Protect audit evidence through independently protected append-only or tamper-evident storage, integrity verification, encryption, least privilege, separation of duties, access auditing and HD-REP-07 recovery controls. Minimise data and redact secrets and sensitive content.

Define security detection, severity, escalation, investigation and evidence-preservation procedures. Customers may inspect/export only their own available project history. Worklexx records customer-managed provider events only within authorised integration visibility; provider-side audit responsibility remains with the customer. AI agents may analyse and prepare evidence but cannot approve gated actions, accept risks, alter protected evidence, change retention or bypass controls.

Validation is required under POC-REP-09-01 through POC-REP-09-12. RSK-29 records the risk of incomplete, altered, exposed or inadequately monitored audit evidence. HD-07 and HD-08 remain controlling. This is architectural approval only: no monitoring activation, provider configuration, SIEM purchase, infrastructure, credentials, customer connections, production integration or Phase 1 is authorised.


## HD-REP-10 — Approved Customer Project Lifecycle, Ownership, Portability and Exit Governance (2026-11-20)

The Project Owner approved a customer-centred lifecycle architecture that complements the one-isolated-repository-per-project model in HD-REP-05. Each generated project must have a unique immutable project identity, customer/tenant association, recorded owner or controlling entity, repository mapping, hosting mode, lifecycle state and auditable transition history. Logical states include Created, Provisioning, Active, Suspended, Archived, Exported/Transferred, Disconnected, Deletion Pending and Deleted. Suspension is not deletion; export is not ownership transfer; disconnecting Worklexx from customer-managed hosting must not delete the customer's repository.

Preserve both HD-REP-05 hosting modes: Worklexx-managed private repositories, available without requiring customers to hold a separate Git hosting account, and customer-managed supported hosting integrations. Hosting administration does not itself confer ownership of customer projects. Customer agreements and project records must distinguish customer-provided content/data, customer-generated code, Worklexx proprietary platform/reusable components/templates, and third-party licensed components. Generated-code ownership and licensing must be governed by applicable agreements and law rather than blanket assumptions.

Provide authenticated customer-scoped export and portability for applicable source, complete Git history, refs, Git LFS where used, documentation, non-secret configuration templates, dependency manifests/lockfiles, entitled artifacts, SBOM/provenance, metadata and customer-entitled audit records. Exports require an inventory, format/version information and integrity checksums, and must identify omissions/provider limitations. Secrets, tokens, passwords and private/signing keys are excluded from ordinary exports and must be re-established securely. Validate independent import and usability.

Separate export, repository transfer, ownership transfer, hosting disconnection and account closure. Exit controls include identity/authority verification, ownership/contract/legal-hold checks, scoped export or transfer, integrity verification, receipt/completion confirmation where applicable, integration credential revocation, retention/archive/deletion processing and audit evidence. Ownership transfer requires explicit authorisation from the current authorised owner and any other required party.

Subscription or entitlement expiry may restrict premium Factory capabilities under disclosed terms but must not automatically delete customer source or data. No universal grace period, retention period or deletion deadline is approved. Record-class-specific retention, legal holds, deletion and backup-expiry behaviour require legal, regulatory, contractual and operational assessment. Deletion must be a controlled, verified workflow across primary storage, Git/LFS, object storage, caches, indexes, jobs, artifacts and replicas; backup restore controls must prevent silent reintroduction of deleted data.

Agents may prepare exports, inventories, transfer documents and recommendations but may not transfer ownership, change visibility, disconnect accounts, revoke customer access, delete repositories/data/backups, alter retention, override legal holds or approve exits. Apply HD-07/HD-08; GATE-02, GATE-03, GATE-04, GATE-05 and GATE-06 according to the actual operation.

**Required validation:** POC-REP-10-01 through POC-REP-10-15 cover project identity/ownership, tenant isolation, hosting responsibility, lifecycle transitions, transfer authority, export completeness, independent import, secret exclusion, entitlement safeguards, retention/legal hold/deletion, backup expiry/restore protection, integration disconnection, exit traceability, agent boundaries and end-to-end recovery/audit evidence. RSK-30 records ownership disputes, incomplete portability and improper suspension/transfer/deletion; risk scores remain pending formal assessment.

**Scope limitation:** Architectural approval only. No customer provisioning, live account/repository connection, OAuth installation, ownership/repository transfer, live customer suspension/archive/deletion, production migration, backup/retention configuration, infrastructure, subscriptions/spending, GitHub permission/settings changes, CI/CD activation, production deployment or Phase 1 is authorised. Applicable validation and separate HD-08 approvals remain mandatory.



## HD-REP-11 — Customer Data Isolation, Privacy Boundaries and Data Governance

The Project Owner approved this architectural direction on 2026-11-20. Establish privacy-by-design and data-governance controls across Factory platform data and customer-generated projects. Classify information as Public, Internal, Confidential or Restricted; document processing purposes, minimisation, lawful/contractual authority, data ownership and controller/processor responsibilities. Apply tenant/project-scoped authorisation to APIs, all six backend deployables, PostgreSQL/RLS, pgvector, object storage, indexes, embeddings, agent memory/context, workflows, queues, caches, multimodal temporary files, build environments, artifacts, logs, backups, exports and restoration. Tenant identifiers supplied by clients or agents are not authority; database RLS supplements service-layer authorisation.

Cover prompts, documents, source code, images, audio, video, transcripts, embeddings, metadata, generated outputs and derived copies. External model providers and subprocessors require documented due diligence and controls for purpose, data scope, location, retention, human access, onward transfers, training use and deletion. Customer data must not be used to train or improve general-purpose external models unless a specific lawful and appropriately authorised arrangement expressly permits it. Agents receive minimum task-scoped permissions and cannot expand access, cross tenant boundaries, approve their own access or transfer information to unauthorised providers. Uploaded and retrieved content is untrusted; prompt injection cannot override policy or authorisation.

Protect confidential/restricted information in transit and at rest, separate keys and secrets from application data, and govern key lifecycle. HD-03 regional choices do not themselves establish transfer legality; assess applicable Nigerian and other jurisdictional laws, safeguards, localisation, subprocessors, backups and support access before live processing. Provide applicable access, correction, export, erasure, restriction, objection and consent-withdrawal mechanisms. Apply record-class retention and legal holds; no universal retention duration is approved. Deletion must include relevant derivatives, indexes, caches, jobs, replicas and backup lifecycle, aligned with HD-REP-07 and HD-REP-10. Align privacy-aware audit and incident monitoring with HD-REP-09, including redaction of secrets and sensitive content from ordinary telemetry.

Distinguish Worklexx-managed and customer-managed hosting responsibilities, customer information, generated project content, Worklexx proprietary components and third-party licensed materials. Add RSK-31 for customer data exposure, unlawful processing and privacy control failure; formal risk scores remain pending. Require POC-REP-11-01 through POC-REP-11-15 before operational reliance. Apply HD-07/HD-08 and GATE-01 through GATE-06 as relevant.

**Scope limitation:** Architectural and documentation approval only. No live customer/personal-data processing, external provider/customer integration, OAuth/app installation, infrastructure/storage/database provisioning or modification, credential/key creation, paid services, GitHub settings/permission changes, production monitoring/workflow activation, migration, deletion/restoration, production deployment or Phase 1 is authorised. Validation and separate applicable approvals remain mandatory.



## HD-REP-12 — Approved Customer Identity, Authentication, Authorisation and Access Lifecycle Governance (2026-11-20)

The Project Owner approved HD-REP-12 on 2026-11-20. Adopt a centralised managed-identity integration model with Worklexx-controlled application authorisation and service-enforced tenant, project and resource boundaries. HD-01's managed identity-provider direction remains in force; authentication does not itself grant application or resource access.

Distinguish individual users, organisations, organisation memberships, project identities/memberships, AI-agent identities, backend service identities, workload identities and external integration identities. Users may belong to multiple organisations with different permissions. Organisation administration does not automatically confer project ownership; HD-REP-10 remains authoritative for project ownership, transfer and exit.

Use configurable RBAC, contextual ABAC and explicit resource-level permissions. Services must derive trusted tenant/project context from server-side identity and membership records; client-supplied identifiers are never proof of authority. RLS supplements, but does not replace, service-layer authorisation. Preserve the six approved backend deployables and HD-REP-06 service-owned schema boundaries.

Provide controlled registration, verification, invitations, membership and role changes, access reviews, suspension, recovery, revocation, deprovisioning and account closure. Distinguish ordinary, privileged and emergency access. Require stronger authentication and scoped, time-limited privileged access where practicable. Emergency access must remain attributable, reviewed and subject to HD-08; it is not an approval bypass.

Each agent invocation must have a distinct attributable identity and explicit task-, tenant-, project-, operation- and time-scoped delegation. Do not inherit a user's blanket authority. The six backend deployables require distinct service identities and least-privilege service-to-service permissions. Prefer short-lived workload credentials. API keys/tokens require ownership, purpose, scope, expiry where practicable, rotation, revocation and audit; do not expose privileged credentials in frontend bundles or ordinary logs.

Revocation and permission changes must propagate across sessions/tokens, all six services, PostgreSQL/RLS, pgvector, object storage, Git/repository integrations, Temporal workflows/queues, agent contexts, build environments, artifacts, caches and external integrations. Define and measure propagation objectives through POC; sensitive operations must not rely solely on stale cached decisions and must fail closed when current authority cannot be established.

Identity information is subject to HD-REP-11 minimisation, purpose limitation, privacy, rights, retention and legal-hold controls. Identity and access events must be attributable and protected under HD-REP-09. Never log passwords, token values, private keys, recovery secrets or authentication secret values.

**Required validation:** POC-REP-12-01 through POC-REP-12-20 cover provider portability; identity mapping; multi-organisation isolation; RBAC/ABAC; cross-tenant/project denial; ownership boundaries; MFA/passkeys/SSO; session lifecycle; account recovery/compromise; agent delegation; service/workload identities; API key/token lifecycle; revocation propagation; privileged/emergency access; audit attribution; lifecycle/deprovisioning; privacy; provider outage/recovery; approval-gate fail-closed behaviour; and concurrent permission changes/stale caches. Unexecuted POCs are not passed. RSK-32 records identity compromise, excessive privilege and access-control failure; likelihood, impact and residual scores remain pending formal assessment.

**Governance and scope limitation:** HD-07/HD-08 remain authoritative. Applicable gates include GATE-01 through GATE-06 according to the actual operation. Architectural and documentation approval only: no identity-provider selection/connection, customer account creation, SSO/OAuth configuration, permission changes, live credential issuance, infrastructure/database changes, paid services, GitHub permission changes, production authentication activation, migrations, production deployment or Phase 1 is authorised. Separate validation and applicable approvals remain mandatory.


## HD-REP-13 — AI Agent Security, Delegation, Execution Boundaries and Human Oversight Governance (Approved 2026-11-20)

Adopt permission-controlled, policy-enforced, sandboxed and auditable agent execution for the 23 logical agent modules. This decision does not add a backend deployable or alter the approved six-deployable architecture. Agent intelligence is not authority: each agent has a distinct identity and bounded task, tenant/project, tool, data and time scope; versioned policies; resource limits; audit attribution; and revocation controls.

Five conceptual permission tiers: Tier 0 Observe; Tier 1 Prepare; Tier 2 Execute within controlled scope; Tier 3 Consequential action subject to independent approval and applicable control; Tier 4 prohibited authority (including self-approval and governance bypass). Tool permissions remain granular: inspect, write, PR creation, review, approval, merge, permission changes, deletion and transfer are separate capabilities. The tool-control boundary validates identity/scope, inputs and destinations, classification, policy and approval, then executes, verifies and audits.

Code execution uses an appropriately isolated sandbox within the approved sandbox-runner boundary: restricted networking, resource/time limits, filesystem/process isolation, credential separation, tenant/project-specific caches and artifact handling, and cleanup. Untrusted documents, source, web content, prompts and tool results are data—not policy or authority—and prompt injection must not override permissions, governance or gates. Delegation is task/time bounded, depth-limited, attributable, revocable and cannot expand the initiating authority.

Agent context and memory are scoped, classified, minimised, governed and tenant/project isolated. Outputs require independent verification appropriate to their risk; verification does not substitute for human approvals required by HD-08. Control retries, loops, concurrency, idempotency, resource/cost limits, cancellation and safe failure. Protected audit and monitoring align with HD-REP-09; privacy and data boundaries with HD-REP-11; identity and delegation with HD-REP-12; execution isolation and supply-chain controls with HD-REP-08; customer lifecycle with HD-REP-10.

Validation requirements: POC-REP-13-01 through POC-REP-13-24 (unexecuted) cover agent identity/scope, least privilege, tool authorization, policy enforcement, tier separation, gate binding, sandbox isolation, network/credential restrictions, resource limits, prompt-injection resistance, untrusted content, tenant/project isolation, delegation depth/authority, context/memory privacy, output verification, human oversight, audit attribution, revocation, concurrent actions/races, loops/retries/cancellation, failure/recovery, cost controls, abuse scenarios and end-to-end governance bypass attempts.

Add RSK-33 — AI Agent Misuse, Unsafe Execution, Privilege Escalation and Governance Bypass. Formal likelihood, impact, inherent and residual scores remain pending assessment; proposed controls do not reduce residual risk until implemented and evidenced.

Project Owner remains sole initial risk acceptance and approval authority under HD-07/HD-08. Applicable gates remain mandatory. This is architecture/documentation approval only: no agent execution in production, sandbox provisioning, external integrations, live customer data, credentials, CI/CD activation, GitHub configuration, database changes, paid services, production deployment or Phase 1 is authorised.

Repository structure should represent agent modules as governed logical components, subject to the tool-control boundary and sandbox-runner—not as independently privileged services. Preserve the six deployables, 23 logical modules and established monorepo/customer-repository boundaries.


## HD-REP-14 — API Contracts, Inter-Service Communication and Integration Governance (Approved 2026-11-20)

Add a governed contract area to the existing monorepo structure for API, event, workflow, integration, agent-tool, schema and governance specifications. The proposed logical layout is contracts/api/<service>, contracts/events, contracts/workflows, contracts/integrations, contracts/agents, contracts/schemas and contracts/governance. This is a proposed logical organization, not an instruction to create directories now. Contract files remain owned and reviewed by the authoritative service/platform owner; shared schemas must not create service-specific dependency cycles or bypass service ownership.

Preserve the six backend deployables and 23 logical agent modules. Do not add a seventh deployable, broker, schema-registry service or other infrastructure through this decision. Contract boundaries must respect the monorepo, independent service releases, customer project repository isolation and service-owned database/migration boundaries. Worklexx platform contracts must remain distinct from customer-generated project contracts and customer-managed external interfaces.

HD-REP-14 requires contract-first, versioned and compatibility-controlled synchronous APIs, asynchronous events, Temporal workflow/activity interfaces, agent-tool interfaces and external APIs/webhooks. Use OpenAPI, JSON Schema and AsyncAPI standards directions where appropriate, subject to POC validation. Contract ownership, versioning, consumers, classifications, compatibility, validation and change traceability must be documented. Add RSK-34; formal scoring remains pending. POC-REP-14-01 through -24 remain unexecuted. Documentation approval does not authorise tooling installation, directory creation, infrastructure, integration, credentials, CI/CD or Phase 1.


## HD-REP-15 — API Gateway Architecture and Edge Governance (Approved 2026-11-20)

Record a policy-enforced API gateway as the controlled external ingress and routing boundary for approved public interfaces. Logical responsibilities include TLS/edge integration, identity-context validation and propagation, policy checks, route control, layered rate limits/quotas, request validation, safe errors, correlation/audit, API version routing and bounded failure controls. The gateway routes to the existing six backend deployables; it does not add a seventh service or require a specific physical topology or vendor.

Internal service-to-service communication remains governed by HD-REP-14 and must independently authenticate, authorize and enforce tenant/project scope. Receiving services remain authoritative for resource-level authorization. Do not expose internal administration, database, Temporal or sandbox management interfaces publicly. Client-supplied tenant/project identifiers are not authority. Preserve the agent tool boundary and independent human approval gates.

Apply layered controls by client, principal, tenant, project, endpoint, network, concurrency and payload/bandwidth. Keep request quotas distinct from spending and agent execution budgets. Protect expensive multimodal and sandbox operations. Require TLS/certificate lifecycle, WAF/DDoS capability, strict request validation, SSRF/destination controls, secure CORS, webhook authenticity/replay, upload validation and sensitive-data redaction. Public API versioning follows HD-REP-14 compatibility and deprecation governance. Fail closed for identity, authorization and approval checks; use bounded retries/timeouts and idempotency.

Add RSK-35; formal scoring pending. Require POC-REP-15-01 through -24; unexecuted. Preserve six backend deployables, 23 agent modules, tenant isolation and all HD-08 gates. Documentation approval does not authorize gateway installation, configuration, activation, infrastructure, credentials, external services, spending, GitHub/CI configuration, live data processing, production deployment or Phase 1.


## HD-REP-16 — Repository Security and Cryptographic Controls (Approved 2026-11-20)

Apply provider-independent, zero-trust-oriented secrets, identity and cryptographic controls across the Factory source repository and the isolated customer project repositories defined by HD-REP-05. No secret, privileged credential, private key, signing key or certificate private material may be committed to source, frontend bundles, Git history, build artifacts, ordinary configuration or logs. Secret scanning must cover commits, PRs, configuration and artifacts, including generated customer projects.

Use separate scoped identities and credentials for humans, services, agents, builds and external integrations. Prefer short-lived workload credentials; enforce tenant/project scope, least privilege, revocation and attributable use. Keep Factory credentials separate from customer build environments and customer-managed integrations. Public frontend credentials are never treated as secrets.

Centralise controlled secret/key lifecycle management. Separate encryption, token-signing, artifact-signing, webhook and transport key purposes. Protect private keys outside repositories and ordinary workflow configuration; use hardware-backed or equivalent isolated protection for high-value signing keys where justified. Require secure rotation, revocation, recovery, audit and compromise response. Protect repository transport, storage, backup, export and artifact flows with appropriate encryption and integrity controls. Signing and provenance verification must be independently verifiable.

Automation must not expose privileged secrets to untrusted PR code, customer builds or agent contexts. Workflow identities and credentials must be narrowly scoped and separated between untrusted validation and trusted release activities. Agents may detect and prepare remediation but cannot grant themselves credentials, extract unrelated secrets, export private keys, weaken controls or bypass HD-08.

Require POC-REP-16-01 through -26; all remain unexecuted. Add RSK-36; formal risk scores pending. Documentation approval does not authorise provider connection, credential/key creation, GitHub configuration, CI/CD activation, subscriptions, infrastructure, customer integration, production changes or Phase 1.



## HD-REP-17 — Secure Development and Application Security Governance (Approved 2026-11-20)

The repository governance model includes a risk-based Secure SDLC for Factory source, five frontend applications, six backend deployables, shared packages, 23 logical agent modules and generated customer projects. Security evidence is maintained as controlled documentation and linked to relevant source changes, tests, vulnerability findings, remediation and release records.

Security-sensitive changes require appropriate threat modelling, independent review, security testing and traceable evidence. SAST, dependency analysis, secret scanning, DAST where appropriate, API/frontend testing and manual review are architectural requirements, not currently activated workflows or installed tools. Generated customer projects require proportionate security profiles and clear disclosure of known limitations; Factory generation is not a security guarantee.

Vulnerability findings follow a recorded discover/classify/prioritise/remediate/verify/close lifecycle. Proposed internal objectives are Critical 24 hours, High 7 calendar days, Medium 30 calendar days and Low 90 calendar days, subject to contextual escalation and documented exceptions. HD-07/HD-08 remain authoritative. Agents may analyse findings and prepare scoped remediation changes but cannot self-approve, accept risk or deploy production fixes.

Required validation POC-REP-17-01 through -24 is defined in TESTING_STRATEGY.md and remains unexecuted. RSK-37 is added to RISK_REGISTER.md with formal scoring pending. This decision authorises documentation only; no security tooling, CI/CD, source changes, credentials, infrastructure, live testing, production activity or Phase 1 is authorised.

---

## HD-REP-18 — Configuration and Environment Governance (Approved 2026-11-21)

Add HD-REP-18 to the approved repository-level decision series. Configuration ownership and change history must be explicit and consistent with the monorepo and six-deployable boundaries. Keep Factory platform configuration separate from each isolated customer-project repository and its tenant/project-scoped configuration. Non-secret configuration may be version-controlled; secrets and privileged credentials must never be committed. Configuration and deployment workflow files require protected review and least-privilege automation. Logical DEV, TEST, STAGING and PRODUCTION environments must remain independently governed; this does not require four physical infrastructure stacks. Agents may inspect and prepare changes within scope but cannot self-approve, apply consequential production changes or bypass HD-08. Require POC-REP-18-01 through -24; all remain unexecuted. Add RSK-38, scores pending. Documentation only; no repository settings, environment provisioning, configuration application, credentials, CI/CD activation, spending, production deployment or Phase 1 is authorised.
