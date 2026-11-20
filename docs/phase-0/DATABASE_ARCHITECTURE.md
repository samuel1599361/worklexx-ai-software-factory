# Worklexx AI Software Factory — Database Architecture

## Document Metadata

- **Document ID:** WLX-ARCH-007
- **Document Title:** Database Architecture
- **Status:** Revised Architecture Blueprint (Phase 0 Revision Cycle — Awaiting Final Human Review and Approval)
- **Author:** Principal Database Architect, Data Security Architect
- **Target Repository:** `https://github.com/samuel1599361/worklexx-ai-software-factory`
- **Classification:** Enterprise Technical Specification
- **Primary Database:** PostgreSQL
- **Vector Search:** PostgreSQL with pgvector preferred initial approach; configuration subject to POC-05
- **Related Documents:** WLX-ARCH-001 through WLX-ARCH-016, excluding this document

---

## 1. Purpose

This document defines the database architecture, data ownership, isolation controls, integrity requirements, storage relationships, and recovery principles for the Worklexx AI Software Factory.

It establishes the database requirements for a secure, multi-tenant, agentic software-development platform.

The architecture must support:

- User and organization data.
- Tenant and project management.
- Agent execution and workflow records.
- Software project metadata and artifact references.
- Multimodal processing metadata.
- Sandbox execution records.
- Usage metering and credit management.
- Payment events and financial ledger records.
- Advertising records.
- Audit and security events.
- Vector embeddings and retrieval metadata.
- Data retention, deletion, backup, and recovery.

This document describes intended architecture and requirements. It does not establish that the database schema has been implemented, tested, or approved for production.

## 2. Database Architecture Principles

The database architecture follows these principles.

### 2.1 Data ownership

Every authoritative data entity must have a clearly identified owning service.

A service must not directly modify another service's authoritative records without an explicitly authorized interface or controlled mechanism.

### 2.2 Tenant isolation

Every tenant-owned record must be protected against unauthorized cross-tenant access.

Tenant isolation must apply to:

- Database queries.
- Database writes.
- Foreign-key relationships.
- Background workers.
- Connection pools.
- Vector retrieval.
- Object storage.
- Git repositories.
- Generated artifacts.
- Audit and reporting interfaces.

### 2.3 Least privilege

Database roles must receive only the permissions required for their responsibilities.

Application services, agents, reporting processes, and migration tools must not share unrestricted database privileges.

### 2.4 Financial integrity

Financial records must use deterministic accounting rules.

AI agents must not directly create or modify authoritative balances or posted ledger entries.

### 2.5 Auditability

Security-relevant and financial operations must leave sufficient evidence for investigation, reconciliation, and authorized review.

### 2.6 Controlled data lifecycle

Data creation, modification, archival, deletion, anonymization, retention, and restoration must follow documented policies.

### 2.7 Explicit consistency

The architecture must distinguish between:

- Authoritative transactional records.
- Derived read models.
- Temporary cache entries.
- Ephemeral notifications.
- Search indexes.
- Vector embeddings.
- External object references.

A cache or derived representation must not silently become the authoritative source of business truth.

## 3. Database Technology Baseline

### 3.1 PostgreSQL

PostgreSQL is the primary relational database technology.

It is intended to provide:

- Transactional consistency.
- Relational integrity.
- Foreign-key enforcement.
- Controlled access.
- Row-Level Security.
- Indexing.
- Audit-related metadata.
- Transactional outbox and inbox support.
- Financial record integrity.

The exact PostgreSQL version, hosting configuration, extensions, and production sizing must be confirmed during implementation planning.

### 3.2 SQLAlchemy

SQLAlchemy is the preferred Python ORM and database-access framework.

Database access must use explicit transaction management and validated data-access patterns.

ORM usage must not be treated as a replacement for database-level integrity and authorization controls.

### 3.3 Alembic

Alembic is the preferred database migration tool for Python services using SQLAlchemy.

Migrations must:

- Have an identifiable owner.
- Be version-controlled.
- Be reviewed before application.
- Be tested against supported database versions.
- Define safe upgrade and rollback or recovery procedures.
- Avoid destructive changes without explicit approval.
- Preserve financial and audit history.

### 3.4 pgvector

PostgreSQL with pgvector is the approved preferred initial approach for vector storage and similarity search. A separate vector-database deployment is not proposed at this stage.

The selected PostgreSQL and pgvector versions, index types, supported dimensions, performance, tenant-filtering behaviour, and operational characteristics require POC-05 before implementation relies on a specific configuration.

### 3.5 Database hosting

Managed PostgreSQL is a candidate hosting approach.

The final provider, regions, high-availability arrangement, backup strategy, and disaster-recovery topology remain unresolved.

## 4. Logical Database Architecture

The database architecture should organize data around service ownership and business boundaries.

The logical ownership domains are:

1. Identity and application membership references.
2. Tenant and organization management.
3. Project and artifact metadata.
4. Agent and workflow execution.
5. Multimodal processing.
6. Sandbox execution.
7. Billing and financial ledger.
8. Advertising.
9. Audit and security events.
10. Embeddings and retrieval metadata.

These are logical data domains, not necessarily ten separate PostgreSQL databases.

The initial implementation may use a shared PostgreSQL cluster while preserving strict service ownership through schemas, database roles, privileges, and controlled interfaces.

The final physical database and schema topology remains subject to review.

## 5. Service Data Ownership

The six backend services are responsible for their respective authoritative data.

| Service | Authoritative data domain |
|---|---|
| `api-gateway` | Gateway configuration and API access operational records |
| `agent-orchestrator` | Agent registry metadata, execution records, task coordination and workflow metadata |
| `multimodal-service` | Media-processing jobs, processing status and media metadata |
| `sandbox-runner` | Sandbox execution records, status and execution evidence |
| `billing-ledger` | Credit accounts, reservations, balances, payment events, charges and ledger entries |
| `adtech-service` | Advertisers, campaigns, creatives, inventory and advertising delivery records |

### 5.1 Ownership enforcement

A service may reference another service's record through a stable identifier.

It must not assume that knowing an identifier grants permission to access or modify the referenced record.

Cross-service access must use:

- Authorized APIs.
- Controlled event interfaces.
- Approved read models.
- Explicitly authorized reporting mechanisms.

### 5.2 Shared database infrastructure

Sharing a PostgreSQL cluster does not imply shared unrestricted access.

The implementation must use appropriate:

- Database roles.
- Schema privileges.
- Table privileges.
- Function privileges.
- Restricted migration roles.
- Tenant isolation controls.
- Audit logging.

### 5.3 Migration ownership

Each schema or table must have an identifiable migration owner.

A service must not independently alter another service's authoritative schema without an approved coordination and migration process.

## 6. Tenant and Organization Data

### 6.1 Tenant model

The platform must support multiple organizations and tenants.

A tenant represents an application-level ownership and isolation boundary.

The architecture must distinguish:

- User identity.
- Organization membership.
- Tenant membership.
- Project membership.
- Application roles.
- Resource ownership.

An authenticated user may belong to multiple organizations or tenants.

### 6.2 User identity

The external identity provider is responsible for primary authentication.

The Worklexx database stores application-level identity references and authorization-related records as required.

