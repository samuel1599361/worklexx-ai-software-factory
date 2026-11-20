# WORKLEXX AI SOFTWARE FACTORY
# RISK REGISTER

## Document Metadata

| Field | Value |
|---|---|
| Document Title | Risk Register |
| Document ID | WLX-ARCH-011 |
| Version | 1.0 |
| Status | Proposed — Phase 0 |
| Classification | Internal |
| Platform | Worklexx AI Software Factory |
| Repository | https://github.com/samuel1599361/worklexx-ai-software-factory |
| Parent Phase | Phase 0 — Architecture and Planning |
| Document Owner | Project Owner — appointment/confirmation pending |
| Risk Acceptance Authority | Project Owner — sole risk acceptance authority during the initial governance phase; no delegation currently authorised (HD-07, 2026-11-19) |
| Review Frequency | At least monthly during active implementation, and after material changes or incidents |
| Related Documents | Architecture Overview, System Architecture, Technology Stack, Repository Structure, Agent Ecosystem, Service Boundaries, Database Architecture, Security Architecture, Deployment Architecture, Development Roadmap, ADR Register, Phase 0 Inspection Report, Testing Strategy, Monitoring and Observability, Cost and Scalability |
| Approval Status | Not formally approved |

---

## 1. Purpose

This Risk Register identifies, describes, evaluates, and tracks risks that may affect the design, development, security, operation, financial integrity, compliance, and delivery of the Worklexx AI Software Factory.

It provides a structured mechanism for:

- Identifying technical, operational, security, financial, legal, privacy, and delivery risks.
- Evaluating risk likelihood and impact.
- Recording proposed preventive and corrective controls.
- Assigning risk and control ownership.
- Tracking mitigation actions and evidence.
- Recording residual risk after controls have been implemented and tested.
- Escalating risks that exceed approved tolerance.
- Supporting informed human decisions at project approval gates.

This document is a planning and governance instrument. It does not establish that any proposed control has been implemented or independently validated.

## 2. Scope

The register covers risks relating to:

1. Platform architecture and service boundaries.
2. Identity, authentication, authorisation, and tenant isolation.
3. AI agents, orchestration, model integration, and tool execution.
4. Multimodal processing and file handling.
5. Sandboxed code execution.
6. Database integrity, data protection, and recovery.
7. Financial transactions, billing, and ledger operations.
8. Advertising technology and data separation.
9. GitHub, source-code, and software supply-chain security.
10. Cloud infrastructure, deployment, and availability.
11. Privacy, regulatory compliance, and cross-border data transfers.
12. Human approvals, privileged access, and operational governance.
13. Delivery timelines, costs, dependencies, and resource constraints.

The register is intended to evolve as architecture decisions are approved, implementation evidence becomes available, and new risks are identified.

## 3. Risk Management Principles

The following principles govern this register:

- **Prevention:** Identify and address risks before implementation wherever practicable.
- **Least privilege:** Grant users, agents, services, and infrastructure only the permissions required for their responsibilities.
- **Separation of duties:** Separate sensitive approval, execution, financial, and administrative responsibilities.
- **Defence in depth:** Do not rely on a single security or operational control.
- **Human accountability:** AI agents may identify, assess, recommend, and coordinate risk responses, but must not assume unauthorised risk acceptance authority.
- **Evidence-based assurance:** A control is not considered effective merely because it appears in an architecture document.
- **Continuous reassessment:** Reassess risks after significant changes, incidents, new integrations, and changes in regulatory obligations.
- **Explicit residual-risk acceptance:** Residual risk must be documented and accepted by an appropriately authorised human decision-maker.

## 4. Risk Identification and Classification

Each risk receives a unique identifier in the format `RSK-NN`.

Risks are classified under the following categories:

| Category | Description |
|---|---|
| Architecture | System design, component boundaries, dependencies, and scalability |
| Security | Threats to confidentiality, integrity, availability, and access control |
| Identity and Access | Authentication, authorisation, sessions, and privilege management |
| AI and Agent Safety | Prompt injection, unsafe tool use, model behaviour, and agent permissions |
| Data and Privacy | Data integrity, privacy, retention, and regulatory obligations |
| Financial | Billing, payment, ledger, fraud, and reconciliation |
| Infrastructure | Cloud services, deployment, availability, and disaster recovery |
| Supply Chain | Source code, dependencies, build systems, and software provenance |
| Operational | Monitoring, incident response, service management, and recovery |
| Compliance and Legal | Applicable laws, contractual obligations, licensing, and intellectual property |
| Project Delivery | Resources, schedule, cost, dependencies, and governance |

A risk may belong to more than one category.

## 5. Risk Assessment Method

Risks are assessed using a five-point likelihood scale and a five-point impact scale.

### 5.1 Likelihood

| Score | Rating | Description |
|---:|---|---|
| 1 | Rare | Highly unlikely under expected operating conditions |
| 2 | Unlikely | Could occur, but is not expected frequently |
| 3 | Possible | Could reasonably occur during the project or operation |
| 4 | Likely | Expected to occur in relevant circumstances |
| 5 | Almost Certain | Expected to occur repeatedly or imminently without intervention |

### 5.2 Impact

| Score | Rating | Description |
|---:|---|---|
| 1 | Insignificant | Minor inconvenience with negligible operational effect |
| 2 | Minor | Limited disruption, readily recoverable |
| 3 | Moderate | Material service, financial, delivery, or compliance impact |
| 4 | Major | Serious disruption, significant loss, or substantial exposure |
| 5 | Severe | Critical business, security, safety, financial, or legal consequences |

Impact assessment should consider the most significant credible consequence, including:

- Customer and tenant harm.
- Confidentiality and privacy exposure.
- Financial loss or ledger corruption.
- Service unavailability.
- Legal or regulatory consequences.
- Intellectual property exposure.
- Reputational damage.
- Recovery time and operational disruption.

### 5.3 Risk Score

The risk score is calculated as:

**Risk Score = Likelihood × Impact**

| Score | Rating | Required Management Response |
|---:|---|---|
| 1–5 | Low | Monitor and manage through routine controls |
| 6–11 | Medium | Document mitigation and review periodically |
| 12–19 | High | Prioritised mitigation, assigned ownership, and escalation |
| 20–25 | Critical | Immediate escalation and an explicit decision before the affected activity proceeds |

A numerical score does not override professional judgement. A risk with severe consequences may require escalation even where its calculated score is lower.

### 5.4 Inherent and Residual Risk

- **Inherent risk** is the estimated exposure before considering the effectiveness of controls.
- **Residual risk** is the remaining exposure after implemented and tested controls have been evaluated.
- **Target risk** is the intended exposure following planned mitigation.

Proposed controls must not be used to claim a reduced residual score before implementation and validation.

The likelihood and impact scores in this register are not treated as final approved assessments unless explicitly reviewed and recorded.

## 6. Risk Status Definitions

| Status | Meaning |
|---|---|
| Identified | Risk has been recorded but not fully assessed |
| Assessing | Likelihood, impact, and exposure are being evaluated |
| Open | Risk requires monitoring or mitigation |
| Mitigation Planned | Response actions have been identified but not completed |
| In Progress | Approved mitigation work is underway |
| Monitoring | Controls have been implemented and the remaining exposure is being monitored |
| Accepted | An authorised decision-maker has explicitly accepted the documented residual risk |
| Closed | Evidence supports closure and the designated authority has confirmed it |
| Escalated | Risk requires a higher-level decision or intervention |

A risk must not be marked Accepted or Closed solely because an AI agent recommends that status.

## 7. Risk Ownership and Accountability

Each risk should have:

- A named risk owner.
- A control owner where controls are assigned separately.
- A mitigation action owner where execution is delegated.
- A review date.
- A target completion date.
- A documented status.
- Supporting evidence.
- An escalation route.
- A residual-risk assessment.
- An authorised acceptance record where acceptance is required.

The Project Owner is the sole risk acceptance authority during the initial Worklexx AI Software Factory governance phase, as approved under HD-07 on 2026-11-19. No delegated risk acceptance authority is currently established. This does not prevent written delegation of risk assessment, investigation, control ownership, mitigation execution, monitoring, or reporting; such delegation does not include accepting residual risk or approving a gated activity.

### 7.1 Risk Acceptance Authority and Limits

- **Low (score 1–5):** The Project Owner may accept documented residual risk after reviewing the assessment, controls, evidence, rationale, and review date.
- **Medium (score 6–11):** The Project Owner may accept documented residual risk with a mitigation plan, accountable owners, monitoring conditions, and a review date.
- **High (score 12–19):** Acceptance is reserved to the Project Owner and requires written justification, documented alternatives, and relevant independent specialist review (for example, security, privacy, legal, financial, safety, or operational review as applicable) before a decision.
- **Critical (score 20–25):** No routine residual-risk acceptance is authorised under this initial model. The affected activity must be stopped, suspended, or not started while the risk is escalated. Prioritise avoidance, elimination, or substantial reduction. Any proposed exceptional governance route requires a separate explicit human decision and cannot waive mandatory legal, regulatory, security, or safety obligations.

The following matters require escalation and specialist review regardless of numerical score where applicable: suspected or actual regulatory breach; unlawful processing or cross-border transfer; personal-data exposure; cross-tenant data leakage; financial ledger corruption or unauthorised balance mutation; sandbox escape or production-credential compromise; unauthorised privileged access or approval-control circumvention; material customer safety risk; and irreversible data loss or failure to preserve legally required records.

Every risk acceptance record must identify the risk; inherent and residual likelihood, impact, and scores; implemented controls and evidence; affected stakeholders; mitigation alternatives; rationale for acceptance; accepting person's identity and authority; decision date; expiry or review date; conditions and monitoring; and triggers for withdrawal or reassessment. Acceptance must be time-limited and revisited after material incidents, architecture or threat changes, changes in legal obligations, or evidence that controls are ineffective.

