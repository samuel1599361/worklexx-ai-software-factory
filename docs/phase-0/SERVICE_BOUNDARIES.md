# Worklexx AI Software Factory — Service Boundaries and Responsibilities

## Document Metadata

- **Document ID:** WLX-ARCH-006
- **Document Title:** Service Boundaries and Responsibilities
- **Status:** Revised Architecture Blueprint (Phase 0 Revision Cycle — Awaiting Final Human Review and Approval)
- **Author:** Principal Software Architect, Distributed Systems Architect
- **Target Repository:** `https://github.com/samuel1599361/worklexx-ai-software-factory`
- **Classification:** Enterprise Technical Specification
- **Architecture Scope:** Six deployable backend service units and their logical modules
- **Related Documents:** WLX-ARCH-001 through WLX-ARCH-016

---

## 1. Purpose

This document defines the service boundaries, responsibilities, interfaces, data ownership, security controls, and deployment relationships for the Worklexx AI Software Factory.

It establishes which backend service is responsible for each major platform capability and prevents responsibilities from becoming duplicated or ambiguously assigned.

The architecture must support:

- Multi-tenant software development and project isolation.
- Agent-based software engineering workflows.
- Multimodal user input and generated media.
- Secure execution of generated code.
- Usage metering, billing, credits, and financial records.
- Advertising operations with strict privacy boundaries.
- Human approval and governance controls.
- Reliable asynchronous workflows.
- Independent service evolution without unnecessary distributed-system complexity.

This document is an architectural specification. It does not establish that any service has been implemented, deployed, tested, or approved for production.

## 2. Architectural Principles

The service architecture follows these principles.

### 2.1 Clear ownership

Every important business capability, authoritative data record, and state transition must have an identified owner.

A service may expose an API to other services, but it must not allow other services to bypass its authorization and business rules by directly modifying its authoritative data.

### 2.2 Six deployable backend service units

The Project Owner approved the six logical backend deployable boundaries on 2026-11-19. Physical topology and consolidation remain subject to implementation validation. The six deployable backend service units are:

1. `api-gateway`
2. `agent-orchestrator`
3. `multimodal-service`
4. `sandbox-runner`
5. `billing-ledger`
6. `adtech-service`

These are logical deployment boundaries in the Phase 0 architecture. Their final physical deployment topology, sizing, and infrastructure placement remain subject to architecture validation and human approval.

### 2.3 Logical modules are not automatically microservices

The 23 Worklexx agents are logical capabilities grouped into five functional modules.

They do not automatically require 23 independently deployed services.

Agents should execute through the agent orchestration architecture and use the appropriate service interfaces.

### 2.4 Deterministic authority

AI agents may interpret requests, plan tasks, recommend actions, and coordinate workflows.

They must not independently become authoritative for:

- Financial balances.
- Ledger postings.
- Payment verification.
- Tenant authorization.
- Production deployment approval.
- Protected GitHub operations.
- Security policy enforcement.
- Final workflow state transitions where deterministic enforcement is required.

These responsibilities belong to deterministic services and controlled human approval mechanisms.

### 2.5 Secure service-to-service communication

Internal service calls must use authenticated service identities, authorized scopes, validated request schemas, and auditable correlation identifiers.

Internal network location alone must not be treated as proof of authorization.

### 2.6 Explicit failure handling

Services must define timeout, retry, idempotency, cancellation, recovery, and reconciliation behaviour for operations that cross service boundaries.

A successful network request must not automatically be interpreted as proof that a downstream business operation completed.

### 2.7 Tenant isolation

Tenant isolation must apply across APIs, databases, object storage, Git repositories, generated artifacts, sandbox execution, background workers, logs, and other tenant-owned resources.

PostgreSQL Row-Level Security is an important control, but it is not a complete tenant-isolation architecture by itself.

## 3. Service Inventory

| Service | Primary responsibility | Authoritative domain |
|---|---|---|
| `api-gateway` | External API access, request validation, identity-token enforcement, routing and API policy | API access and request admission |
| `agent-orchestrator` | Agent execution, planning, workflow coordination and task state | Agent and workflow execution |
| `multimodal-service` | Input processing, media preparation, model-assisted media operations and generated media coordination | Multimodal job and media-processing metadata |
| `sandbox-runner` | Isolated execution of generated or user-supplied code | Sandbox execution and execution evidence |
| `billing-ledger` | Credits, usage charges, payment events, financial balances and ledger records | Financial records and billing state |
| `adtech-service` | Advertising inventory, campaigns, delivery, measurement and advertiser operations | Advertising records and campaign state |

The service inventory is an architectural responsibility map. It does not imply that every service must initially be deployed on separate infrastructure.

Any proposed consolidation or separation must preserve the ownership, authorization, audit, and isolation requirements defined here.

## 4. High-Level Service Interaction

The intended high-level interaction is:

1. A user accesses one of the Worklexx frontend applications.
2. The request reaches the appropriate application backend-for-frontend or API entry point.
3. `api-gateway` validates the request, verifies the identity token, enforces API access policies, and routes authorized requests.
4. `agent-orchestrator` manages agent execution and coordinates the required services.
5. `multimodal-service` processes supported text, image, audio, video, or other media-related tasks.
6. `sandbox-runner` executes authorized code or test workloads in an isolated environment.
7. `billing-ledger` authoritatively validates credit availability, records usage, processes verified payment events, and maintains financial records.
8. `adtech-service` handles authorized advertising operations without receiving access to private prompts, source code, uploaded confidential files, credentials, or confidential user activity.
9. Results and workflow status are returned through authorized service interfaces to the frontend.

