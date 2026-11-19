# COST AND SCALABILITY ARCHITECTURE

## Document Metadata

| Field | Value |
|---|---|
| Document Title | Cost and Scalability Architecture |
| Document ID | WLX-ARCH-016 |
| File Name | `COST_AND_SCALABILITY.md` |
| Version | 1.0.0 |
| Status | Proposed — Pending Project Owner Review and Approval |
| Date | 19 November 2026 |
| Project | Worklexx AI Software Factory |
| Organisation | Worklexx Business Enterprise |
| Architecture Phase | Phase 0 — Architecture and Design |
| Classification | Internal — Technical Architecture |
| Repository | [https://github.com/samuel1599361/worklexx-ai-software-factory](https://github.com/samuel1599361/worklexx-ai-software-factory) |
| Document Owner | Project Owner — Worklexx Business Enterprise |
| Approval Authority | Project Owner |
| Related Documents | WLX-ARCH-001 through WLX-ARCH-015 |

---

## 1. Purpose

This document defines the proposed architecture principles, governance controls and operational strategies for managing the cost, resource consumption, performance and scalability of the Worklexx AI Software Factory.

It establishes a framework for ensuring that the platform can grow from its initial operating capacity to larger user populations, workloads, geographic markets and AI-powered services without unnecessary architectural complexity or uncontrolled expenditure.

The document covers:

- Infrastructure and cloud expenditure.
- AI model and token consumption.
- Multimodal processing and storage.
- Backend and frontend resource utilisation.
- Database and network costs.
- Sandbox execution costs.
- Observability and security-related costs.
- Cost allocation, budgets and financial controls.
- Horizontal and vertical scalability.
- Capacity planning and performance management.
- Graceful degradation and resilience.
- Disaster recovery cost considerations.

This document is an architectural proposal. It does not constitute approval to purchase, deploy, provision or activate any cloud service.

## 2. Scope

The proposed cost and scalability architecture applies to the complete Worklexx AI Software Factory.

It covers the following architectural components:

1. Five frontend applications.
2. Six deployable backend units.
3. Twenty-three logical AI agents.
4. AI Gateway and model-routing capability.
5. Data and persistence infrastructure.
6. Workflow orchestration and messaging.
7. Multimodal processing and storage.
8. Secure sandbox execution.
9. Billing and financial accounting.
10. Advertising technology.
11. Monitoring, logging and observability.
12. Development, testing, staging and production environments.
13. Backup, recovery and disaster recovery infrastructure.

The architecture must support growth while preserving security, privacy, tenant isolation, financial integrity and service reliability.

## 3. Architectural Context

The cost and scalability strategy must remain consistent with the previously defined system architecture.

### 3.1 Frontend applications

The architecture recognises five frontend applications:

1. `worklexx.ai`
2. `app.worklexx.ai`
3. `video.worklexx.ai`
4. `images.worklexx.ai`
5. `docs.worklexx.ai`

These applications may have different traffic patterns, storage requirements and processing demands.

### 3.2 Deployable backend units

The architecture recognises six deployable backend units:

1. `api-gateway`
2. `agent-orchestrator`
3. `multimodal-service`
4. `sandbox-runner`
5. `billing-ledger`
6. `adtech-service`

These six units form the established backend deployment boundary.

The cost and scalability architecture must not introduce additional deployable backend services without a formally reviewed architectural decision.

### 3.3 Logical AI agents

The platform contains twenty-three logical AI agents.

These agents are logical capabilities coordinated through the established agent architecture. They are not twenty-three independently deployed microservices.

Agent execution, model usage, workflow activity and resource consumption must be measurable independently where technically appropriate, without requiring a separate deployment for every agent.

### 3.4 AI Gateway

AI Gateway and model-routing functionality is a logical platform capability.

It must not be interpreted as a seventh deployable backend unit.

## 4. Cost and Scalability Objectives

The principal objectives are:

- Maintain visibility of platform expenditure.
- Align resource consumption with actual business and technical demand.
- Prevent uncontrolled AI model and token expenditure.
- Provide measurable cost attribution.
- Support progressive growth in user and workload volumes.
- Avoid premature infrastructure overprovisioning.
- Maintain performance and security during scaling.
- Prevent resource contention between tenants.
- Protect financial records and billing integrity.
- Establish measurable capacity and performance baselines.
- Enable continuous cost and performance improvement.

Cost reduction must not undermine security, privacy, reliability, data integrity or user experience.

## 5. Architectural Principles

The following principles govern the proposed design.

### 5.1 Cost awareness by design

Every major architectural component should have identifiable resource-consumption characteristics.

### 5.2 Measure before optimising

Resource optimisation decisions should be based on observed usage, performance measurements and workload evidence rather than assumptions.

### 5.3 Scale according to demand

Resources should be provisioned and adjusted according to workload requirements, subject to approved capacity limits.

### 5.4 Separate logical capabilities from deployment units

The twenty-three agents must remain logically identifiable without unnecessarily multiplying infrastructure deployment units.

### 5.5 Protect financial integrity

Financial records must remain under the authority of the deterministic billing-ledger.

### 5.6 Preserve tenant isolation

Cost optimisation must never weaken tenant data separation or security controls.

### 5.7 Optimise continuously

Cost and performance reviews should be recurring operational activities.

### 5.8 Avoid vendor lock-in where practical

Architectural choices should consider portability, interoperability and future migration costs.

## 6. Cost Governance Model

The proposed governance model establishes accountability for resource consumption and expenditure.

It includes:

- Project-level financial oversight.
- Service-level cost ownership.
- Environment-level expenditure tracking.
- AI model and usage accounting.
- Infrastructure and storage monitoring.
- Budget approval and expenditure limits.
- Periodic financial reviews.
- Cost anomaly investigation.
- Documented approval of material cost changes.

Every production resource should have an identifiable business purpose, technical owner, environment and cost allocation category.

No financial authority should be inferred merely from an application's administrative or agent role.

## 7. Cost Classification and Allocation

Costs should be classified into meaningful categories.

| Cost Category | Examples |
|---|---|
| Compute | Backend execution, containers, serverless workloads |
| AI and ML | Model inference, tokens, embeddings, model hosting |
| Storage | Databases, object storage, backups |
| Networking | Bandwidth, ingress, egress, inter-region transfer |
| Database | Managed database capacity, replicas, connections |
| Multimodal | Image, audio and video processing |
| Sandbox | Isolated code execution and temporary storage |
| Observability | Metrics, logs, traces and monitoring |
| Security | Identity, key management, security monitoring |
| Delivery | CDN, frontend hosting and application delivery |
| Development | CI/CD, test environments and build resources |
| Disaster Recovery | Replication, backups and recovery infrastructure |
| Software and vendors | Licences, subscriptions and third-party services |

Cost attribution should be available at appropriate levels, including:

- Organisation.
- Product.
- Application.
- Backend service.
- Environment.
- Tenant, subject to privacy and access controls.
- AI agent.
- Model provider and model.
- Workflow or execution category.

Where direct attribution is not technically possible, shared costs should be allocated using documented and consistently applied allocation methods.

## 8. Budgeting and Financial Controls

The platform should adopt budgets at multiple levels:

1. Overall platform budget.
2. Environment budget.
3. Backend service budget.
4. AI and model usage budget.
5. Storage and data-processing budget.
6. Sandbox execution budget.
7. Observability and security budget.
8. Development and testing budget.

Actual monetary budgets have not yet been approved.

The following controls are proposed:

- Budget definitions before production deployment.
- Usage thresholds and expenditure alerts.
- Approved spending limits.
- Service quotas where supported.
- Maximum execution limits for expensive workloads.
- Periodic budget-versus-actual reviews.
- Escalation for unexpected expenditure.
- Documented approval for material budget increases.

A budget alert does not automatically stop expenditure unless an explicitly configured and tested enforcement mechanism exists.

## 9. Cost Forecasting and Anomaly Detection

Cost forecasting should use historical consumption, projected demand and known pricing information.

The forecasting model should consider:

- Active users.
- Concurrent users.
- AI requests per user.
- Average tokens per request.
- Model selection and routing.
- Image, audio and video processing volume.
- File uploads and downloads.
- Sandbox execution frequency.
- Database transactions.
- Storage growth.
- Network traffic.
- Backup retention.
- Monitoring and logging volume.

Cost anomaly detection should identify unusual changes in consumption.

Examples include:

- Sudden increases in model token usage.
- Unexpectedly high video-processing activity.
- Abnormal sandbox execution volume.
- Unusual storage growth.
- Unexpected network egress.
- Repeated workflow retries.
- Excessive logging or tracing.
- Unusual database utilisation.

An anomaly should generate an investigation and escalation workflow. Automated suspension of a service must be governed by approved safety, business-continuity and financial policies.

## 10. AI Model and Token Cost Management

AI inference is a potentially significant variable cost category.

The architecture must support measurement and control of model consumption across the platform.

### 10.1 Usage measurement

Where supported by the provider and model, record:

- Model provider.
- Model identifier and version.
- Request identifier.
- Logical agent identifier.
- Tenant or authorised cost-allocation identifier.
- Input token usage.
- Output token usage.
- Cached token usage, where applicable.
- Request duration.
- Retry count.
- Estimated or provider-reported cost.
- Execution outcome.

Sensitive prompts, confidential uploads and private user content must not be exposed in general cost reports.

### 10.2 Model routing

The logical AI Gateway should support model selection based on:

- Task complexity.
- Required quality.
- Supported modalities.
- Latency requirements.
- Security and privacy requirements.
- Availability.
- Provider pricing.
- Approved model policies.

Less expensive models may be considered for suitable tasks, while complex or high-value tasks may require more capable models.

Routing must not silently reduce output quality below the requirements of a task.

### 10.3 Token controls

The architecture should support:

- Per-request token limits.
- Agent-level usage limits.
- Tenant-level quotas.
- Model-specific limits.
- Retry limits.
- Request timeouts.
- Context-window management.
- Usage alerts.
- Budget-aware routing.

Any limits introduced must be configurable and approved.

### 10.4 AI cost optimisation

Potential optimisation methods include:

- Prompt optimisation.
- Context reduction.
- Reuse of suitable results.
- Caching where safe.
- Batch processing where appropriate.
- Model selection based on task requirements.
- Avoiding unnecessary repeated inference.
- Monitoring unsuccessful requests and retries.

Caching must respect tenant boundaries, data sensitivity and the validity of the underlying information.

## 11. Multimodal Processing Costs

The multimodal-service must account for the different resource characteristics of image, audio, video and document processing.

Cost drivers include:

- File size.
- Resolution and duration.
- Processing frequency.
- Model inference requirements.
- Transcription and speech generation.
- Image analysis.
- Video frame extraction.
- Document parsing.
- Temporary storage.
- Retention periods.
- Data transfer.

The architecture should support:

- File-size limits.
- Supported-format validation.
- Processing-duration limits.
- Workload quotas.
- Asynchronous processing for long-running tasks.
- Temporary-file lifecycle management.
- Appropriate compression and transformation.
- Secure object storage.
- Retention and deletion policies.

Multimodal processing limits must be configurable and consistent with the product's functional requirements.

## 12. Storage and Data Lifecycle Costs

Storage costs should be controlled through deliberate data lifecycle management.

The proposed architecture should distinguish:

- Transactional database storage.
- User-uploaded files.
- AI-generated outputs.
- Temporary processing files.
- Application logs.
- Audit records.
- Backups.
- Archived data.

Potential controls include:

- Data classification.
- Retention schedules.
- Automated lifecycle policies.
- Compression where appropriate.
- Removal of expired temporary files.
- Storage tiering where supported.
- Backup retention management.
- Monitoring of storage growth.

Deletion policies must respect legal, contractual, security and audit requirements.

Financial and audit records must not be removed merely to reduce storage expenditure.

## 13. Compute Resource Management

Compute resources should be matched to actual workload requirements.

The architecture should consider:

- CPU utilisation.
- Memory utilisation.
- GPU requirements where applicable.
- Execution duration.
- Concurrency.
- Request volume.
- Queue depth.
- Background processing demand.
- Peak and average utilisation.

Potential optimisation methods include:

- Right-sizing compute resources.
- Separating workloads with materially different resource profiles.
- Using asynchronous execution.
- Avoiding permanently running resources where unnecessary.
- Applying workload-specific resource limits.
- Reviewing idle and underutilised resources.

Specific compute types, instance sizes and hosting products remain subject to technical evaluation and approval.

## 14. Network and Data Transfer Costs

Network expenditure should be included in cost forecasting.

Potential cost drivers include:

- User traffic.
- API requests.
- File uploads and downloads.
- AI provider communication.
- Object storage access.
- Database connections.
- Inter-service communication.
- Cross-region replication.
- CDN delivery.
- Video streaming and processing.

The architecture should minimise unnecessary data movement while preserving security and availability.

Potential controls include:

- CDN usage where suitable.
- Efficient payload design.
- Compression.
- Appropriate caching.
- Regional data placement.
- Avoiding repeated downloads.
- Monitoring network egress.
- Reviewing cross-region data-transfer patterns.

Data residency, privacy and regulatory requirements take priority over cost-only regional decisions.

## 15. Database Cost and Scalability

Database expenditure and capacity must be managed as a core architectural concern.

The database architecture should support:

- Appropriate database sizing.
- Connection pooling.
- Query optimisation.
- Index management.
- Monitoring of slow queries.
- Storage growth monitoring.
- Backup and retention management.
- Read-replica evaluation where justified.
- Connection and concurrency limits.
- Capacity forecasting.

Database scaling options may include vertical scaling, read replicas, partitioning or other suitable approaches.

The choice must be based on measured workload requirements and the approved database architecture.

### 15.1 Tenant isolation

Database optimisation must preserve tenant isolation.

Where PostgreSQL Row-Level Security is adopted, scaling and connection-pooling arrangements must preserve the correct tenant context for every transaction.

A connection pool must not allow one tenant's session context or data to leak into another tenant's request.

### 15.2 Vector search

The previously identified pgvector embedding-dimension decision remains unresolved.

The proposed 3072-dimension requirement must not be treated as approved until the relevant architecture decision is completed.

Vector storage, indexing, query performance and infrastructure costs must be evaluated using representative data and workloads.

## 16. Backend Service Scalability

The six established backend units should be independently scalable where the selected deployment platform supports this safely.

| Backend Unit | Principal Scaling Considerations |
|---|---|
| `api-gateway` | Request volume, concurrent connections, rate limits |
| `agent-orchestrator` | Active workflows, task concurrency, queue depth |
| `multimodal-service` | CPU/GPU demand, file size, processing duration |
| `sandbox-runner` | Concurrent isolated executions, memory and CPU limits |
| `billing-ledger` | Transaction throughput, consistency and durable writes |
| `adtech-service` | Campaign activity, event volume and delivery demand |

Independent scaling does not mean each service must use a separate infrastructure product or technology.

Deployment topology must remain consistent with the six-unit architecture unless an approved ADR changes it.

## 17. Horizontal and Vertical Scaling

Two primary scaling approaches should be supported where technically appropriate.

### 17.1 Vertical scaling

Vertical scaling increases the resources available to an existing execution unit.

Examples include:

- More CPU.
- More memory.
- Increased database capacity.
- Higher storage throughput.

Vertical scaling may be appropriate where workload characteristics or platform constraints favour a larger instance.

Its limitations include maximum resource ceilings and potential maintenance or restart requirements.

### 17.2 Horizontal scaling

Horizontal scaling increases the number of execution instances handling a workload.

Examples include:

- Multiple API gateway instances.
- Multiple agent-orchestrator workers.
- Additional multimodal processing workers.
- Additional isolated sandbox execution capacity.

Horizontal scaling should be preferred for workloads that can be safely distributed across multiple instances.

Stateful operations require appropriate shared persistence, coordination and consistency controls.

## 18. Stateless Service Design

Stateless execution should be preferred for services that need horizontal scalability.

A stateless instance should not depend on local memory or local disk as the sole location for durable business state.

Durable state should be held in approved shared persistence systems.

The design should support:

- Restartable service instances.
- Independent scaling.
- Load balancing.
- Health checks.
- Graceful shutdown.
- Recovery from instance failure.
- Externalised configuration.
- Secure session management.

Temporary local storage may be used where its lifecycle and security are properly controlled.

## 19. Queue-Based and Asynchronous Processing

Long-running or resource-intensive workloads should use asynchronous processing where appropriate.

Potential use cases include:

- Complex multi-agent workflows.
- Image processing.
- Audio transcription.
- Video processing.
- Document extraction.
- Large file operations.
- Background reporting.
- Batch inference.

The architecture must account for the previously established messaging principles:

- Pub/Sub is an ephemeral messaging mechanism, not a durable system of record.
- Delivery may occur more than once.
- Consumers must support idempotent processing.
- Durable workflow state must be maintained through an appropriate persistence mechanism.
- Outbox and inbox patterns should be evaluated where needed.
- Retries must be bounded and controlled.
- Dead-letter queues should support failed-message investigation.
- Reconciliation must address incomplete or inconsistent operations.

The workflow-orchestration technology decision, including Temporal Cloud versus self-hosted Temporal, remains pending the required proof of concept and architecture decision.

## 20. Autoscaling and Capacity Limits

Autoscaling is a proposed capability, not an approved implementation.

Where supported by the selected hosting platform, autoscaling may use:

- CPU utilisation.
- Memory utilisation.
- Request rate.
- Concurrent requests.
- Queue depth.
- Processing latency.
- Worker utilisation.
- Other workload-specific metrics.

Scaling policies should include minimum and maximum capacity boundaries.

The architecture should prevent uncontrolled scaling that creates unexpected expenditure.

Scale-in operations must not terminate active financial transactions, corrupt workflow state or interrupt durable processing.

## 21. Caching Strategy

Caching may improve performance and reduce repeated computation or data retrieval.

Potential caching locations include:

- CDN.
- Application layer.
- API gateway.
- Database query layer.
- AI inference workflow.
- Frequently accessed reference data.

Caching decisions must define:

- What may be cached.
- Cache lifetime.
- Invalidation rules.
- Tenant separation.
- Data sensitivity.
- Consistency requirements.
- Maximum storage consumption.

Private prompts, confidential files, authentication tokens and tenant-specific data must never be exposed through incorrectly scoped shared caches.

Caching must not compromise financial accuracy or the consistency of authoritative records.

## 22. Sandbox Execution Cost and Isolation

The sandbox-runner may create substantial and variable resource demand.

The architecture should support:

- CPU limits.
- Memory limits.
- Execution timeouts.
- Disk quotas.
- Network restrictions.
- Concurrent execution limits.
- Temporary workspace cleanup.
- Secure isolation.
- Execution monitoring.
- Per-tenant usage accounting.

gVisor remains a candidate isolation technology, not an approved implementation or a guarantee of zero security risk.

Sandbox capacity must be planned separately from ordinary API request capacity.

Expensive or unusually long-running workloads should be subject to explicit policy controls.

## 23. Billing-Ledger and Financial Integrity

The billing-ledger remains the authoritative financial record system.

Cost monitoring, cloud billing reports, AI usage metrics and operational dashboards must not replace the billing-ledger as the source of truth for platform financial transactions.

The billing-ledger should preserve:

- Durable transaction records.
- Idempotent financial operations.
- Appropriate audit trails.
- Reconciliation capability.
- Controlled financial state transitions.
- Access restrictions.
- Data integrity.

The architecture must distinguish between:

1. Infrastructure and operational expenditure.
2. AI provider usage expenditure.
3. Customer-facing product usage.
4. Customer charges and account balances.
5. Revenue and other business financial records.

These categories may be related, but they must not be treated as interchangeable.

Cost optimisation must never weaken financial consistency or transaction integrity.

## 24. Advertising Technology Cost Controls

The adtech-service should have measurable resource consumption and operational cost attribution.

Its cost controls should include:

- Event-volume monitoring.
- Campaign-processing limits.
- Request and delivery quotas.
- Storage and retention controls.
- Fraud and abuse monitoring.
- Budget-aware campaign operations.
- Performance monitoring.

Advertising-related processing must remain strictly separated from confidential user activity.

The adtech-service must not obtain private AI prompts, source code, uploaded confidential files, credentials or protected workflow content for advertising purposes.

Cost optimisation does not justify weakening this separation.

## 25. Observability and Monitoring Costs

Monitoring infrastructure itself consumes resources and may create significant costs at scale.

The architecture should account for:

- Metrics ingestion.
- Log ingestion and retention.
- Distributed tracing.
- Alerting.
- Dashboards.
- Security monitoring.
- Audit logging.
- Storage and indexing.

OpenTelemetry remains the proposed instrumentation approach.

Prometheus, Grafana, Loki, Tempo, Jaeger, Google Cloud Operations and Sentry remain candidate technologies, subject to the decisions in the monitoring and observability architecture.

Potential controls include:

- Log-level management.
- Sampling policies.
- Trace sampling.
- Retention policies.
- Metric cardinality controls.
- Sensitive-data filtering.
- Cost monitoring for observability systems.

Security, financial and audit records must retain the level of detail required by approved policies.

## 26. Frontend Scalability and Delivery

The five frontend applications should be designed to support increasing traffic without requiring unnecessary backend resource consumption.

Potential measures include:

- CDN delivery.
- Static asset optimisation.
- Image optimisation.
- Browser caching.
- Lazy loading.
- Efficient API communication.
- Code splitting.
- Appropriate server-side or client-side rendering.
- Frontend performance monitoring.

Vercel remains subject to the existing technology-stack and deployment decisions.

Its runtime, bandwidth, build and execution limitations must be evaluated before production workloads are assigned to it.

Frontend scaling must be coordinated with backend capacity to prevent traffic increases from overwhelming downstream services.

## 27. Tenant Isolation and Noisy-Neighbour Protection

The platform must prevent one tenant's activity from degrading the service available to other tenants.

Noisy-neighbour controls should be considered across:

- API request volume.
- AI model usage.
- Workflow concurrency.
- Database connections.
- Storage consumption.
- File processing.
- Sandbox execution.
- Network bandwidth.

Potential controls include:

- Per-tenant quotas.
- Rate limiting.
- Resource reservations where justified.
- Fair-use scheduling.
- Concurrency limits.
- Workload prioritisation.
- Usage alerts.
- Abuse detection.

Tenant isolation must be preserved across PostgreSQL, object storage, Git repositories, sandbox environments and workflow execution.

The cost and scalability design must not weaken the tenant-isolation requirements established in the security and database architecture documents.

## 28. Backpressure, Rate Limiting and Graceful Degradation

The platform should remain controlled when incoming demand exceeds available capacity.

Potential controls include:

- API rate limiting.
- Request timeouts.
- Bounded queues.
- Concurrency limits.
- Retry backoff.
- Circuit breakers.
- Admission control.
- Workload prioritisation.
- Temporary feature restrictions.
- Clear user-facing service responses.

Graceful degradation may temporarily reduce non-essential functionality while preserving critical operations.

Financial transactions, security enforcement and durable workflow state must receive appropriate protection.

The platform must not silently discard financial operations or represent an incomplete transaction as successful.

## 29. Performance and Load Testing

Performance and load testing should establish evidence for capacity planning.

Testing should cover:

- Normal operating loads.
- Peak traffic.
- Concurrent users.
- API throughput.
- Agent workflow concurrency.
- AI inference latency.
- Multimodal processing.
- Database performance.
- Sandbox execution.
- Queue backlogs.
- Failure recovery.
- Tenant isolation under load.

Testing should identify:

- Throughput limits.
- Latency characteristics.
- Resource saturation.
- Database bottlenecks.
- Queue accumulation.
- Memory leaks.
- Unexpected cost increases.
- Scaling delays.
- Failure conditions.

The testing strategy defined in WLX-ARCH-014 should govern the testing approach.

No throughput, latency or concurrency target should be treated as achieved until supported by repeatable test evidence.

## 30. Capacity Planning and Service Objectives

Capacity planning must be evidence-based.

The following indicators should be considered:

| Area | Proposed Measurement |
|---|---|
| API | Requests per second, latency, error rate |
| Agents | Workflow volume, execution time, concurrency |
| AI | Tokens, model latency, cost per task |
| Multimodal | Files processed, processing time, storage |
| Sandbox | Concurrent executions, CPU and memory |
| Database | Query latency, connections, transaction throughput |
| Messaging | Queue depth, delivery latency, retry rate |
| Storage | Growth rate, access volume, retention |
| Network | Bandwidth, egress and transfer volume |
| Financial | Transaction volume, reconciliation exceptions |

Service-level objectives, service-level agreements, capacity targets and alert thresholds remain pending evidence and Project Owner approval.

They must be defined using actual business requirements, representative workload tests and operational capability.

## 31. Disaster Recovery and Resilience Cost Considerations

Disaster recovery introduces additional infrastructure, storage, replication and operational costs.

The architecture should consider:

- Backup frequency.
- Backup retention.
- Database recovery.
- Object storage recovery.
- Configuration recovery.
- Application redeployment.
- Regional recovery options.
- Data replication.
- Recovery testing.
- Operational staffing and procedures.

The choice between active-active, active-passive, warm standby or other recovery patterns must be based on business requirements, technical feasibility and approved expenditure.

Cloud SQL high availability must not be treated as equivalent to complete disaster recovery.

Recovery Point Objective (RPO) and Recovery Time Objective (RTO) remain pending decisions.

No recovery capability should be described as operational until it has been implemented and tested.

## 32. Technology and Vendor Cost Considerations

Technology selection should consider total cost of ownership rather than initial subscription or hosting price alone.

Evaluation should include:

- Usage-based pricing.
- Minimum commitments.
- Licensing.
- Support charges.
- Data transfer.
- Storage.
- Scaling charges.
- Security features.
- Regional availability.
- Migration costs.
- Vendor lock-in.
- Operational complexity.
- Exit costs.

Candidate technologies and vendors identified in the other architecture documents remain subject to evaluation.

This document does not approve Google Cloud, Vercel, Temporal, any AI model provider or any other vendor for production use.

Vendor pricing and service capabilities must be verified at the time of procurement because they can change.

## 33. Security, Privacy and Cost Trade-offs

Cost optimisation must remain subordinate to mandatory security, privacy and data-protection requirements.

The following controls must not be removed merely to reduce expenditure:

- Tenant isolation.
- Authentication and authorisation.
- Encryption requirements.
- Secure secret management.
- Financial auditability.
- Sandbox isolation.
- Confidential-data protection.
- Backup and recovery safeguards.
- Required security monitoring.

Any proposed reduction in a security or resilience control must undergo formal risk assessment and approval.

Cost savings must be evaluated alongside their effect on reliability, performance, security and business continuity.

## 34. Outstanding Architecture and Financial Decisions

The following matters remain unresolved and require Project Owner decisions or supporting technical evidence.

| Decision ID | Outstanding Decision | Required Resolution |
|---|---|---|
| HD-01 | Identity provider | Select and approve the identity architecture |
| HD-02 | Temporal Cloud versus self-hosted Temporal | Complete proof of concept and cost evaluation |
| HD-03 | Primary and disaster recovery regions | Evaluate latency, residency, resilience and cost |
| HD-04 | Six-service deployment topology | Confirm hosting and deployment arrangements |
| HD-05 | pgvector embedding dimension | Validate model requirements and database impact |
| HD-06 | RPO and RTO | Establish business-approved recovery targets |
| HD-07 | Risk acceptance authority | Confirm who may accept residual risks |
| HD-08 | Definitions of all six architecture gates | Complete and approve gate definitions |

Additional financial decisions required include:

- Approved initial and recurring budgets.
- Approved cloud and software vendors.
- AI model-provider strategy.
- Model-specific spending limits.
- Environment-level budgets.
- Cost allocation rules.
- Storage retention and lifecycle policies.
- Production capacity targets.
- Service-level objectives.
- Cost alert thresholds.
- Procurement and renewal authority.

No monetary estimates, capacity commitments or service guarantees are established by this document.

## 35. Cost and Scalability Risk Register

The following risks should be tracked alongside the central project risk register.

| Risk ID | Risk | Potential Impact | Proposed Control |
|---|---|---|---|
| CS-01 | Uncontrolled AI token consumption | Unexpected expenditure | Token limits, usage monitoring and budget alerts |
| CS-02 | Multimodal workload growth | Compute and storage cost increases | File limits, quotas and lifecycle controls |
| CS-03 | Uncontrolled autoscaling | Unexpected infrastructure expenditure | Scaling boundaries and expenditure monitoring |
| CS-04 | Database capacity bottlenecks | Slow transactions and service disruption | Load testing and capacity planning |
| CS-05 | Excessive network egress | Increased operating costs | Transfer monitoring and efficient delivery |
| CS-06 | Sandbox resource abuse | Resource exhaustion and security exposure | Execution limits and isolation |
| CS-07 | Unbounded retries | Increased AI and infrastructure consumption | Retry budgets, backoff and dead-letter handling |
| CS-08 | Inadequate tenant quotas | Noisy-neighbour effects | Per-tenant resource controls |
| CS-09 | Observability cost growth | Increased operational expenditure | Sampling and retention controls |
| CS-10 | Inadequate disaster recovery planning | Recovery failure or excessive recovery cost | Approved recovery strategy and testing |
| CS-11 | Vendor price changes | Budget instability | Pricing reviews and alternative evaluation |
| CS-12 | Inaccurate cost attribution | Poor financial decisions | Consistent allocation and reconciliation |
| CS-13 | Premature overprovisioning | Unnecessary recurring expenditure | Evidence-based sizing |
| CS-14 | Underprovisioning | Poor performance and availability | Capacity testing and scaling policies |
| CS-15 | Cross-tenant resource contention | Service degradation | Isolation, quotas and fair-use controls |

These risks should be reconciled with the central risk register in WLX-ARCH-011.

Risk ratings and residual-risk decisions must follow the established project risk methodology.

## 36. Roles and Responsibilities

The proposed responsibility model is:

| Role | Responsibility |
|---|---|
| Project Owner | Approves budgets, architecture decisions and material expenditure |
| Architecture Lead | Maintains architectural consistency and scalability principles |
| Backend Engineering | Implements efficient service execution and resource controls |
| AI Engineering | Controls model routing, token consumption and inference efficiency |
| Database Engineering | Manages database performance, storage and connection efficiency |
| DevOps / Platform Engineering | Manages infrastructure utilisation, deployment and scaling |
| Security Lead | Ensures cost optimisation does not weaken security controls |
| Finance / Financial Controller | Reviews budgets, expenditure and financial reporting |
| QA / Performance Engineering | Validates performance, load and capacity assumptions |
| Operations / SRE | Monitors service health, capacity and operational expenditure |

These are proposed responsibilities. Formal appointments and delegated approval authorities remain subject to Project Owner confirmation.

## 37. Implementation Roadmap

The following roadmap is indicative and does not authorise implementation.

| Stage | Proposed Activity | Expected Output |
|---|---|---|
| Phase 0 | Define cost and scalability architecture | Approved design baseline |
| Phase 1 | Establish requirements and decision records | Approved implementation scope |
| Phase 2 | Develop cost and capacity models | Initial cost and capacity estimates |
| Phase 3 | Implement foundational monitoring and usage measurement | Measurable resource consumption |
| Phase 4 | Implement service and AI usage controls | Operational cost governance |
| Phase 5 | Conduct performance and load testing | Verified capacity baselines |
| Phase 6 | Implement approved scaling and resilience mechanisms | Tested scaling capability |
| Phase 7 | Review and optimise operating costs | Evidence-based optimisation |
| Phase 8 | Continuous monitoring and improvement | Sustainable operational model |

Actual dates and deliverables must be established through the approved development roadmap.

## 38. Acceptance Criteria

This document may be considered architecturally ready for Project Owner review when:

1. Cost governance principles are documented.
2. Cost categories and allocation requirements are defined.
3. AI model and token usage controls are specified.
4. Multimodal processing costs are addressed.
5. Storage and data lifecycle considerations are documented.
6. Compute and network expenditure are covered.
7. Database cost and scalability requirements are defined.
8. The six backend deployment units are consistently represented.
9. The twenty-three agents remain logical modules rather than separate deployment units.
10. AI Gateway remains a logical capability rather than an additional backend service.
11. Horizontal and vertical scaling strategies are documented.
12. Queue-based processing and idempotency requirements are preserved.
13. Autoscaling controls and capacity boundaries are addressed.
14. Tenant isolation and noisy-neighbour protections are documented.
15. Sandbox resource limits and cost controls are specified.
16. Billing-ledger authority is preserved.
17. Adtech privacy separation is preserved.
18. Observability expenditure is addressed.
19. Disaster recovery cost considerations are documented.
20. Outstanding decisions are identified.
21. Cost and scalability risks are recorded.
22. No unapproved vendor, budget or capacity commitment is represented as approved.
23. No implementation or production deployment is implied.

## 39. Approval and Change Control

This document is a proposed architecture baseline.

Its status remains:

**Proposed — Pending Project Owner Review and Approval.**

Approval must be explicitly recorded by the Project Owner.

Any material change to the cost governance model, backend deployment boundaries, AI usage controls, scaling architecture, financial authority or disaster recovery strategy should be reviewed for consistency with the other Phase 0 architecture documents.

Changes should be recorded through the project's architecture decision and change-control processes.

Approval of this document does not automatically approve cloud procurement, infrastructure provisioning, production deployment or Phase 1 implementation.

## 40. Phase 0 Boundary and Authorisation Statement

This document is part of Phase 0 architecture and design documentation.

The following activities have not been authorised by this document:

- Cloud infrastructure provisioning.
- Production environment deployment.
- Paid cloud or AI service activation.
- Vendor procurement or financial commitments.
- Database provisioning or migration.
- Production autoscaling configuration.
- Production monitoring deployment.
- Implementation of cost enforcement mechanisms.
- Production disaster recovery deployment.
- Phase 1 development or implementation.

All technical recommendations remain subject to review, evidence, approval and the relevant architecture gates.

The Phase 0 objective is to establish a coherent, cost-aware and scalable architecture before implementation begins.

---

## 41. References and Related Architecture Documents

### 41.1 Internal architecture references

This document should be read alongside:

- WLX-ARCH-001 — Architecture Overview.
- WLX-ARCH-002 — System Architecture.
- WLX-ARCH-003 — Technology Stack.
- WLX-ARCH-005 — Agent Ecosystem.
- WLX-ARCH-006 — Service Boundaries.
- WLX-ARCH-007 — Database Architecture.
- WLX-ARCH-008 — Security Architecture.
- WLX-ARCH-009 — Deployment Architecture.
- WLX-ARCH-010 — Development Roadmap.
- WLX-ARCH-011 — Risk Register.
- WLX-ARCH-012 — ADR Register.
- WLX-ARCH-014 — Testing Strategy.
- WLX-ARCH-015 — Monitoring and Observability.

### 41.2 External architecture references

The following publications provide general guidance for cost optimisation, cloud resource management and performance engineering. They are reference material, not vendor-selection or procurement approvals.

1. Google Cloud Well-Architected Framework — Cost Optimization Pillar: https://docs.cloud.google.com/architecture/framework/cost-optimization
2. Google Cloud Well-Architected Framework — Manage and Optimize Cloud Resources: https://docs.cloud.google.com/architecture/framework/operational-excellence/manage-and-optimize-cloud-resources
3. Google Cloud Well-Architected Framework — Performance Optimization Pillar: https://docs.cloud.google.com/architecture/framework/performance-optimization
4. AWS Well-Architected Framework — Cost Optimization: https://docs.aws.amazon.com/wellarchitected/latest/framework/cost-optimization.html

---

**END OF DOCUMENT — WLX-ARCH-016**

**Document Status:** Proposed — Pending Project Owner Review and Approval.

**Implementation Status:** Not authorised.

**Phase 1 Status:** Not authorised.