It must not become an unnecessary duplicate credential store.

### 6.3 Membership

Membership records must establish the relationship between users and tenants or organizations.

Authorization must consider:

- Membership status.
- Assigned role.
- Project membership.
- Resource ownership.
- Applicable policy.
- Required approval.

A historical membership record must not automatically grant active access.

### 6.4 Tenant status

Tenant lifecycle records should support appropriate states, such as:

- Pending.
- Active.
- Suspended.
- Deactivated.
- Pending deletion.
- Archived, where applicable.

The final status model must be defined during schema design.

### 6.5 Tenant deletion

Tenant deletion must be a controlled lifecycle operation.

It must not blindly cascade-delete financial, legal, or security-relevant history.

The deletion process must consider retention obligations, legal holds, anonymization, backup retention, Git history, object storage, and external systems.

## 7. Tenant Isolation and PostgreSQL Row-Level Security

### 7.1 RLS requirement

PostgreSQL Row-Level Security must be used for tenant-owned tables where applicable.

RLS policies must restrict both reading and writing.

The architecture must not rely exclusively on application-layer filtering.

### 7.2 Policy requirements

RLS policies must account for:

- Tenant ownership.
- Authorized service identity.
- User or worker context where applicable.
- Read permissions.
- Insert permissions.
- Update permissions.
- Delete permissions.
- Administrative exceptions.
- Cross-tenant operations that are explicitly authorized.

### 7.3 FORCE ROW LEVEL SECURITY

`FORCE ROW LEVEL SECURITY` should be applied to tenant-owned tables where appropriate to reduce the risk of table-owner bypass.

The final policy must account for PostgreSQL superuser and `BYPASSRLS` privileges, which can bypass ordinary RLS protections.

Application services must not connect using superuser or unrestricted bypass roles.

### 7.4 Tenant context

The application may establish a transaction-scoped tenant context, for example through a controlled database setting such as:

`app.current_tenant_id`

However, this value alone is not a security control.

The architecture must ensure that:

- The context is derived from authenticated and authorized application state.
- The client cannot arbitrarily establish trusted tenant context.
- Database roles are restricted.
- Transaction boundaries are explicit.
- Context is set for every relevant transaction.
- Context is cleared or safely reset when connections are returned to pools.
- Background workers establish their own validated context.
- Connection reuse cannot leak one tenant's context into another tenant's request.

### 7.5 Connection pooling

Connection pools introduce risks when tenant context is session-scoped or incorrectly reused.

The implementation must use transaction-scoped context where appropriate and test:

- Successful context initialization.
- Context reset after commit.
- Context reset after rollback.
- Connection reuse.
- Concurrent requests.
- Worker reuse.
- Failed transactions.
- Cancellation and timeout paths.

### 7.6 Composite tenant-aware foreign keys

Tenant-owned relationships should use composite tenant-aware foreign keys where appropriate.

For example, if a project belongs to a tenant, a referencing record should not be able to associate a resource with a project from another tenant merely because it knows that project's identifier.

The database design must enforce tenant consistency through relational constraints, not only application checks.

### 7.7 Adversarial isolation testing

Testing must attempt to:

- Read another tenant's records.
- Modify another tenant's records.
- Insert records referencing another tenant's resources.
- Delete another tenant's records.
- Reuse stale tenant context.
- Exploit pooled connection reuse.
- Access data through background workers.
- Retrieve another tenant's vector embeddings.
- Access another tenant's object-storage artifacts.

Any cross-tenant access must be treated as a security defect.

## 8. Project and Artifact Metadata

### 8.1 Project records

Project records should include the necessary ownership and lifecycle metadata, such as:

- Project identifier.
- Tenant identifier.
- Project name.
- Description.
- Status.
- Creation timestamp.
- Last-modified timestamp.
- Owner or creator reference.
- Repository reference where applicable.
- Project configuration reference.

### 8.2 Artifact metadata

Artifact metadata may include:

- Artifact identifier.
- Tenant identifier.
- Project identifier.
- Artifact type.
- Storage reference.
- Version.
- Content digest.
- Creation timestamp.
- Source workflow or task.
- Security-validation status.
- Approval status.
- Retention metadata.

### 8.3 Artifact storage

Large files, generated media, source bundles, and other binary artifacts should normally be stored in object storage or an appropriate Git repository.

PostgreSQL should store metadata, authorization context, version references, and relevant transactional records.

### 8.4 Artifact integrity

Artifacts should have cryptographic content digests where appropriate.

The platform should be able to associate an artifact with its source revision, workflow, generating operation, and validation evidence.

A content digest supports integrity verification but does not by itself prove that an artifact is safe or authorized.

### 8.5 Project isolation

Generated project artifacts must remain isolated from the Worklexx platform repository unless a specifically authorized operation permits otherwise.

Repository references and artifact metadata must not be treated as authorization credentials.

## 9. Agent and Workflow Data

### 9.1 Agent registry

The Agent Orchestrator owns authoritative agent registry and execution metadata.

The registry may record:

- Agent identifier.
- Agent name.
- Agent version.
- Functional module.
- Capability metadata.
- Status.
- Policy references.
- Configuration version.
- Registration timestamp.

The 23 agents are logical capabilities, not 23 independent database or microservice deployments.

### 9.2 Agent execution records

Agent execution records should capture:

- Execution identifier.
- Tenant identifier.
- Project identifier where applicable.
- Agent identifier and version.
- Workflow identifier.
- Input and output artifact references.
- Start and completion timestamps.
- Execution status.
- Authorized tool activity metadata.
- Usage references.
- Error information.
- Relevant approval references.

### 9.3 Workflow records

Workflow records should capture the state and history of agent workflows.

The baseline lifecycle is:

`Created → Validating → Queued → Running → AwaitingApproval → Completed / Failed / Cancelled`

The implementation must define valid transitions and enforce them through the workflow engine and associated persistence mechanisms.

### 9.4 Workflow engine persistence

Temporal is the preferred candidate, subject to proof of concept.

Temporal Cloud is approved as the preferred initial hosting approach, subject to POC-06 and due diligence; self-hosted Temporal remains a future alternative.

Temporal persistence must be treated as workflow-engine state, not as a replacement for the authoritative business records owned by other services.

### 9.5 Foreign-key relationships

Where an agent execution references a workflow, the relationship must be defined consistently.

The design must not create a foreign key to a workflow table that is not part of the same authoritative database or controlled schema.

If workflow state is owned externally by the workflow engine, store and validate the appropriate workflow identifier and reference rather than inventing an unsupported relational dependency.

### 9.6 Execution history

Execution history must be retained according to security, operational, and privacy requirements.

Sensitive prompts, credentials, confidential source code, and unnecessary personal data must not be copied into general-purpose audit or execution logs.

## 10. Multimodal Processing Data

The Multimodal Service owns authoritative processing metadata.

Records may include:

- Media job identifier.
- Tenant identifier.
- Project identifier where applicable.
- Input artifact reference.
- Output artifact reference.
- Media type.
- Processing status.
- Model or provider reference.
- Model version where available.
- Processing timestamps.
- Usage measurement reference.
- Error and retry metadata.
- Security-validation status.

### 10.1 Media content