Risk acceptance is distinct from activity authorisation and gate approval. Accepting residual risk does not authorise or bypass Phase 1, production deployment, protected GitHub operations, database migrations, external integrations, financial commitments, or any other controlled activity. Applicable approval gates and separate authorisations remain mandatory.

AI agents may identify, assess, summarise, recommend, monitor, and prepare risk records. They must not accept risk, approve an exception, or impersonate an authorised human decision-maker.

## 8. Risk Register Summary

The following 28 risks form the current Phase 0 register, including subsequent additions RSK-26 through RSK-28.

| ID | Risk | Category | Initial Priority |
|---|---|---|---|
| RSK-01 | Architectural complexity and integration failure | Architecture | To be assessed |
| RSK-02 | Service boundary violations and uncontrolled coupling | Architecture | To be assessed |
| RSK-03 | Infrastructure capacity, availability, and scalability failure | Infrastructure | To be assessed |
| RSK-04 | Workflow orchestration and distributed transaction failure | Operational | To be assessed |
| RSK-05 | AI model dependency, availability, and performance risk | AI and Agent Safety | To be assessed |
| RSK-06 | Multimodal processing and malicious file exposure | Security | To be assessed |
| RSK-07 | Payment fraud, disputes, and payment-provider limitations | Financial | To be assessed |
| RSK-08 | Copyright, intellectual property, and generated-content infringement | Compliance and Legal | To be assessed |
| RSK-09 | Sandbox escape or unsafe execution | Security | To be assessed |
| RSK-10 | Data loss, corruption, and inadequate recovery | Data and Infrastructure | To be assessed |
| RSK-11 | Software supply-chain and dependency compromise | Supply Chain | To be assessed |
| RSK-12 | Advertising data misuse, privacy exposure, and click fraud | Data and Privacy | To be assessed |
| RSK-13 | Model catalogue changes and provider integration obsolescence | AI and Architecture | To be assessed |
| RSK-14 | Project schedule, resource, and cost overrun | Project Delivery | To be assessed |
| RSK-15 | Monitoring, alerting, and incident detection deficiencies | Operational | Medium — score 10 |
| RSK-16 | Inadequate governance, approvals, or change control | Operational | To be assessed |
| RSK-17 | Third-party service and vendor dependency failure | Architecture and Operational | To be assessed |
| RSK-18 | Cross-tenant data leakage or isolation bypass | Security and Data | To be assessed |
| RSK-19 | Identity compromise, session abuse, or privilege escalation | Identity and Access | To be assessed |
| RSK-20 | Prompt injection and unauthorised agent tool execution | AI and Agent Safety | To be assessed |
| RSK-21 | Backup, restoration, and disaster recovery failure | Infrastructure and Data | To be assessed |
| RSK-22 | Human approval bypass, tampering, or replay | Security and Governance | To be assessed |
| RSK-23 | Privacy, regulatory, and cross-border data-transfer non-compliance | Compliance and Legal | To be assessed |
| RSK-24 | Ledger inconsistency or unauthorised financial balance mutation | Financial and Data | To be assessed |
| RSK-25 | Insider threat and privileged-access abuse | Security and Operational | To be assessed |
| RSK-26 | Uncontrolled or unsafe database schema migration | Data Integrity and Operational | To be assessed |
| RSK-27 | Repository backup failure, incomplete recovery, or cross-tenant restoration | Operational Resilience and Security | To be assessed |
| RSK-28 | Compromised build workflow, dependency, credential or untrusted artifact | Supply Chain and Security | To be assessed |

The initial priority column is a planning classification, not a completed risk assessment. RSK-15 retains its previously identified score of 10, which maps to Medium under the scoring method in Section 5. Any decision to apply a higher severity override must be explicitly documented and approved.

---

## 9. Detailed Risk Register

### RSK-01 — Architectural Complexity and Integration Failure

**Category:** Architecture

**Risk statement:** The platform's multiple frontend applications, backend services, agents, infrastructure components, and external integrations may become difficult to coordinate, resulting in integration failures, duplicated capabilities, performance bottlenecks, or excessive maintenance costs.

**Potential causes:**
- Unresolved architecture decisions.
- Inconsistent interface contracts.
- Uncontrolled expansion of components.
- Unclear ownership of shared capabilities.
- Incompatible service versions.
- Insufficient integration testing.

**Potential consequences:**
- Delayed delivery.
- Unreliable workflows.
- Increased operating costs.
- Difficult troubleshooting.
- Rework across multiple services.

**Proposed controls:**
- Maintain approved architecture and service-boundary documents.
- Use versioned API contracts and compatibility testing.
- Maintain a dependency register.
- Prevent undocumented additional deployable services.
- Require architecture review for material design changes.
- Validate integration assumptions through controlled proofs of concept.

**Monitoring indicators:** Contract-test failures, integration defects, dependency conflicts, repeated interface changes, and unplanned service proliferation.

**Accountability:** Architecture owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Likelihood, impact, and residual risk require formal assessment.

### RSK-02 — Service Boundary Violations and Uncontrolled Coupling

**Category:** Architecture

**Risk statement:** Services or agents may access data or execute responsibilities outside their authorised boundaries, creating hidden dependencies and weakening security, maintainability, and accountability.

**Potential causes:**
- Shared database access without controlled ownership.
- Direct service-to-service access that bypasses approved interfaces.
- Agents performing deterministic business functions.
- Uncontrolled internal APIs.
- Introduction of additional deployable services without architecture approval.

**Potential consequences:**
- Inconsistent business rules.
- Privilege escalation.
- Data integrity problems.
- Difficult upgrades and incident containment.

**Proposed controls:**
- Maintain six approved deployable backend service units as the architectural baseline.
- Treat the 23 agents as logical modules, not 23 independently deployed microservices.
- Enforce service identity and least-privilege access.
- Document API ownership and data ownership.
- Use contract testing and architecture conformance checks.
- Keep AI model routing as a logical capability rather than introducing an undocumented seventh deployable service.

**Monitoring indicators:** Unapproved service additions, direct database access, undocumented API dependencies, and boundary violations.

**Accountability:** Architecture owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-03 — Infrastructure Capacity, Availability, and Scalability Failure

**Category:** Infrastructure

**Risk statement:** Cloud infrastructure or hosting services may fail to meet platform demand, resulting in slow responses, service outages, resource exhaustion, or unpredictable operating costs.

**Potential causes:**
- Inadequate capacity planning.
- Incorrect autoscaling configuration.
- Runtime limitations.
- Regional outages.
- Resource-intensive AI workloads.
- Insufficient load and stress testing.

**Potential consequences:**
- Service unavailability.
- Failed or delayed user workflows.
- Increased cloud expenditure.
- Customer dissatisfaction.
- Loss of revenue.

**Proposed controls:**
- Establish workload-specific capacity requirements.
- Conduct load, stress, soak, and failure testing.
- Separate long-running workloads from request-response frontend runtimes.
- Define resource quotas, autoscaling limits, and cost alerts.
- Monitor service latency, saturation, error rates, and availability.
- Validate deployment and recovery behaviour under failure conditions.

**Monitoring indicators:** CPU and memory saturation, queue growth, latency, error rates, autoscaling failures, and cloud expenditure anomalies.

**Accountability:** Infrastructure owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-04 — Workflow Orchestration and Distributed Transaction Failure

**Category:** Operational

**Risk statement:** Distributed workflows may become inconsistent or fail during retries, cancellations, timeouts, worker failures, or external service outages.

**Potential causes:**
- Assuming exactly-once execution of external side effects.
- Non-idempotent activity implementations.
- Inadequate retry and timeout policies.
- Missing compensation logic.
- Inadequate dead-letter handling.
- Loss of durable workflow state.

**Potential consequences:**
- Duplicate transactions.
- Incomplete bookings or orders.
- Stuck workflows.
- Inconsistent business records.
- Difficult manual recovery.

**Proposed controls:**
- Evaluate Temporal through a proof of concept before selecting Cloud or self-hosted deployment.
- Design for at-least-once activity execution.
- Use idempotency keys for external side effects.
- Implement bounded retries, timeouts, cancellation, and compensation.
- Use durable workflow state and explicit recovery procedures.
- Implement outbox/inbox patterns where required.
- Establish dead-letter queues and manual recovery procedures.
- Reconcile external provider state with internal records.

**Monitoring indicators:** Retry rates, duplicate-operation detection, stuck workflows, failed compensations, and unreconciled transactions.

**Accountability:** Workflow engineering owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-05 — AI Model Dependency, Availability, and Performance Risk

**Category:** AI and Agent Safety

**Risk statement:** Dependence on external or internally hosted AI models may cause service interruption, unpredictable performance, cost increases, model behaviour changes, or inconsistent outputs.

**Potential causes:**
- Provider outages.
- Model deprecation.
- Rate limits.
- Pricing changes.
- Context-window or capability changes.
- Inadequate fallback arrangements.
- Model-specific prompt or tool incompatibility.

**Potential consequences:**
- Failed agent workflows.
- Reduced output quality.
- Higher operating costs.
- Service interruption.
- Inconsistent user experience.

**Proposed controls:**
- Maintain a capability-based model catalogue.
- Track provider, model identifier, version, supported modalities, limits, and pricing.
- Use controlled routing and fallback policies.
- Test model changes against representative evaluation datasets.
- Establish provider timeout, retry, and circuit-breaker policies.
- Avoid hardcoding stale model identifiers throughout the application.
- Monitor model performance, cost, and availability.

**Monitoring indicators:** Provider errors, latency, token consumption, cost per workflow, evaluation drift, and model deprecation notices.

**Accountability:** AI platform owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-06 — Multimodal Processing and Malicious File Exposure

**Category:** Security

**Risk statement:** Uploaded or captured images, audio, video, documents, and other files may contain malicious payloads, unsafe content, malformed data, or sensitive information that is improperly exposed during processing.

**Potential causes:**
- Treating uploaded files as trusted.
- Inadequate file validation.
- Vulnerable parsers and media libraries.
- Excessive file sizes or decompression.
- Insecure temporary storage.
- Cross-tenant access to uploaded assets.

