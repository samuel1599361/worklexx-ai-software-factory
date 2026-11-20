# WORKLEXX AI SOFTWARE FACTORY
# TESTING STRATEGY

**Document ID:** WLX-ARCH-014  
**Document Name:** TESTING_STRATEGY.md  
**Document Classification:** Phase 0 Architecture Document  
**Status:** Proposed — Pending Project Owner Review and Approval  
**Phase:** Phase 0 — Architecture and Governance  
**Repository:** `samuel1599361/worklexx-ai-software-factory`  
**Document Version:** 1.0.0  
**Date:** 19 November 2026  
**Document Owner:** Worklexx AI Software Factory Project Owner  

## Repository and Source-Control Reference

**Authoritative GitHub Repository:**  
https://github.com/samuel1599361/worklexx-ai-software-factory

**Primary Branch:** `main`

**Documentation Location:** `docs/phase-0/`

**Document:** `TESTING_STRATEGY.md`

**Document ID:** `WLX-ARCH-014`

The GitHub repository is the authoritative source for project source code, version-controlled documentation, testing configuration, and implementation evidence.

All testing strategy changes, test definitions, test reports, quality gates, and associated evidence must be maintained through the project's approved GitHub workflows.

The presence of this repository reference does not imply that automated testing, CI/CD pipelines, branch protections, or other testing infrastructure have already been implemented or approved.
---

## 1. Purpose

This document establishes the proposed testing strategy, testing architecture, quality assurance principles, validation requirements, test governance, and acceptance criteria for the Worklexx AI Software Factory.

The testing strategy is designed to validate the reliability, security, correctness, usability, scalability, operational readiness and governance of the platform.

It covers the six deployable backend services, five frontend applications, the 23-agent ecosystem, supporting infrastructure, third-party integrations, generated software, and the platform's operational workflows.

This document defines a proposed testing framework. It does not establish that any test suite, testing infrastructure, testing automation or testing control has already been implemented.

## 2. Scope

The testing strategy applies to:

1. The five frontend applications.
2. The six deployable backend services.
3. The 23-agent ecosystem.
4. Agent orchestration and workflow execution.
5. AI model routing and provider integrations.
6. Multimodal processing.
7. Generated applications, code and artifacts.
8. Authentication, authorisation and identity management.
9. Tenant isolation and data security.
10. Database architecture and persistence.
11. Billing, payments, credits and financial operations.
12. Advertising and monetisation boundaries.
13. Sandbox execution environments.
14. API integrations and external services.
15. CI/CD pipelines and release processes.
16. Monitoring, observability and incident workflows.
17. Infrastructure, backup and disaster recovery.
18. Accessibility, performance and scalability.
19. Data privacy, compliance-related controls and auditability.

Testing applies across development, local testing, CI, controlled staging, release qualification and production monitoring.

Production testing must not introduce unapproved destructive operations, uncontrolled financial transactions, exposure of private data or unauthorised changes to production infrastructure.

## 3. Testing Principles

### 3.1 Testing is evidence-based

Testing results must be supported by reproducible test executions, documented procedures, identifiable test environments and traceable results.

A proposed control must not be represented as implemented merely because it is documented.

### 3.2 Testing must be risk-based

Testing effort must be prioritised according to the severity, likelihood and impact of failure.

Critical areas include:

- Financial transactions.
- Tenant isolation.
- Authentication and authorisation.
- AI agent permissions.
- Sandbox isolation.
- Data integrity.
- Protected GitHub operations.
- Production deployment controls.
- Privacy and security.
- Disaster recovery.

### 3.3 Deterministic controls must be tested deterministically

Financial calculations, permissions, approval gates, tenant access, API validation, transaction integrity and other deterministic controls must be tested using deterministic software tests wherever practicable.

AI model reasoning must not be relied upon as the sole mechanism for enforcing security, permissions, financial correctness or governance.

### 3.4 AI systems require additional evaluation

AI agents and AI-generated applications require evaluation beyond traditional software testing.

Testing must consider:

- Model variability.
- Prompt injection.
- Tool misuse.
- Hallucinated outputs.
- Incorrect code generation.
- Unsafe actions.
- Model/provider changes.
- Multimodal input variations.
- Cost and latency variability.

### 3.5 Testing must not bypass governance

Test execution must not bypass:

- GATE-01 — Product requirements, scope and architecture approval.
- GATE-02 — Financial or credit expenditure approval.
- GATE-03 — Production deployment approval.
- GATE-04 — Protected GitHub operations approval.
- GATE-05 — Destructive database operations approval.
- GATE-06 — Consequential external integrations and live account actions.

Testing activities must operate within the applicable permissions and approval boundaries.

### 3.6 Test environments must be appropriately isolated

Testing must use environments, identities, credentials, data and resources appropriate to the risk and scope of the test.

Production credentials and confidential production data must not be unnecessarily exposed to development, test or sandbox environments.

### 3.7 Testing must support continuous improvement

Test failures, defects, security incidents, production incidents, AI evaluation failures and release findings must contribute to continuous improvement of the platform.

## 4. Testing Architecture

The testing architecture should integrate automated and manual testing throughout the software development lifecycle.

### 4.1 Testing layers

The proposed testing layers are:

1. Static analysis and code quality checks.
2. Unit testing.
3. Component testing.
4. Integration testing.
5. API contract testing.
6. Database and persistence testing.
7. Agent evaluation.
8. Workflow testing.
9. End-to-end testing.
10. Security testing.
11. Performance and load testing.
12. Accessibility testing.
13. Multimodal testing.
14. Financial integrity testing.
15. Sandbox isolation testing.
16. Disaster recovery testing.
17. Release acceptance testing.
18. Production verification and monitoring.

### 4.2 Testing pyramid

Testing should prioritise fast, deterministic tests at the lower levels while maintaining appropriate coverage of integrated and end-to-end behaviour.

- Unit tests should validate individual functions, components and deterministic business rules.
- Integration tests should validate interactions between components and services.
- Contract tests should validate service and external API expectations.
- End-to-end tests should validate critical user journeys.
- AI evaluations should validate model and agent behaviour against defined evaluation datasets and criteria.
- Security, resilience and operational tests should validate the platform's protection and recovery capabilities.

The testing pyramid must not be used to justify neglecting high-risk system-level testing.

### 4.3 Testing environments

The proposed testing environments are:

**Local development environment**

Used for individual developer testing, local component execution, debugging and isolated development.

**Automated CI environment**

Used for automated validation of code changes, pull requests, build processes, test execution and quality checks.

**Controlled staging environment**

Used for integration testing, system testing, release qualification, security validation, operational checks and human acceptance.

**Production environment**

Used for controlled production verification, monitoring, observability and approved operational testing.

Production testing must be non-destructive and appropriately authorised.

Environment configuration, secrets, permissions, data and infrastructure must be separated according to the security architecture.

## 5. Test Governance and Lifecycle

### 5.1 Test planning

Each significant feature, service, agent, workflow or release should have a documented testing plan proportionate to its risk.

Test plans should identify:

- Scope.
- Requirements.
- Test objectives.
- Test cases.
- Test data.
- Test environment.
- Dependencies.
- Expected results.
- Acceptance criteria.
- Risks.
- Responsible reviewers.
- Required approvals.

### 5.2 Test execution

Test execution should produce traceable evidence.

Each test result should record, where applicable:

- Test identifier.
- Test name.
- Test version.
- Date and time.
- Test environment.
- Application or service version.
- Test inputs.
- Expected result.
- Actual result.
- Pass, fail or blocked status.
- Defect reference.
- Execution evidence.
- Reviewer or responsible identity.

### 5.3 Defect management

Defects should be categorised according to severity, priority, security impact and release implications.

Proposed defect severity categories:

**Critical**

A defect that creates a severe security, financial, data-integrity, tenant-isolation or system-wide operational risk.

**High**

A defect that significantly compromises a critical feature, security control, workflow or service.

**Medium**

A defect that affects functionality, usability, reliability or performance but does not constitute a critical failure.

**Low**

A defect with limited operational or functional impact.

Critical and high-severity defects affecting security, financial integrity, tenant isolation or release safety must be resolved or formally risk-assessed before the affected release is authorised.

### 5.4 Regression testing

Regression testing must validate that changes do not unintentionally compromise existing functionality, integrations, security controls, workflows or data integrity.

Regression test coverage should prioritise:

- Authentication.
- Tenant isolation.
- Agent permissions.
- Financial transactions.
- Payment processing.
- Database integrity.
- Sandbox security.
- GitHub operations.
- Deployment governance.
- Multimodal processing.
- Core user journeys.