Not every request requires every service.

The orchestration layer must invoke only the capabilities necessary for the requested task and permitted by the applicable policies and approvals.

## 5. API Gateway — `api-gateway`

### 5.1 Purpose

The API Gateway is the controlled entry point for external API requests and approved internal API routing.

It protects backend services from direct, uncontrolled external access.

It is not the identity provider and does not own user passwords or primary authentication credentials.

### 5.2 Responsibilities

The API Gateway is responsible for:

- External API routing.
- Request validation and schema enforcement.
- Authentication-token verification.
- Authorization-policy enforcement at the API boundary.
- Tenant and project context validation.
- Rate limiting and abuse controls.
- Request-size and upload admission limits.
- API versioning and compatibility controls.
- Request correlation and trace propagation.
- Webhook ingress routing.
- Controlled access to approved streaming endpoints.
- API error normalization.
- Security-relevant access logging.
- Rejection of unauthorized or malformed requests.

### 5.3 Authentication boundary

The external identity provider owns primary authentication responsibilities, including:

- Credential management.
- MFA.
- Identity-provider sessions.
- Authentication recovery.
- Identity-provider token issuance.

The Worklexx application owns its own:

- Organization memberships.
- Tenant membership.
- Project membership.
- Application-level roles.
- Feature entitlements.
- Application-specific authorization policies.

The Gateway validates identity tokens and applies relevant API access policies.

It must not assume that a valid identity-provider token automatically grants access to every tenant, project, resource, or operation.

### 5.4 Token validation

Token validation must include the applicable checks for:

- Approved signing algorithm.
- Signature verification.
- Issuer.
- Audience.
- Expiration.
- Not-before time.
- Subject.
- Key identifier and trusted JWKS source.
- Relevant scopes and claims.
- Revocation or session-status policy where required.

The Gateway must reject tokens with unsupported algorithms, invalid signatures, incorrect audiences, expired validity, or otherwise invalid claims.

### 5.5 Tenant context

The Gateway may derive tenant and project context from an authorized request and validated application membership.

It must not trust a client-supplied tenant identifier without checking the authenticated user's membership and access rights.

Tenant context must be propagated to downstream services through authenticated, integrity-protected internal requests.

Downstream services must independently validate the context relevant to their own responsibilities.

### 5.6 API Gateway and identity-provider separation

The Gateway must remain logically separate from the identity provider.

The Gateway may integrate with a managed or internally operated OIDC identity provider, but the identity-provider deployment decision remains pending human approval.

The API Gateway must not become an undocumented replacement identity provider.

### 5.7 AI model routing distinction

AI model routing is a logical platform capability, not a seventh deployable backend service in the current six-service baseline.

Its final internal placement must be selected during implementation planning.

The architecture must not create an additional independently deployed AI Gateway merely by interpreting a logical routing capability as a separate service.

### 5.8 Deployment and ingress considerations

The Gateway's protection requirements must cover all relevant external ingress paths, including:

- Public API endpoints.
- Authentication callbacks where applicable.
- Payment-provider webhooks.
- Approved streaming endpoints.
- Administrative endpoints.
- Other externally reachable service interfaces.

Cloud Armor or another perimeter security product must not be assumed to protect every frontend or serverless ingress automatically.

Actual protection depends on the hosting topology, routing configuration, and supported integration.

### 5.9 Non-responsibilities

The Gateway does not:

- Own financial balances.
- Post ledger entries.
- Execute arbitrary user code.
- Own agent workflow state.
- Replace the identity provider.
- Make final production deployment decisions.
- Grant protected GitHub permissions without the applicable authorization.
- Provide direct access to confidential advertising-excluded data.

## 6. Agent Orchestrator — `agent-orchestrator`

### 6.1 Purpose

The Agent Orchestrator coordinates the Worklexx 23-agent ecosystem and manages execution of authorized software-engineering workflows.

It provides the central execution and coordination environment for logical agents.

### 6.2 Responsibilities

The Agent Orchestrator is responsible for:

- Agent registration and capability discovery.
- Agent selection and task assignment.
- Task planning and dependency coordination.
- Workflow initiation and progression.
- Agent execution context.
- Agent-to-agent coordination.
- Workflow status management.
- Retry and timeout policy.
- Cancellation handling.
- Human approval requests.
- Approval-state integration.
- Tool-call authorization checks.
- Execution audit metadata.
- Result aggregation.
- Usage-event generation.
- Workflow recovery and reconciliation coordination.

### 6.3 Agent execution model

The 23 agents are logical execution components.

They may be implemented as modules, workers, or other internal execution units within the orchestration architecture.

The exact runtime model must be validated during implementation.

The agent count must not be used as a reason to create unnecessary independent services.

### 6.4 Workflow orchestration

Temporal is the preferred workflow-orchestration candidate, subject to a proof of concept.

The final choice between Temporal Cloud and self-hosted Temporal remains unresolved.

The selected workflow engine must support the required durability, retry, timeout, cancellation, observability, and recovery characteristics.

Workflow state must not depend solely on an in-memory process or ephemeral message.

### 6.5 Workflow lifecycle

The baseline workflow lifecycle is:

`Created → Validating → Queued → Running → AwaitingApproval → Completed / Failed / Cancelled`

Not every workflow must enter `AwaitingApproval`.

The orchestration layer must define valid state transitions and reject invalid transitions.

A workflow must not be marked `Completed` merely because an agent returned a successful message.

Completion must reflect the verified outcome of the required workflow activities.