**Potential consequences:**
- Malware execution.
- Data leakage.
- Service disruption.
- Unauthorised access to private files.
- Increased infrastructure costs.

**Proposed controls:**
- Treat new uploads as pending or quarantined until validated.
- Validate file signatures, MIME types, sizes, and permitted formats.
- Apply malware scanning and safe processing pipelines.
- Use isolated processing environments.
- Restrict temporary-file access and retention.
- Apply tenant-aware object storage permissions.
- Use short-lived, scoped signed URLs where appropriate.
- Record processing provenance and security outcomes.

**Monitoring indicators:** Malware detections, rejected uploads, parser failures, abnormal processing resource use, and access-control violations.

**Accountability:** Multimodal service owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-07 — Payment Fraud, Disputes, and Payment-Provider Limitations

**Category:** Financial

**Risk statement:** Payment fraud, chargebacks, disputes, provider outages, or limitations in payment-provider controls may result in financial loss, delayed settlement, or inaccurate payment status.

**Potential causes:**
- Stolen payment credentials.
- Account takeover.
- Disputed transactions.
- Inadequate transaction verification.
- Provider API failures.
- Incorrect assumptions about provider fraud-detection capabilities.
- Poor reconciliation between provider and internal records.

**Potential consequences:**
- Direct financial loss.
- Chargeback fees.
- Customer disputes.
- Incorrect account balances.
- Delayed settlement.
- Regulatory or contractual exposure.

**Proposed controls:**
- Assess the actual capabilities and contractual terms of each payment provider.
- Do not assume Paystack offers controls equivalent to Stripe Radar or any other provider-specific product.
- Implement provider-scoped idempotency.
- Verify payment status using authenticated provider mechanisms.
- Use signed webhook verification and replay protection.
- Establish risk-based transaction monitoring.
- Define dispute evidence, escalation, and response procedures.
- Reconcile provider settlement records with the internal ledger.
- Define fraud thresholds and monitoring windows using documented data and approved policy.

**Monitoring indicators:** Chargeback rate, disputed transaction value, failed payments, webhook verification failures, settlement differences, and suspicious transaction patterns.

**Accountability:** Finance and payments owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-08 — Copyright, Intellectual Property, and Generated-Content Infringement

**Category:** Compliance and Legal

**Risk statement:** User inputs, uploaded materials, source code, generated outputs, or training and reference data may contain copyrighted, licensed, confidential, or otherwise protected material that is used or distributed without appropriate rights.

**Potential causes:**
- Unlicensed source material.
- Inadequate provenance records.
- Generated outputs resembling protected works.
- Users uploading third-party confidential material.
- Misuse of open-source software.
- Overreliance on prompt restrictions or similarity filters.

**Potential consequences:**
- Copyright or licensing disputes.
- Injunctions or takedown demands.
- Financial liability.
- Loss of customer trust.
- Restrictions on product distribution.

**Proposed controls:**
- Maintain source and content provenance records.
- Define acceptable-use and user-content policies.
- Track open-source licences and obligations.
- Apply appropriate similarity and policy screening.
- Provide takedown and complaint procedures.
- Require legal review for material licensing and distribution questions.
- Do not treat a so-called clean-room prompt as sufficient copyright protection.
- Record the origin, licence, permissions, and processing purpose of relevant datasets and assets.

**Monitoring indicators:** Copyright complaints, takedown requests, licence exceptions, provenance gaps, and repeated similarity-screening alerts.

**Accountability:** Legal and compliance owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-09 — Sandbox Escape or Unsafe Execution

**Category:** Security

**Risk statement:** Code or commands executed by the sandbox may escape intended isolation, access unauthorised resources, compromise the host, or consume excessive resources.

**Potential causes:**
- Vulnerabilities in isolation technology.
- Unsafe container configuration.
- Excessive permissions.
- Unrestricted network access.
- Cloud metadata access.
- Weak filesystem isolation.
- Resource exhaustion.
- Inadequate cleanup of execution environments.

**Potential consequences:**
- Host compromise.
- Cross-tenant exposure.
- Credential theft.
- Data exfiltration.
- Infrastructure disruption.
- Significant financial loss.

**Proposed controls:**
- Evaluate gVisor and alternative microVM-based isolation approaches.
- Do not treat gVisor or any single sandbox technology as escape-proof.
- Apply non-root execution and least privilege.
- Deny unnecessary network egress by default.
- Restrict cloud metadata and sensitive internal endpoints.
- Apply CPU, memory, disk, process, and execution-time limits.
- Use short-lived credentials with narrowly scoped permissions.
- Enforce filesystem restrictions and environment cleanup.
- Perform adversarial escape and isolation testing before production use.

**Monitoring indicators:** Unexpected network connections, abnormal process activity, resource-limit violations, suspicious filesystem access, and sandbox termination events.

**Accountability:** Sandbox security owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-10 — Data Loss, Corruption, and Inadequate Recovery

**Category:** Data and Infrastructure

**Risk statement:** Platform data may be lost, corrupted, deleted, or rendered unavailable because of software defects, operator errors, infrastructure failures, malicious activity, or inadequate backup and recovery arrangements.

**Potential causes:**
- Failed database operations.
- Incorrect migrations.
- Accidental deletion.
- Backup failures.
- Corrupted storage.
- Ransomware or destructive access.
- Inadequate recovery testing.

**Potential consequences:**
- Loss of customer records.
- Incomplete business transactions.
- Financial and audit inconsistencies.
- Extended service interruption.
- Legal and contractual exposure.

**Proposed controls:**
- Establish approved backup policies.
- Test database and object-storage restoration.
- Define and approve RPO and RTO targets.
- Protect backups with appropriate access restrictions and encryption.
- Maintain backup integrity and restoration evidence.
- Include workflow state, Git assets, object storage, ledger records, identity configuration, KMS dependencies, and infrastructure configuration in recovery planning.
- Test recovery of dependent systems as a complete platform.
- Ensure restored backups do not unintentionally reintroduce data that was validly deleted or placed under a legal hold.

**Monitoring indicators:** Backup failures, restoration-test results, replication lag, data-integrity alerts, and recovery time.

**Accountability:** Database and infrastructure owners to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending. Tiered architectural RPO/RTO objectives were approved under HD-06 on 2026-11-19; achievement remains unverified and depends on POC-15, operational validation, and tested recovery controls.

### RSK-11 — Software Supply-Chain and Dependency Compromise

**Category:** Supply Chain

**Risk statement:** Vulnerable, malicious, compromised, or incorrectly maintained third-party packages and build dependencies may introduce security vulnerabilities or compromise software integrity.

**Potential causes:**
- Dependency confusion.
- Typosquatting.
- Compromised package registries.
- Malicious maintainer activity.
- Unpinned dependencies.
- Unverified build artifacts.
- Inadequate vulnerability monitoring.

**Potential consequences:**
- Remote code execution.
- Credential exposure.
- Supply-chain compromise.
- Data theft.
- Unauthorised software changes.
- Service disruption.

**Proposed controls:**
- Pin dependencies and maintain reproducible lockfiles.
- Generate and retain Software Bills of Materials.
- Scan dependencies and container images.
- Verify package provenance and integrity where supported.
- Use signed build artifacts and build provenance.
- Restrict package installation to approved sources.
- Review new and changed dependencies.
- Establish an exception process for vulnerable or restricted packages.
- Treat package-age rules, including blocking packages published within the previous seven days, as limited heuristics rather than reliable security controls.
- Use hash verification and provenance checks in addition to package-age policies.

**Monitoring indicators:** Critical vulnerability alerts, unexpected dependency changes, package provenance failures, and unsigned or unverified artifacts.

**Accountability:** DevSecOps owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-12 — Advertising Data Misuse, Privacy Exposure, and Click Fraud

**Category:** Data and Privacy

**Risk statement:** Advertising and monetisation features may process personal or sensitive information improperly, expose confidential platform data, or become targets for fraudulent traffic and invalid advertising activity.

**Potential causes:**
- Unauthorised access to private prompts or uploads.
- Excessive collection of identifiers.
- Inadequate consent or transparency.
- Invalid clicks and automated traffic.
- Unsafe advertisements or landing pages.
- Incorrect assumptions that hashed identifiers are anonymous.
- Weak advertiser verification.

**Potential consequences:**
- Privacy violations.
- Regulatory action.
- Advertiser disputes.
- Financial loss.
- Reputational damage.
- Exposure of confidential customer information.

**Proposed controls:**
- Keep `adtech-service` separate from private application data.
- Restrict Agent23 and advertising components to explicitly authorised public or appropriately aggregated data.
- Prohibit access to private prompts, source code, uploads, credentials, and confidential activity.
- Enforce service identity, network, schema, and database-role separation.
- Apply data minimisation and purpose limitation.
- Assess consent, legal basis, retention, and disclosure requirements.
- Treat salted or hashed IP addresses as potentially pseudonymous personal data, not automatically anonymous data.
- Review advertiser identity, creative content, landing pages, and prohibited categories.
- Apply click-fraud detection and invalid-traffic controls.
- Review the applicable terms and permitted uses of any external safe-browsing or reputation API.

**Monitoring indicators:** Unauthorised data access, invalid click rates, suspicious traffic, advertiser complaints, privacy requests, and data-retention exceptions.

**Accountability:** Advertising and privacy owners to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-13 — Model Catalogue Changes and Provider Integration Obsolescence

**Category:** AI and Architecture

**Risk statement:** Model identifiers, API versions, capabilities, pricing, or provider interfaces may change or become unavailable, causing failures in agent workflows and inconsistent model selection.

**Potential causes:**
- Provider deprecation.
- Model replacement.
- API changes.
- Capability changes.
- Pricing changes.
- Inadequate compatibility testing.

**Potential consequences:**
- Agent workflow failures.
- Increased inference cost.
- Reduced output quality.
- Unplanned engineering work.
- Service interruption.