### 5.5 Test evidence retention

Test evidence must be retained according to the proposed records-management, security, privacy and retention policies.

Evidence must be protected against unauthorised modification and access.

Test evidence must not unnecessarily contain confidential source code, private user prompts, credentials, tokens, sensitive documents or personal data.

## 6. Static Analysis and Code Quality Testing

Static analysis and code quality checks should be integrated into automated development and CI workflows.

Proposed checks include:

- Syntax validation.
- Type checking.
- Linting.
- Formatting validation.
- Dependency analysis.
- Software composition analysis.
- Secret detection.
- Static application security testing.
- Infrastructure configuration analysis.
- Container image analysis.
- License compliance checks where applicable.
- Database migration review.
- API schema validation.
- Code quality and maintainability analysis.

Static analysis results must be interpreted according to the tool's limitations.

Passing static analysis does not establish that a system is secure or correct.

## 7. Unit Testing

Unit tests must validate individual functions, modules, components and deterministic business rules.

### 7.1 Backend unit testing

Backend unit tests should cover:

- Input validation.
- Business logic.
- Permissions.
- Policy enforcement.
- Error handling.
- Idempotency.
- Retry logic.
- Data transformation.
- Financial calculations.
- Workflow state transitions.
- API response generation.
- Configuration handling.
- Boundary conditions.

### 7.2 Frontend unit testing

Frontend unit tests should cover:

- UI components.
- Input validation.
- Navigation.
- State management.
- Error handling.
- Accessibility-related component behaviour.
- Permission-dependent rendering.
- Loading and empty states.
- Form submission.
- Responsive interface behaviour where applicable.

### 7.3 Unit testing acceptance criteria

Unit tests should:

- Execute reproducibly.
- Validate expected and unexpected conditions.
- Include meaningful assertions.
- Avoid reliance on live external services.
- Avoid unnecessary dependence on execution order.
- Provide traceable test results.

## 8. Integration Testing

Integration tests must validate interactions between services, components, databases, queues, workflow systems and external integrations.

Integration testing should cover:

- API Gateway and backend services.
- Agent Orchestrator and agent modules.
- Agent Orchestrator and Temporal.
- Multimodal Service and AI providers.
- Sandbox Runner and execution infrastructure.
- Billing Ledger and payment providers.
- AdTech Service and approved advertising integrations.
- PostgreSQL and application services.
- Redis and approved caching or coordination workflows.
- Object storage and application services.
- Background workers and durable workflows.
- Frontend applications and backend APIs.

Integration tests should validate:

- Authentication.
- Authorisation.
- Request and response contracts.
- Error handling.
- Retry behaviour.
- Timeout behaviour.
- Idempotency.
- Transaction boundaries.
- Data integrity.
- Tenant isolation.
- Service availability.
- Dependency failure handling.

External services should be tested using controlled test accounts, mock services, simulators or sandbox environments where available.

## 9. API Contract Testing

API contract testing must validate the expected behaviour, schemas and compatibility of API interfaces.

Testing should cover:

- API request schemas.
- API response schemas.
- Authentication requirements.
- Authorisation requirements.
- Input validation.
- Error responses.
- Rate limits.
- Version compatibility.
- Tenant context.
- Idempotency.
- Pagination.
- API documentation consistency.
- External integration contracts.

API contract changes must be reviewed for compatibility with dependent services and clients.

Breaking changes should follow a controlled versioning and migration strategy.

## 10. Database and Persistence Testing

Database testing must validate the correctness, integrity, security and performance of the platform's persistence architecture.

### 10.1 Database integrity

Testing should cover:

- Primary keys.
- Foreign keys.
- Unique constraints.
- Check constraints.
- Transaction boundaries.
- Referential integrity.
- Concurrent transactions.
- Data consistency.
- Migration correctness.
- Rollback procedures where supported.
- Partitioning behaviour.
- Index performance.
- Data lifecycle and retention.

### 10.2 Tenant isolation

Tenant-isolation tests must validate that tenant-owned records, files, workflows, projects, artifacts and services cannot be accessed or modified by unauthorised tenants.

Testing should cover:

- Row-Level Security.
- Application-level tenant context.
- Database connection context.
- Cross-tenant queries.
- Cross-tenant references.
- API access.
- Object storage access.
- Git repositories.
- Sandbox environments.
- Agent access.
- Workflow access.
- Background worker execution.
- Tenant-specific configurations.

Tenant-isolation testing must include both positive and negative tests.

A passing tenant-isolation test suite does not establish complete isolation unless the scope, test coverage, configuration and evidence are reviewed.

### 10.3 Migration testing

Database migrations should be tested in controlled environments before approval.

Migration testing should cover:

- Schema changes.
- Data transformations.
- Migration ordering.
- Migration failures.
- Compatibility with application versions.
- Rollback or recovery procedures.
- Expand-and-contract migrations.
- Data integrity.
- Migration execution permissions and service-owned schema boundaries.
- Independent migration-history integrity, immutable identifiers and checksum verification.
- Least-privilege migration identities and absence of DDL privileges in runtime credentials.
- Attempts to modify another service's schema must be denied.
- Concurrent migration attempts, migration locks, bounded timeouts and interrupted execution.
- Fresh installation and upgrade from every supported prior schema version.
- Rolling-deployment compatibility while old and new application versions coexist.
- Transactional behavior where supported and forward-fix recovery where rollback is unsafe.
- Backup/PITR readiness, restoration, and post-recovery integrity checks.
- Tenant RLS policy preservation and adversarial cross-tenant tests before, during, and after migration.
- `billing-ledger` double-entry integrity, immutable history, idempotency, and reconciliation after migration.
- Migration audit evidence, including approval references, actor, target, versions, checksum, result and recovery actions.

Destructive database operations must require GATE-05. Production migration activity also requires applicable GATE-03 authorization. Test execution does not authorize production migration execution.

## 11. Financial Integrity and Payment Testing

Financial integrity is a critical testing domain.

The Billing Ledger and deterministic financial software must be tested independently of AI agent reasoning.

### 11.1 Financial transaction testing

Testing must validate:

- Double-entry accounting.
- Debit and credit balancing.
- Currency-specific balances.
- Atomic journal posting.
- Immutable posted entries.
- Transaction consistency.
- Concurrent transactions.
- Idempotency.
- Duplicate transaction prevention.
- Reversals.
- Refunds.
- Reconciliation.
- Transaction auditability.

### 11.2 Payment integration testing

Payment integrations must be tested using approved provider test environments.

Testing should cover:

- Payment initiation.
- Payment success.
- Payment failure.
- Pending payments.
- Timeouts.
- Duplicate callbacks.
- Webhook signature verification.
- Invalid signatures.
- Replay attempts.
- Provider status verification.
- Refunds.
- Reconciliation.
- Payment disputes where supported.
- Provider API failures.
- Network interruptions.
- Payment credential handling.

### 11.3 Webhook testing

Webhook testing must validate:

- Provider-specific signature verification.
- Correct handling of valid events.
- Rejection of invalid signatures.
- Duplicate event handling.
- Idempotent processing.
- Replay protection.
- Event ordering where applicable.
- Retry handling.
- Failure recovery.
- Audit records.

Stripe and Paystack must use their respective provider-specific verification procedures.

### 11.4 Credits, billing and invoices

Testing should cover:

- Credit allocation.
- Credit consumption.
- Credit limits.
- Usage metering.
- Billing calculations.
- Subscription transitions.
- Billing failures.
- Refunds.
- Invoice generation.
- Receipt generation.
- Financial reconciliation.
- Credit expiry where applicable.
- Concurrent credit consumption.

Invoice generation must not be treated as evidence of payment.

### 11.5 Financial acceptance criteria

Financial acceptance requires evidence that:

- Journal entries balance per currency.
- Duplicate payment events do not create duplicate financial postings.
- Invalid webhooks are rejected.
- Posted financial records cannot be improperly modified.
- Refunds and reversals are represented through approved compensating entries.
- Reconciliation discrepancies are detectable.
- Concurrent transactions preserve financial integrity.

## 12. Authentication, Authorisation and Session Testing

Authentication and session controls must be tested across the frontend applications, APIs, services, agents and workers.

Testing should cover:

- Login.
- Logout.
- MFA.
- Account recovery.
- Session expiration.
- Session revocation.
- Refresh-token rotation.
- Refresh-token reuse detection.
- OIDC/OAuth2 flows.
- PKCE.
- Redirect URI validation.
- Issuer validation.
- Audience validation.
- CSRF.
- CORS.
- Cookie security.
- Privilege escalation.
- Role-based access control.
- Permission-based access control.
- Service identities.
- API credential management.
- Identity-provider failures.