### 6.6 Agent authority restrictions

Agents may:

- Interpret user instructions.
- Generate plans.
- Produce proposed code and documentation.
- Request authorized tool operations.
- Coordinate tests.
- Report findings.
- Recommend actions.

Agents must not bypass the deterministic services or human approval requirements that govern protected operations.

### 6.7 Agent21 and financial operations

Agent21 is an advisory and coordination capability.

It may:

- Explain available credits using authorized information.
- Estimate likely task costs.
- Recommend usage plans.
- Explain billing events.
- Request a billing operation through an authorized interface.

It must not:

- Directly modify balances.
- Create authoritative ledger entries.
- Bypass credit reservations.
- Confirm payments based solely on browser redirects.
- Override financial policy.
- Change billing records through direct database access.

All authoritative financial operations belong to `billing-ledger`.

### 6.8 Agent22 and multimodal operations

Agent22 coordinates multimodal tasks through `multimodal-service`.

It must not bypass that service's validation, file handling, media-processing, and security controls.

### 6.9 Agent23 and advertising operations

Agent23 coordinates advertising-related capabilities through `adtech-service`.

It must not gain access to private prompts, confidential source code, uploaded confidential files, credentials, or confidential user activity to improve advertising targeting.

### 6.10 Non-responsibilities

The Agent Orchestrator does not:

- Replace the API Gateway.
- Own authoritative financial balances.
- Execute untrusted code directly in its own process.
- Replace the multimodal-processing service.
- Become the authoritative advertising database.
- Independently authorize production deployment.
- Independently authorize protected GitHub operations.

## 7. Multimodal Service — `multimodal-service`

### 7.1 Purpose

The Multimodal Service handles media-related processing and coordination for the Worklexx platform.

It provides a controlled boundary for processing text-associated media, images, audio, video, and other supported input or output formats.

### 7.2 Responsibilities

The service is responsible for:

- Media-upload processing.
- Media metadata extraction.
- File-format validation.
- Image-processing workflows.
- Audio-processing workflows.
- Video-processing workflows.
- Speech transcription and related processing.
- Text extraction from supported media.
- Media conversion and preparation.
- Approved model-provider integrations for media tasks.
- Generated media coordination.
- Media-processing job status.
- Media-related usage measurements.
- Controlled media artifact storage integration.
- Security checks before media is made available for downstream processing.

### 7.3 Supported media categories

The architecture may support:

- Text.
- Images.
- Audio.
- Video.
- Documents.
- Other formats approved through the platform's capability and security process.

Actual supported formats, maximum sizes, duration limits, resolution limits, and model capabilities must be defined and tested during implementation.

### 7.4 Upload security

Newly uploaded files must be treated as pending or quarantined until required security checks have completed.

The upload lifecycle should distinguish:

1. Upload initiated.
2. Upload received.
3. File quarantined.
4. Format and content validation.
5. Malware and policy scanning.
6. Approved for processing, rejected, or held for review.
7. Processing completed.
8. Retained, archived, or deleted under the applicable policy.

A successful upload must not automatically mean that a file is safe.

### 7.5 Storage boundary

The service may coordinate with object storage for large media assets.

Object storage must enforce:

- Tenant-specific access control.
- Encryption.
- Authorized upload and download.
- Short-lived signed access where appropriate.
- Versioning and retention policy.
- Malware quarantine.
- Controlled deletion.
- Auditability.
- Backup and recovery requirements.

Large binary media should not be stored directly in PostgreSQL merely because PostgreSQL is available.

PostgreSQL may store the relevant metadata, ownership, status, and references.

### 7.6 Model-provider boundary

The Multimodal Service may call approved external or internal model providers.

Provider credentials must be held in an approved secrets-management system.

The service must enforce:

- Approved model and provider configuration.
- Tenant and data-access policies.
- Request-size limits.
- Provider timeout and retry policies.
- Usage measurement.
- Data-handling restrictions.
- Provider-specific retention and privacy requirements.

Model-provider availability and performance must not be treated as guaranteed.

### 7.7 Non-responsibilities

The Multimodal Service does not:

- Own financial balances.
- Authorize payment settlement.
- Execute arbitrary generated software as a sandbox.
- Own the central agent workflow.
- Authorize production deployments.
- Grant unrestricted access to uploaded files.

## 8. Sandbox Runner — `sandbox-runner`

### 8.1 Purpose

The Sandbox Runner executes authorized code, generated projects, and test workloads in isolated execution environments.

It is a security-sensitive boundary because generated or user-supplied code must be treated as potentially untrusted.

### 8.2 Responsibilities

The service is responsible for:

- Sandbox provisioning and lifecycle.
- Authorized code execution.
- Build and test execution.
- Dependency installation under policy.
- Resource and execution-time limits.
- Filesystem isolation.
- Process isolation.
- Network-egress restrictions.
- Execution logs and evidence.
- Artifact collection.
- Sandbox termination and cleanup.
- Execution status reporting.
- Isolation and security telemetry.

### 8.3 Execution authorization

A sandbox execution request must include an authorized project or task context.

The service must verify:

- Requesting service identity.
- Tenant and project authorization.
- Approved execution policy.
- Input artifact references.
- Resource limits.
- Applicable approval requirements.
- Execution expiry and cancellation rules.

The service must not accept arbitrary external execution requests without authorization.

### 8.4 Isolation model

A hardened sandbox runtime such as gVisor on GKE is a candidate architecture.

It remains subject to a security and operational proof of concept.

The selected environment must address:

- Non-root execution.
- Process isolation.
- Filesystem restrictions.
- CPU and memory limits.
- Disk and storage limits.
- Execution timeouts.
- Default-deny network egress.
- DNS and IPv6 restrictions.
- Cloud metadata-service access prevention.
- Credential isolation.
- Container and image hardening.
- Sandbox cleanup.
- Escape testing.
- Monitoring and incident response.

gVisor must not be represented as eliminating all sandbox escape or isolation risks.

MicroVM-based alternatives may be evaluated where stronger isolation is required.

### 8.5 Network policy

Generated code must not receive unrestricted outbound network access.

Any permitted network access must be explicitly scoped and controlled.

Controls must address:

- Private network access.
- Internal service endpoints.
- Cloud metadata services.
- DNS resolution.
- IPv4 and IPv6.
- Localhost and host-network exposure.
- Redirects and DNS rebinding.
- Unauthorized data exfiltration.

### 8.6 Artifact handling

Artifacts produced by a sandbox must be associated with:

- Tenant.
- Project.
- Workflow or task.
- Execution identifier.
- Source revision or input digest where applicable.
- Execution timestamp.
- Relevant toolchain and runtime versions.
- Validation and test results.
- Security scan results where available.

Artifacts must pass applicable validation and security checks before being promoted to a trusted project artifact or release candidate.

### 8.7 Non-responsibilities

The Sandbox Runner does not:

- Decide whether a user is authorized to access a tenant.
- Own billing balances.
- Authorize production deployment.
- Merge protected GitHub branches independently.
- Serve as the primary workflow engine.
- Treat generated code as trusted merely because an AI agent produced it.

## 9. Billing Ledger — `billing-ledger`

### 9.1 Purpose

The Billing Ledger is the authoritative financial service for Worklexx.

It manages credits, usage charges, payment-provider events, financial balances, billing records, and ledger transactions.

Its business rules must be deterministic, auditable, and independent of AI-generated decisions.

### 9.2 Responsibilities

The service is responsible for:

- Credit accounts.
- Credit balances.
- Credit reservations.
- Credit consumption.
- Usage metering records.
- Billing calculations.
- Payment-provider integration.
- Payment-event verification.
- Financial ledger records.
- Invoice and receipt records.
- Refund and reversal processing.
- Reconciliation.
- Financial audit history.
- Billing-related idempotency.
- Financial reporting data.

### 9.3 Financial authority

Only `billing-ledger` owns authoritative financial balances and ledger postings.

Other services must use approved APIs or controlled event interfaces to request financial operations.

Direct modification of financial records by agents or unrelated services is prohibited.

### 9.4 Credit lifecycle

The baseline credit lifecycle is:

1. Estimate expected usage and cost.
2. Validate account, tenant, policy, and available balance.
3. Reserve the required credits atomically.
4. Authorize the associated task.
5. Measure actual usage.
6. Calculate the final charge.
7. Settle the reservation.
8. Release unused reserved credits or perform a controlled compensation.
9. Reconcile any discrepancy.

A task must not consume credits based solely on an AI agent's unverified estimate.

### 9.5 Ledger integrity

Financial records must follow controlled accounting rules.

The architecture requires:

- Atomic double-entry posting per transaction and currency.
- Balanced posted transactions.
- Immutable posted entries.
- Controlled draft-to-posted transitions.
- Compensating entries for reversals and corrections.
- Unique provider-scoped idempotency keys.
- Reconciliation with payment-provider records.
- Restricted financial database permissions.
- Auditable administrative adjustments.

A posted financial entry must not be silently edited or deleted to correct an error.

### 9.6 Payment-provider events

Payment webhooks must be verified using the provider-specific signature mechanism.

For example:

- Paystack webhook verification must use the applicable HMAC-SHA512 signature procedure against the raw request body.
- Stripe webhook verification must use Stripe's provider-specific signature verification procedure.

The implementation must not assume that two payment providers use interchangeable signature formats.

The processing sequence must include:

1. Receive the event.
2. Verify its signature and integrity.
3. Validate the provider and event type.
4. Persist the verified event or a durable processing record.
5. Apply provider-scoped deduplication and idempotency.
6. Process the event through controlled financial logic.
7. Record the resulting ledger state.
8. Reconcile incomplete or disputed outcomes.

Browser redirects and client-side success messages are not proof of payment.

### 9.7 Usage metering

Usage records may originate from the Agent Orchestrator, Multimodal Service, Sandbox Runner, or other authorized components.

The Billing Ledger must validate the source and required attributes before using usage events for charging.

Usage events should include appropriate identifiers, such as:

- Tenant.
- Project.
- User or authorized principal where applicable.
- Workflow or task.
- Service or capability.
- Usage category.
- Quantity and unit.
- Provider or model identifier where relevant.
- Timestamp.
- Idempotency identifier.

### 9.8 Agent21 boundary

Agent21 may explain or recommend billing actions.

It must not create authoritative balances or directly post financial transactions.

The Billing Ledger must independently validate every financial operation.

### 9.9 Non-responsibilities

The Billing Ledger does not:

- Execute agents.
- Run generated code.
- Authorize GitHub merges.
- Approve production deployments.
- Own advertising campaign delivery.
- Trust unverified browser payment results.

## 10. Advertising Technology Service — `adtech-service`

### 10.1 Purpose

The Advertising Technology Service manages the platform's advertising capabilities and associated commercial operations.

It provides a controlled boundary for advertiser management, campaign configuration, inventory, delivery, measurement, and advertising-related records.

### 10.2 Responsibilities