Large media content should normally be stored outside PostgreSQL.

Database records should reference the authorized storage location and metadata.

### 10.2 Upload state

New uploads must default to a pending or quarantined state.

The database must distinguish:

- Received.
- Pending validation.
- Quarantined.
- Approved for processing.
- Rejected.
- Processing.
- Completed.
- Failed.
- Deleted or expired.

The exact state machine must be established during implementation.

### 10.3 File integrity

File metadata should support content digests, detected format, size, ownership, and validation evidence.

File extension alone must not be accepted as proof of file type.

### 10.4 Access control

A valid media job identifier must not automatically grant access to its input or output artifacts.

The requesting tenant, project, user, or service identity must be authorized.

## 11. Sandbox Execution Data

The Sandbox Runner owns sandbox execution records.

The database should capture:

- Execution identifier.
- Tenant identifier.
- Project identifier.
- Workflow or task reference.
- Source artifact or revision digest.
- Runtime and toolchain versions.
- Execution policy reference.
- Resource limits.
- Start and end timestamps.
- Execution status.
- Exit status.
- Test result references.
- Security scan references.
- Output artifact references.
- Cleanup status.

### 11.1 Execution evidence

Execution logs and test reports should be associated with the relevant execution record.

Sensitive data must be excluded or appropriately redacted.

### 11.2 Isolation

Sandbox records must be tenant-scoped.

The database must not become a mechanism for one tenant to discover another tenant's source artifacts or execution evidence.

### 11.3 Retention

Execution records and artifacts must follow defined retention policies.

Temporary execution environments and temporary artifacts must be cleaned up according to documented lifecycle rules.

## 12. Billing and Financial Database Architecture

### 12.1 Financial authority

The `billing-ledger` service owns authoritative financial data.

No AI agent or unrelated service may directly modify financial balances or posted ledger entries.

### 12.2 Financial entities

The logical financial data model may include:

- Credit accounts.
- Account ownership.
- Currency definitions.
- Ledger accounts.
- Journal transactions.
- Journal entries.
- Credit reservations.
- Usage charges.
- Payment-provider events.
- Invoices.
- Receipts.
- Refunds.
- Reversals.
- Reconciliation records.

The final physical schema and table names must be approved during implementation design.

### 12.3 Double-entry accounting

Each posted financial transaction must satisfy double-entry accounting requirements.

For each transaction and currency:

- Total debits must equal total credits.
- Entries must belong to the same valid transaction.
- Accounts must be valid for the transaction.
- Currency must be consistent.
- Required transaction metadata must exist.
- Posting must occur through an authorized process.

### 12.4 Atomic posting

A financial transaction must be posted atomically.

The implementation must prevent partial posting in which only some entries are committed.

A failed transaction must not leave an apparently completed but unbalanced financial record.

### 12.5 Draft-to-posted transition

Financial transactions may have a controlled lifecycle such as:

`Draft → Validated → Posted`

Additional states may be required for cancellation, rejection, or reversal.

The exact state model must be defined during schema design.

A database constraint or trigger must not unintentionally block the legitimate transition from draft to posted.

The posting mechanism must validate the complete transaction at the appropriate transaction boundary.

### 12.6 Immutable posted entries

Once posted, financial entries must not be silently updated or deleted.

Corrections must use compensating entries, reversals, or other controlled accounting procedures.

Database permissions and application logic must both enforce this requirement.

### 12.7 Balance calculation

Financial balances must be derived or maintained through controlled accounting logic.

If cached or materialized balances are used, they must be reconcilable against the authoritative ledger.

No agent may write a balance directly.

### 12.8 Currency controls

Currency must be explicitly identified for each financial transaction and account.

The database must enforce valid currency references and prevent invalid mixing of currencies within a transaction.

Currency precision and rounding rules must be defined per supported currency.

Floating-point arithmetic must not be used for authoritative monetary values.

### 12.9 Credit reservations

Credit reservation records must support:

- Reservation identifier.
- Tenant and account reference.
- Requested amount.
- Currency or credit unit.
- Related task or workflow.
- Reservation status.
- Creation timestamp.
- Expiry where applicable.
- Settlement reference.
- Release or compensation reference.

Reservation and balance updates must be atomic.

### 12.10 Credit lifecycle

The baseline lifecycle is:

1. Estimate expected usage.
2. Validate account and policy.
3. Check available balance.
4. Reserve credits atomically.
5. Authorize the task.
6. Measure actual usage.
7. Calculate the final charge.
8. Settle the reservation.
9. Release unused credits or compensate.
10. Reconcile discrepancies.

The database must prevent duplicate settlement and unauthorized reuse of expired or consumed reservations.

### 12.11 Payment-provider events

Payment-provider events must be stored with sufficient information to support verification, deduplication, processing, and reconciliation.

Records should include:

- Provider identifier.
- Provider event identifier.
- Event type.
- Verification result.
- Received timestamp.
- Processing status.
- Related account or transaction reference.
- Relevant provider transaction reference.
- Processing outcome.
- Error or reconciliation status.

Sensitive payment information must not be stored unnecessarily.

### 12.12 Provider-scoped idempotency

Idempotency keys must be unique within the appropriate provider and operation scope.

The design must not assume that an event identifier from one provider is globally unique across all providers.

Duplicate webhook delivery must not create duplicate financial postings.

### 12.13 Reconciliation

The Billing Ledger must support reconciliation between internal records and payment-provider records.

Reconciliation must identify:

- Missing events.
- Duplicate events.
- Failed processing.
- Amount discrepancies.
- Currency discrepancies.
- Refund inconsistencies.
- Unmatched transactions.
- Unresolved settlement states.

### 12.14 Financial deletion restrictions

Financial history must not be destroyed through ordinary cascading deletion.

Account deactivation, retention, anonymization, and legally required deletion must be handled through controlled procedures.

## 13. Database Integrity Constraints

Database constraints must enforce important business invariants wherever practical.

Examples include:

- Primary keys.
- Foreign keys.
- Unique constraints.
- Not-null constraints.
- Check constraints.
- Tenant-aware composite foreign keys.
- Valid status transitions.
- Valid currency references.
- Positive or non-negative monetary values where appropriate.
- Balanced financial posting rules.
- Unique provider-scoped idempotency keys.
- Valid artifact ownership relationships.

Application-level validation remains necessary, but it must not be the only protection for critical data invariants.

### 13.1 Cascading deletes

Cascading deletes must be used cautiously.

They must not destroy:

- Posted financial history.
- Required audit records.
- Legal evidence.
- Security incident records.
- Records subject to retention obligations.

Where appropriate, use deactivation, archival, controlled anonymization, or restricted deletion workflows.

### 13.2 Timestamp handling

Timestamp fields should use an appropriate timezone-aware representation.

The platform should store timestamps consistently, normally in UTC, and convert them for user display.

Creation, modification, posting, and event timestamps must have clearly defined meanings.

### 13.3 Defaults

Database defaults must be used only where they accurately represent the business event.

For example, a `posted_at` timestamp must not be populated merely because a draft record was inserted.

It should represent the actual authorized posting event.

## 14. Audit and Security Event Data

### 14.1 Audit requirements