Testing must validate that users, agents, workers and services cannot perform actions beyond their authorised permissions.

## 13. AI Agent Testing and Evaluation

The 23-agent ecosystem must be tested through a combination of deterministic tests, behavioural evaluations, policy tests, workflow tests and controlled adversarial testing.

### 13.1 Agent execution contract

Each agent should be evaluated against its defined execution contract, including:

- Agent identity.
- Agent version.
- Instructions.
- Configuration.
- Input schema.
- Output schema.
- Tool permissions.
- Project access.
- Tenant restrictions.
- Model configuration.
- Execution budget.
- Timeout.
- Retry behaviour.
- Cancellation.
- Idempotency.
- Error handling.
- Audit events.
- Approval requirements.

### 13.2 Agent evaluation datasets

Each agent should have a versioned evaluation dataset appropriate to its function.

Evaluation datasets should contain:

- Representative inputs.
- Expected outcomes.
- Expected structured outputs where applicable.
- Invalid inputs.
- Edge cases.
- Adversarial inputs.
- Permission-boundary tests.
- Failure scenarios.
- Regression cases.

Evaluation datasets must not unnecessarily contain private production data.

### 13.3 Agent evaluation metrics

Agent evaluation should use metrics appropriate to the agent's role.

Potential metrics include:

- Task completion rate.
- Output validity.
- Schema compliance.
- Tool-call correctness.
- Permission compliance.
- Error rate.
- Retry rate.
- Latency.
- Cost per task.
- Human correction rate.
- Workflow completion rate.
- Evaluation reproducibility.

No single metric should be treated as a universal measure of agent quality.

### 13.4 Agent permission testing

Testing must validate that agents:

- Use only authorised tools.
- Access only authorised resources.
- Respect tenant boundaries.
- Respect project boundaries.
- Respect execution budgets.
- Respect approval gates.
- Cannot independently authorise prohibited actions.
- Cannot bypass deterministic security controls.
- Cannot bypass protected GitHub operations.
- Cannot independently authorise production deployment.
- Cannot independently authorise destructive database operations.
- Cannot independently authorise consequential live integrations.

### 13.5 Prompt injection and untrusted inputs

Testing must evaluate the system's resistance to prompt injection and malicious content in:

- User prompts.
- Uploaded files.
- Source code.
- Documentation.
- External websites.
- API responses.
- Multimodal inputs.
- Generated outputs.
- Repository content.

Testing must validate that untrusted content cannot override trusted platform instructions, deterministic permissions or human approval requirements.

### 13.6 AI model and provider regression testing

Model or provider changes must be evaluated against appropriate regression datasets before being approved for critical workflows.

Testing should consider:

- Output quality.
- Reliability.
- Safety.
- Latency.
- Cost.
- Tool-use behaviour.
- Structured output compliance.
- Multimodal capability.
- Provider availability.
- Privacy and contractual requirements.

Model evaluation results must not be assumed to remain valid after significant model, prompt, configuration or workflow changes.

## 14. Generated Application Testing

The Worklexx AI Software Factory must evaluate the quality and reliability of applications generated through its agentic development workflows.

### 14.1 Generated application validation

Generated applications should be tested for:

- Syntax correctness.
- Build success.
- Dependency compatibility.
- Type correctness where applicable.
- Linting.
- Unit tests.
- Integration tests.
- API contract compliance.
- UI functionality.
- Responsive behaviour.
- Accessibility.
- Security.
- Data persistence.
- Error handling.
- Configuration.
- Deployment readiness.

### 14.2 Generated application acceptance

Generated applications should not be automatically declared production-ready merely because they compile or build successfully.

Production readiness requires appropriate validation of:

- Functional requirements.
- Security.
- Data integrity.
- Permissions.
- Performance.
- Accessibility.
- Deployment configuration.
- Secrets management.
- Operational readiness.
- Human acceptance where required.

### 14.3 Generated application failure handling

The system should test and document its behaviour when generated applications:

- Fail to compile.
- Fail to build.
- Fail automated tests.
- Have dependency conflicts.
- Contain vulnerabilities.
- Fail deployment.
- Have missing configurations.
- Have incomplete requirements.
- Produce invalid artifacts.

The system must not promise universal successful compilation or deployment of AI-generated applications.

## 15. Sandbox and Hostile-Code Testing

Sandbox testing is a critical security domain because the platform may execute generated code and user-supplied code.

Testing must validate the sandbox's isolation controls and resource limits.

### 15.1 Isolation testing

Testing should cover:

- Filesystem isolation.
- Process isolation.
- Network isolation.
- DNS restrictions.
- Cloud metadata endpoint restrictions.
- Container or microVM boundaries.
- Tenant isolation.
- Host isolation.
- Access to secrets.
- Access to environment variables.
- Access to mounted volumes.
- Access to host services.
- Access to internal infrastructure.
- Sandbox lifecycle management.

### 15.2 Resource limit testing

Testing should validate:

- CPU limits.
- Memory limits.
- Disk limits.
- Process limits.
- Execution-time limits.
- Network limits where applicable.
- Tenant quotas.
- Concurrent execution limits.

### 15.3 Hostile-code testing

Controlled hostile-code testing should evaluate:

- Privilege escalation attempts.
- Filesystem escape attempts.
- Container escape attempts.
- Network access attempts.
- DNS tunnelling attempts where relevant.
- Cloud metadata access attempts.
- Credential discovery attempts.
- Resource exhaustion.
- Malicious dependency behaviour.
- Process abuse.
- Persistence attempts.
- Cross-tenant access attempts.

Hostile-code tests must be conducted in authorised, isolated environments.

### 15.4 Sandbox acceptance criteria

Sandbox acceptance requires evidence that the tested controls enforce their defined boundaries and resource limits.

No sandbox technology should be represented as providing zero risk or guaranteed escape prevention.

## 16. Multimodal Testing

The platform must validate multimodal processing across supported input and output modalities.

### 16.1 Supported modalities

Testing should cover applicable:

- Text.
- Images.
- Audio.
- Voice.
- Video.
- Documents.
- Source code.
- Structured data.

### 16.2 Multimodal test cases

Testing should cover:

- Input validation.
- Format compatibility.
- File size limits.
- Media duration limits.
- Encoding.
- Decoding.
- Quality.
- Processing latency.
- Error handling.
- Malformed inputs.
- Unsupported formats.
- Model/provider failures.
- Output validation.
- Resource consumption.
- Privacy.
- Security.

### 16.3 Language testing

Testing should evaluate supported languages and language-dependent workflows.

Where applicable, testing should include:

- Language identification.
- Text processing.
- Speech recognition.
- Voice generation.
- Multilingual responses.
- Language switching.
- Mixed-language inputs.
- Nigerian English.
- Nigerian Pidgin.
- Hausa.
- Yoruba.
- Igbo.
- Additional supported languages.

Language testing must use appropriate evaluation datasets and human review where necessary.

### 16.4 Multimodal security testing

Testing must validate that multimodal inputs cannot bypass:

- Authentication.
- Authorisation.
- Tenant isolation.
- Agent permissions.
- Privacy protections.
- Sandbox restrictions.
- Approval gates.

## 17. Accessibility Testing

Accessibility testing should validate the usability of frontend applications for users with diverse accessibility requirements.

Testing should cover applicable accessibility requirements based on the approved accessibility standard.

Proposed testing areas include:

- Keyboard navigation.
- Focus management.
- Screen reader compatibility.
- Semantic HTML.
- Accessible labels.
- Colour contrast.
- Text scaling.
- Responsive layouts.
- Accessible forms.
- Error messages.
- Navigation consistency.
- Media accessibility.
- Captions where applicable.
- Alternative text.
- Reduced motion.
- Touch target usability.

Automated accessibility testing should be complemented by manual testing.

Accessibility acceptance criteria must be established for the relevant release scope.

## 18. Performance, Load and Scalability Testing

Performance testing must evaluate the platform under expected and adverse workloads.

### 18.1 Performance testing types

Testing should include:

- Baseline performance testing.
- Load testing.
- Stress testing.
- Spike testing.
- Soak testing.
- Capacity testing.
- Concurrency testing.
- Resource exhaustion testing.
- Recovery testing.

### 18.2 Performance testing areas

Testing should cover:

- Frontend loading.
- API latency.
- API throughput.
- Database performance.
- Agent execution latency.
- Workflow execution.
- AI model latency.
- Multimodal processing.
- Sandbox execution.
- Background worker performance.
- Object storage.
- Queue processing.
- Payment processing.
- Concurrent user workloads.