**Proposed controls:**
- Maintain a central, capability-based model catalogue.
- Track model and provider versions.
- Separate model selection policy from agent business logic.
- Maintain fallback and deprecation procedures.
- Test model changes using representative evaluation datasets.
- Record model configuration and relevant provenance for reproducibility.
- Avoid relying on hardcoded model IDs without lifecycle management.

**Monitoring indicators:** Deprecation notices, API errors, model-routing failures, cost changes, and evaluation regressions.

**Accountability:** AI platform owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-14 — Project Schedule, Resource, and Cost Overrun

**Category:** Project Delivery

**Risk statement:** The project may exceed planned delivery dates, available resources, or approved budgets because of technical complexity, external dependencies, changing requirements, or inadequate estimation.

**Potential causes:**
- Unresolved human decisions.
- Scope expansion.
- Limited engineering capacity.
- Integration delays.
- Unexpected cloud or AI costs.
- Rework caused by architecture changes.
- Vendor dependency delays.

**Potential consequences:**
- Delayed milestones.
- Reduced delivery quality.
- Budget overruns.
- Deferred features.
- Operational readiness gaps.

**Proposed controls:**
- Maintain a phase-based roadmap with explicit acceptance criteria.
- Separate estimates from approved commitments.
- Track scope, dependencies, risks, and resource requirements.
- Establish change-control procedures.
- Require cost estimates and approval before spending commitments.
- Use milestone reviews and evidence-based progress reporting.
- Reassess delivery dates after material changes.

**Monitoring indicators:** Schedule variance, cost variance, unresolved dependencies, resource gaps, and scope-change volume.

**Accountability:** Project Manager or designated delivery owner.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending. Roadmap dates are indicative, not approved delivery commitments.

### RSK-15 — Monitoring, Alerting, and Incident Detection Deficiencies

**Category:** Operational

**Risk statement:** Inadequate monitoring, logging, alerting, or incident-detection capability may delay identification and response to security, reliability, performance, or financial incidents.

**Potential causes:**
- Missing telemetry.
- Inadequate alert thresholds.
- Poor log correlation.
- Incomplete service coverage.
- Excessive alert noise.
- Inadequate incident ownership.
- Insufficient retention or access controls for logs.

**Potential consequences:**
- Longer incident duration.
- Delayed containment.
- Increased operational losses.
- Undetected unauthorised activity.
- Reduced auditability.

**Proposed controls:**
- Define platform-wide logging, metrics, and tracing requirements.
- Establish service-level indicators and alert thresholds.
- Correlate events using trace and workflow identifiers.
- Protect logs from unauthorised modification and access.
- Define incident severity and escalation procedures.
- Test incident response and alert delivery.
- Establish audit logging for privileged actions, approvals, financial events, and sensitive data access.

**Monitoring indicators:** Alert coverage, detection delay, response time, uncorrelated events, missing logs, and incident recurrence.

**Accountability:** Site Reliability Engineering or operational owner to be designated.

**Status:** Open — mitigation planned.

**Initial assessment:** Score 10 — Medium, based on the existing Phase 0 assessment. This score is provisional and must be validated. Any severity override must be explicitly documented and approved.

### RSK-16 — Inadequate Governance, Approvals, or Change Control

**Category:** Operational

**Risk statement:** Unclear authority, incomplete approvals, or uncontrolled changes may result in unauthorised implementation, deployment, financial commitments, or changes to protected resources.

**Potential causes:**
- Ambiguous approval-gate definitions.
- Unclear role assignments.
- Approval not bound to a specific action or artifact.
- Uncontrolled changes after approval.
- Inadequate audit records.
- Confusion between technical access and approval authority.

**Potential consequences:**
- Unauthorised deployments.
- Unapproved expenditure.
- Loss of source-code integrity.
- Security incidents.
- Governance disputes.
- Untraceable decisions.

**Proposed controls:**
- Define approval authority and gate criteria.
- Separate GATE-03 production deployment approval from GATE-04 protected GitHub operations approval.
- Bind approvals to the specific action, project or tenant, artifact or commit digest, environment, authorised approver, and expiry.
- Invalidate approvals after material changes.
- Use replay-resistant and single-use approvals where applicable.
- Retain approval evidence and audit records.
- Do not assume that Owner or Administrator status automatically grants authority for every approval gate.
- Keep unresolved GATE-01, GATE-02, GATE-05, and GATE-06 definitions pending explicit decisions.

**Monitoring indicators:** Approval exceptions, unapproved changes, expired approvals, bypass attempts, and missing audit records.

**Accountability:** Project governance owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-17 — Third-Party Service and Vendor Dependency Failure

**Category:** Architecture and Operational

**Risk statement:** Failure, compromise, discontinuation, contractual change, or performance degradation of third-party services may affect platform functionality or expose the platform to operational and compliance risks.

**Potential causes:**
- Vendor outages.
- Contract changes.
- API deprecation.
- Provider account suspension.
- Regional restrictions.
- Vendor security incidents.
- Inadequate exit arrangements.

**Potential consequences:**
- Service interruption.
- Data access or processing disruption.
- Increased costs.
- Customer dissatisfaction.
- Vendor lock-in.
- Compliance exposure.

**Proposed controls:**
- Maintain a third-party dependency inventory.
- Record service owners, data processed, contractual terms, and criticality.
- Review vendor security and privacy documentation.
- Define fallback and business-continuity arrangements.
- Monitor service availability and API changes.
- Establish exit and migration strategies for critical dependencies.
- Review data-processing agreements and applicable transfer obligations.

**Monitoring indicators:** Vendor incidents, service-level breaches, contract changes, API deprecation, and dependency concentration.

**Accountability:** Vendor and procurement owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-18 — Cross-Tenant Data Leakage or Isolation Bypass

**Category:** Security and Data

**Risk statement:** A user, agent, worker, service, or administrator may access or modify data belonging to another tenant because tenant isolation is missing, misconfigured, bypassed, or inconsistently enforced.

**Potential causes:**
- Inadequate PostgreSQL Row-Level Security.
- Missing tenant filters.
- Unsafe connection pooling.
- Privileged database roles bypassing policies.
- Incorrect object-storage permissions.
- Cross-tenant Git or sandbox access.
- Insecure background jobs.
- Tenant context injection or confusion.

**Potential consequences:**
- Confidential data exposure.
- Unauthorised data modification.
- Regulatory violations.
- Loss of customer trust.
- Financial and legal liability.

**Proposed controls:**
- Apply PostgreSQL Row-Level Security to tenant-owned data.
- Use restricted application roles and FORCE ROW LEVEL SECURITY where appropriate.
- Use transaction-scoped tenant context.
- Validate tenant identity at trusted service boundaries.
- Use composite tenant-aware foreign keys where appropriate.
- Prevent pooled database connections from retaining another tenant's context.
- Do not treat `app.current_tenant_id` alone as a security control.
- Enforce tenant isolation in object storage, Git operations, sandbox execution, caches, and workflow state.
- Conduct adversarial cross-tenant access tests.
- Verify that administrative and background-worker privileges cannot silently bypass isolation requirements.

**Monitoring indicators:** Cross-tenant access denials, unexpected tenant identifiers, RLS test failures, object-storage permission anomalies, and tenant-context mismatches.

**Accountability:** Security and database owners to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending. This risk requires explicit security review before production.

### RSK-19 — Identity Compromise, Session Abuse, or Privilege Escalation

**Category:** Identity and Access

**Risk statement:** An attacker may compromise an account, steal or misuse a session, exploit token-validation weaknesses, or obtain privileges beyond those authorised.

**Potential causes:**
- Weak authentication.
- Missing MFA for privileged roles.
- Insecure token validation.
- Session theft.
- Refresh-token reuse.
- Inadequate account recovery.
- Incorrect role or membership checks.
- Insecure redirect handling.

**Potential consequences:**
- Account takeover.
- Unauthorised data access.
- Privilege escalation.
- Administrative compromise.
- Financial fraud.
- Data destruction.

**Proposed controls:**
- Use a properly configured OIDC identity provider.
- Use Authorization Code with PKCE for applicable browser-based flows.
- Validate issuer, audience, expiry, not-before, subject, signing algorithm, and key identifiers.
- Reject unsecured or unsupported token algorithms.
- Apply MFA and stronger controls to privileged accounts.
- Rotate refresh tokens and detect reuse where supported.
- Protect sessions using secure cookie and CSRF controls.
- Use exact redirect URI validation and state/nonce protections.
- Separate identity-provider responsibilities from Worklexx organisation membership and application authorisation.
- Establish account recovery, revocation, and incident-response procedures.

**Monitoring indicators:** Failed logins, unusual session activity, token validation failures, privilege changes, and refresh-token reuse alerts.

**Accountability:** Identity and security owners to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-20 — Prompt Injection and Unauthorised Agent Tool Execution

**Category:** AI and Agent Safety

**Risk statement:** Malicious or misleading instructions contained in user inputs, uploaded files, external content, or tool outputs may manipulate an AI agent into disclosing information or executing unauthorised actions.

**Potential causes:**
- Treating untrusted content as trusted instructions.
- Excessive agent permissions.
- Weak tool authorisation.
- Inadequate separation between data and instructions.
- Unsafe chaining of agent outputs.
- Missing human approval for consequential actions.

**Potential consequences:**
- Data disclosure.
- Unauthorised transactions.
- Unsafe code execution.
- Privilege escalation.
- Destructive or fraudulent actions.
- Loss of user trust.

**Proposed controls:**
- Treat user content, external documents, retrieved content, and tool outputs as untrusted data.
- Enforce tool permissions outside the model.
- Use narrowly scoped agent identities and capabilities.
- Validate and authorise every consequential action at deterministic service boundaries.
- Require human approval for designated sensitive actions.
- Apply input and output validation.
- Separate confidential system instructions from user-controlled content.
- Test direct and indirect prompt-injection scenarios.
- Log tool calls and authorisation decisions.
- Do not expose private chain-of-thought; provide appropriate progress, tool activity, status, concise explanations, and results.