The platform must retain appropriate evidence for security-sensitive and business-critical operations.

Audit records may cover:

- Authentication-related application events.
- Tenant membership changes.
- Role and permission changes.
- Protected operations.
- Approval requests and decisions.
- Financial postings.
- Payment events.
- Administrative actions.
- Sensitive data access.
- Security policy violations.
- Data deletion and retention actions.

### 14.2 Audit record attributes

Audit records should capture relevant attributes such as:

- Event identifier.
- Timestamp.
- Actor or service identity.
- Tenant context where applicable.
- Project context where applicable.
- Operation.
- Target resource.
- Result.
- Correlation identifier.
- Relevant approval reference.
- Source or request context where appropriate.

### 14.3 Audit integrity

Audit records must be protected against unauthorized modification and deletion.

Controls may include restricted database roles, append-oriented write paths, protected archival, and tamper-evidence mechanisms.

An append-only application design alone must not be described as cryptographic immutability.

### 14.4 Sensitive information

Audit records must not contain raw passwords, authentication secrets, API keys, private signing keys, or unnecessary confidential content.

Prompts and source code should not be copied into audit records unless an explicitly approved and justified requirement exists.

### 14.5 Audit access

Audit access must be restricted to authorized roles.

Sensitive audit queries must be logged where appropriate.

## 15. Vector Database and Embedding Architecture

### 15.1 pgvector

PostgreSQL with pgvector is the approved preferred initial approach for vector storage and similarity search. A separate vector-database deployment is not proposed at this stage.

POC-05 must validate the selected PostgreSQL and pgvector versions, index types, supported dimensions, retrieval quality, tenant-filtering behaviour, performance, and operational characteristics before implementation relies on a specific configuration.

### 15.2 Embedding metadata

Each embedding record should carry sufficient metadata to identify:

- Tenant.
- Project or authorized data domain.
- Source artifact.
- Source record.
- Content version or digest.
- Embedding model identifier.
- Model version.
- Vector dimension.
- Creation timestamp.
- Access classification.
- Applicable ACL or authorization reference.
- Retention status.

### 15.3 Tenant isolation

Vector retrieval must enforce tenant and authorization filters.

Similarity alone must never grant access to a document, source file, project, or other tenant's content.

The retrieval process must validate authorization before returning the underlying content.

### 15.4 Model and dimension compatibility

Embedding vectors from incompatible models or dimensions must not be mixed in the same logical index without a defined compatibility strategy.

The architecture must record the model and dimension used to create each vector.

### 15.5 Index strategy

POC-05 must compare suitable exact and approximate search strategies and, where applicable, full-precision and half-precision representations.

It must evaluate:

- Search latency.
- Recall.
- Index size.
- Write performance.
- Update and deletion performance.
- Tenant filtering.
- Concurrency.
- Data volume.
- Re-embedding cost.

### 15.6 Dimension decision

A 3,072-dimensional embedding configuration is not a platform-wide requirement. Embedding dimensions must be selected according to the chosen model and use case, and recorded with model/provider and version metadata. Model- or dimension-incompatible vectors must not be mixed in a logical index without a validated compatibility strategy.

POC-05 must test 3,072-dimensional workloads where required by a selected model, including relevant full-precision and half-precision storage/index options. It must measure retrieval quality against exact-search baselines as well as latency, index size, memory, filtering behaviour, and operational cost. No precision or index configuration is approved solely by this architectural decision.

### 15.7 Re-embedding

When embedding models or source content change, the platform must define:

- Re-embedding triggers.
- Version coexistence.
- Migration strategy.
- Re-indexing.
- Validation.
- Retirement of old vectors.
- Failure recovery.

### 15.8 Deletion and access changes

Deleting or restricting a source record must trigger the corresponding vector lifecycle action.

A stale embedding must not remain accessible after its underlying content is no longer authorized.

## 16. File and Object Storage Metadata

### 16.1 Storage separation

PostgreSQL stores metadata and references for large objects.

Object storage or Git repositories hold appropriate binary files, generated artifacts, and source history.

### 16.2 Metadata requirements

File metadata should include:

- File identifier.
- Tenant identifier.
- Project identifier where applicable.
- Storage object key or reference.
- Original filename where appropriate.
- Detected content type.
- Size.
- Content digest.
- Upload status.
- Security-validation status.
- Version.
- Creation timestamp.
- Retention policy.
- Deletion status.

### 16.3 Upload lifecycle

New uploads must default to pending or quarantined.

They must not be treated as trusted merely because the upload completed.

The database must support the upload-validation and release lifecycle defined by the Multimodal Service.

### 16.4 Signed access

Object-storage access should use appropriately scoped and short-lived signed URLs where suitable.

A signed URL must not be treated as a substitute for correct tenant ownership and authorization.

### 16.5 Versioning

File version records must have a controlled sequence and unique version identity within the relevant ownership scope.

Concurrent uploads and version creation must not result in ambiguous or duplicate authoritative versions.

### 16.6 Deletion

Deletion must account for:

- Primary objects.
- Object versions.
- Replicas.
- Derived media.
- Cached copies.
- Embeddings.
- Search indexes.
- Backups.
- Legal holds.

The database must track the lifecycle sufficiently to prevent deleted or unauthorized content from being reintroduced into normal application access.

## 17. Database Migrations and Schema Evolution

### 17.1 Service ownership and independent migration histories

Each of the six deployable backend services owns its authoritative schema, migration scripts, migration metadata/version history, and migration lifecycle:

- `api-gateway`
- `agent-orchestrator`
- `multimodal-service`
- `sandbox-runner`
- `billing-ledger`
- `adtech-service`

Each service maintains an independent, ordered migration history with immutable migration identifiers and checksums. A service must not independently modify another service's authoritative schema. No global migration history or unrestricted central migration runner is adopted by this decision.

This is a logical ownership boundary, not a physical topology decision. A shared PostgreSQL cluster or database remains possible if restricted schemas, service-specific roles, tenant isolation, and controlled interfaces are enforced. Six physical databases are not required.

### 17.2 Migration review and compatibility

Migrations must be reviewed for:

- Data integrity and tenant isolation.
- Backward compatibility across supported application versions.
- Locking, bounded execution time, and downtime risk.
- Index creation impact and data volume.
- Transaction boundaries and concurrency.
- Rollback safety or forward-fix/recovery.
- Security and privilege consequences.
- Financial-history preservation and reconciliation.
- Affected services, API/event consumers, and deployment sequence.

Cross-service data exchange should use authorised APIs, events, or controlled read models rather than direct coupling to another service's authoritative tables.

### 17.3 Expand-and-contract approach

Where possible, breaking schema changes should follow an expand-and-contract approach:

1. Introduce backward-compatible schema changes.
2. Deploy application versions that support the old and new representations.
3. Migrate or backfill existing data in controlled, observable batches where appropriate.
4. Verify data integrity, application compatibility, and dependent consumers.
5. Remove obsolete structures only after dependent versions and consumers have been retired and the removal is separately authorised.

Use migration locks and bounded timeouts to prevent conflicting execution. Prefer transactional migrations where supported. Do not assume application-code rollback reverses a schema or data migration.

### 17.4 Destructive migrations and approval gates