The service is responsible for:

- Advertiser accounts.
- Campaign management.
- Advertising inventory.
- Campaign eligibility.
- Creative management.
- Creative validation.
- Advertising placement.
- Delivery coordination.
- Impression and click measurement.
- Campaign budget records.
- Advertising performance reporting.
- Fraud and abuse signals.
- Advertiser billing integration through authorized Billing Ledger interfaces.
- Advertising policy enforcement.
- Advertising audit records.

### 10.3 Privacy boundary

The Advertising Service must not receive unrestricted access to:

- Private user prompts.
- Confidential source code.
- Private project repositories.
- Uploaded confidential files.
- API keys and credentials.
- Secrets and tokens.
- Confidential workflow content.
- Private agent conversations.
- Confidential user activity.

Advertising operations must use explicitly authorized advertising data, public inventory information, or approved aggregated information.

### 10.4 Separation controls

Advertising separation must be enforced through multiple controls, including:

- Dedicated service identity.
- Restricted API scopes.
- Database schemas or roles.
- Tenant and advertiser authorization.
- Network access controls.
- Explicitly approved data feeds.
- Restricted event subscriptions.
- Data minimization.
- Audit logging.
- Privacy and retention policies.

A policy statement alone is insufficient to enforce this boundary.

The architecture must not claim that a cryptographic air gap exists unless such a design has actually been implemented and independently validated.

### 10.5 Campaign and creative controls

Advertising content must be subject to applicable policy and safety checks.

The service should support:

- Advertiser verification.
- Creative review.
- Destination and landing-page review.
- Prohibited-content controls.
- Campaign approval.
- Budget and delivery limits.
- Fraud monitoring.
- Complaint and takedown handling.

### 10.6 Financial integration

Advertising campaign charges, deposits, refunds, or other financial transactions must use authorized Billing Ledger interfaces.

`adtech-service` may maintain campaign budget and delivery records, but it must not independently modify authoritative financial balances.

### 10.7 Agent23 boundary

Agent23 may coordinate advertising operations through `adtech-service`.

It must not bypass advertising privacy controls or obtain confidential platform data for targeting.

### 10.8 Non-responsibilities

The Advertising Service does not:

- Own user authentication.
- Own platform-wide financial balances.
- Execute generated code.
- Coordinate all 23 agents.
- Access private prompts or source repositories by default.
- Override platform security or privacy policies.

## 11. Cross-Service Communication

### 11.1 Communication principles

Service communication must be explicit, authenticated, versioned, and observable.

The preferred communication mechanism depends on the operation.

Synchronous APIs are appropriate for operations requiring an immediate response or authorization decision.

Asynchronous events are appropriate for decoupled notifications and long-running workflow coordination.

### 11.2 Synchronous communication

Internal API calls must define:

- Authenticated caller identity.
- Authorized operation.
- Request and response schemas.
- Timeout.
- Error contract.
- Correlation identifier.
- Idempotency behaviour where applicable.
- Version compatibility.
- Audit requirements.

Services must not trust an internal request merely because it originates from a private network.

### 11.3 Asynchronous communication

Asynchronous messaging may be used for:

- Workflow notifications.
- Usage events.
- Media-processing status.
- Sandbox execution results.
- Billing events.
- Advertising delivery events.
- Reconciliation notifications.

Event contracts must define:

- Event identifier.
- Event type.
- Schema version.
- Producer identity.
- Tenant and project context where appropriate.
- Event timestamp.
- Correlation and causation identifiers.
- Idempotency or deduplication key.
- Data classification.
- Authorized consumers.

### 11.4 Redis Pub/Sub

Redis Pub/Sub may support ephemeral notifications, cache-related events, or wake-up signals.

It must not be treated as the durable system of record for:

- Financial transactions.
- Workflow history.
- Approval decisions.
- Project artifacts.
- Payment events.
- Other business-critical records.

Durable operations require persistent storage or a durable workflow and messaging mechanism.

### 11.5 Delivery semantics

The architecture must assume that asynchronous activities may be delivered or executed more than once.

It must not claim exactly-once external side effects without a demonstrated mechanism that supports that claim.

Consumers must use appropriate:

- Idempotency.
- Deduplication.
- Durable state.
- Bounded retries.
- Dead-letter handling.
- Reconciliation.
- Compensation.
- Manual recovery.

### 11.6 Transactional outbox and inbox

Where a database transaction must reliably produce an event, use an appropriate transactional outbox pattern.

Where event consumption must be recorded reliably, use an inbox or equivalent deduplication mechanism.

The exact implementation must be defined during service design and validated under failure conditions.

## 12. Workflow and Long-Running Operations

### 12.1 Workflow ownership

The Agent Orchestrator owns the coordination of agent workflows.

Individual services own the state of their respective business operations.

For example:

- The Agent Orchestrator owns the agent workflow state.
- The Multimodal Service owns multimodal job state.
- The Sandbox Runner owns sandbox execution state.
- The Billing Ledger owns financial transaction state.
- The AdTech Service owns campaign and advertising-delivery state.

The Gateway does not become the authoritative owner of these downstream business records.

### 12.2 Workflow engine

Temporal remains the preferred workflow-engine candidate, subject to a proof of concept.

The proof of concept must evaluate:

- Workflow durability.
- Activity retries.
- Timeouts.
- Cancellation.
- Recovery.
- Versioning.
- Observability.
- Worker scaling.
- Database compatibility.
- Backup and restoration.
- Upgrade procedures.
- Operational complexity.
- Cost.