**Monitoring indicators:** Blocked unauthorised tool calls, prompt-injection test failures, suspicious tool sequences, and unexpected data-access attempts.

**Accountability:** AI safety and security owners to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-21 — Backup, Restoration, and Disaster Recovery Failure

**Category:** Infrastructure and Data

**Risk statement:** Backup and disaster recovery arrangements may be incomplete, untested, unavailable, or unable to restore the complete platform within approved recovery objectives.

**Potential causes:**
- Incomplete backup scope.
- Corrupt backups.
- Unavailable encryption keys.
- Missing infrastructure configuration.
- Unrestorable workflow state.
- Uncoordinated regional recovery.
- Failure to test restoration.
- Unclear recovery responsibilities.

**Potential consequences:**
- Extended outages.
- Permanent data loss.
- Inconsistent financial records.
- Failed business continuity.
- Regulatory and contractual consequences.

**Proposed controls:**
- Establish platform-wide recovery plans.
- Define RPO and RTO through explicit human decisions.
- Test restoration of databases, object storage, Git repositories, workflow state, and required configuration.
- Include identity, KMS, secrets, and infrastructure dependencies in recovery planning.
- Maintain protected and independently recoverable backup copies where appropriate.
- Test regional recovery and dependency ordering.
- Document restoration procedures and evidence.
- Test post-restoration integrity and reconciliation.
- Prevent deleted or legally restricted data from being inadvertently reintroduced through backup restoration.

**Monitoring indicators:** Backup completion, restore-test success, key-recovery readiness, replication health, and recovery-time measurements.

**Accountability:** Disaster recovery owner to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending. RPO and RTO remain unresolved decisions.

### RSK-22 — Human Approval Bypass, Tampering, or Replay

**Category:** Security and Governance

**Risk statement:** A sensitive action may proceed without valid approval, or an approval may be reused, altered, forged, or applied to a different action or artifact.

**Potential causes:**
- Weak approval-token design.
- Approval not bound to an artifact digest.
- Reuse of approval identifiers.
- Missing expiry or revocation.
- Material change after approval.
- Inadequate separation of approver and executor.
- Incomplete audit logging.

**Potential consequences:**
- Unauthorised production deployment.
- Unapproved GitHub operations.
- Unauthorised financial or administrative actions.
- Security compromise.
- Loss of accountability.

**Proposed controls:**
- Bind each approval to the exact action and scope.
- Include project or tenant, artifact or commit digest, environment, authorised approver, and expiry.
- Use unique, single-use approval identifiers where applicable.
- Prevent replay and detect duplicate approval use.
- Invalidate approval when the approved artifact or material scope changes.
- Enforce approver authority independently of the requester.
- Maintain tamper-evident approval records.
- Keep GATE-03 and GATE-04 independent.
- Require explicit decisions for the unresolved approval gates.

**Monitoring indicators:** Approval replay attempts, approval-scope mismatches, expired approvals, and unauthorised execution attempts.

**Accountability:** Security and governance owners to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-23 — Privacy, Regulatory, and Cross-Border Data-Transfer Non-Compliance

**Category:** Compliance and Legal

**Risk statement:** The platform may process, store, transfer, or disclose personal or regulated data without satisfying applicable legal, regulatory, contractual, or privacy requirements.

**Potential causes:**
- Unclear data-controller and processor responsibilities.
- Inadequate legal basis or consent.
- Excessive data collection.
- Uncontrolled international transfers.
- Incomplete retention and deletion policies.
- Inadequate vendor agreements.
- Failure to assess jurisdiction-specific obligations.

**Potential consequences:**
- Regulatory penalties.
- Litigation.
- Processing restrictions.
- Customer complaints.
- Contractual disputes.
- Reputational harm.

**Proposed controls:**
- Maintain a data inventory and processing-purpose register.
- Identify applicable jurisdictions and data-protection obligations.
- Assess controller and processor roles.
- Document lawful basis, consent where required, and transparency obligations.
- Review cross-border transfers and recipient safeguards.
- Assess applicable Nigerian data-protection requirements, including NDPA obligations, and other relevant jurisdictional requirements.
- Do not assume that standard contractual clauses, adequacy arrangements, or any single transfer mechanism automatically satisfies every transfer.
- Establish retention, deletion, access, correction, and data-subject request procedures.
- Review vendor processing agreements.
- Obtain qualified legal and privacy review before processing high-risk categories of data.

**Monitoring indicators:** Privacy complaints, overdue data requests, transfer-assessment gaps, retention exceptions, and regulatory changes.

**Accountability:** Data protection and legal owners to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

### RSK-24 — Ledger Inconsistency or Unauthorised Financial Balance Mutation

**Category:** Financial and Data

**Risk statement:** Financial records, balances, or transaction states may become inconsistent or be altered without proper authority, resulting in incorrect customer balances, inaccurate reporting, or financial loss.

**Potential causes:**
- Agent-controlled financial updates.
- Non-atomic posting.
- Duplicate payment processing.
- Mutable posted entries.
- Missing reconciliation.
- Weak transaction isolation.
- Inadequate audit history.
- Unauthorised administrative changes.

**Potential consequences:**
- Financial misstatement.
- Customer losses.
- Fraud.
- Payment disputes.
- Audit failure.
- Regulatory exposure.

**Proposed controls:**
- Make `billing-ledger` the deterministic financial authority.
- Restrict Agent21 to advisory and coordination responsibilities.
- Enforce atomic double-entry postings per transaction and currency.
- Use controlled draft-to-posted transitions.
- Make posted ledger entries immutable.
- Correct posted transactions through authorised compensating entries.
- Use provider-scoped idempotency.
- Reconcile internal records with payment-provider records.
- Enforce role separation and approval for sensitive adjustments.
- Retain audit records and protect financial history from cascading deletion.
- Define controlled retention, anonymisation, and legal-hold procedures.

**Monitoring indicators:** Ledger imbalance, duplicate posting, reconciliation differences, unauthorised adjustments, and failed posting transitions.

**Accountability:** Finance, database, and security owners to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending. Financial controls require validation before handling real funds.

### RSK-25 — Insider Threat and Privileged-Access Abuse

**Category:** Security and Operational

**Risk statement:** An employee, contractor, administrator, service operator, or other authorised individual may intentionally or accidentally misuse privileged access to expose, alter, destroy, or improperly transfer platform data or resources.

**Potential causes:**
- Excessive privileges.
- Shared accounts.
- Weak access reviews.
- Uncontrolled break-glass access.
- Inadequate separation of duties.
- Poor offboarding.
- Incomplete audit logging.
- Conflicts of interest.

**Potential consequences:**
- Data theft or destruction.
- Financial fraud.
- Unauthorised deployments.
- Security compromise.
- Service disruption.
- Legal and reputational harm.

**Proposed controls:**
- Apply least privilege and role-based access.
- Use individual identities and prohibit shared privileged accounts.
- Require MFA for privileged access.
- Review access periodically and after role changes.
- Implement prompt access revocation during offboarding.
- Record privileged actions in protected audit logs.
- Establish controlled break-glass procedures with justification, time limits, and retrospective review.
- Require dual control for designated high-impact operations.
- Separate approval, execution, and review responsibilities where practicable.
- Monitor unusual administrative activity.

**Monitoring indicators:** Privileged access changes, break-glass events, unusual data exports, unauthorised configuration changes, and access-review exceptions.

**Accountability:** Security and operations owners to be designated.

**Status:** Open — mitigation planned.

**Assessment:** Formal scoring pending.

---

### RSK-26 — Schema Migration Drift, Cross-Service Modification, or Unsafe Migration Execution

**Category:** Data Integrity, Security, and Operational Resilience

**Risk statement:** A service migration may alter another service's authoritative schema, execute with excessive privileges, conflict with another migration, break rolling-version compatibility, or cause data loss/inconsistency.

**Potential causes:**
- Shared or unrestricted migration credentials.
- A global migration history that obscures service ownership.
- Runtime credentials with DDL privileges.
- Concurrent migrations without effective locking.
- Unreviewed destructive changes or incomplete impact analysis.
- Incompatible schema and application release sequencing.
- Missing backup, PITR, integrity checks, or forward-fix planning.
- Tenant RLS or financial invariants unintentionally weakened during schema evolution.

**Potential consequences:**
- Cross-service data corruption or outage.
- Tenant-isolation failure or unauthorised data access.
- Failed releases and prolonged recovery.
- Lost, duplicated, or inconsistent financial records.
- Incomplete audit history and regulatory/contractual exposure.

**Proposed controls:**
- Enforce HD-REP-06 service-owned schemas and independent migration histories for all six backend services.
- Restrict each migration identity to its owned schema; remove DDL privileges from runtime identities.
- Use immutable migration identifiers/checksums, review, migration locks, bounded timeouts, and transactional execution where supported.
- Use expand-and-contract changes and validate compatibility across supported rolling application versions.
- Require impact analysis, backup/PITR readiness, integrity checks, and forward-fix/recovery plans.
- Apply GATE-05 to destructive migrations and applicable GATE-03 approval to production migration activity.
- Test cross-service schema boundaries, tenant RLS, failure recovery, and `billing-ledger` reconciliation.

**Monitoring indicators:** Migration checksum mismatch, migration lock conflicts, DDL attempts by runtime identities, cross-schema DDL attempts, failed migration rate, schema/application version incompatibility, restore-test failures, and ledger reconciliation differences.

**Accountability:** Database and service owners to be designated.

**Status:** Open — mitigation planned; controls are architectural requirements and are not yet implemented or validated.

**Assessment:** Formal likelihood, impact, and residual scoring pending.

## 10. Cross-Cutting Risk Controls

The following control areas apply across multiple risks and must be treated as platform-wide requirements.

### 10.1 Identity and Access Management