Destructive migrations require impact analysis, explicit review, verified backup/recovery readiness, and authorization under HD-08 GATE-05. Production migration activity also requires applicable GATE-03 authorization. A migration design approval, code review, or PR merge is not execution authorization.

They must not be executed merely because a development tool or AI agent recommends them.

### 17.5 Migration credentials and privileges

Migration credentials must be separate from ordinary application credentials. Each service's migration identity must be restricted to its owned schema. Runtime application credentials must not have DDL/schema-changing privileges. Credentials must be protected and used only through separately approved deployment or maintenance procedures.

### 17.6 Migration evidence and recovery

Migration execution, when separately authorized, must record:

- Service and migration identifier/checksum.
- Target environment and database/schema.
- Source and target application/schema versions.
- Execution time, duration, and authorised actor/service.
- Approval references and execution result.
- Integrity/compatibility verification.
- Errors, lock/timeout events, and recovery or forward-fix action.

Plans must address backup/PITR readiness, restoration dependencies, data integrity, and safe forward recovery. No migration is authorised by this Phase 0 document.

## 18. Indexing and Query Performance

### 18.1 Index design

Indexes must be based on actual query patterns and measured performance.

Potential index categories include:

- Primary-key indexes.
- Foreign-key lookup indexes.
- Tenant-scoped indexes.
- Project-scoped indexes.
- Status and timestamp indexes.
- Unique idempotency indexes.
- Financial transaction indexes.
- Workflow lookup indexes.
- Vector indexes.

### 18.2 Tenant-aware indexing

Frequently used tenant-scoped queries should be designed with appropriate tenant-aware indexes.

Indexing must not replace RLS or authorization enforcement.

### 18.3 Query safety

Queries must use parameterized operations or safe ORM mechanisms.

Untrusted values must not be concatenated into executable SQL.

Dynamic identifiers and database commands require strict allowlisting and validation.

### 18.4 Query performance

Performance testing must include realistic:

- Tenant counts.
- Record volumes.
- Data distributions.
- Query concurrency.
- Transaction contention.
- Index sizes.
- Read/write patterns.

No untested query-latency guarantee is established by this document.

## 19. Transactions and Concurrency

### 19.1 Transaction boundaries

Transactions must be scoped to the business operation being performed.

Long-running external operations must not unnecessarily hold database transactions open.

### 19.2 Concurrency control

The implementation must use suitable concurrency controls, such as:

- Unique constraints.
- Row-level locking.
- Optimistic concurrency.
- Atomic updates.
- Serializable transactions where justified.
- Idempotency controls.

### 19.3 Financial concurrency

Credit reservation and settlement operations must protect against concurrent spending or duplicate settlement.

A balance check performed outside the authoritative transaction is insufficient.

### 19.4 Duplicate operations

Repeated requests, webhook delivery, worker retries, and network timeouts must not cause duplicate authoritative financial or business operations.

### 19.5 Deadlocks and retry

The implementation must define deadlock handling, bounded retry, transaction timeout, and safe recovery behaviour.

Retries must not repeat an external side effect without first establishing whether the earlier operation succeeded.

## 20. Background Workers and Database Security

### 20.1 Worker identity

Background workers must use identifiable service credentials and restricted database roles.

### 20.2 Tenant context

Workers must establish and validate tenant context for every tenant-owned operation.

They must not inherit untrusted tenant context from a previous pooled connection or unrelated job.

### 20.3 Job payloads

Job payloads must contain validated identifiers and required context.

A job payload's tenant identifier must be checked against the authorized record and service permissions before execution.

### 20.4 Privileged operations

Administrative and cross-tenant operations must use separately controlled identities and explicit authorization.

They must be auditable.

### 20.5 Database credential protection

Database credentials must be stored in an approved secrets-management system.

They must not be exposed to:

- Agent prompts.
- Generated code.
- Client-side applications.
- Logs.
- Public artifacts.
- Untrusted sandbox processes.

## 21. Cache and Derived Data

### 21.1 Cache distinction

Caches are performance mechanisms, not authoritative business databases.

Cached information must not override authoritative financial, membership, approval, or workflow state.

### 21.2 Redis

Redis may be used for:

- Ephemeral notifications.
- Caching.
- Rate-limiting support.
- Short-lived coordination data.
- Other explicitly approved temporary functions.

Redis Pub/Sub is not a durable event store.

### 21.3 Cache authorization

Tenant-specific cache keys and entries must be isolated.

Cache retrieval must not bypass authorization checks.

### 21.4 Invalidation

The implementation must define cache invalidation or expiration for:

- Membership changes.
- Permission changes.
- Project access changes.
- Artifact deletion.
- Financial status changes.
- Sensitive configuration changes.

### 21.5 Recovery

The loss of ephemeral cache data must not corrupt authoritative database records or permanently lose business-critical workflow state.

## 22. Backup and Disaster Recovery

### 22.1 Backup requirements

The final database hosting design must provide an approved backup strategy.

It should consider:

- Automated backups.
- Point-in-time recovery.
- Backup encryption.
- Backup access control.
- Retention.
- Backup integrity verification.
- Restoration testing.
- Regional recovery requirements.

### 22.2 Point-in-time recovery

Point-in-time recovery capabilities must be confirmed for the selected database provider and configuration.

The existence of a backup feature does not prove that a complete recovery process works.

### 22.3 Restoration testing

Restoration tests must verify:

- Database availability.
- Schema integrity.
- Referential integrity.
- Tenant isolation.
- Financial ledger consistency.
- Application compatibility.
- Required extensions.
- Recovery of related state.

### 22.4 Full-platform recovery

Database restoration alone does not constitute full-platform disaster recovery.

Recovery planning must include relevant dependencies, including:

- Temporal persistence and workflow recovery.
- Object storage.
- Git repositories.
- Financial records.
- Identity configuration.
- KMS.
- Secrets.
- Infrastructure configuration.
- Required external provider integrations.

### 22.5 Approved Tiered RPO and RTO Objectives — HD-06

The Project Owner approved the following tiered values as architectural recovery objectives on 2026-11-19:

| Workload / data class | RPO | RTO |
|---|---:|---:|
| Financial ledger, payment and credit records | ≤ 5 minutes | ≤ 1 hour |
| Core platform database and tenant/business records | ≤ 15 minutes | ≤ 2 hours |
| Durable agent and workflow state | ≤ 5 minutes | ≤ 1 hour |
| Core API and essential user access | Not applicable to service availability itself; persistent state follows its data-class RPO | ≤ 1 hour |
| Multimodal processing and sandbox workloads | ≤ 1 hour for recoverable workload state; original uploads and completed customer artifacts require separately classified protection | ≤ 4 hours |
| Analytics, reporting and non-critical derived data | ≤ 24 hours | ≤ 24 hours |

These are planning objectives only. They are not evidence of current capability, contractual service levels, or guaranteed recovery performance. POC-15 and operational validation must measure the actual recovery point and recovery time before any claim of achievement.

Validation must cover PostgreSQL and pgvector, financial records, Temporal workflow state, object storage, Git repositories and build artifacts, identity configuration, KMS and secrets, infrastructure configuration, and required external dependencies. Financial recovery must preserve ledger integrity and reconcile authoritative payment-provider records while preventing duplicate external side effects.