The decision between managed and self-hosted deployment remains pending.

### 12.3 External side effects

External side effects must be designed for retry and recovery.

Examples include:

- Payment-provider operations.
- GitHub operations.
- Object-storage writes.
- Sandbox creation.
- Model-provider calls.
- Email or notification delivery.

A retry must not accidentally create duplicate financial charges, duplicate releases, duplicate external records, or unauthorized repeated actions.

### 12.4 Compensation

Where an operation cannot be rolled back, the service must define a compensating action or a manual recovery procedure.

Compensation must be recorded and auditable.

## 13. Service Data Ownership

| Service | Data it owns authoritatively | Data it may reference |
|---|---|---|
| `api-gateway` | API access configuration and gateway-specific operational records | Identity claims, tenant membership and downstream resource identifiers |
| `agent-orchestrator` | Agent registry metadata, task coordination records and workflow execution metadata | Project artifacts, media job references, sandbox results and billing usage references |
| `multimodal-service` | Media-processing job metadata and processing status | Object-storage references, project metadata and authorized model-provider responses |
| `sandbox-runner` | Sandbox execution metadata, execution status and execution evidence | Source revisions, approved input artifacts and project metadata |
| `billing-ledger` | Credit accounts, balances, reservations, usage charges, payment events and ledger entries | Tenant and project identifiers, service usage references and provider transaction references |
| `adtech-service` | Advertisers, campaigns, creative records, inventory and advertising delivery records | Approved public or aggregated data and authorized billing references |

### 13.1 Data ownership enforcement

Other services must not directly write to another service's authoritative data tables.

Cross-service data access must use authorized APIs, controlled events, or explicitly approved read models.

Shared PostgreSQL infrastructure does not remove service ownership boundaries.

### 13.2 Database access

Database roles must follow least privilege.

Where services share a PostgreSQL cluster:

- Use separate database roles.
- Restrict schema access.
- Restrict write permissions.
- Enforce tenant isolation.
- Avoid broad cross-service privileges.
- Audit privileged operations.
- Apply migration ownership rules.

The database architecture must define the authoritative owner of each table and migration.

### 13.3 Tenant-owned data

Tenant isolation must be enforced across every service that stores tenant-owned data.

Controls must include appropriate combinations of:

- Tenant-scoped database records.
- PostgreSQL Row-Level Security.
- Composite tenant-aware foreign keys.
- Restricted database roles.
- Transaction-scoped tenant context.
- Object-storage access controls.
- Git repository authorization.
- Sandbox isolation.
- Background-worker tenant validation.
- Adversarial cross-tenant testing.

A session variable such as `app.current_tenant_id` is not sufficient on its own to establish tenant isolation.

### 13.4 Audit and retention

Financial and security-relevant audit records must be protected against unauthorized modification or deletion.

Retention and deletion must consider:

- Primary databases.
- Replicas.
- Backups.
- Object storage.
- Git history.
- Exported artifacts.
- Logs.
- Legal holds.
- Applicable privacy and retention obligations.

Deleting an application account must not automatically destroy legally required financial or security records.

## 14. Identity, Authorization and Approval Boundaries

### 14.1 Service identity

Each service must have an identifiable service identity.

Service-to-service authorization must be based on explicit permissions and the intended operation.

Shared static credentials across unrelated services should be avoided.

### 14.2 User identity and application authorization

The identity provider establishes authenticated identity.

Worklexx establishes application-level access through tenant membership, project membership, roles, and applicable policies.

The Gateway and downstream services must enforce the authorization relevant to their responsibilities.

### 14.3 Approval gates

The architecture recognizes six approval gates, GATE-01 through GATE-06.

Their complete definitions remain subject to human approval.

Two known approval boundaries must remain separate:

- **GATE-03:** Production deployment approval.
- **GATE-04:** Protected GitHub operations approval.
- **GATE-05:** Designated destructive database operations and migrations; complete scope and enforcement pending Project Owner confirmation.
- **GATE-06:** Designated consequential external integrations and live-account actions; complete scope and enforcement pending Project Owner confirmation.

GATE-01 and GATE-02 remain pending formal definition. GATE-05 and GATE-06 have identified intended control areas, but their complete scope, exceptions, approval authority, enforcement, and evidence requirements remain subject to explicit Project Owner confirmation. No gate automatically satisfies another.

### 14.4 Approval binding

A protected approval must be bound to the relevant:

- Authorized principal.
- Tenant and project.
- Action.
- Artifact, source revision, or commit digest where applicable.
- Target environment where applicable.
- Approval gate.
- Expiry.
- Single-use or replay-prevention control.
- Audit record.

Material changes to the approved action or artifact must invalidate the approval where the change affects the approval's scope.

### 14.5 Service enforcement

The service responsible for executing a protected operation must verify the applicable approval immediately before execution.

An agent's statement that an operation is approved is not sufficient evidence.

### 14.6 Owner and administrator authority

A user holding an owner or administrator role must not automatically be assumed to possess every protected approval authority.

The approval authority and delegation model remain explicit human decisions.

## 15. GitHub and External Development Integrations

### 15.1 GitHub boundary

GitHub operations are initiated through authorized platform capabilities and controlled integration credentials.

The Agent Orchestrator may coordinate GitHub-related work, but it does not replace GitHub's own access controls.

### 15.2 Protected operations

Protected operations may include:

- Branch creation.
- Commit creation.
- Push.
- Pull-request creation.
- Pull-request review or approval.
- Merge.
- Release creation.
- Protected branch changes.

The exact protected-operation list and approval workflow must be defined and approved.