### 18.3 Performance metrics

Performance testing should measure:

- Request throughput.
- Latency percentiles.
- Error rate.
- CPU usage.
- Memory usage.
- Disk usage.
- Database connections.
- Database query latency.
- Queue backlog.
- Workflow backlog.
- Worker utilisation.
- AI inference latency.
- AI token consumption.
- Cost per operation.
- Resource consumption per tenant.

### 18.4 Capacity testing

Capacity testing should evaluate expected workload scenarios, growth assumptions and resource requirements.

Testing should inform:

- Service sizing.
- Worker concurrency.
- Database capacity.
- Storage capacity.
- Rate limits.
- Quotas.
- Autoscaling policies.
- AI provider limits.
- Cost projections.

Performance and capacity results must be documented and interpreted within the conditions of the test.

## 19. Security Testing

Security testing must be integrated throughout the development and release lifecycle.

### 19.1 Security testing categories

Security testing should include:

- Static application security testing.
- Dynamic application security testing.
- Software composition analysis.
- Dependency vulnerability testing.
- Container security testing.
- Infrastructure configuration testing.
- API security testing.
- Authentication testing.
- Authorisation testing.
- Tenant-isolation testing.
- Secret detection.
- Penetration testing.
- Threat-model validation.
- Sandbox security testing.
- Prompt-injection testing.
- AI safety testing.
- Privacy testing.

### 19.2 Security testing scope

Security testing should cover:

- Frontend applications.
- Backend services.
- APIs.
- Agents.
- AI integrations.
- Databases.
- Object storage.
- GitHub repositories.
- CI/CD workflows.
- Sandbox execution.
- Identity.
- Payment integrations.
- Advertising systems.
- Infrastructure.
- Secrets.
- Logging.
- Monitoring.
- Network boundaries.

### 19.3 Security test findings

Security findings must be recorded, assessed, prioritised and tracked.

Critical security findings must not be ignored or silently accepted.

Security exceptions must be documented, justified, approved by the authorised risk owner and subject to appropriate review.

### 19.4 Security testing limitations

Security testing does not establish absolute security.

Testing results must be interpreted according to their scope, methodology, environment, coverage and limitations.

## 20. Privacy and Data Protection Testing

Privacy-related testing should validate the platform's handling of personal data and confidential information.

Testing should cover:

- Data access.
- Data minimisation.
- Tenant boundaries.
- Data retention.
- Deletion workflows.
- Export workflows where applicable.
- Consent-related controls where applicable.
- Privacy-sensitive logs.
- Confidential uploads.
- API data exposure.
- Data access permissions.
- Third-party integrations.

Testing must validate that private prompts, source code, credentials, uploaded documents and confidential project activity are not improperly exposed through advertising, telemetry or unauthorised integrations.

## 21. Advertising and Monetisation Boundary Testing

The AdTech Service and advertising-related agent functionality must be tested for enforceable separation from confidential platform activity.

Testing should validate that advertising components cannot improperly access:

- Private source code.
- Confidential user prompts.
- Private project discussions.
- Uploaded private documents.
- Credentials.
- API keys.
- Tokens.
- Private application workspaces.
- Confidential development activity.
- Protected tenant data.

Testing should also validate:

- Advertising labelling.
- Consent-related controls where applicable.
- Approved contextual data usage.
- Access permissions.
- Data-flow restrictions.
- Advertising workflow boundaries.

Advertising must not interrupt or interfere with core software development, code generation, testing, deployment or security workflows.

## 22. Workflow, Retry and Resilience Testing

Durable workflow orchestration must be tested for reliability and recovery.

Testing should cover:

- Workflow initiation.
- Workflow completion.
- Workflow failure.
- Retry behaviour.
- Timeout handling.
- Cancellation.
- Idempotency.
- Duplicate events.
- Delayed events.
- Event ordering.
- Worker failures.
- Worker restarts.
- Workflow replay where applicable.
- Dead-letter handling.
- Reconciliation.
- Recovery after dependency failure.

Temporal-related testing must validate the proposed workflow architecture and operational assumptions before production adoption.

Testing must not assume that workflow execution, event delivery or external integrations are exactly-once without supporting evidence.

## 23. GitHub, CI/CD and Release Governance Testing

GitHub operations and CI/CD workflows must be tested against the repository security and release governance requirements.

Testing should cover:

- Pull-request validation.
- Branch protection.
- Required checks.
- Permission boundaries.
- CI credentials.
- Secrets.
- Dependency workflows.
- Build workflows.
- Artifact integrity.
- Release workflows.
- Deployment approvals.
- Rollback procedures.
- Auditability.

Testing must validate that autonomous agents cannot independently bypass protected-branch controls or perform unauthorised protected GitHub operations.

GATE-04 must govern applicable protected GitHub operations.

GATE-03 must govern production deployment approval.

A successful CI build must not automatically constitute production approval.

## 24. Disaster Recovery and Backup Testing

Disaster recovery testing must validate the ability to recover critical platform components and data.

Testing should cover:

- Database backup and restoration.
- Database recovery.
- Object storage recovery.
- Git repository recovery.
- Temporal persistence recovery.
- Queue recovery.
- Dead-letter recovery.
- Identity and session recovery.
- Secrets and configuration recovery.
- Generated artifact recovery.
- Service recovery.
- Regional recovery where applicable.

### 24.1 Recovery objectives

Recovery Point Objectives (RPO) and Recovery Time Objectives (RTO) must be defined for critical systems.

Proposed objectives must not be treated as achieved until supported by implementation and testing evidence.

### 24.2 Recovery testing

Recovery testing should include:

- Backup verification.
- Restore verification.
- Recovery procedures.
- Data integrity verification.
- Recovery dependencies.
- Recovery sequencing.
- Recovery permissions.
- Recovery documentation.
- Recovery evidence.
- Lessons learned.

### 24.3 Disaster recovery acceptance

Disaster recovery acceptance requires evidence that the tested recovery procedures meet the approved recovery objectives under the tested conditions.

A backup configuration alone does not establish disaster recovery readiness.

## 25. Test Coverage and Quality Thresholds

The following thresholds are proposed for discussion and approval. They are not current implementation results or approved release guarantees.

| Testing area | Proposed threshold or acceptance principle |
|---|---|
| Critical deterministic business logic | 100% of identified critical requirements have corresponding tests |
| Financial integrity | All identified critical financial scenarios tested and passed |
| Tenant isolation | All defined critical tenant-isolation scenarios tested and passed |
| Authentication and authorisation | All identified critical access-control scenarios tested and passed |
| Approval gates | All defined gate enforcement and bypass scenarios tested and passed |
| Critical API contracts | All critical API contract tests passed |
| Agent permission boundaries | All defined critical permission-boundary tests passed |
| Sandbox security | Defined critical sandbox controls tested with documented results |
| Critical security findings | No unresolved critical findings without formally authorised risk disposition |
| High security findings | Resolution or documented risk disposition required before applicable release approval |
| Accessibility | Release acceptance against the approved accessibility criteria |
| Performance | Release acceptance against approved workload and performance targets |
| Disaster recovery | Recovery tests completed against approved recovery objectives |
| AI evaluations | Defined evaluation datasets and release thresholds established for critical agents |
| Generated applications | Defined acceptance checks completed for the application's intended release scope |

### 25.1 Coverage metrics

Coverage metrics should include, where applicable:

- Line coverage.
- Branch coverage.
- Function coverage.
- Requirement coverage.
- API contract coverage.
- Security test coverage.
- Agent evaluation coverage.
- Workflow coverage.
- Tenant-isolation scenario coverage.
- Financial scenario coverage.

Code coverage must not be treated as a substitute for test quality, risk coverage or meaningful assertions.

### 25.2 Proposed coverage targets

The Project Owner and technical owners should establish appropriate numerical coverage targets for deterministic software components.

Numerical coverage targets must account for component criticality, testing methodology, architecture and practical limitations.

Coverage targets should not be used to encourage superficial or low-quality tests.

## 26. CI Testing Pipeline

The proposed CI testing pipeline should progressively validate changes.

### 26.1 Pull-request validation

Proposed checks include:

1. Source validation.
2. Formatting checks.
3. Linting.
4. Type checking.
5. Static analysis.
6. Secret detection.
7. Dependency analysis.
8. Unit tests.
9. Component tests.
10. API contract tests.
11. Relevant integration tests.
12. Build verification.
13. Artifact validation.
14. Test result reporting.