Backup and recovery controls must address encryption, access restrictions, retention, geographic separation, integrity verification, restoration testing, and immutability where appropriate. Before normal access resumes, restored data must be reconciled against valid deletion requests, anonymisation, legal holds, revoked credentials, access changes, and tenant deactivation.

POC-15 must record the test environment, scenarios, dependency ordering, measured data-loss window, measured restoration time, integrity and reconciliation results, limitations, and remediation actions. The objectives must be reviewed if evidence shows they cannot be achieved safely or economically.

This approval does not select a backup frequency, retention period, replication mechanism, database or storage configuration, or authorize infrastructure provisioning, subscriptions, production failover, a production recovery commitment, or Phase 1 implementation. Those remain subject to separate validation and authorization.

### 22.6 Restored data and deletion requests

A restored backup must not silently reintroduce records that were validly deleted or anonymized after the backup was created.

The recovery process must reconcile applicable deletion requests, retention requirements, and legal holds before restoring normal access.

## 23. Data Retention, Deletion and Privacy

### 23.1 Retention policy

Each data category must have an approved retention period or retention rule.

Retention must consider:

- Business necessity.
- Security.
- Financial obligations.
- Legal requirements.
- Privacy obligations.
- Contractual commitments.
- Operational requirements.

### 23.2 Deletion lifecycle

Deletion may involve:

1. Request validation.
2. Authorization.
3. Legal-hold check.
4. Retention assessment.
5. Access restriction.
6. Primary-data deletion or anonymization.
7. Derived-data cleanup.
8. Object-storage cleanup.
9. Search and vector-index cleanup.
10. Backup-retention handling.
11. Completion evidence.

### 23.3 Personal data

Personal data must be collected and retained only for justified purposes.

The implementation must define the applicable lawful basis, access policy, retention, and deletion procedure.

### 23.4 Cross-border processing

Cross-border data transfers and processing must undergo appropriate legal and privacy assessment.

Compliance with a data-protection framework must not be assumed merely because encryption or regional hosting is available.

### 23.5 Backups and replicas

Deletion from a primary database does not automatically delete every replica, backup, export, or external copy.

The retention and restoration design must account for these copies and ensure that restored data is reconciled against valid deletion requirements.

## 24. Data Classification

The platform should classify database information according to sensitivity and access requirements.

A proposed classification model is:

| Classification | Examples | Required protection |
|---|---|---|
| Public | Public product information and approved public documentation | Integrity and availability controls |
| Internal | Internal operational metadata | Authenticated access and appropriate logging |
| Confidential | Private project metadata, source references and business records | Strict authorization, tenant isolation and encryption |
| Restricted | Credentials, sensitive security information and protected financial data | Strong access restriction, encryption, monitoring and controlled handling |

The final classification policy must define handling, storage, sharing, logging, retention, and deletion requirements.

## 25. Database Testing and Acceptance

### 25.1 Schema testing

Verify:

- Table definitions.
- Data types.
- Constraints.
- Relationships.
- Indexes.
- Defaults.
- Migration behaviour.

### 25.2 Tenant-isolation testing

Verify RLS, tenant-aware foreign keys, connection pooling, worker context, and cross-tenant access rejection.

### 25.3 Financial testing

Verify:

- Double-entry balance.
- Atomic posting.
- Draft-to-posted transition.
- Immutable posted entries.
- Currency consistency.
- Credit reservation.
- Duplicate event rejection.
- Idempotent settlement.
- Reconciliation.

### 25.4 Migration testing

Test upgrades, compatibility, failure recovery, and destructive-change safeguards.

### 25.5 Backup and restoration testing

Verify restoration and reconciliation under documented failure scenarios.

### 25.6 Vector testing

Evaluate retrieval accuracy, tenant filtering, performance, index behaviour, and re-embedding.

### 25.7 Security testing

Test SQL injection resistance, role restrictions, RLS bypass scenarios, unauthorized database access, secret exposure, and privilege escalation.

### 25.8 Acceptance evidence

Acceptance requires documented test results, identified defects, remediation evidence, and authorized review.

A proposed schema or test plan is not evidence that the database has been implemented or tested.

## 26. Human Decisions Pending

The following decisions remain open.

| Decision ID | Decision | Required outcome |
|---|---|---|
| HD-DB-01 | PostgreSQL version | Select the supported version |
| HD-DB-02 | Hosting provider | Approve the managed or self-hosted database arrangement |
| HD-DB-03 | Physical database topology | Approve shared-cluster or separated-database deployment |
| HD-DB-04 | Service schema ownership | Confirm schemas, roles, and migration ownership |
| HD-DB-05 | pgvector configuration | Approve version, index strategy, dimensions, and performance criteria |
| HD-DB-06 | Embedding model | Approve model and versioning strategy |
| HD-DB-07 | Database regions | HD-03 approved architectural direction: AWS Cape Town (`af-south-1`) primary and Ireland (`eu-west-1`) DR, subject to validation |
| HD-DB-08 | Backup retention | Approve backup schedule and retention |
| HD-DB-09 | RPO and RTO | Approve tested recovery objectives |
| HD-DB-10 | Data retention | Approve data-category retention and deletion policies |
| HD-DB-11 | Financial schema | Approve final ledger, currency, reservation, and posting design |
| HD-DB-12 | Audit architecture | Approve audit retention and integrity controls |

## 27. Phase 0 Execution Boundary

This document belongs to Phase 0 architecture documentation.

Phase 0 activities are limited to:

- Database architecture review.
- Data ownership definition.
- Tenant-isolation requirements.
- Financial integrity requirements.
- Security and privacy requirements.
- Identification of technical risks.
- Identification of unresolved decisions.
- Cross-document consistency review.
- Preparation for human approval.

This document does not authorize:

- Creating databases.
- Creating tables.
- Writing or executing SQL.
- Creating or running Alembic migrations.
- Changing database configuration.
- Provisioning cloud database infrastructure.
- Modifying production data.
- Running destructive commands.
- Creating Git branches.
- Committing or pushing changes.
- Deploying application services.
- Beginning Phase 1.

All such activities require separate explicit authorization and applicable approval gates.

## 28. Related Architecture Documents

| Document ID | Document |
|---|---|
| WLX-ARCH-001 | ARCHITECTURE_OVERVIEW.md |
| WLX-ARCH-002 | SYSTEM_ARCHITECTURE.md |
| WLX-ARCH-003 | TECHNOLOGY_STACK.md |
| WLX-ARCH-004 | REPOSITORY_STRUCTURE.md |
| WLX-ARCH-005 | AGENT_ECOSYSTEM.md |
| WLX-ARCH-006 | SERVICE_BOUNDARIES.md |
| WLX-ARCH-008 | SECURITY_ARCHITECTURE.md |
| WLX-ARCH-009 | DEPLOYMENT_ARCHITECTURE.md |
| WLX-ARCH-010 | DEVELOPMENT_ROADMAP.md |
| WLX-ARCH-011 | RISK_REGISTER.md |
| WLX-ARCH-012 | ADR_REGISTER.md |
| WLX-ARCH-013 | PHASE_0_INSPECTION_REPORT.md |
| WLX-ARCH-014 | TESTING_STRATEGY.md |
| WLX-ARCH-015 | MONITORING_AND_OBSERVABILITY.md |
| WLX-ARCH-016 | COST_AND_SCALABILITY.md |