- Establish a defined identity-provider architecture.
- Separate authentication from application-level authorisation.
- Apply least privilege and role-based access.
- Enforce token validation and session protections.
- Review privileged access and account lifecycle.
- Maintain auditable access decisions.

### 10.2 Tenant Isolation

- Apply tenant-aware authorisation across databases, storage, Git, sandbox execution, caches, and workflows.
- Enforce isolation through service and infrastructure boundaries.
- Test tenant isolation adversarially.
- Prevent background workers from carrying stale tenant context.

### 10.3 AI and Agent Governance

- Treat agents as permission-controlled logical modules.
- Enforce authorisation in deterministic services rather than relying on model instructions.
- Restrict tool access and external side effects.
- Maintain traceable agent actions.
- Require human approval for designated sensitive operations.
- Evaluate models and agent workflows against defined test cases.

### 10.4 Financial Integrity

- Keep deterministic financial authority within `billing-ledger`.
- Separate advisory AI responsibilities from posting and balance mutation.
- Use idempotency, reconciliation, and immutable posted records.
- Protect financial audit history.
- Require controlled approval for sensitive adjustments.

### 10.5 Software Supply Chain

- Pin dependencies.
- Maintain lockfiles and SBOMs.
- Scan source, dependencies, and build artifacts.
- Verify provenance and signatures where supported.
- Protect GitHub workflows and secrets.
- Review changes before merging or releasing.

### 10.6 Data Protection

- Classify data by sensitivity.
- Apply encryption in transit and at rest.
- Restrict access and retention.
- Define backup, deletion, and recovery procedures.
- Protect logs and audit records.
- Assess applicable privacy and cross-border requirements.

### 10.7 Operational Resilience

- Monitor service health and workflow execution.
- Establish incident response procedures.
- Test failure recovery.
- Define approved RPO and RTO.
- Maintain service ownership and escalation paths.
- Review operational performance and recurring incidents.

## 11. Risk Treatment Options

Each risk owner should recommend one or more of the following treatments:

| Treatment | Meaning |
|---|---|
| Avoid | Change the design or activity so the risk is eliminated or no longer applicable |
| Mitigate | Implement controls to reduce likelihood or impact |
| Transfer or Share | Allocate defined portions of exposure through insurance, contracts, or service arrangements where appropriate |
| Accept | Formally accept the residual exposure through an authorised human decision |
| Monitor | Maintain oversight where additional treatment is not currently justified or practicable |

Risk transfer does not remove accountability for vendor oversight, regulatory obligations, or residual exposure.

Risk acceptance must never be inferred from silence, document publication, or an AI-generated recommendation.

## 12. Risk Escalation Framework

| Risk Rating | Escalation Requirement |
|---|---|
| Low | Risk owner monitors and records changes |
| Medium | Risk owner documents treatment and reports material changes |
| High | Escalate to the designated project governance authority; prioritise mitigation |
| Critical | Escalate immediately; affected activity must not proceed without an explicit authorised decision and required safeguards |

Where a risk involves suspected security compromise, data leakage, financial fraud, or unsafe execution, incident-response procedures take precedence over routine reporting schedules.

The final escalation authority and risk-acceptance thresholds require explicit organisational approval.

## 13. Risk Review and Reporting

Risk reviews should occur:

- At least monthly during active implementation.
- Before a major phase transition.
- Before production deployment.
- After material architecture or technology changes.
- After significant security or operational incidents.
- When new vendors, data categories, or integrations are introduced.
- When regulatory or contractual obligations materially change.

Each review should record:

1. Risk identifier.
2. Current description.
3. Likelihood and impact.
4. Inherent and residual scores.
5. Control implementation status.
6. Evidence of control effectiveness.
7. Mitigation progress.
8. Risk owner and control owner.
9. Target completion date.
10. Escalation or acceptance decision.
11. Next review date.

## 14. Required Risk Evidence

Evidence may include:

- Approved architecture decisions.
- Security assessment reports.
- Penetration-test results.
- Tenant-isolation test results.
- API and contract-test results.
- Backup and restoration records.
- Disaster recovery exercise reports.
- Vulnerability and dependency scan reports.
- SBOMs and build provenance.
- Access-review records.
- Approval and audit logs.
- Payment reconciliation records.
- Privacy assessments and legal reviews.
- Incident reports and corrective-action records.
- Performance and capacity-test reports.

Evidence must identify its date, scope, environment, version, result, and responsible reviewer.

A proposed control, policy statement, or untested configuration is not sufficient evidence of effectiveness.

## 15. Human Decisions Required

The following decisions remain unresolved and must be addressed by the appropriate human authority.

| Decision ID | Decision Required | Why It Matters | Status |
|---|---|---|---|
| HD-01 | Select the identity-provider approach | Determines identity ownership, MFA, session, and recovery architecture | Approved — managed identity-provider approach; validation remains required |
| HD-02 | Select Temporal Cloud or self-hosted deployment | Determines workflow operations, availability, cost, and recovery | Approved — Temporal Cloud preferred initially, conditional |
| HD-03 | Approve primary and disaster-recovery regions | Determines data residency, latency, and recovery design | Approved architectural direction — AWS Cape Town primary, Ireland DR; validations pending |
| HD-04 | Confirm the six-deployable backend topology | Establishes the approved deployment boundary | Approved — six logical deployables; physical topology validation remains required |
| HD-05 | Validate pgvector embedding dimension and configuration | Affects storage, indexing, retrieval, and compatibility | Approved — PostgreSQL/pgvector preferred initially; model-specific dimensions and POC-05 required |
| HD-06 | Approve platform RPO and RTO | Determines backup and disaster-recovery requirements | Approved — tiered architectural objectives; POC-15 and operational validation required |
| HD-07 | Designate risk acceptance authority | Establishes who may accept residual risk and under what conditions | Approved — Project Owner is sole initial risk acceptance authority; no delegation |
| HD-08 | Define GATE-01 through GATE-06 | Establishes approval requirements and separation of duties | Approved — six independent gates; Project Owner is sole initial approval authority |
| HD-REP-06 | Establish service-owned schema and migration governance | Prevents schema drift, cross-service privilege, and unsafe migration execution | Approved — independent schema ownership and migration histories for all six services; implementation validation and GATE-03/GATE-05 controls remain required |
| HD-REP-07 | Establish repository backup, disaster recovery and restoration governance | Reduces repository/data loss, incomplete recovery, provider dependency and cross-tenant restore exposure | Approved — layered provider-independent architecture; implementation and recovery testing remain required |

These decisions must be recorded through the appropriate governance process and, where applicable, the ADR Register.

## 16. Risk Register Maintenance

The register is a controlled architecture and governance document.

Changes should include:

- New risk identifiers for newly identified risks.
- Version history for material amendments.
- Clear reasons for changes in likelihood, impact, or priority.
- Recorded mitigation owners and target dates.
- Evidence references for completed controls.
- Explicit acceptance and closure records.
- Links to relevant ADRs, incidents, and corrective actions.

Existing risk identifiers should not be silently reassigned or reused.

When a risk is retired, its history should remain available for audit and future reference.

## 17. Relationship to Other Architecture Documents

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
- `ADR_REGISTER.md`
- `PHASE_0_INSPECTION_REPORT.md`
- `TESTING_STRATEGY.md`
- `MONITORING_AND_OBSERVABILITY.md`
- `COST_AND_SCALABILITY.md`

Where a risk identifies an architecture weakness, the relevant architecture document or ADR should be updated through the approved change-control process.

This register does not independently approve architecture decisions or supersede other controlled documents.

## 18. Phase 0 Risk Governance Limitations

This document establishes an initial risk baseline only.

The following activities have not been authorised by this document:

- Production deployment.
- Cloud resource provisioning.
- Database migration execution.
- Financial transaction processing.
- External provider integration.
- Creation or modification of protected GitHub resources.
- Acceptance of High or Critical risks.
- Phase 1 implementation.

Risk controls described here are proposed controls unless implementation and validation evidence is separately recorded.

The existence of this register does not establish that the platform is secure, compliant, production-ready, or free from unacceptable risk.

## 19. Final Status

**Document status:** Proposed — Phase 0.

**Document ID:** WLX-ARCH-011.

**Version:** 1.0.

**Risk baseline:** 28 identified risks, RSK-01 through RSK-28.

**Risk acceptance authority:** Project Owner — sole risk acceptance authority during the initial governance phase under HD-07; no delegation.

**Formal risk assessment:** Outstanding for risks not assigned a validated score.

**Control implementation and effectiveness:** Not established by this document.

**Approval:** Pending authorised human review.

**Implementation authority:** This document does not authorise Phase 1 or any production activity.

The Risk Register is intended to provide a traceable foundation for risk assessment, mitigation planning, governance decisions, and future operational assurance.

### RSK-27 — Repository Backup Failure, Incomplete Recovery, or Cross-Tenant Restoration

**Category:** Operational Resilience, Security, Data Protection and Customer Trust

**Risk statement:** Repository content, Git LFS objects, development metadata, release artifacts or associated project records may be lost, corrupted, exposed or incompletely restored because backups are absent, inconsistent, inaccessible, compromised, provider-dependent or insufficiently tested. A restore may also overwrite newer work or breach tenant/project boundaries.

**Potential causes:** Reliance on Git hosting alone; incomplete capture of metadata/LFS/artifacts; shared backup credentials; mutable or same-account-only copies; unverified encryption-key recovery; unclear customer-managed hosting responsibilities; inadequate retention/legal-hold handling; untested restore procedures; inconsistent snapshots; or insufficient tenant-aware restore controls.

**Potential consequences:** Permanent source/history or metadata loss, prolonged Factory/customer-project outage, supply-chain compromise, unauthorised cross-tenant disclosure, failed customer export, contractual/privacy exposure, and inability to establish trustworthy release provenance.