### 26.2 Staging validation

Staging validation should include:

- Integration testing.
- End-to-end testing.
- Security validation.
- Tenant-isolation testing.
- Financial integration testing using controlled test environments.
- AI agent evaluation.
- Multimodal validation.
- Performance testing.
- Accessibility testing.
- Workflow testing.
- Operational verification.
- Release acceptance testing.

### 26.3 Production release validation

Production release validation must be subject to the applicable governance approvals.

Production validation should include:

- Release artifact verification.
- Deployment verification.
- Configuration verification.
- Service health.
- API health.
- Monitoring verification.
- Smoke tests.
- Critical workflow verification.
- Rollback readiness.
- Human approval where required.

Production release validation must not bypass GATE-03 or applicable GATE-04 controls.

## 27. Release Acceptance Criteria

A release should not be considered ready for approval unless the applicable acceptance criteria have been satisfied.

The proposed release acceptance criteria are:

1. Required test plans are documented.
2. Required tests have been executed.
3. Test results are recorded.
4. Critical functional requirements have been validated.
5. Critical security controls have been validated.
6. Tenant-isolation testing has been completed for the applicable scope.
7. Financial integrity testing has been completed for the applicable scope.
8. Agent permission-boundary tests have been completed.
9. Sandbox security tests have been completed for the applicable scope.
10. Critical defects have been resolved.
11. High-severity defects have been resolved or formally risk-assessed.
12. Performance acceptance criteria have been met.
13. Accessibility acceptance criteria have been met where applicable.
14. Operational monitoring is available for the applicable scope.
15. Recovery procedures are documented for critical services.
16. Required human approvals have been obtained.
17. Release evidence has been retained.
18. Deployment and rollback procedures have been reviewed.

Acceptance must be specific to the release scope.

## 28. Testing Responsibilities

Testing responsibilities should be assigned according to the proposed governance structure.

### 28.1 Project Owner

The Project Owner should:

- Approve testing policy and major testing objectives.
- Approve applicable release criteria.
- Review material risks.
- Authorise applicable governance gates.
- Review critical testing findings.
- Approve relevant risk acceptance.

### 28.2 Architecture and technical owners

Technical owners should:

- Define technical test requirements.
- Review architecture-related test findings.
- Validate service boundaries.
- Review critical integration tests.
- Define technical acceptance criteria.
- Maintain test architecture.

### 28.3 Development teams and agents

Development teams and authorised agents should:

- Implement appropriate tests.
- Execute authorised tests.
- Report failures.
- Preserve test evidence.
- Avoid bypassing testing controls.
- Respect repository and environment permissions.

### 28.4 Security and quality reviewers

Authorised security and quality reviewers should:

- Review applicable test evidence.
- Assess critical findings.
- Validate testing scope.
- Review security and quality exceptions.
- Recommend release readiness.

AI agents must not independently approve their own consequential actions where human approval is required.

## 29. Testing Risks and Limitations

Testing introduces risks and limitations that must be managed.

These include:

- Incomplete test coverage.
- False positives.
- False negatives.
- AI model variability.
- AI evaluation limitations.
- Dependency failures.
- Environment differences.
- Test data limitations.
- Unidentified vulnerabilities.
- Incomplete threat models.
- Inadequate performance test workloads.
- Unverified recovery assumptions.
- Third-party service limitations.
- Incomplete observability.
- Testing infrastructure failures.

Testing must not be represented as providing absolute guarantees of security, correctness, reliability, scalability or AI performance.

## 30. Testing Strategy Implementation Roadmap

The testing strategy should be implemented progressively.

### Phase 0 — Architecture and governance

- Define the testing strategy.
- Define testing principles.
- Define testing layers.
- Define test governance.
- Define proposed acceptance criteria.
- Identify critical testing domains.
- Identify outstanding decisions.

### Phase 1 — Testing foundation

Subject to Phase 0 approval:

- Establish test tooling.
- Establish automated CI testing.
- Establish unit testing conventions.
- Establish test reporting.
- Establish controlled test environments.
- Establish initial test data management.
- Establish baseline quality checks.

### Phase 2 — Service and integration testing

- Implement service-level test suites.
- Implement integration testing.
- Implement API contract testing.
- Implement database integrity tests.
- Implement tenant-isolation tests.
- Implement workflow tests.

### Phase 3 — Security and AI evaluation

- Implement agent evaluation datasets.
- Implement permission-boundary tests.
- Implement prompt-injection testing.
- Implement sandbox testing.
- Implement security testing.
- Implement financial integrity testing.

### Phase 4 — Operational testing

- Implement performance testing.
- Implement load and capacity testing.
- Implement accessibility testing.
- Implement monitoring validation.
- Implement disaster recovery testing.
- Implement release qualification testing.

### Phase 5 — Continuous improvement

- Review test effectiveness.
- Improve coverage.
- Refine test datasets.
- Review incidents.
- Improve regression suites.
- Refine quality thresholds.
- Improve testing automation.

This roadmap is proposed and does not constitute implementation authorisation.

## 31. Outstanding Decisions

The following decisions require Project Owner or authorised technical review where applicable:

1. Approved testing tools and frameworks.
2. Test coverage thresholds.
3. CI testing requirements.
4. Test environment architecture.
5. Test data management policy.
6. AI evaluation methodology.
7. Security testing scope.
8. Accessibility acceptance criteria.
9. Performance acceptance criteria.
10. Disaster recovery acceptance criteria.
11. Test evidence retention requirements.
12. Release acceptance authority.
13. Defect risk acceptance authority.
14. Testing budget.
15. Testing implementation roadmap.

These decisions should be recorded in the appropriate Architecture Decision Records, governance records or approved project documentation.

## 32. Phase 0 Status

This document establishes a proposed testing strategy for the Worklexx AI Software Factory.

The document is an architectural and governance specification. It does not establish that the proposed testing tools, infrastructure, test suites, CI pipelines, security tests, evaluation datasets, performance tests or disaster recovery tests have been implemented.

Implementation requires the applicable Phase 0 approval and subsequent development authorisation.

Phase 1 remains unauthorised until the applicable Phase 0 review, human decisions, governance requirements and Project Owner approval have been completed.

## 33. Approval Record

| Approval field | Value |
|---|---|
| Document ID | WLX-ARCH-014 |
| Document | TESTING_STRATEGY.md |
| Version | 1.0.0 |
| Status | Proposed — Pending Review |
| Project Owner | Pending |
| Technical Review | Pending |
| Security Review | Pending |
| Approval Date | Pending |
| Approval Evidence | Pending |

---

**End of Document — WLX-ARCH-014**

## 34. Repository Backup and Disaster-Recovery Verification

Under approved HD-REP-07, repository recovery testing must cover the distinct classes of Factory platform source, Worklexx-managed customer projects, customer-managed connected repositories (within authorised scope), and supporting development records/artifacts.

Required test scenarios and retained evidence:

1. Restore Git objects, complete reachable history, branches, tags and references; verify repository integrity.
2. Restore Git LFS objects and confirm object availability and checksums.
3. Recover supported issues, pull requests, reviews, comments, labels, milestones, releases and governance metadata; record provider/API limitations.
4. Recover release/build artifacts and verify checksums, provenance and associated source references.
5. Demonstrate tenant/project isolation, including negative tests for cross-tenant backup discovery, restore, credentials, jobs, caches and artifact access.
6. Simulate accidental deletion, compromised ordinary repository credentials and ransomware; demonstrate protected-copy availability and clean recovery-point selection.
7. Restore into an isolated compatible environment or independent provider and verify export/portability without silently overwriting newer customer work.
8. Verify encryption-key recovery, backup identity separation, access logging, retention expiry and legal-hold preservation.
9. Validate customer-managed hosting responsibility boundaries and the exact scope of customer-authorised Worklexx copies.
10. Measure actual RPO and RTO for each data class and compare with HD-REP-07 objectives and HD-06/POC-15 requirements.

This strategy records architectural test requirements only; it does not authorise backup configuration, infrastructure provisioning, spending, repository permission changes, customer account connections, backup/restore/migration execution, CI/CD activation, production implementation or Phase 1. Applicable HD-08 approvals remain mandatory.\n\nA successful scheduled backup is not sufficient evidence of recoverability. Record test date, scope, source/recovery point, environment, method, integrity results, measured RPO/RTO, defects, limitations, reviewer and remediation. Tests must not use production data or perform consequential production restoration without the applicable approvals.

## 35. Build Integrity and Software Supply-Chain Validation — HD-REP-08