## 29. Final Status

The database architecture establishes the intended data ownership, tenant-isolation, integrity, security, and recovery requirements for the Worklexx AI Software Factory.

The architecture defines:

- PostgreSQL as the primary relational database.
- Six service-owned data domains.
- Tenant-aware data relationships.
- PostgreSQL RLS requirements.
- Restricted database roles.
- Transaction-scoped tenant context.
- Financial double-entry integrity.
- Controlled credit reservations and settlement.
- Provider-scoped payment idempotency.
- Protected audit history.
- pgvector as a candidate vector-storage extension.
- Object-storage metadata and quarantine requirements.
- Service-owned migration histories and controlled schema evolution.
- Backup, restoration, retention, and deletion requirements.

The following remain unresolved:

- PostgreSQL version and hosting.
- Physical database topology.
- Final physical database/schema topology and service deployment connectivity.
- pgvector version and configuration.
- Embedding model and dimension.
- Database regions.
- Backup and recovery configuration.
- Final RPO and RTO.
- Data retention and deletion policies.
- Financial schema approval.
- Audit architecture.

**Document status:** Revised Architecture Blueprint — Awaiting Final Human Review and Approval.

**Implementation status:** Not implemented or verified by this document.

**Security status:** Requirements defined; implementation and independent validation outstanding.

**Testing status:** Acceptance requirements defined; execution evidence outstanding.

**Phase 1 authorization:** Not granted.


## Customer Data Isolation, Privacy Boundaries and Data Governance — HD-REP-11

The Project Owner approved HD-REP-11 on 2026-11-20. Database and data-access design must support a privacy-by-design, tenant- and project-scoped architecture across all Factory services and customer projects.

### Data classification and authoritative scope

Classify records as Public, Internal, Confidential or Restricted according to sensitivity and applicable legal/contractual requirements. Every material data object and processing activity must have an authoritative tenant/project association where applicable, a documented purpose, permitted access, retention/deletion rule and audit context. Tenant identity must be established by trusted authentication and authorisation; a client-supplied tenant identifier is never sufficient authority.

### PostgreSQL, RLS and pgvector controls

Preserve HD-REP-06 service-owned schema and migration boundaries and HD-05's PostgreSQL/pgvector direction. Enforce tenant-aware service authorisation and database policies, including RLS where appropriate. Runtime roles remain least-privileged and distinct from migration identities. RLS is defence in depth, not a replacement for service-layer authorisation. Cross-tenant negative tests must cover joins, indirect object references, alternate query paths, background jobs, caches and administrative paths. Vector retrieval must enforce tenant/project scope before results are exposed to an agent or user; record model/index identity and handle deletion/revocation of embeddings and derived representations.

### Data lifecycle and derived information

The governed data inventory includes customer records, source code, files, prompts, images, audio, video, transcripts, embeddings, metadata, AI outputs, workflow state, logs and derived copies. Access, retention, export and deletion controls must consider associated object storage, Git/LFS, search indexes, vectors, caches, temporary files, queues/jobs, replicas and backups. Apply record-class retention and legal holds; no universal duration is approved. Align deletion and restoration with HD-REP-07 and HD-REP-10 so deleted or restricted information is not silently reintroduced from backups.

### External processing and regional data flows

Do not grant external AI providers or subprocessors unrestricted database or repository access. Before data is transmitted, document purpose, categories, location, retention, human access, onward disclosure, training-use restrictions, deletion and contractual safeguards. Customer data must not be used to train/improve general-purpose external models absent a specific lawful and authorised arrangement. HD-03's Cape Town/Ireland and Temporal Ireland choices do not themselves establish legal authority for international transfers; jurisdictional, localisation and transfer assessments are prerequisites to live processing.

### Privacy, security and validation

Apply encryption in transit/at rest to confidential and restricted data, separate keys/secrets from application data, and govern key access, rotation, revocation and recovery. Support applicable data-subject access, correction, export, erasure, restriction, objection and consent-withdrawal workflows. Align audit redaction and privacy incident evidence with HD-REP-09. Require POC-REP-11-01 through POC-REP-11-15, including classification, tenant/RLS isolation, vector filtering/deletion, agent permissions, multimodal handling, provider controls, key management, cross-border assessment, rights/export, deletion/backup, log redaction and end-to-end privacy/security testing. Add RSK-31; formal risk scores remain pending.

**Governance boundary:** HD-07 and HD-08 apply. This is an architectural decision only; it does not authorise live data processing, customer/provider connections, schema or database changes, credential/key creation, infrastructure, spending, migrations, deletion/restoration, production deployment or Phase 1. Unexecuted validation is not passed.


## Customer Identity and Access-Control Data Governance — HD-REP-12

The Project Owner approved HD-REP-12 on 2026-11-20. Database and data-access architecture must support distinct identities for users, organisations, memberships, projects, agents, services, workloads and external integrations. Identity-provider authentication records and Worklexx application authorisation records have distinct responsibilities; authentication does not itself confer resource access.

Worklexx application records must support stable identity mapping, organisation and project membership, role/permission assignments, ownership references, delegated authority, identity status, expiry/revocation and auditable lifecycle transitions. A user may belong to multiple organisations with different permissions. Organisation administration must not silently confer project ownership; HD-REP-10 governs project ownership and transfer.

Authorisation context must be derived from trusted server-side identity and membership records. Client-supplied tenant, organisation or project identifiers are selectors at most, never proof of authority. Enforce tenant/project/resource scope at service boundaries and database access paths. PostgreSQL RLS may provide defence in depth but does not replace service-layer authorisation. Preserve HD-REP-06 service-owned schema/migration boundaries: each backend service owns its authoritative schema and migration history; no service may modify another service's schema.

Identity and access data may include user-to-organisation memberships, project memberships, role bindings, permission grants, invitations, delegated agent tasks, service/workload identity references, API-key/token metadata (never secret values), session/revocation references, access-review decisions and audit correlation identifiers. Store only attributes necessary for documented purposes. Authentication secrets, raw tokens, private keys and recovery secrets must not be stored in ordinary application records or logs; use approved identity and secret-management mechanisms subject to separate authorisation.

Access revocation and membership/role changes must invalidate or refresh relevant authorisation decisions across services, RLS contexts, pgvector filters, storage, repositories, workflows, agent contexts, caches and integrations. Do not rely solely on stale cached permissions. Define propagation objectives and failure behaviour through POC-REP-12; sensitive operations must fail closed when current authority cannot be established.

Identity records are personal or organisational data and must follow HD-REP-11 classification, minimisation, purpose limitation, access, correction, export, erasure, retention and legal-hold controls. Identity lifecycle and access decisions must generate protected, attributable audit events under HD-REP-09. No universal retention duration or revocation latency is approved by this decision.