GATE-04 is the designated protected GitHub operations approval boundary.

### 15.3 Repository isolation

Generated projects must remain isolated from the Worklexx platform repository unless an explicitly authorized operation requires otherwise.

Agent access must be restricted to the intended repository, branch, project, and operation.

### 15.4 Credential handling

GitHub tokens and integration credentials must be:

- Stored in approved secret-management infrastructure.
- Scoped to the minimum required permissions.
- Protected from agent prompts and generated logs.
- Rotated or revoked under policy.
- Audited.
- Excluded from generated source artifacts.

### 15.5 Failure handling

GitHub operations must record:

- Requested operation.
- Authorized actor or service identity.
- Target repository.
- Target branch or reference.
- Relevant artifact or commit digest.
- Approval evidence where required.
- Result.
- Failure details.
- Retry or manual-recovery status.

A network timeout must not be interpreted as proof that a GitHub operation failed. The resulting external state must be checked before retrying a potentially non-idempotent operation.

## 16. Security and Operational Boundaries

### 16.1 Least privilege

Every service must receive only the permissions required for its assigned responsibilities.

### 16.2 Secrets

Secrets must be managed through an approved secret-management mechanism.

They must not be stored in source code, agent prompts, logs, public artifacts, or generated project documentation.

### 16.3 Encryption and key management

Data must be protected in transit and at rest.

KMS integration does not automatically guarantee that every key or secret rotates correctly.

The implementation must define:

- Key ownership.
- Key versions.
- Data-encryption keys.
- Key-encryption keys.
- Envelope encryption.
- Rotation.
- Re-encryption where required.
- Revocation.
- Recovery.
- Audit.

### 16.4 Observability

Services must expose appropriate:

- Structured logs.
- Metrics.
- Distributed traces.
- Health checks.
- Readiness checks.
- Error rates.
- Latency measurements.
- Queue and worker metrics.
- Security events.

Observability data must be designed to avoid exposing credentials, private prompts, confidential source code, or unnecessary personal data.

### 16.5 Failure isolation

A failure in one service must not automatically cause uncontrolled failure in every other service.

Use appropriate:

- Timeouts.
- Bounded retries.
- Circuit breakers.
- Bulkheads.
- Queue limits.
- Backpressure.
- Graceful degradation.
- Recovery procedures.

### 16.6 Operational readiness

Each service must eventually have:

- An identified technical owner.
- Deployment configuration.
- Health and readiness checks.
- Monitoring and alerting.
- Backup or recovery requirements where applicable.
- Incident-response procedures.
- Access-control policies.
- Documented dependencies.
- Upgrade and rollback procedures.

These are implementation requirements, not claims of current readiness.

## 17. Deployment Boundaries and Scaling

### 17.1 Logical and physical deployment

The six-service baseline defines logical deployable units.

It does not prescribe that all six must run on separate clusters, nodes, or cloud accounts.

Physical placement must be determined through implementation design, security review, performance testing, and operational evaluation.

### 17.2 Independent scaling

Services should be capable of scaling according to their workload characteristics.

Examples include:

- Gateway request volume.
- Agent worker concurrency.
- Multimodal processing intensity.
- Sandbox CPU and memory consumption.
- Billing transaction volume.
- Advertising delivery volume.

Scaling targets and concurrency limits must be validated under realistic workloads.

### 17.3 No unsupported capacity assumptions

Specific concurrency limits, latency guarantees, minimum instance counts, or cost projections must not be treated as established facts until tested under the intended deployment conditions.

Cloud Run minimum instances, for example, do not guarantee the complete absence of cold starts or latency variation.

### 17.4 Long-running tasks

Long-running agent, media, and sandbox tasks must not depend on request lifetimes that are shorter than their execution requirements.

Use durable workflow coordination and appropriate worker execution environments.

Vercel runtime limits vary by plan and runtime configuration. Long-running jobs should be handled by suitable backend workers rather than assumed to fit within frontend request limits.

### 17.5 Disaster recovery

Service recovery must be considered at platform level.

Cloud SQL high availability is not, by itself, a complete disaster-recovery solution.

Recovery planning must include the relevant state and dependencies, such as:

- PostgreSQL.
- Workflow-engine persistence.
- Object storage.
- Git repositories.
- Financial ledger records.
- Identity configuration.
- KMS and secrets.
- Infrastructure configuration.
- Required external integration state.

Final RPO and RTO targets remain pending human decisions and recovery testing.

## 18. Service Interface and Contract Requirements

Each service must publish and maintain an interface contract.

The contract should define:

- Service name and owner.
- API or event version.
- Authentication requirements.
- Authorization requirements.
- Request schema.
- Response schema.
- Error model.
- Timeout.
- Retry policy.
- Idempotency requirements.
- Tenant-context requirements.
- Data classification.
- Audit requirements.
- Rate and resource limits.
- Compatibility and deprecation policy.

### 18.1 API compatibility

Breaking API changes must follow an explicit versioning and migration policy.

Consumers must not silently depend on undocumented implementation details.

### 18.2 Runtime validation

Static types alone do not guarantee that runtime messages conform to the intended contract.

Use runtime validation, generated API types where appropriate, and contract tests.

### 18.3 Event compatibility

Event producers and consumers must support an explicit schema-versioning strategy.

Incompatible event changes must not be introduced without an approved migration plan.

## 19. Service Testing and Acceptance Requirements

Each service must undergo appropriate testing before implementation acceptance.

### 19.1 Functional testing

Verify that each service performs only its assigned responsibilities and correctly handles valid and invalid requests.