The following proof-of-concept validations are required before production reliance on the approved architecture. Each test must record scope, environment, method, expected result, actual result, evidence, limitations, defects, remediation and reviewer. No test is considered passed merely because it is specified here.

| Validation ID | Required validation |
|---|---|
| POC-REP-08-01 | Verify workflow permissions are least-privilege, read-only by default and narrowly scoped per job |
| POC-REP-08-02 | Demonstrate isolation of untrusted pull-request code from privileged secrets and trusted release workflows |
| POC-REP-08-03 | Verify lockfile enforcement, dependency integrity and pinned tool/action versions |
| POC-REP-08-04 | Demonstrate vulnerability, secret and licence scanning, with risk-based triage |
| POC-REP-08-05 | Generate and validate machine-readable SBOMs in SPDX or CycloneDX format |
| POC-REP-08-06 | Verify artifact checksums, signatures, provenance and source-to-artifact traceability |
| POC-REP-08-07 | Test build environment, filesystem, network, credential and cache isolation |
| POC-REP-08-08 | Test Factory/customer-project separation and cross-tenant negative access scenarios |
| POC-REP-08-09 | Demonstrate credential minimisation, short-lived access where supported, protection and revocation |
| POC-REP-08-10 | Verify separate validation, build, release approval, publication and deployment permissions |
| POC-REP-08-11 | Simulate compromised dependency, malicious workflow and untrusted build-script scenarios |
| POC-REP-08-12 | Verify audit records, provenance retention, artifact recovery and end-to-end traceability |

Tests must cover Worklexx platform source, Worklexx-managed customer projects and customer-managed repositories within authorised scope. Build caches, artifacts, credentials and execution jobs must be checked for tenant/project isolation. Signing-key custody and recovery must be tested without exposing private keys in source or ordinary workflow configuration.

These are validation requirements only. They do not authorise CI/CD activation, repository setting changes, credential creation, paid services, production builds, publication, release creation, deployment or Phase 1. Applicable HD-08 gates remain mandatory.


## 36. Repository Observability, Audit Logging and Security Monitoring Validation — HD-REP-09

The following proof-of-concept validations are required before operational reliance on the approved HD-REP-09 architecture. Each test must record scope, environment, method, expected and actual results, evidence, limitations, defects, remediation and reviewer. A listed test is not evidence that it has been executed or passed.

| Validation ID | Required validation |
|---|---|
| POC-REP-09-01 | Verify event-source coverage and completeness across repository, identity, workflow, agent, supply-chain, integration and backup domains; document provider gaps |
| POC-REP-09-02 | Validate event schema consistency, actor attribution, tenant/project context, correlation and timestamp/time-source accuracy |
| POC-REP-09-03 | Demonstrate tamper detection, integrity verification, append-only protection and restricted deletion/modification |
| POC-REP-09-04 | Test tenant/project isolation, including negative access attempts against other customers' audit records and exports |
| POC-REP-09-05 | Validate secret redaction, privacy controls, data minimisation and separation of telemetry from security audit evidence |
| POC-REP-09-06 | Measure security-detection coverage, false positives and false negatives using controlled scenarios |
| POC-REP-09-07 | Validate alert severity, ownership, escalation, incident investigation and closure evidence |
| POC-REP-09-08 | Test retention schedules, legal holds, customer export, controlled deletion and auditability of policy changes |
| POC-REP-09-09 | Restore audit records from protected backups and verify integrity, completeness and access controls |
| POC-REP-09-10 | Verify customer-managed provider event visibility, authorised integration scope and documented coverage limitations |
| POC-REP-09-11 | Test AI-agent permissions and prohibited actions, including approval, risk acceptance, evidence deletion, retention changes and monitoring disablement |
| POC-REP-09-12 | Demonstrate end-to-end traceability from initiating action through identity, repository, workflow, artifact and incident evidence |

Tests must cover Factory source, Worklexx-managed customer projects and customer-managed repositories only within authorised scope. Use synthetic or appropriately controlled test data. Do not activate production telemetry, change provider settings, connect customer accounts or perform consequential production actions as part of these specifications without separate approval. Applicable HD-08 gates remain mandatory.


## 37. Customer Project Lifecycle, Ownership, Portability and Exit Validation — HD-REP-10

The following proof-of-concept validations are required before operational reliance on the approved HD-REP-10 architecture. Each test must record scope, environment, method, expected and actual results, evidence, limitations, defects, remediation and reviewer. A listed validation is a requirement, not evidence that the test has been executed or passed. Use synthetic or appropriately controlled data; do not perform consequential live-customer operations without separate authorisation.

| Validation ID | Required validation |
|---|---|
| POC-REP-10-01 | Verify unique immutable project identity and correct customer/tenant/owner/controller/repository mapping |
| POC-REP-10-02 | Test tenant/project isolation, including negative cross-tenant access to source, metadata, exports, jobs, caches and artifacts |
| POC-REP-10-03 | Verify Worklexx-managed versus customer-managed hosting responsibility, permission and recovery boundaries |
| POC-REP-10-04 | Test all lifecycle state transitions, invalid transitions, authorisation, audit history and recovery behaviour |
| POC-REP-10-05 | Verify owner, collaborator, administrator and transfer authority, including required-party approval and rejection of unauthorised requests |
| POC-REP-10-06 | Verify export completeness for source, Git history, branches, tags, refs, Git LFS and applicable project metadata |
| POC-REP-10-07 | Import an exported project into an independent supported Git environment and verify integrity and usability |
| POC-REP-10-08 | Verify that passwords, tokens, private/signing keys and other secrets are excluded from ordinary exports and can be securely re-established |
| POC-REP-10-09 | Test subscription/entitlement expiry, notification, suspension and retrieval safeguards; prove that expiry does not automatically delete customer assets |
| POC-REP-10-10 | Test record-class retention, archival, legal holds, authorised deletion and verification across primary, derived and provider-controlled stores |
| POC-REP-10-11 | Verify backup expiry and restore controls prevent deleted information from being silently reintroduced into active systems |
| POC-REP-10-12 | Disconnect a test external integration and verify scoped credential revocation without deletion of customer-owned repositories |
| POC-REP-10-13 | Exercise customer exit, export/transfer completion, ownership confirmation, notification and audit evidence end to end |
| POC-REP-10-14 | Test agent prohibited actions, including ownership transfer, visibility changes, disconnection, access revocation, deletion, retention changes and legal-hold override |
| POC-REP-10-15 | Demonstrate end-to-end lifecycle traceability, failure recovery, integrity verification and customer-scoped evidence retrieval |

Tests must distinguish export from ownership transfer, suspension from deletion, and repository hosting administration from project ownership. Provider/API limitations and customer-managed responsibility boundaries must be documented. Retention periods and legal-hold behaviour must be validated against approved legal, regulatory and contractual requirements; no universal duration is assumed.

**Governance and scope:** Apply HD-07 and HD-08, including GATE-02, GATE-03, GATE-04, GATE-05 and GATE-06 according to the operation. These are validation requirements only; they do not authorise customer provisioning, account connections, OAuth installation, repository/ownership transfer, live customer suspension/deletion, production migration, backup/retention configuration, infrastructure, spending, CI/CD activation, production deployment or Phase 1.



## 38. Customer Data Isolation, Privacy Boundaries and Data Governance Validation — HD-REP-11

The following proof-of-concept validations are required before operational reliance on the approved HD-REP-11 architecture. Each test must record scope, synthetic/controlled dataset, environment, method, expected and actual results, evidence, limitations, defects, remediation and reviewer. A listed validation is a requirement, not evidence that the test has been executed or passed. Do not use live customer or personal data without separate authorisation and applicable legal/security approvals.