**Validation and boundaries:** Require POC-REP-12-01 through POC-REP-12-20, including identity mapping, membership and tenant isolation, RLS/service-layer enforcement, role/attribute policies, concurrency, revocation propagation, service identities, agent delegation, privacy, audit and recovery. These are requirements, not evidence of completed tests. HD-REP-12 authorises documentation only; no schema creation/modification, migration, credential, permission, identity-provider integration, live data processing, production rollout or Phase 1 is authorised. Applicable HD-08 gates remain mandatory.


## HD-REP-13 — AI Agent Security, Delegation, Execution Boundaries and Human Oversight Governance (Approved 2026-11-20)

Adopt permission-controlled, policy-enforced, sandboxed and auditable agent execution for the 23 logical agent modules. This decision does not add a backend deployable or alter the approved six-deployable architecture. Agent intelligence is not authority: each agent has a distinct identity and bounded task, tenant/project, tool, data and time scope; versioned policies; resource limits; audit attribution; and revocation controls.

Five conceptual permission tiers: Tier 0 Observe; Tier 1 Prepare; Tier 2 Execute within controlled scope; Tier 3 Consequential action subject to independent approval and applicable control; Tier 4 prohibited authority (including self-approval and governance bypass). Tool permissions remain granular: inspect, write, PR creation, review, approval, merge, permission changes, deletion and transfer are separate capabilities. The tool-control boundary validates identity/scope, inputs and destinations, classification, policy and approval, then executes, verifies and audits.

Code execution uses an appropriately isolated sandbox within the approved sandbox-runner boundary: restricted networking, resource/time limits, filesystem/process isolation, credential separation, tenant/project-specific caches and artifact handling, and cleanup. Untrusted documents, source, web content, prompts and tool results are data—not policy or authority—and prompt injection must not override permissions, governance or gates. Delegation is task/time bounded, depth-limited, attributable, revocable and cannot expand the initiating authority.

Agent context and memory are scoped, classified, minimised, governed and tenant/project isolated. Outputs require independent verification appropriate to their risk; verification does not substitute for human approvals required by HD-08. Control retries, loops, concurrency, idempotency, resource/cost limits, cancellation and safe failure. Protected audit and monitoring align with HD-REP-09; privacy and data boundaries with HD-REP-11; identity and delegation with HD-REP-12; execution isolation and supply-chain controls with HD-REP-08; customer lifecycle with HD-REP-10.

Validation requirements: POC-REP-13-01 through POC-REP-13-24 (unexecuted) cover agent identity/scope, least privilege, tool authorization, policy enforcement, tier separation, gate binding, sandbox isolation, network/credential restrictions, resource limits, prompt-injection resistance, untrusted content, tenant/project isolation, delegation depth/authority, context/memory privacy, output verification, human oversight, audit attribution, revocation, concurrent actions/races, loops/retries/cancellation, failure/recovery, cost controls, abuse scenarios and end-to-end governance bypass attempts.

Add RSK-33 — AI Agent Misuse, Unsafe Execution, Privilege Escalation and Governance Bypass. Formal likelihood, impact, inherent and residual scores remain pending assessment; proposed controls do not reduce residual risk until implemented and evidenced.

Project Owner remains sole initial risk acceptance and approval authority under HD-07/HD-08. Applicable gates remain mandatory. This is architecture/documentation approval only: no agent execution in production, sandbox provisioning, external integrations, live customer data, credentials, CI/CD activation, GitHub configuration, database changes, paid services, production deployment or Phase 1 is authorised.


### Agent governance testing
Track POC-REP-13-01 through POC-REP-13-24 individually with test owner, scope, environment, preconditions, expected result, evidence, outcome, issue references and retest. Include tier-boundary, cross-tenant, injection, sandbox, delegation, revocation, human gate, cost/loop, audit and failure/recovery tests. These POCs remain unexecuted.


## HD-REP-14 — API and Event Data Contracts: Database Architecture Implications (Approved 2026-11-20)

Service-owned API, event and workflow contracts must not undermine HD-REP-06 authoritative schema ownership. A contract describing a data structure does not grant a consumer direct database access or permission to modify another service's schema. Cross-service data exchange must use authorised service interfaces, events or explicitly governed read models; no shared-table coupling or cross-service DDL is implied. Contract payloads must identify authoritative producer/owner and define identifiers, invariants, classification, version and compatibility expectations.

Tenant/project context must be derived from trusted server-side identity and authorization under HD-REP-11/12; payload-supplied tenant/project identifiers are not authority. Apply minimisation to event and API payloads, avoid secrets and unnecessary personal/customer data, and align retention, deletion, legal holds and audit with HD-REP-09/11. Event replay, duplicate delivery and delayed messages must not resurrect deleted data, bypass revocation or duplicate financial effects. Billing-ledger contracts require idempotency, immutable financial history, double-entry invariants and reconciliation. Contract changes do not authorise schema creation/modification, migration, data processing, credentials or production rollout. Require POC-REP-14-01 through -24; all remain unexecuted.


## HD-REP-15 — API Gateway and Database Architecture Implications (Approved 2026-11-20)

The gateway is an ingress and policy-enforcement boundary, not a database access layer. It must not connect directly to PostgreSQL, pgvector or service-owned schemas, and must not expose database administration or migration interfaces. Requests route to authorised service interfaces; each service remains responsible for resource authorization, tenant/project isolation and access to its own authoritative schema under HD-REP-06 and HD-REP-11/12.

Tenant/project context must be derived from trusted server-side identity and authorization, not accepted as authority from client payloads. Gateway request validation and rate limits complement, but do not replace, database constraints, service-layer checks or RLS. Gateway logs and telemetry must not duplicate sensitive payloads, credentials or secrets; align minimisation, redaction, retention and deletion with HD-REP-09/11. Retries and replay must preserve idempotency and must not duplicate billing-ledger effects, bypass revocation or resurrect deleted data. No schema, database, role, credential or migration change is implied. Require POC-REP-15-01 through -24; all remain unexecuted.


## HD-REP-16 — Database and Data-Protection Implications (Approved 2026-11-20)

Database services must not store plaintext credentials, private signing keys or unrestricted secret material in application tables. Where database-held credential metadata is necessary, store only appropriately protected values or references to an approved secrets/key-management boundary, with purpose, owner, scope, version, lifecycle state and audit metadata as appropriate. Database credentials must be unique and least-privileged; runtime service identities must not receive unnecessary DDL or key-administration permissions.

Protect PostgreSQL, pgvector, object/multimodal storage, backups, exports and replicas with encryption in transit and at rest under controlled key lifecycle. Key separation and availability must be considered in backup restoration and disaster recovery; a recoverable database backup is not sufficient if its required decryption keys are unavailable. Key compromise/revocation must be coordinated with restore and recovery procedures and must not silently resurrect revoked credentials or deleted data.

Tenant/project authorization remains service-enforced and RLS remains a supplementary control. Secret/key metadata, access events and cryptographic failures must align with HD-REP-09 audit and HD-REP-11 data minimisation/redaction; do not log secret values, tokens, private keys or sensitive payloads. Webhook/event replay and retries must preserve idempotency, credential revocation, deletion and billing-ledger integrity. The gateway must not connect directly to PostgreSQL/pgvector or service-owned schemas.

Require POC-REP-16-01 through -26; all remain unexecuted. No schema, database, role, credential, key, migration or production configuration change is authorised by this decision.