### 19.2 Authorization testing

Verify:

- Unauthenticated access rejection.
- Unauthorized operation rejection.
- Tenant isolation.
- Project isolation.
- Service identity enforcement.
- Approval enforcement.
- Credential protection.

### 19.3 Failure testing

Verify:

- Timeouts.
- Retry behaviour.
- Duplicate event handling.
- Partial failures.
- Worker interruption.
- Cancellation.
- Recovery.
- Reconciliation.
- Dead-letter processing.

### 19.4 Security testing

Test the relevant threat scenarios for each service, including privilege escalation, unauthorized data access, injection, secrets exposure, and service-to-service abuse.

### 19.5 Performance testing

Measure actual throughput, latency, concurrency, resource consumption, and cost under documented test conditions.

Targets must be distinguished from measured results.

### 19.6 Cross-service integration testing

Verify that the six services interact through their documented contracts without bypassing ownership or authorization boundaries.

### 19.7 Acceptance evidence

Acceptance must be supported by documented test results, review evidence, unresolved defects, and an authorized decision.

A proposed test plan is not evidence that testing has occurred.

## 20. Human Decisions Pending

The following decisions remain open and must not be silently treated as approved.

| Decision ID | Decision | Required outcome |
|---|---|---|
| HD-SB-01 | Final physical deployment topology | Approve the deployment arrangement for the six service units |
| HD-SB-02 | Identity provider | Select managed or internally operated OIDC identity provider |
| HD-SB-03 | Workflow engine hosting | Select Temporal Cloud or self-hosted Temporal after proof of concept |
| HD-SB-04 | AI model-routing placement | Confirm its internal placement without creating an undocumented seventh deployable |
| HD-SB-05 | Database and schema ownership | Approve final service-owned data and migration boundaries |
| HD-SB-06 | Event and messaging architecture | Approve durable messaging, event delivery, and recovery design |
| HD-SB-07 | Sandbox runtime | Approve the isolation technology after security and operational testing |
| HD-SB-08 | Service availability and recovery | Approve service-level availability, RPO, RTO, and recovery objectives |
| HD-SB-09 | Approval authority | Identify authorized approvers and final GATE-01 through GATE-06 definitions |
| HD-SB-10 | Service consolidation | Decide whether any services may initially share infrastructure without weakening logical boundaries |

## 21. Phase 0 Execution Boundary

This document is part of Phase 0 architecture documentation.

Phase 0 activities are limited to:

- Architecture review.
- Documentation correction.
- Requirements clarification.
- Service-boundary definition.
- Identification of risks and unresolved decisions.
- Consistency review across architecture documents.
- Human approval preparation.

This document does not authorize:

- Creating backend services.
- Writing application implementation code.
- Creating database migrations.
- Provisioning cloud infrastructure.
- Creating or modifying production resources.
- Creating Git branches.
- Committing or pushing changes.
- Executing protected GitHub operations.
- Deploying services.
- Activating payment processing.
- Launching advertising operations.
- Beginning Phase 1.

Such activities require their own explicit authorization and applicable approval gates.

## 22. Related Architecture Documents

| Document ID | Document |
|---|---|
| WLX-ARCH-001 | ARCHITECTURE_OVERVIEW.md |
| WLX-ARCH-002 | SYSTEM_ARCHITECTURE.md |
| WLX-ARCH-003 | TECHNOLOGY_STACK.md |
| WLX-ARCH-004 | REPOSITORY_STRUCTURE.md |
| WLX-ARCH-005 | AGENT_ECOSYSTEM.md |
| WLX-ARCH-007 | DATABASE_ARCHITECTURE.md |
| WLX-ARCH-008 | SECURITY_ARCHITECTURE.md |
| WLX-ARCH-009 | DEPLOYMENT_ARCHITECTURE.md |
| WLX-ARCH-010 | DEVELOPMENT_ROADMAP.md |
| WLX-ARCH-011 | RISK_REGISTER.md |
| WLX-ARCH-012 | ADR_REGISTER.md |
| WLX-ARCH-013 | PHASE_0_INSPECTION_REPORT.md |
| WLX-ARCH-014 | TESTING_STRATEGY.md |
| WLX-ARCH-015 | MONITORING_AND_OBSERVABILITY.md |
| WLX-ARCH-016 | COST_AND_SCALABILITY.md |

## 23. Final Status

The six-service architecture establishes the intended backend service responsibilities and their logical boundaries.

The architecture recognizes:

- Six deployable backend service units.
- Twenty-three logical agents organized into functional modules.
- Centralized agent workflow coordination.
- Dedicated multimodal processing.
- Isolated code execution.
- Deterministic financial authority.
- Advertising privacy separation.
- Explicit service ownership.
- Tenant-aware security.
- Durable workflow and event-handling requirements.
- Separate production deployment and protected GitHub approval gates.

The following remain unresolved:

- Final physical deployment topology.
- Identity-provider selection.
- Workflow-engine hosting.
- AI model-routing placement.
- Final service-owned database and migration boundaries.
- Durable messaging implementation.
- Sandbox runtime selection.
- Availability and disaster-recovery objectives.
- Final approval authority and gate definitions.
- Service consolidation decisions.

**Document status:** Revised Architecture Blueprint — Awaiting Final Human Review and Approval.

**Implementation status:** Not implemented or verified by this document.

**Security status:** Requirements defined; implementation and independent security validation outstanding.

**Testing status:** Acceptance requirements defined; execution evidence outstanding.

**Phase 1 authorization:** Not granted.