**Proposed controls:**
- Apply approved HD-REP-07 protection classes, backup scope, retention and recovery objectives.
- Maintain multiple independently controlled copies, including off-site and immutable/deletion-resistant protection.
- Separate backup identities, encryption keys and administrative duties from ordinary repository accounts.
- Verify Git refs/objects, Git LFS, supported metadata, artifacts, checksums and project mappings independently.
- Enforce tenant/project isolation in backup storage, restore workflows, credentials, jobs and artifact delivery; run negative cross-tenant tests.
- Document Worklexx-managed versus customer-managed hosting responsibilities, export, disconnection and provider limitations.
- Exercise isolated restoration, ransomware/deletion scenarios, portability, retention/legal holds and measured RPO/RTO; retain evidence and remediate failures.
- Prevent silent overwrite of newer customer work; use controlled reconciliation.

**Validation evidence required:** Successful restore exercises for each repository class; integrity/checksum reports; LFS and metadata recovery evidence; tenant-isolation tests; key-recovery evidence; provider-outage/export test; retention/legal-hold tests; measured RPO/RTO; and approved customer responsibility terms.

**Risk status:** Identified — residual likelihood, impact and score require formal assessment. Proposed controls do not reduce residual risk until implemented and evidenced. Risk acceptance remains exclusively with the Project Owner under HD-07.



### RSK-28 — Compromised Build Workflow, Dependency, Credential or Untrusted Artifact

**Category:** Software Supply Chain, Security and Operational Integrity

**Risk statement:** Malicious or compromised source, workflow actions, dependencies, build scripts, automation credentials, caches or build infrastructure may introduce unauthorised code, expose secrets or customer data, corrupt artifacts, or cause an unverified or compromised release to be published or deployed.

**Potential causes:** Over-privileged CI workflows; unpinned third-party actions; untrusted pull-request code accessing secrets; compromised direct or transitive dependencies; unverified downloads; shared build caches; weak tenant/project isolation; long-lived credentials; exposed signing keys; missing SBOM/provenance; insufficient artifact integrity checks; or conflation of successful builds with release/deployment approval.

**Potential consequences:** Supply-chain compromise, malicious software distribution, Factory or customer source compromise, credential theft, cross-tenant disclosure, integrity loss, financial or operational harm, regulatory/contractual exposure and loss of customer trust.

**Proposed controls:**
- Apply HD-REP-08 least-privilege workflow permissions, short-lived credentials where supported, immutable action pinning and reviewed workflow definitions.
- Separate untrusted PR validation from trusted release builds and prevent untrusted code from accessing privileged secrets.
- Enforce lockfiles, pinned tooling, dependency integrity, vulnerability/secret/licence scanning, dependency review, SAST/applicable DAST and SBOM generation.
- Isolate build environments, caches, credentials, jobs and artifacts by trust boundary, tenant and project.
- Verify artifact checksums/signatures and retain source-to-artifact provenance; protect signing keys through approved key management.
- Keep build, verification, release approval, publication and deployment as separate permissioned activities under HD-08.
- Exercise POC-REP-08-01 through POC-REP-08-12 and retain reproducible evidence; remediate findings before production reliance.

**Validation evidence required:** Workflow permission tests; untrusted PR isolation results; dependency/action pinning and integrity evidence; vulnerability/secret/licence scan results; SBOM validation; artifact checksum/signature/provenance verification; build/cache/tenant isolation negative tests; credential revocation evidence; compromised dependency/workflow exercises; and audit/recovery traceability.

**Risk status:** Identified — likelihood, impact and residual score require formal assessment. Proposed controls do not reduce residual risk until implemented and evidenced. Risk acceptance remains exclusively with the Project Owner under HD-07.
undefined

### RSK-29 — Incomplete, Altered, Exposed or Inadequately Monitored Audit Evidence

**Category:** Security, Governance, Privacy, Operational Resilience and Customer Trust

**Risk statement:** Audit events may be missing, inaccurate, delayed, altered, exposed, improperly retained or unavailable during an investigation because event sources are incomplete, identities or timestamps are unreliable, provider audit capabilities are limited, audit storage is insufficiently protected, monitoring is ineffective, or tenant boundaries are not enforced.

**Potential causes:** Incomplete event-source coverage; inconsistent schemas; clock drift; shared or overprivileged audit administration; mutable/deletable logs; inadequate integrity verification; secrets or sensitive content in logs; missing provider events; alert fatigue or detection gaps; weak retention/legal-hold processes; compromised credentials; insufficient backup/restore testing; or cross-tenant access defects.

**Potential consequences:** Inability to attribute consequential actions; delayed or missed detection of compromise; loss of evidence for incident response, disputes, legal or regulatory inquiries; exposure of customer or personal information; unauthorised cross-tenant disclosure; ineffective governance assurance; and reduced customer trust.

**Proposed controls:**
- Implement approved HD-REP-09 event coverage and a versioned event envelope with reliable actor, scope, action, outcome, timestamp and correlation metadata.
- Use independently protected append-only or tamper-evident audit storage, cryptographic integrity checks, encryption, least privilege, separation of duties and audit-store access logging.
- Minimise collected data; redact secrets and sensitive content; separate operational telemetry from security audit evidence.
- Enforce tenant/project isolation and customer-scoped visibility/export; document customer-managed provider visibility and responsibility limitations.
- Establish risk-based detection, severity, escalation, incident investigation, evidence preservation, retention, legal hold and controlled disposal.
- Protect audit evidence through HD-REP-07 backup/recovery and validate restoration and integrity.
- Complete POC-REP-09-01 through POC-REP-09-12, including negative tenant-access tests and AI-agent prohibited-action tests.

**Risk assessment:** Likelihood, impact, inherent score and residual score are **Pending formal assessment**. Do not infer a numeric score or claim that proposed controls reduce residual risk before implementation and evidence.

**Risk owner:** Project Owner pending assignment of operational control owners.

**Status:** Identified — assessment and control implementation pending.

**Related decisions:** HD-07, HD-08, HD-REP-05, HD-REP-07, HD-REP-08 and HD-REP-09.


### RSK-30 — Customer Project Ownership Disputes, Incomplete Portability or Improper Suspension, Transfer or Deletion

**Category:** Customer Trust, Data and Privacy, Compliance and Legal, Security, Operational Governance and Project Delivery

**Risk statement:** A customer may lose control of, be unable to retrieve, or experience unauthorised access, transfer, suspension, archival or deletion of a generated project because project ownership and authority are ambiguous, lifecycle transitions are inadequately controlled, exports are incomplete, hosting responsibilities are misunderstood, retention/legal holds are not enforced, or customer exit and integration-disconnection processes fail.

**Potential causes:** Missing or mutable project identity/ownership mapping; confusion between repository hosting administration and project ownership; unclear generated-code/IP/licence terms; cross-tenant authorisation defects; incomplete Git history/LFS/metadata/artifact exports; secret leakage in exports; unauthorised transfer or collaborator changes; automatic deletion following entitlement expiry; inconsistent retention and backup expiry; restoration of deleted data; inadequate legal-hold checks; provider API/portability limitations; or agents performing prohibited lifecycle actions.

**Potential consequences:** Customer source or business-data loss; ownership disputes; unauthorised disclosure or transfer; inability to migrate to another provider; contractual, privacy, regulatory or intellectual-property disputes; prolonged service disruption; accidental reintroduction of deleted data; financial/reputational harm; and loss of customer trust.

**Proposed controls:**
- Enforce HD-REP-05 one-repository-per-project isolation and immutable project identity with explicit customer/tenant, owner/controller, hosting and repository mapping.
- Distinguish project ownership from hosting administration; disclose customer-generated code, Worklexx platform/reusable components and third-party licence boundaries in applicable agreements and project records.
- Implement authenticated lifecycle state transitions, separation of export/transfer/disconnection/deletion, least-privilege collaborator access and explicit owner/required-party transfer authorisation.
- Provide customer-scoped export inventories, Git history/refs/LFS and applicable metadata/artifacts, integrity checksums, omission/provider-limit disclosures, secret exclusion and independent import validation.
- Prevent subscription/entitlement expiry from automatically deleting customer assets; define notification, suspension and retrieval safeguards under contract.
- Establish record-class-specific retention, legal-hold, archival, deletion and backup-expiry policies; verify deletion across primary and derived stores and prevent silent reintroduction from backups.
- Revoke only the relevant integration credentials on disconnection; do not delete customer-owned external repositories.
- Enforce agent prohibited-action boundaries and retain lifecycle/transfer/export/deletion audit evidence under HD-REP-09.
- Complete POC-REP-10-01 through POC-REP-10-15, including negative tenant/authority tests and end-to-end portability/exit exercises.

**Risk assessment:** Likelihood, impact, inherent score and residual score are **Pending formal assessment**. Proposed controls do not reduce residual risk until implemented and evidenced. No numeric score is inferred.

**Risk owner:** Project Owner pending assignment of operational control owners.

**Status:** Identified — assessment and control implementation pending.

**Related decisions:** HD-07, HD-08, HD-REP-05, HD-REP-07, HD-REP-08, HD-REP-09 and HD-REP-10.



### RSK-31 — Customer Data Exposure, Unlawful Processing and Privacy Control Failure

**Category:** Security, Privacy, Legal and Regulatory Compliance, Customer Trust, Data Governance and Operational Resilience

**Risk statement:** Customer or personal information may be exposed, processed without appropriate authority, transferred unlawfully, retained longer than permitted, incompletely deleted or used for an unauthorised purpose because tenant/project isolation, data classification, purpose limitation, agent permissions, external provider controls, regional transfer safeguards, derived-data lifecycle controls or privacy monitoring are incomplete or ineffective.

**Potential causes:** Cross-tenant access through APIs, databases, RLS gaps, pgvector, caches, jobs or agent context; excessive agent permissions; prompt injection or untrusted content; unauthorised model-provider training or onward disclosure; inadequate minimisation or processing records; unassessed cross-border flows; exposed multimodal data, transcripts or embeddings; incomplete deletion across indexes, replicas and backups; sensitive content in logs; unclear controller/processor and customer/provider responsibilities.