| Validation ID | Required validation |
|---|---|
| POC-REP-11-01 | Verify data classification, processing inventory, purpose, data minimisation and ownership/controller/processor mapping |
| POC-REP-11-02 | Test tenant/project isolation across all six backend services, APIs, storage, jobs, queues, caches, artifacts, exports and administrative paths, including negative cross-tenant cases |
| POC-REP-11-03 | Validate PostgreSQL row-level security, service-layer authorisation, joins, indirect references, runtime-role restrictions and bypass resistance |
| POC-REP-11-04 | Verify tenant/project-scoped pgvector filtering, retrieval authorisation, embedding provenance and deletion/revocation |
| POC-REP-11-05 | Test agent least privilege, task scope, duration, context isolation and prohibited access/permission-expansion actions |
| POC-REP-11-06 | Simulate prompt injection and malicious/untrusted instructions in documents, source code, prompts, web content and multimodal transcripts; verify policy and authorisation cannot be overridden |
| POC-REP-11-07 | Validate secure upload, processing, temporary-file handling, transcript/metadata controls, derivative tracking and deletion for images, audio and video |
| POC-REP-11-08 | Verify external model/subprocessor due diligence controls, data minimisation, location, retention, human access, onward processing, training-use restrictions and deletion terms |
| POC-REP-11-09 | Validate encryption in transit/at rest, key separation, least privilege, rotation, revocation, recovery and secret non-disclosure |
| POC-REP-11-10 | Validate data-flow mapping, applicable jurisdictional assessment, cross-border transfer safeguards, localisation and provider/support/backup locations |
| POC-REP-11-11 | Exercise applicable data-subject/customer access, correction, export, erasure, restriction, objection and consent-withdrawal workflows with authority checks |
| POC-REP-11-12 | Verify record-class retention, legal holds, deletion and non-reintroduction across primary data, Git/LFS, object storage, indexes, embeddings, caches, jobs, replicas and backups |
| POC-REP-11-13 | Test privacy-aware audit coverage, sensitive-data redaction, audit integrity, incident detection, escalation and evidence handling aligned with HD-REP-09 |
| POC-REP-11-14 | Verify Worklexx-managed versus customer-managed hosting, data responsibility, provider visibility and contractual boundary controls |
| POC-REP-11-15 | Conduct end-to-end privacy/security assessment, including cross-tenant negative testing, external transfer controls, derived-data lifecycle and recovery behaviour |

Tests must cover prompts, source code, documents, images, audio, video, transcripts, embeddings, metadata, generated outputs and derived copies. Validate that tenant identity comes from trusted authentication/authorisation rather than client-supplied identifiers. RLS supplements service-layer authorisation. External provider training restrictions must be verified contractually and technically where possible. No universal retention duration is assumed; test the approved record-class schedule and applicable legal holds.

**Governance and scope:** Add RSK-31 for customer data exposure, unlawful processing and privacy control failure; formal likelihood/impact/residual scoring remains pending. Apply HD-07 and HD-08, including GATE-01/02/03/04/05/06 according to the activity. These validation requirements do not authorise live personal/customer-data processing, customer/provider integrations, infrastructure/database/storage changes, credentials/keys, spending, production monitoring/workflows, migrations, deletion/restoration, deployment or Phase 1.


## 39. Customer Identity, Authentication, Authorisation and Access Lifecycle Validation — HD-REP-12

The following proof-of-concept validations are required before operational reliance on the approved HD-REP-12 architecture. Each test must record scope, synthetic/controlled dataset, environment, method, expected and actual results, evidence, limitations, defects, remediation and reviewer. A listed validation is a requirement, not evidence that it has been executed or passed. Do not create live customer accounts, connect identity providers or process live personal data without separate authorisation and applicable legal/security approvals.

| Validation ID | Required validation |
|---|---|
| POC-REP-12-01 | Verify managed identity-provider integration, standards interoperability and provider-independent identity mapping |
| POC-REP-12-02 | Verify user, organisation, membership, project, agent, service, workload and external-integration identity mapping |
| POC-REP-12-03 | Test multi-organisation membership and strict tenant isolation for users with different roles in different organisations |
| POC-REP-12-04 | Validate RBAC, ABAC and resource-level policy enforcement, including policy precedence and deny behaviour |
| POC-REP-12-05 | Conduct cross-tenant and cross-project negative-access tests using guessed, altered and client-supplied identifiers |
| POC-REP-12-06 | Verify separation of organisation administration, project ownership, hosting administration and transfer authority |
| POC-REP-12-07 | Evaluate MFA, phishing-resistant methods/passkeys, SSO and federation, including recovery and fallback controls |
| POC-REP-12-08 | Test session creation, renewal, expiry, concurrent sessions, logout and revocation |
| POC-REP-12-09 | Exercise account recovery, lost-device and compromised-account containment without unauthorised takeover |
| POC-REP-12-10 | Verify distinct agent identity, task/tenant/project/operation/time scope and prohibition on inherited blanket human authority |
| POC-REP-12-11 | Verify distinct service/workload identities and least-privilege service-to-service permissions across all six deployables |
| POC-REP-12-12 | Test API-key/token ownership, purpose, scope, expiry, storage, rotation, revocation and secret redaction |
| POC-REP-12-13 | Measure revocation propagation across sessions, services, RLS, pgvector, storage, Git, workflows, agent contexts, caches and integrations |
| POC-REP-12-14 | Test privileged access, stronger authentication, time limits, emergency access, evidence and post-event review |
| POC-REP-12-15 | Verify complete and tamper-evident audit attribution for authentication, membership, permissions, delegation, recovery and revocation |
| POC-REP-12-16 | Test invitation, acceptance, role changes, periodic access review, suspension, restoration and deprovisioning lifecycle |
| POC-REP-12-17 | Validate identity-data minimisation, access restrictions, correction/export/erasure and retention/legal-hold handling |
| POC-REP-12-18 | Simulate identity-provider outage, degraded operation, recovery and safe handling of cached authentication/authorisation state |
| POC-REP-12-19 | Verify HD-08 approval-gate enforcement, human attribution, action/resource binding, expiry, revocation and fail-closed behaviour |
| POC-REP-12-20 | Test concurrent role/membership changes, stale permission caches, queued workflows and race conditions; prove revoked authority cannot be reused |

Tests must distinguish authentication from authorisation and prove that a valid login or token does not grant access beyond the identity's current tenant, project and resource permissions. Test all six backend services and supporting systems. Agent and service identities must be independently attributable. Define and measure revocation propagation objectives; do not assume instantaneous invalidation. Provider/API limitations, recovery dependencies and failure modes must be recorded.

**Governance and scope:** Add RSK-32 for identity compromise, excessive privilege and access-control failure; formal likelihood/impact/residual scoring remains pending. Apply HD-07 and HD-08, including GATE-01/02/03/04/05/06 according to the actual activity. These validation requirements do not authorise identity-provider connection, live account creation, SSO/OAuth configuration, permission changes, credential issuance, infrastructure/database changes, paid services, GitHub settings changes, production authentication activation, migrations, production deployment or Phase 1.


## HD-REP-13 — AI Agent Security, Delegation, Execution Boundaries and Human Oversight Governance (Approved 2026-11-20)

Adopt permission-controlled, policy-enforced, sandboxed and auditable agent execution for the 23 logical agent modules. This decision does not add a backend deployable or alter the approved six-deployable architecture. Agent intelligence is not authority: each agent has a distinct identity and bounded task, tenant/project, tool, data and time scope; versioned policies; resource limits; audit attribution; and revocation controls.

Five conceptual permission tiers: Tier 0 Observe; Tier 1 Prepare; Tier 2 Execute within controlled scope; Tier 3 Consequential action subject to independent approval and applicable control; Tier 4 prohibited authority (including self-approval and governance bypass). Tool permissions remain granular: inspect, write, PR creation, review, approval, merge, permission changes, deletion and transfer are separate capabilities. The tool-control boundary validates identity/scope, inputs and destinations, classification, policy and approval, then executes, verifies and audits.

Code execution uses an appropriately isolated sandbox within the approved sandbox-runner boundary: restricted networking, resource/time limits, filesystem/process isolation, credential separation, tenant/project-specific caches and artifact handling, and cleanup. Untrusted documents, source, web content, prompts and tool results are data—not policy or authority—and prompt injection must not override permissions, governance or gates. Delegation is task/time bounded, depth-limited, attributable, revocable and cannot expand the initiating authority.

Agent context and memory are scoped, classified, minimised, governed and tenant/project isolated. Outputs require independent verification appropriate to their risk; verification does not substitute for human approvals required by HD-08. Control retries, loops, concurrency, idempotency, resource/cost limits, cancellation and safe failure. Protected audit and monitoring align with HD-REP-09; privacy and data boundaries with HD-REP-11; identity and delegation with HD-REP-12; execution isolation and supply-chain controls with HD-REP-08; customer lifecycle with HD-REP-10.

Validation requirements: POC-REP-13-01 through POC-REP-13-24 (unexecuted) cover agent identity/scope, least privilege, tool authorization, policy enforcement, tier separation, gate binding, sandbox isolation, network/credential restrictions, resource limits, prompt-injection resistance, untrusted content, tenant/project isolation, delegation depth/authority, context/memory privacy, output verification, human oversight, audit attribution, revocation, concurrent actions/races, loops/retries/cancellation, failure/recovery, cost controls, abuse scenarios and end-to-end governance bypass attempts.

Add RSK-33 — AI Agent Misuse, Unsafe Execution, Privilege Escalation and Governance Bypass. Formal likelihood, impact, inherent and residual scores remain pending assessment; proposed controls do not reduce residual risk until implemented and evidenced.

Project Owner remains sole initial risk acceptance and approval authority under HD-07/HD-08. Applicable gates remain mandatory. This is architecture/documentation approval only: no agent execution in production, sandbox provisioning, external integrations, live customer data, credentials, CI/CD activation, GitHub configuration, database changes, paid services, production deployment or Phase 1 is authorised.


### POC-REP-13 — Agent Governance Validation
All 24 tests described in HD-REP-13 are required; test cases are requirements, not evidence of completion. Include negative, adversarial, race-condition and end-to-end checks, with traceable results and evidence. Do not represent them as passed before execution.


### POC-REP-14 — API Contracts, Inter-Service Communication and Integration Validation
All 24 validations required by HD-REP-14 are test requirements, not evidence of completion. Track POC-REP-14-01 through -24 individually with owner, scope, environment, preconditions, expected result, evidence, outcome, defects and retest. Coverage: OpenAPI, JSON Schema, AsyncAPI, consumer/provider conformance, compatibility and breaking-change detection, contract ownership, service boundaries, authentication/authorization, tenant/project isolation, safe errors/redaction, idempotency, event duplication/order/replay, retries/timeouts/failure containment, dead-letter/recovery, Temporal replay and cancellation, agent-tool permissions, independent approval/gate binding, external schema drift/provider failure, webhook authenticity/replay, SSRF/destination/payload security, billing/ledger integrity and end-to-end audit/release traceability. Include negative, adversarial, concurrency and failure-injection cases. All POCs remain unexecuted until evidence is recorded and reviewed.


### POC-REP-15 — API Gateway, Routing, Rate Limiting and Edge Security Validation
All 24 validations required by HD-REP-15 are test requirements, not evidence of completion. Track each test individually with owner, scope, environment, preconditions, expected result, evidence, outcome, defects and retest. Required tests:

- POC-REP-15-01 external ingress and route isolation.
- POC-REP-15-02 authentication and token validation.
- POC-REP-15-03 receiving-service authorization enforcement.
- POC-REP-15-04 tenant/project isolation, including negative tests.
- POC-REP-15-05 agent identity and delegated-scope propagation.
- POC-REP-15-06 approval-gate enforcement for consequential operations.
- POC-REP-15-07 per-user, tenant and project rate limiting.
- POC-REP-15-08 subscription and entitlement quota enforcement.
- POC-REP-15-09 concurrent request and resource-exhaustion protection.
- POC-REP-15-10 payload-size and content-type enforcement.
- POC-REP-15-11 multimodal upload security and isolation.
- POC-REP-15-12 WAF, DDoS and malformed-request protection.
- POC-REP-15-13 SSRF and outbound-destination restrictions.
- POC-REP-15-14 CORS and browser-origin controls.
- POC-REP-15-15 webhook authenticity and replay protection.
- POC-REP-15-16 API-version compatibility and deprecation.
- POC-REP-15-17 timeout, retry and idempotency behaviour.
- POC-REP-15-18 circuit breaking and backpressure.
- POC-REP-15-19 safe errors and sensitive-data redaction.
- POC-REP-15-20 audit, correlation and trace completeness.
- POC-REP-15-21 gateway failure and fail-closed security behaviour.
- POC-REP-15-22 regional resilience and recovery.
- POC-REP-15-23 performance, latency and capacity under load.
- POC-REP-15-24 adversarial testing and independent security review.

Include cross-tenant negative tests, race/concurrency tests, failure injection and end-to-end traces. All tests remain unexecuted until results and evidence are recorded and reviewed.


## HD-REP-16 — API Security, Secrets and Cryptographic Controls Validation (Required; Not Executed)

Track each test individually with owner, scope, environment, preconditions, expected result, evidence, outcome, defects and retest. Required tests:

- POC-REP-16-01 secret storage and retrieval security.
- POC-REP-16-02 absence of secrets in source code, Git history and frontend bundles.
- POC-REP-16-03 secret-scanning coverage and detection accuracy.
- POC-REP-16-04 workload identity and service authentication.
- POC-REP-16-05 token issuer, audience, expiry and signature validation.
- POC-REP-16-06 API key scope, tenant binding and revocation.
- POC-REP-16-07 refresh-token rotation and reuse detection.
- POC-REP-16-08 secret rotation without unintended service interruption.
- POC-REP-16-09 key generation, separation and lifecycle controls.
- POC-REP-16-10 key-management access-control enforcement.
- POC-REP-16-11 encryption in transit.
- POC-REP-16-12 encryption at rest and backup protection.
- POC-REP-16-13 certificate issuance, renewal and revocation.
- POC-REP-16-14 artifact and provenance signature verification.
- POC-REP-16-15 webhook authenticity and replay protection.
- POC-REP-16-16 cross-service authentication and authorisation.
- POC-REP-16-17 tenant and project credential isolation.
- POC-REP-16-18 agent secret-access restrictions.
- POC-REP-16-19 prompt-injection attempts to extract secrets.
- POC-REP-16-20 secret redaction in logs and error responses.
- POC-REP-16-21 credential compromise and revocation propagation.
- POC-REP-16-22 key compromise, recovery and replacement.
- POC-REP-16-23 cryptographic integrity and tampering detection.
- POC-REP-16-24 backup restoration and key availability.
- POC-REP-16-25 security monitoring and incident evidence.
- POC-REP-16-26 adversarial testing and independent security review.

All tests remain unexecuted until results and evidence are recorded and reviewed.



## HD-REP-17 — Application Security and Secure SDLC Validation Requirements (Approved 2026-11-20)

The following proof-of-concept and validation requirements apply across five frontend applications, six backend deployables, shared packages, 23 logical agent modules and generated customer projects. They are requirements only; all tests are unexecuted until separately authorised and performed. Record owner, scope, environment, preconditions, expected result, evidence, outcome, issue references and retest for each.

| ID | Validation requirement |
|---|---|
| POC-REP-17-01 | Secure SDLC traceability from requirements to release evidence. |
| POC-REP-17-02 | Threat-modelling completeness and review process. |
| POC-REP-17-03 | Secure coding standards applicability across supported languages. |
| POC-REP-17-04 | SAST coverage and finding accuracy. |
| POC-REP-17-05 | Direct and transitive dependency vulnerability detection and prioritisation. |
| POC-REP-17-06 | Secret detection across source, Git history and artifacts. |
| POC-REP-17-07 | DAST suitability and authorised testing boundaries. |
| POC-REP-17-08 | API authentication and resource-authorisation testing. |
| POC-REP-17-09 | Frontend security and browser attack-surface testing. |
| POC-REP-17-10 | Input validation, output encoding and injection resistance. |
| POC-REP-17-11 | Tenant and project isolation under adversarial conditions. |
| POC-REP-17-12 | File-upload and multimodal-processing security. |
| POC-REP-17-13 | Agent-generated code security and execution restrictions. |
| POC-REP-17-14 | Vulnerability severity classification consistency. |
| POC-REP-17-15 | Critical and high vulnerability escalation procedures. |
| POC-REP-17-16 | Remediation deadlines, exception expiry and overdue escalation. |
| POC-REP-17-17 | Independent remediation verification and regression testing. |
| POC-REP-17-18 | Security testing authorisation and scope enforcement. |
| POC-REP-17-19 | False-positive review and vulnerability closure evidence. |
| POC-REP-17-20 | Security exceptions and Project Owner risk acceptance. |
| POC-REP-17-21 | Generated customer project security evidence and disclosures. |
| POC-REP-17-22 | Security evidence integrity and audit traceability. |
| POC-REP-17-23 | Security incident and vulnerability disclosure coordination. |
| POC-REP-17-24 | Independent application security assessment and adversarial review. |

**Vulnerability remediation objectives (proposed, not SLAs):** Critical 24 hours; High 7 calendar days; Medium 30 calendar days; Low 90 calendar days. Validate triage, contextual prioritisation, escalation, compensating controls, exception expiry, overdue handling and retest. Active exploitation or material exposure may require immediate action. Critical findings require immediate escalation and assessment of suspension/containment. Do not downgrade severity to meet a target.

**Execution boundary:** Testing must be explicitly authorised and scoped. No live penetration testing, external target testing, production scanning, live customer-data processing or production changes are authorised by this architecture decision. Tool selection, installation, subscriptions and CI/CD activation remain separately gated. All POC-REP-17 tests remain **Not Run**.