**Potential consequences:** Harm to individuals or customers; confidentiality breach; regulatory investigation, enforcement or notification obligations; contractual breach, claims or litigation; operational disruption; loss of customer trust and reputation; financial loss; suspension of processing or service.

**Proposed controls:**
- Implement HD-REP-11 data classification, processing inventory, purpose limitation, minimisation and documented legal/contractual authority.
- Enforce trusted tenant/project identity and least-privilege authorisation across all services, databases/RLS, vector retrieval, storage, indexes, caches, jobs, agent context, multimodal processing, builds, artifacts, backups and exports.
- Apply agent task scoping, untrusted-content handling and prompt-injection controls; agents cannot expand permissions or transfer data to unauthorised providers.
- Complete external model/subprocessor due diligence for data scope, location, retention, human access, onward processing, training use, deletion and incident terms. Prohibit general-purpose model training on customer data absent a specific lawful and authorised arrangement.
- Assess applicable jurisdictional, localisation and cross-border transfer requirements before live processing; HD-03 regional selection is not legal transfer approval.
- Protect confidential/restricted data through encryption, key/secret separation, controlled key lifecycle and privacy-aware logging/redaction.
- Establish applicable access, correction, export, erasure, restriction, objection and consent-withdrawal processes; define record-class retention and legal holds without assuming a universal duration.
- Verify deletion across primary, derived, vector, cache, job, replica and backup data; prevent backup restoration from silently reintroducing deleted/restricted data, aligned with HD-REP-07/10.
- Align privacy audit events, incident detection and evidence with HD-REP-09; define containment, investigation, remediation and legally required notification procedures.
- Complete POC-REP-11-01 through POC-REP-11-15, including cross-tenant negative tests and end-to-end privacy/security assessment.

**Risk assessment:** Likelihood, impact, inherent score and residual score are **Pending formal assessment**. Proposed controls do not reduce residual risk until implemented and evidenced. No numeric score is inferred.

**Risk owner:** Project Owner pending assignment of operational control owners.

**Status:** Identified — assessment and control implementation pending.

**Related decisions:** HD-07, HD-08, HD-03, HD-05, HD-REP-05, HD-REP-06, HD-REP-07, HD-REP-09, HD-REP-10 and HD-REP-11.


### RSK-32 — Identity Compromise, Excessive Privilege and Access-Control Failure

**Category:** Security, Privacy, Customer Trust, Governance and Operational Resilience

**Risk statement:** A human, agent, service or workload identity may be compromised, misidentified, overprivileged, incorrectly associated with a tenant/project, or inadequately revoked, resulting in unauthorised access or consequential actions across customer data, generated projects, repositories, workflows, financial records or platform administration.

**Potential causes:** Weak authentication or account recovery; compromised credentials/sessions; incomplete MFA or federation controls; incorrect organisation/project membership; excessive or stale role/attribute permissions; reliance on client-supplied tenant identifiers; service identity sharing; agent authority inherited from initiating users; long-lived or exposed API keys; incomplete revocation propagation; stale caches or queued workflows; inadequate privileged-access controls; identity-provider outage; or insufficient audit attribution.

**Potential consequences:** Cross-tenant or cross-project data exposure; unauthorised source/repository changes; fraudulent financial or billing actions; privilege escalation; unauthorised ownership or access changes; misuse of agent or service identities; failure to contain compromised accounts; privacy/regulatory/contractual consequences; service disruption and loss of customer trust.

**Proposed controls:**
- Retain HD-01 managed identity-provider direction and separate authentication from Worklexx application authorisation.
- Enforce trusted tenant/project/resource scope server-side using least-privilege RBAC, ABAC and explicit resource permissions; client-supplied identifiers are not authority.
- Separate human, organisation, membership, project, agent, service, workload and external integration identities.
- Require scoped, task- and time-limited agent delegation; prevent agents from self-granting access, approving their own access or bypassing HD-08.
- Use distinct service identities, short-lived workload credentials where practicable, and controlled API-key/token issuance, expiry, rotation and revocation.
- Govern registration, invitations, membership, role changes, access reviews, suspension, recovery, deprovisioning and privileged/emergency access.
- Propagate revocation across sessions, all six services, databases/RLS, pgvector, storage, repositories, workflows, agent contexts, caches and integrations; fail closed for sensitive operations when current authority cannot be established.
- Protect identity data and secrets, minimise collection, and align retention/rights with HD-REP-11 and audit attribution with HD-REP-09.
- Complete POC-REP-12-01 through POC-REP-12-20, including cross-tenant negative tests, compromised-account scenarios, concurrent permission changes and revocation validation.

**Risk assessment:** Likelihood, impact, inherent score and residual score are **Pending formal assessment**. Proposed controls do not reduce residual risk until implemented and evidenced. No numeric score is inferred.

**Risk owner:** Project Owner pending assignment of operational control owners.

**Status:** Identified — assessment and control implementation pending.

**Related decisions:** HD-01, HD-07, HD-08, HD-REP-05, HD-REP-06, HD-REP-09, HD-REP-10 and HD-REP-11.


## HD-REP-13 — AI Agent Security, Delegation, Execution Boundaries and Human Oversight Governance (Approved 2026-11-20)

Adopt permission-controlled, policy-enforced, sandboxed and auditable agent execution for the 23 logical agent modules. This decision does not add a backend deployable or alter the approved six-deployable architecture. Agent intelligence is not authority: each agent has a distinct identity and bounded task, tenant/project, tool, data and time scope; versioned policies; resource limits; audit attribution; and revocation controls.

Five conceptual permission tiers: Tier 0 Observe; Tier 1 Prepare; Tier 2 Execute within controlled scope; Tier 3 Consequential action subject to independent approval and applicable control; Tier 4 prohibited authority (including self-approval and governance bypass). Tool permissions remain granular: inspect, write, PR creation, review, approval, merge, permission changes, deletion and transfer are separate capabilities. The tool-control boundary validates identity/scope, inputs and destinations, classification, policy and approval, then executes, verifies and audits.

Code execution uses an appropriately isolated sandbox within the approved sandbox-runner boundary: restricted networking, resource/time limits, filesystem/process isolation, credential separation, tenant/project-specific caches and artifact handling, and cleanup. Untrusted documents, source, web content, prompts and tool results are data—not policy or authority—and prompt injection must not override permissions, governance or gates. Delegation is task/time bounded, depth-limited, attributable, revocable and cannot expand the initiating authority.

Agent context and memory are scoped, classified, minimised, governed and tenant/project isolated. Outputs require independent verification appropriate to their risk; verification does not substitute for human approvals required by HD-08. Control retries, loops, concurrency, idempotency, resource/cost limits, cancellation and safe failure. Protected audit and monitoring align with HD-REP-09; privacy and data boundaries with HD-REP-11; identity and delegation with HD-REP-12; execution isolation and supply-chain controls with HD-REP-08; customer lifecycle with HD-REP-10.

Validation requirements: POC-REP-13-01 through POC-REP-13-24 (unexecuted) cover agent identity/scope, least privilege, tool authorization, policy enforcement, tier separation, gate binding, sandbox isolation, network/credential restrictions, resource limits, prompt-injection resistance, untrusted content, tenant/project isolation, delegation depth/authority, context/memory privacy, output verification, human oversight, audit attribution, revocation, concurrent actions/races, loops/retries/cancellation, failure/recovery, cost controls, abuse scenarios and end-to-end governance bypass attempts.

Add RSK-33 — AI Agent Misuse, Unsafe Execution, Privilege Escalation and Governance Bypass. Formal likelihood, impact, inherent and residual scores remain pending assessment; proposed controls do not reduce residual risk until implemented and evidenced.

Project Owner remains sole initial risk acceptance and approval authority under HD-07/HD-08. Applicable gates remain mandatory. This is architecture/documentation approval only: no agent execution in production, sandbox provisioning, external integrations, live customer data, credentials, CI/CD activation, GitHub configuration, database changes, paid services, production deployment or Phase 1 is authorised.


### RSK-33 — AI Agent Misuse, Unsafe Execution, Privilege Escalation and Governance Bypass
**Description:** Agents or delegated agents may exceed scope, misuse tools, execute unsafe code, leak data, exploit untrusted content, escalate privilege or bypass approvals.
**Proposed controls:** HD-REP-13 bounded identity/scope and tiering; policy-enforced tool boundary; sandbox isolation; delegation limits; untrusted-content handling; human gate integration; independent verification; audit/monitoring; revocation; tenant isolation; resource limits and POC validation.
**Likelihood/impact/inherent/residual score:** Pending formal assessment. Controls do not reduce residual risk until implemented and evidenced.
**Status:** Identified; assessment and implementation pending.
**Related decisions:** HD-07, HD-08, HD-REP-05, HD-REP-08, HD-REP-09, HD-REP-10, HD-REP-11, HD-REP-12, HD-REP-13.


### RSK-34 — Contract Failure, Interface Drift, Integration Abuse and Communication Integrity
**Description:** Incompatible, undocumented, insecure or improperly governed API, event, workflow, agent-tool or external integration contracts may cause service failures, data exposure, tenant-isolation violations, financial errors, unsafe agent execution, workflow corruption or operational disruption.
**Proposed controls:** HD-REP-14 contract ownership and versioning; machine-readable schemas; consumer/provider contract testing; compatibility checks; explicit breaking-change governance; trusted authorization and tenant/project enforcement; idempotency and bounded retries; event replay/duplicate handling; Temporal replay compatibility; webhook authenticity and replay protection; destination/SSRF restrictions; privacy/provider due diligence; financial integrity tests; agent-tool permission controls; audit and release traceability.
**Likelihood/impact/inherent/residual score:** Pending formal assessment. Proposed or unimplemented controls do not reduce residual risk until implemented and evidenced.
**Status:** Identified; assessment and implementation pending.
**Related decisions:** HD-07, HD-08, HD-REP-05, HD-REP-06, HD-REP-08, HD-REP-09, HD-REP-11, HD-REP-12, HD-REP-13 and HD-REP-14.
