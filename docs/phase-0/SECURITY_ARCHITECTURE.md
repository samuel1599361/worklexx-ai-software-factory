# WORKLEXX AI SOFTWARE FACTORY
# SECURITY ARCHITECTURE

**Document ID:** WLX-ARCH-008  
**Document Name:** Security Architecture  
**Version:** 1.0  
**Status:** Phase 0 — Architecture Baseline  
**Classification:** Internal — Architecture and Security Planning  
**Repository:** https://github.com/samuel1599361/worklexx-ai-software-factory  
**Document Owner:** Project Owner (designation and authority to be formally confirmed)  
**Review Requirement:** Cross-document architecture review before Phase 1 implementation

---

## Document Metadata

| Attribute | Value |
|---|---|
| Document ID | WLX-ARCH-008 |
| Document Title | Security Architecture |
| Document Version | 1.0 |
| Document Status | Phase 0 — Architecture Baseline |
| Architecture Stage | Architecture definition and review |
| Security Model | Defence in depth, least privilege, zero trust, risk-based controls |
| Target Platform | Worklexx AI Software Factory |
| Repository | https://github.com/samuel1599361/worklexx-ai-software-factory |
| Related Documents | WLX-ARCH-001 through WLX-ARCH-016, excluding this document |
| Implementation Status | Not implemented or independently verified |
| Approval Status | Pending formal review and approval |

---

## 1. Purpose

This document defines the security architecture, security boundaries, security responsibilities, protection mechanisms, risk controls and security verification requirements for the Worklexx AI Software Factory.

The platform is designed to enable users to build, modify, test, execute, deploy and manage software projects through AI-assisted and agentic workflows.

Because the platform may handle source code, credentials, personal information, financial transactions, private project files, third-party integrations, executable code and autonomous AI actions, security must be a foundational architectural requirement.

This document establishes a security baseline that subsequent implementation phases must use to design, build, test, deploy and operate the platform.

The document does not constitute evidence that any security control has already been implemented, tested, certified or approved.

---

## 2. Security Architecture Objectives

The security architecture shall seek to achieve the following objectives:

1. Protect user accounts, identities and authentication credentials.
2. Prevent unauthorized access to tenant, organization and project data.
3. Maintain confidentiality, integrity and availability of platform services.
4. Prevent AI agents from exceeding authorized permissions.
5. Prevent unauthorized code execution, system access and data exfiltration.
6. Protect financial transactions, credits, payments and ledger records.
7. Protect uploaded files, multimodal content, source code and generated artifacts.
8. Secure integrations with external AI providers, payment providers and third-party services.
9. Maintain reliable security audit records.
10. Protect infrastructure, secrets, cryptographic keys and deployment environments.
11. Prevent approval bypass, replay, privilege escalation and unauthorized deployment.
12. Support incident detection, investigation, containment and recovery.
13. Support applicable privacy, data protection and contractual obligations.
14. Integrate security testing into the software development lifecycle.
15. Establish evidence-based security acceptance requirements.

---

## 3. Security Architecture Principles

The platform shall follow these principles.

### 3.1 Least privilege

Every user, agent, service, worker, integration and administrative account shall receive only the permissions required for its authorized responsibilities.

Permissions shall not be granted merely because an account belongs to an administrator, agent, developer or service.

### 3.2 Zero-trust approach

Network location, tenant membership, application identity or prior authorization shall not automatically establish trust.

Access decisions shall consider authenticated identity, requested action, resource, tenant, permission, policy, context and risk.

### 3.3 Defence in depth

Security shall be implemented through multiple independent and complementary controls.

Security shall not depend exclusively on a single authentication provider, API gateway, firewall, database policy, AI model, security scanner or approval mechanism.

### 3.4 Separation of duties

Critical functions shall be separated where practical, particularly:

- Identity administration.
- Platform administration.
- Security administration.
- Financial operations.
- Deployment authorization.
- Protected GitHub operations.
- Production access.
- Risk acceptance.
- Incident response.

### 3.5 Secure by default

New users, tenants, projects, uploads, sandbox environments, integrations and agent capabilities shall default to restrictive security settings.

Unverified content, unknown integrations, unapproved actions and newly uploaded executable material shall not automatically receive trusted status.

### 3.6 Explicit authorization

Every sensitive operation shall require an explicit authorization decision.

The decision shall be enforced by a deterministic security control rather than relying on AI-generated instructions, model output or a user interface indication alone.

### 3.7 Accountability and traceability

Security-sensitive actions shall be traceable to the initiating identity, authorization context, affected resource, action, timestamp, outcome and applicable approval or policy.

### 3.8 Security over convenience

Where a security decision cannot be reliably established, the platform shall fail closed for security-sensitive operations, while maintaining safe availability and recovery mechanisms where possible.

### 3.9 No assumption of perfect AI behaviour

AI models and agents shall be treated as potentially unreliable, manipulable or compromised decision-making components.

AI output shall not constitute a security control.

---

## 4. Security Scope and Protected Assets

The security architecture covers all platform components, users, tenants, services, workflows and data.

### 4.1 Protected assets

Protected assets include:

- User identities and account credentials.
- Authentication tokens and session information.
- Tenant and organization records.
- Private project files and source code.
- Git repositories and repository credentials.
- AI prompts, conversation data and contextual information.
- Agent instructions, configurations and tool permissions.
- Workflow execution state.
- Uploaded documents, images, videos, audio and other files.
- Generated code, artifacts and application builds.
- Sandbox execution environments.
- Database records and database credentials.
- Financial balances, reservations, ledger entries and payment records.
- Payment-provider secrets and webhook verification keys.
- Cryptographic keys and secrets.
- Infrastructure configuration.
- Deployment credentials and environment variables.
- Approval records and approval tokens.
- Security logs and audit events.
- User personal data.
- Third-party API credentials.
- Advertiser, analytics and public marketplace information.
- Backup and disaster-recovery assets.

### 4.2 Security boundaries

The platform shall protect the boundaries between:

- Users and the platform.
- Tenants and other tenants.
- Organizations and other organizations.
- Projects and other projects.
- Frontend applications and backend services.
- API Gateway and internal services.
- Identity provider and application authorization.
- AI agents and deterministic services.
- AI models and confidential platform data.
- Sandbox workloads and host infrastructure.
- Sandbox workloads and external networks.
- Billing and non-financial services.
- AdTech and private platform data.
- Production and non-production environments.
- Platform administrators and user-owned resources.
- Worklexx and third-party providers.
- Uploaded content and trusted application instructions.
- Approved operations and unapproved operations.

---

## 5. Security Architecture Overview

Security shall be implemented across the platform's five frontend applications, API Gateway and six deployable backend service units.

### 5.1 Frontend applications

The platform has five frontend applications:

1. `worklexx.ai`
2. `app.worklexx.ai`
3. `video.worklexx.ai`
4. `images.worklexx.ai`
5. `docs.worklexx.ai`

Frontend applications shall not independently establish authoritative security decisions.

Frontend security responsibilities include:

- Secure user interaction.
- Authentication flow initiation.
- Secure session handling through approved architecture.
- CSRF protections where applicable.
- Secure rendering and input handling.
- Protection against unsafe HTML and script injection.
- Request validation.
- Error handling without exposing confidential details.
- Safe handling of user-uploaded content.
- Display of authorization and approval requirements.
- Prevention of accidental exposure of confidential information.
- Secure transport to approved backend endpoints.

Frontend applications shall not store long-lived privileged credentials or independently grant security-sensitive permissions.

### 5.2 API Gateway

`api.worklexx.ai` shall serve as the designated API Gateway entry point.

Gateway responsibilities shall include:

- Request routing.
- Authentication token validation.
- Request-level authorization checks.
- Rate limiting.
- Request size limits.
- Abuse protection.
- Security policy enforcement.
- Input and request validation where appropriate.
- Request correlation.
- Controlled access to internal services.
- API version and endpoint policy management.
- Monitoring and security event generation.

The API Gateway shall not replace service-level authorization.

Backend services shall independently verify authorization for sensitive operations and shall not assume that every internal request is automatically trusted.

The API Gateway shall remain architecturally separate from the identity provider.

### 5.3 Six deployable backend service units

The security architecture shall cover the six deployable backend service units:

1. `api-gateway`
2. `agent-orchestrator`
3. `multimodal-service`
4. `sandbox-runner`
5. `billing-ledger`
6. `adtech-service`

The 23-agent ecosystem shall be implemented as logical agent modules and capabilities, not as 23 separately deployable microservices by default.

### 5.4 AI Gateway and model routing

AI model routing shall remain a logical platform capability within the approved architecture.

It shall not create an undocumented seventh deployable backend service.

AI Gateway capabilities shall be governed by model-provider policies, tenant authorization, data classification, permitted use, rate limits, usage controls, provider-specific security requirements and auditable routing decisions.

### 5.5 Internal service communications

Internal service communication shall use authenticated service identities and approved communication channels.

The architecture shall establish:

- Service identity.
- Service-to-service authorization.
- Network access controls.
- Credential lifecycle.
- Request validation.
- Service-specific permissions.
- Communication logging.
- Failure handling.

Internal network access shall not automatically confer unrestricted service authorization.

---

## 6. Identity and Authentication Architecture

### 6.1 Identity provider

A dedicated identity provider shall manage authentication and identity-related security functions.

The final identity provider remains a Human Decision Pending.

The selected identity provider shall support, as applicable:

- OpenID Connect.
- OAuth 2.0.
- Authorization Code flow.
- PKCE.
- Multi-factor authentication.
- Credential lifecycle.
- Session management.
- Account recovery.
- Login protection.
- Identity federation.
- Administrative controls.
- Authentication event logging.
- Token management.
- User lifecycle management.
- Appropriate security and privacy controls.

### 6.2 Authentication ownership

The identity provider shall be authoritative for authentication credentials and identity authentication mechanisms.

Worklexx shall remain responsible for platform-specific:

- Tenant membership.
- Organization membership.
- Project membership.
- Application roles.
- Resource permissions.
- Agent permissions.
- Business-level authorization.
- Platform policies.

Authentication and application authorization shall remain distinct.

### 6.3 Authentication methods

The implementation shall assess secure support for:

- Password-based authentication where required.
- MFA.
- Passkeys and WebAuthn.
- Social or federated identity providers.
- Enterprise identity federation.
- Secure account recovery.
- Device and session management.

MFA shall be required for designated privileged accounts and sensitive administrative operations, subject to final security policy.

### 6.4 Password security

If Worklexx or its identity provider manages passwords:

- Passwords shall never be stored in plaintext.
- Password hashing shall use an approved password-hashing algorithm.
- Password salts shall be generated appropriately.
- Credential exposure shall be monitored where appropriate.
- Password reset procedures shall be securely implemented.
- Password reset tokens shall be short-lived and single-use.
- Password policy shall follow applicable current guidance.
- Password reset shall not bypass MFA or privileged access safeguards.

### 6.5 Account lifecycle

Account lifecycle controls shall include:

- Registration.
- Identity verification where required.
- Account activation.
- Account suspension.
- Account recovery.
- MFA enrollment.
- Role changes.
- Tenant membership changes.
- Session revocation.
- Account deletion.
- Administrative account lifecycle.
- Service account lifecycle.

Suspended or revoked accounts shall not retain unauthorized access through stale sessions, API credentials or background workflows.

---

## 7. Session Management and OAuth/OIDC Security

### 7.1 Authentication flow

The platform shall use OAuth 2.0 Authorization Code flow with PKCE for browser-based authentication where appropriate.

The architecture shall address:

- State validation.
- Nonce validation.
- PKCE challenge and verifier.
- Exact redirect URI validation.
- Authorization code handling.
- Token validation.
- Session establishment.
- Session termination.
- Token refresh.
- Revocation.
- CSRF protection.

### 7.2 Browser session architecture

A Backend-for-Frontend (BFF) pattern is the preferred candidate for managing browser authentication sessions where applicable.

The PKCE verifier and sensitive token handling shall remain in an appropriately protected server-side context.

The final architecture shall explicitly define whether any access or refresh token is exposed to browser JavaScript. The preferred baseline is to avoid exposing long-lived tokens to browser JavaScript.

### 7.3 Cookie security

Authentication cookies shall be configured with appropriate security attributes, including:

- `Secure`
- `HttpOnly`
- `SameSite`
- Appropriate path restrictions.
- Appropriate host restrictions.
- Session expiration and revocation.

The `__Host-` cookie prefix shall be used where compatible with the chosen architecture and browser requirements. Such cookies require `Secure`, `Path=/` and no `Domain` attribute.

Cookie configuration shall be validated against the actual frontend and BFF deployment topology.

### 7.4 CSRF protection

The platform shall implement CSRF protection appropriate to its authentication and session architecture.

Controls shall include, where applicable:

- SameSite cookies.
- CSRF tokens.
- Origin validation.
- Referer validation where appropriate.
- Request method restrictions.
- Protection against cross-origin state-changing requests.

### 7.5 Session lifecycle

The platform shall define:

- Session creation.
- Session expiry.
- Idle timeout.
- Absolute timeout.
- Session rotation.
- Logout.
- Logout across devices.
- Session revocation.
- Privilege change handling.
- MFA reauthentication requirements.
- Risk-based reauthentication.
- Session audit events.

### 7.6 Refresh token protection

If refresh tokens are used:

- Rotation shall be supported.
- Reuse detection shall be implemented where supported.
- Refresh token storage shall be protected.
- Token revocation shall be supported.
- Tokens shall be scoped and audience-restricted.
- Compromise handling shall be documented.
- Refresh token use shall be logged appropriately.

---

## 8. JWT and Token Validation

JWT validation shall be deterministic and performed by approved authentication components.

### 8.1 Validation requirements

The implementation shall validate:

- Cryptographic signature.
- Approved algorithm.
- Issuer.
- Audience.
- Expiration (`exp`).
- Not-before (`nbf`) where present.
- Subject (`sub`).
- Required scopes and claims.
- Token type and context where applicable.
- Signing key validity.
- Clock skew within an approved limit.

### 8.2 Algorithm restrictions

JWT validation shall use an explicit algorithm allowlist.

The platform shall reject:

- `none` algorithm tokens.
- Unsupported algorithms.
- Algorithm substitution attacks.
- Unexpected token types.
- Invalid signatures.
- Tokens from untrusted issuers.
- Tokens intended for another audience.

### 8.3 Signing key management

Signing keys shall be protected, rotated and managed through the approved identity-provider or cryptographic key-management architecture.

The platform shall support:

- Key identifiers (`kid`).
- Trusted JWKS retrieval where applicable.
- Key rotation.
- Revocation or replacement.
- Cache management.
- Failure handling.
- Key recovery and lifecycle management.

### 8.4 Token scope

Tokens shall not contain excessive privileges.

Authorization scopes and claims shall reflect appropriate permissions and contexts.

A valid authentication token shall not automatically authorize every resource or operation.

---

## 9. Tenant, Organization and Project Security

### 9.1 Tenant isolation

Tenant isolation is a foundational security requirement.

A tenant shall not be able to access another tenant's:

- User records.
- Projects.
- Source code.
- Files.
- Conversations.
- Agent execution data.
- Workflow records.
- Sandbox environments.
- Billing data.
- Credits.
- Ledger entries.
- Integration credentials.
- Generated artifacts.
- Embeddings.
- Logs.
- Private metadata.

### 9.2 Tenant authorization

Every tenant-scoped operation shall validate the tenant context and the user's or service's permission to access the requested resource.

Tenant context shall be established from trusted authentication and authorization mechanisms.

Client-provided tenant identifiers shall not independently establish authorization.

### 9.3 Organization and project authorization

Tenant membership shall not automatically grant unrestricted access to every organization, project or resource within a tenant.

The platform shall support appropriate permission boundaries for:

- Organizations.
- Projects.
- Project collaborators.
- Project administrators.
- Billing administrators.
- Tenant administrators.
- Platform administrators.
- Agent permissions.
- Service identities.

### 9.4 Database enforcement

PostgreSQL Row-Level Security shall be used for tenant-owned data where appropriate.

The implementation shall address:

- RLS policies.
- Restricted database roles.
- `FORCE ROW LEVEL SECURITY` where appropriate.
- Transaction-scoped tenant context.
- Connection pool isolation.
- Background worker context.
- Tenant-aware foreign keys.
- Tenant-aware unique constraints.
- Tenant-aware indexes.
- Adversarial tenant-isolation testing.

A variable such as `app.current_tenant_id` shall not be treated as a security control by itself.

The database role, transaction context, authorization path, connection management and policy enforcement shall be evaluated together.

### 9.5 Tenant context leakage

The implementation shall prevent tenant context leakage through:

- Connection pooling.
- Reused database connections.
- Background jobs.
- Worker processes.
- Cache entries.
- Shared storage.
- Vector retrieval.
- Search indexes.
- Logging.
- Service-to-service communication.

Tenant context shall be appropriately established and cleared for every execution context.

### 9.6 Tenant isolation beyond the database

Tenant isolation shall also be enforced in:

- Object storage.
- Git repositories.
- Sandbox environments.
- Artifact storage.
- Vector retrieval.
- Cache.
- Workflow execution.
- Logs.
- API authorization.
- File processing.
- Third-party integrations.

Database RLS alone shall not be considered sufficient for complete tenant isolation.

---

## 10. Role-Based and Resource-Based Access Control

### 10.1 Authorization model

The platform shall use an authorization model combining appropriate role-based and resource-based controls.

RBAC may provide organizational roles.

Resource-based authorization shall evaluate the actual resource, tenant, organization, project, ownership, permissions, state and requested action.

### 10.2 Authorization requirements

The authorization system shall support:

- Users.
- Organizations.
- Tenants.
- Projects.
- Agents.
- Service identities.
- Administrative roles.
- Permissions.
- Resource ownership.
- Resource sharing.
- Role assignments.
- Revocation.
- Approval requirements.

### 10.3 Default-deny

Access shall be denied unless explicitly permitted.

Unknown roles, invalid permission combinations, missing tenant context and incomplete authorization checks shall not result in implicit permission.

### 10.4 Privilege escalation prevention

The platform shall protect against:

- Role escalation.
- Tenant escalation.
- Organization escalation.
- Project escalation.
- Agent permission escalation.
- Service privilege escalation.
- Administrative impersonation.
- Unauthorized permission assignment.

### 10.5 Administrative access

Administrative access shall be limited, monitored and appropriately protected.

Administrative privileges shall not bypass all tenant, data, financial, approval or security controls by default.

Break-glass access shall be documented, controlled, logged, time-limited and reviewed.

---

## 11. AI Agent Security Architecture

### 11.1 Agent security model

AI agents shall be treated as constrained, policy-governed execution components.

Agents shall not receive unrestricted access to:

- Databases.
- Filesystems.
- GitHub.
- Payment systems.
- Production infrastructure.
- External APIs.
- User credentials.
- Cryptographic keys.
- Administrative controls.

### 11.2 Permission-controlled agents

Each agent shall have a defined:

- Identity.
- Purpose.
- Capability.
- Input scope.
- Data access scope.
- Tool permissions.
- Tenant context.
- Project context.
- Execution context.
- Policy constraints.
- Rate limits.
- Resource limits.
- Audit requirements.
- Approval requirements.
- Failure handling.
- Revocation mechanism.

### 11.3 Agent authorization

Agent permissions shall be granted through explicit authorization policies.

An agent shall not acquire additional permissions merely because an upstream agent, model or user prompt requests them.

Agents shall not independently modify their own security policy, permissions or approval requirements.

### 11.4 Agent-to-agent communication

Agent-to-agent communication shall use controlled orchestration mechanisms.

Agents shall not directly access another agent's private data or execution state unless the relevant policy authorizes the access.

Agent communication shall include appropriate:

- Identity.
- Request context.
- Tenant context.
- Project context.
- Capability authorization.
- Correlation identifiers.
- Audit records.

### 11.5 Agent tool execution

Tools shall be registered, described, permissioned and validated.

The platform shall enforce:

- Tool allowlists.
- Input schemas.
- Authorization.
- Resource scope.
- Rate limits.
- Execution limits.
- Output validation.
- Sensitive data restrictions.
- Approval gates.
- Tool invocation logging.

AI-generated tool arguments shall be treated as untrusted input.

### 11.6 Agent revocation

The platform shall be able to suspend or revoke agent execution, credentials, tool access and workflow permissions when necessary.

Revocation shall be addressed for running workflows, pending tool calls and background execution.

---

## 12. AI Safety, Prompt Injection and Untrusted Content

### 12.1 Prompt injection

The platform shall treat prompt injection as a security threat.

Prompt injection may originate from:

- User prompts.
- Uploaded files.
- Documents.
- Websites.
- Repository content.
- Code comments.
- Emails.
- Images.
- OCR output.
- Video transcripts.
- Audio transcripts.
- External APIs.
- Agent memory.
- Tool output.

### 12.2 Trust separation

The architecture shall distinguish:

- Platform policy.
- Trusted system configuration.
- Developer instructions.
- User instructions.
- Retrieved content.
- Uploaded content.
- Tool output.
- External provider output.
- AI-generated content.

Untrusted content shall not override platform authorization, security policies or deterministic control mechanisms.

### 12.3 Prompt injection defence

Controls shall include, as appropriate:

- Input and source classification.
- Instruction and data separation.
- Context isolation.
- Tool allowlists.
- Tool-specific authorization.
- Least privilege.
- Output validation.
- Human approval for sensitive operations.
- Prompt-injection testing.
- Adversarial testing.
- Safe handling of external content.
- Monitoring for suspicious tool requests.

No single prompt or model instruction shall be considered sufficient protection against prompt injection.

### 12.4 Retrieval security

Retrieved information shall be subject to tenant, resource, project and permission filtering before it is provided to an agent or model.

The retrieval layer shall not assume that an embedding, document identifier or similarity result implies permission to access the underlying content.

### 12.5 AI output security

AI-generated outputs shall be validated before:

- Database writes.
- Tool execution.
- File operations.
- Code execution.
- Deployment.
- Financial operations.
- Permission changes.
- External communication.
- User-facing rendering.

AI-generated outputs shall not directly bypass deterministic authorization or business rules.

### 12.6 Chain-of-thought confidentiality

The platform shall not expose internal chain-of-thought or private reasoning traces as a user-facing feature.

Users may receive concise explanations, execution progress, tool activity, decisions, relevant evidence, summaries, errors and results without exposing private internal reasoning.

---

## 13. Agent Approval and Human Authorization Security

### 13.1 Approval architecture

Sensitive operations shall use deterministic approval enforcement.

AI agents may recommend or request approval but shall not independently authorize their own sensitive actions.

### 13.2 Approval gates

The architecture recognizes:

- GATE-03: Production deployment approval.
- GATE-04: Protected GitHub operations approval.

The definitions, policies and operational requirements for GATE-01, GATE-02, GATE-05 and GATE-06 remain pending formal determination.

### 13.3 GATE-03

Production deployment shall require an appropriate authorization decision.

The approval shall be bound to the applicable:

- Project.
- Tenant.
- Deployment target.
- Artifact or commit digest.
- Deployment action.
- Environment.
- Approver identity.
- Approval time.
- Expiration.
- Applicable policy.

Material changes to the approved artifact, target or deployment action shall invalidate the approval.

### 13.4 GATE-04

Protected GitHub operations shall require appropriate authorization.

The approval shall be bound to the applicable:

- Repository.
- Tenant or project.
- Branch or protected resource.
- Operation.
- Artifact, commit or change reference where applicable.
- Approver identity.
- Approval time.
- Expiration.
- Applicable policy.

Material changes to the approved operation or target shall invalidate the approval.

### 13.5 Approval security controls

Approval controls shall include:

- Approver authentication.
- Authorization verification.
- Approval scope.
- Single-use or replay-resistant approval where applicable.
- Expiration.
- Revocation.
- Tamper-resistant audit records.
- Change invalidation.
- Separation of duties where appropriate.
- Explicit confirmation.
- Enforcement outside the AI model.

### 13.6 Approval bypass prevention

The platform shall not permit AI-generated claims of approval to authorize protected operations.

Approval status shall be determined by the authoritative approval service or approved deterministic mechanism.

### 13.7 Administrative authority

Administrator status shall not automatically imply authority to approve every gate.

Approval authority shall be defined by an approved permission model.

---

## 14. Secure Code Generation and Software Development

### 14.1 Secure software lifecycle

Security shall be integrated into the software development lifecycle.

The platform shall establish secure development practices covering:

- Architecture.
- Requirements.
- Design.
- Code generation.
- Code review.
- Testing.
- Dependency management.
- Build.
- Artifact generation.
- Deployment.
- Monitoring.
- Maintenance.
- Vulnerability remediation.

### 14.2 Generated code

AI-generated code shall be treated as untrusted until reviewed and validated.

Generated code shall undergo appropriate:

- Syntax validation.
- Type checking.
- Linting.
- Unit testing.
- Integration testing.
- Security testing.
- Dependency analysis.
- Secret scanning.
- Code review.
- Policy validation.

### 14.3 Security scanning

Security scanning shall be integrated into appropriate workflows.

The platform shall assess:

- Static application security testing (SAST).
- Dependency scanning.
- Software composition analysis (SCA).
- Secret scanning.
- Container image scanning.
- Infrastructure-as-code scanning.
- Dynamic application security testing (DAST).
- API security testing.
- License analysis.
- Malware scanning.
- Vulnerability management.

Security scanners shall be treated as detection and risk-reduction tools, not guarantees of security.

### 14.4 Software supply chain

The platform shall maintain a software supply-chain security baseline.

Requirements shall include, where appropriate:

- Dependency pinning.
- Lockfiles.
- Approved package sources.
- Package integrity validation.
- SBOM generation.
- Build provenance.
- Artifact integrity.
- Signed artifacts.
- Vulnerability monitoring.
- Dependency update policy.
- Build isolation.
- Release controls.

### 14.5 Vulnerability management

The platform shall establish a vulnerability management process covering:

- Discovery.
- Classification.
- Severity.
- Ownership.
- Remediation.
- Verification.
- Exception handling.
- Risk acceptance.
- Escalation.
- Reporting.

Vulnerability severity shall not be based solely on automated scanner scores.

### 14.6 Secure development references

The platform shall consider applicable secure development standards and guidance, including:

- NIST SP 800-218 Secure Software Development Framework.
- OWASP application security guidance.
- OWASP API Security guidance.
- OWASP ASVS where applicable.
- OWASP Top 10 as an awareness and assessment resource.
- Applicable secure cloud and container guidance.

Standards adoption, certification and compliance claims shall require formal assessment.

---

## 15. API Security

### 15.1 API authorization

Every API endpoint shall enforce authentication and appropriate authorization.

API access shall be restricted by:

- Identity.
- Tenant.
- Organization.
- Project.
- Resource.
- Action.
- Scope.
- Policy.
- Context.

### 15.2 API input validation

API inputs shall be validated using explicit schemas and appropriate validation rules.

Controls shall include:

- Type validation.
- Size limits.
- Range validation.
- Enum validation.
- Structural validation.
- Format validation.
- Business-rule validation.
- Injection prevention.
- Unexpected-field handling.

### 15.3 API abuse protection

The API Gateway and relevant services shall enforce:

- Rate limits.
- Burst limits.
- Request quotas.
- Authentication failure controls.
- Abuse detection.
- Request size limits.
- Resource consumption limits.
- Endpoint-specific protection.
- Appropriate throttling.

### 15.4 API versioning

API versioning shall be controlled.

Breaking changes shall require an appropriate migration and compatibility plan.

### 15.5 Error handling

API errors shall not expose:

- Secrets.
- Tokens.
- Passwords.
- Private database information.
- Internal filesystem paths.
- Confidential source code.
- Unnecessary infrastructure details.
- Sensitive stack traces.

Detailed diagnostic information shall remain available through appropriately protected logs.

### 15.6 Internal APIs

Internal APIs shall be authenticated, authorized and restricted to approved callers.

Internal endpoints shall not be assumed secure merely because they are not publicly exposed.

---

## 16. Frontend Security

Frontend applications shall implement security controls appropriate to their frameworks, runtime and deployment configuration.

### 16.1 Browser security

The frontend security baseline shall assess:

- Cross-Site Scripting (XSS).
- Cross-Site Request Forgery (CSRF).
- Clickjacking.
- Unsafe redirects.
- DOM manipulation.
- Script injection.
- Authentication state.
- Session handling.
- Content exposure.
- Browser storage.
- Third-party scripts.
- Dependency vulnerabilities.

### 16.2 Content Security Policy

Content Security Policy (CSP) shall be evaluated and implemented where applicable.

The policy shall be compatible with the approved application architecture and shall restrict unauthorized script execution and other content sources as appropriate.

CSP shall not be treated as the sole XSS defence.

### 16.3 Security headers

The frontend and applicable backend ingress shall implement appropriate security headers, including:

- Content-Security-Policy.
- Strict-Transport-Security.
- X-Content-Type-Options.
- Referrer-Policy.
- Frame restrictions through appropriate mechanisms.
- Permissions-Policy where applicable.

Header configuration shall be evaluated for each actual ingress and runtime.

### 16.4 Frontend hosting and ingress

Security controls shall be mapped to the actual hosting architecture.

Cloud Armor shall not be assumed to protect every Vercel-hosted frontend, backend ingress, webhook endpoint or WebSocket/SSE path automatically.

The security architecture shall identify the ingress path, security controls and responsibility for each exposed endpoint.

### 16.5 Client-side state

Client-side state shall not be treated as authoritative for:

- Authorization.
- Tenant membership.
- Financial balances.
- Workflow completion.
- Approval status.
- Permissions.
- Security policy.

Server-side validation shall enforce authoritative state.

---

## 17. Multimodal Security and File Handling

### 17.1 Multimodal service

The `multimodal-service` shall handle multimodal processing through controlled, permission-aware workflows.

Supported processing may include:

- Images.
- Audio.
- Video.
- Documents.
- OCR.
- Transcription.
- Classification.
- Extraction.
- Transformation.
- AI-assisted analysis.

### 17.2 Upload security

Uploads shall default to pending or quarantined status until appropriate processing and security checks have been completed.

The platform shall not automatically treat an upload as safe merely because it was submitted by an authenticated user.

### 17.3 Upload controls

The implementation shall establish:

- File size limits.
- File type validation.
- MIME validation.
- Content validation.
- Malware scanning where appropriate.
- Safe file naming.
- Storage isolation.
- Access control.
- Quarantine.
- Processing limits.
- Upload authorization.
- Download authorization.
- Retention.
- Deletion.

File extension, MIME type and user-supplied metadata shall not independently establish trust.

### 17.4 File processing

File processing shall occur in controlled environments.

Processing shall address:

- Parser vulnerabilities.
- Malicious files.
- Archive bombs.
- Decompression limits.
- Memory limits.
- CPU limits.
- Processing timeouts.
- Unsafe embedded content.
- External references.
- File format abuse.

### 17.5 Object storage security

Object storage shall enforce:

- Tenant isolation.
- Access authorization.
- Encryption.
- Controlled object access.
- Secure upload mechanisms.
- Secure download mechanisms.
- Versioning where appropriate.
- Retention policy.
- Deletion policy.
- Backup policy.
- Audit logging.

Signed URLs shall not replace authorization checks.

Signed URLs shall have appropriately restricted permissions, expiration and resource scope.

### 17.6 Multimodal provider data handling

External multimodal and AI providers shall be assessed for:

- Data processing.
- Retention.
- Training use.
- Access.
- Security.
- Privacy.
- Transfer.
- Contractual obligations.
- Provider-specific limitations.

Sensitive content shall not be sent to a provider unless the applicable policy and authorization permit it.

---

## 18. Sandbox and Code Execution Security

### 18.1 Sandbox security objective

The `sandbox-runner` shall execute user-generated and AI-generated code in controlled, isolated environments.

The sandbox shall not be treated as a trusted execution environment for unrestricted access to the platform.

### 18.2 Sandbox technology

gVisor with GKE is a candidate sandbox architecture.

The selection remains subject to a security and operational proof of concept.

Other isolation technologies, including microVM-based alternatives, may be evaluated where appropriate.

### 18.3 Isolation requirements

Sandbox workloads shall be isolated from:

- Host infrastructure.
- Other tenants.
- Other projects.
- Platform secrets.
- Production databases.
- Administrative systems.
- Internal service networks.
- Cloud metadata services.
- Unrestricted external networks.
- Other sandbox workloads.

### 18.4 Sandbox controls

The implementation shall assess and enforce:

- Non-root execution.
- Restricted capabilities.
- Filesystem restrictions.
- Process limits.
- Memory limits.
- CPU limits.
- Execution timeouts.
- Disk limits.
- Network restrictions.
- DNS restrictions.
- IPv4 restrictions.
- IPv6 restrictions.
- Metadata service restrictions.
- Container image controls.
- Image integrity.
- Credential restrictions.
- Environment variable restrictions.
- Workspace cleanup.
- Logging.
- Isolation verification.

### 18.5 Network egress

Sandbox network egress shall default to deny.

Permitted egress shall require explicit policies and appropriate controls.

Controls shall address:

- DNS.
- IPv4.
- IPv6.
- IP ranges.
- Internal networks.
- Cloud metadata.
- Redirects.
- Proxy bypass.
- External service access.
- Data exfiltration.
- Connection limits.

### 18.6 Sandbox credentials

Sandbox workloads shall not receive unrestricted platform credentials.

Credentials shall be:

- Short-lived where practical.
- Scoped.
- Restricted.
- Revocable.
- Protected.
- Auditable.

### 18.7 Sandbox lifecycle

Sandbox environments shall have controlled:

- Creation.
- Authorization.
- Initialization.
- Execution.
- Monitoring.
- Termination.
- Cleanup.
- Recovery.
- Resource release.

### 18.8 Sandbox security testing

Sandbox security testing shall include adversarial tests for:

- Escape attempts.
- Privilege escalation.
- Network bypass.
- Metadata access.
- Filesystem access.
- Cross-tenant access.
- Credential exposure.
- Resource exhaustion.
- Process abuse.
- Persistence.
- Malicious package execution.

gVisor or another selected sandbox technology shall not be described as zero-risk or escape-proof.

---

## 19. Database Security

### 19.1 Database security baseline

The database security architecture shall align with WLX-ARCH-007, DATABASE_ARCHITECTURE.md.

Database security shall include:

- Authentication.
- Authorization.
- Restricted database roles.
- Tenant isolation.
- RLS.
- Encryption.
- Connection management.
- Secrets management.
- Audit logging.
- Backup protection.
- Migration controls.
- Data retention.
- Recovery.
- Security testing.

### 19.2 Least privilege database roles

Database roles shall have restricted permissions.

Application roles shall not automatically receive:

- Superuser privileges.
- Unrestricted schema access.
- Unrestricted table access.
- RLS bypass.
- Administrative privileges.
- Migration privileges.
- Unrestricted data export.

### 19.3 RLS security

RLS policies shall be tested for:

- SELECT.
- INSERT.
- UPDATE.
- DELETE.
- Tenant context.
- Missing tenant context.
- Incorrect tenant context.
- Connection reuse.
- Worker access.
- Administrative access.
- Policy bypass.
- Composite relationships.

### 19.4 Database credentials

Database credentials shall be protected and managed through an approved secrets-management architecture.

Credentials shall not be committed to Git, embedded in frontend applications, printed in logs or exposed through agent output.

### 19.5 Database encryption

Encryption shall be assessed for:

- Transport.
- Storage.
- Backups.
- Replicas.
- Sensitive columns where appropriate.
- Key management.
- Recovery.

### 19.6 Database migration security

Migrations shall be reviewed and authorized.

Migration execution shall use appropriately restricted credentials.

Destructive migrations shall require explicit authorization and appropriate backup and recovery considerations.

### 19.7 Database security testing

Database security testing shall include:

- Tenant-isolation tests.
- RLS tests.
- Authorization tests.
- Injection tests.
- Role privilege tests.
- Connection pool tests.
- Backup restoration tests.
- Migration safety tests.
- Sensitive data access tests.

---

## 20. Financial, Billing and Payment Security

### 20.1 Financial authority

The `billing-ledger` shall be the authoritative deterministic service for financial records, credit balances, reservations, settlement and ledger operations.

AI agents shall not independently create authoritative financial balances or modify posted ledger entries.

### 20.2 Financial security

The financial security architecture shall address:

- Authorization.
- Tenant isolation.
- Payment provider verification.
- Idempotency.
- Ledger integrity.
- Atomic transactions.
- Fraud detection.
- Reconciliation.
- Auditability.
- Dispute handling.
- Administrative controls.
- Refunds.
- Compensating transactions.

### 20.3 Credit lifecycle

The approved credit lifecycle shall include:

1. Usage estimate.
2. Policy and balance check.
3. Atomic credit reservation.
4. Task authorization.
5. Usage measurement.
6. Settlement.
7. Release of unused reservations.
8. Compensation or reconciliation where required.

### 20.4 Ledger integrity

The ledger shall implement:

- Double-entry principles.
- Atomic posting.
- Per-transaction currency consistency.
- Immutable posted entries.
- Controlled draft-to-posted transition.
- Compensating entries.
- Provider-scoped idempotency.
- Reconciliation.
- Audit records.

Posted entries shall not be silently overwritten or deleted to correct errors.

### 20.5 Payment provider security

Payment provider integrations shall implement provider-specific verification.

For Paystack, webhook verification shall use the provider's documented HMAC-SHA512 verification procedure, including verification of the appropriate raw request body and signature using the applicable secret.

Stripe shall use its separate provider-specific verification procedure.

Provider-specific verification procedures shall not be assumed interchangeable.

### 20.6 Webhook processing

Webhook processing shall include:

- Signature verification.
- Provider event identification.
- Unique event tracking.
- Idempotent processing.
- Durable event handling.
- Appropriate acknowledgment.
- Retry handling.
- Reconciliation.
- Monitoring.
- Audit logging.

Browser redirects shall not constitute proof of payment.

### 20.7 Financial access control

Financial operations shall require appropriate permissions.

Financial administration, refunds, ledger adjustments, payment configuration and sensitive financial actions shall be subject to explicit authorization and additional controls where appropriate.

### 20.8 Financial records and deletion

Financial records shall be protected from inappropriate cascading deletion.

Retention, legal requirements, anonymization and correction shall follow approved policies.

---

## 21. AdTech Security and Data Separation

### 21.1 AdTech security boundary

The `adtech-service` shall be architecturally separated from confidential platform data.

The AdTech service shall not have unrestricted access to:

- Private prompts.
- Source code.
- Uploaded files.
- Credentials.
- Secrets.
- Private conversations.
- Confidential project activity.
- Sensitive financial information.
- Restricted agent execution data.

### 21.2 AdTech access

AdTech access shall be limited to authorized advertising data, approved public or aggregated feeds and explicitly permitted information.

Access shall be enforced through:

- Service identity.
- Authorization.
- Database roles.
- Schema separation.
- Network restrictions.
- Data minimization.
- Data classification.
- Audit logging.

### 21.3 Advertising data

Advertising data shall be subject to appropriate:

- Privacy controls.
- Retention.
- Consent where required.
- Data minimization.
- Purpose limitation.
- Access controls.
- Security monitoring.
- Fraud detection.
- Review.

### 21.4 AdTech security testing

Testing shall verify that AdTech cannot access restricted data through:

- Database queries.
- API requests.
- Logs.
- Cache.
- Agent output.
- Search.
- Embeddings.
- Shared storage.
- Analytics.
- Background workers.

---

## 22. Secrets Management and Cryptographic Security

### 22.1 Secrets management

The platform shall use an approved secrets-management solution.

Secrets shall not be stored in:

- Source code.
- Public repositories.
- Frontend bundles.
- Unprotected configuration files.
- Logs.
- AI prompts without explicit authorization.
- Unrestricted database records.
- Sandbox environments without scoped authorization.

### 22.2 Secret types

Secrets may include:

- API keys.
- Database credentials.
- OAuth client secrets.
- Signing keys.
- Payment provider secrets.
- Webhook secrets.
- Cloud credentials.
- GitHub credentials.
- Service credentials.
- Encryption keys.
- Recovery secrets.

### 22.3 Secret lifecycle

The platform shall define:

- Secret creation.
- Storage.
- Access.
- Distribution.
- Rotation.
- Revocation.
- Expiration.
- Recovery.
- Monitoring.
- Incident handling.

### 22.4 Key management

KMS shall be evaluated for cryptographic key management.

KMS does not automatically rotate every application secret or encryption key.

The architecture shall define:

- Key types.
- Key ownership.
- Key hierarchy.
- DEK and KEK roles.
- Envelope encryption where appropriate.
- Key versioning.
- Rotation.
- Re-encryption.
- Revocation.
- Recovery.
- Access controls.
- Audit.
- Cryptographic destruction where applicable.

### 22.5 Encryption

The platform shall assess encryption at rest and in transit.

Approved cryptographic algorithms, key lengths, protocols and implementation libraries shall be selected based on current security guidance.

### 22.6 TLS

Public and internal communications shall use appropriately configured TLS where applicable.

The implementation shall assess:

- Certificate lifecycle.
- Certificate renewal.
- TLS versions.
- Cipher configuration.
- Certificate validation.
- Internal communication.
- Public ingress.
- API endpoints.
- Webhooks.
- External integrations.

### 22.7 Secret exposure response

Exposed secrets shall be treated as security incidents.

The response shall include:

- Identification.
- Revocation.
- Rotation.
- Impact assessment.
- Access review.
- Log review.
- Remediation.
- Incident documentation.

Removing a secret from a current file or commit shall not be considered sufficient if it remains exposed in Git history, logs, backups or other copies.

---

## 23. Infrastructure, Cloud and Network Security

### 23.1 Infrastructure security

Infrastructure shall be provisioned and operated under an approved security baseline.

Infrastructure security shall address:

- Cloud accounts.
- Projects.
- IAM.
- Network.
- Compute.
- Containers.
- Kubernetes.
- Storage.
- Databases.
- Secrets.
- KMS.
- Monitoring.
- Backups.
- Infrastructure configuration.

### 23.2 Network segmentation

The architecture shall establish appropriate network boundaries between:

- Public ingress.
- Frontend workloads.
- API Gateway.
- Backend services.
- Database.
- Sandbox workloads.
- Internal management.
- Build systems.
- External integrations.

### 23.3 Network access

Network access shall default to restrictive policies.

Access shall be permitted only when required by an approved service, workflow or infrastructure policy.

### 23.4 Cloud IAM

Cloud IAM shall implement:

- Least privilege.
- Service identities.
- Restricted permissions.
- Role separation.
- MFA for privileged access.
- Credential lifecycle.
- Audit.
- Privileged access review.

### 23.5 Kubernetes security

If GKE is adopted, the implementation shall assess:

- Cluster access.
- Workload identity.
- RBAC.
- Network policies.
- Admission controls.
- Pod security.
- Image integrity.
- Secrets.
- Resource limits.
- Logging.
- Monitoring.
- Node security.
- Cluster upgrades.
- Vulnerability management.
- Sandbox isolation.

### 23.6 Cloud metadata security

Workloads shall not have unrestricted access to cloud metadata services.

Metadata access shall be restricted and tested, particularly for sandbox workloads.

### 23.7 Infrastructure as code

Infrastructure as code shall be reviewed, validated and scanned.

Security requirements shall include:

- Change review.
- Authorization.
- Version control.
- Secret protection.
- Configuration validation.
- Policy enforcement.
- Scanning.
- Controlled deployment.

---

## 24. Deployment, CI/CD and GitHub Security

### 24.1 CI/CD security

The software build and deployment pipeline shall be protected.

Controls shall address:

- Pipeline authorization.
- Runner security.
- Secret protection.
- Dependency integrity.
- Artifact integrity.
- Build isolation.
- Deployment authorization.
- Branch protection.
- Review.
- Logging.
- Pipeline access.
- Pipeline configuration.

### 24.2 GitHub security

The platform repository and project repositories shall be protected through approved GitHub security settings.

Requirements shall assess:

- Repository access.
- Organization access.
- Branch protection.
- Protected branches.
- Pull request review.
- Required checks.
- Commit integrity.
- Secret scanning.
- Dependabot or equivalent.
- Code scanning.
- Audit logs.
- Token permissions.
- GitHub Actions security.
- Repository secrets.
- Workflow permissions.

### 24.3 GitHub token security

GitHub credentials shall be appropriately scoped, protected, monitored and revoked.

Tokens shall not be exposed to untrusted code or unrestricted sandbox execution.

### 24.4 Build artifacts

Build artifacts shall have integrity controls.

Where appropriate, the platform shall implement:

- Artifact signing.
- Provenance.
- SBOM.
- Integrity verification.
- Build traceability.
- Approved release procedures.

### 24.5 Deployment security

Production deployment shall require GATE-03 authorization.

Deployment authorization shall be bound to the relevant artifact, commit, project, target, environment and action.

Material changes shall invalidate prior approvals.

### 24.6 Protected GitHub operations

Protected GitHub operations shall require GATE-04 authorization.

GATE-04 shall not be merged with GATE-03.

GitHub approval and production deployment approval shall remain separate authorization controls.

### 24.7 Environment separation

The architecture shall establish appropriate separation between:

- Development.
- Testing.
- Staging.
- Production.
- Sandbox execution.
- Build environments.
- Administrative environments.

Production credentials and data shall not automatically be available in development, testing or sandbox environments.

---

## 25. Logging, Monitoring and Security Audit

### 25.1 Security logging

The platform shall maintain appropriate security logs.

Logs shall support:

- Security monitoring.
- Incident investigation.
- Authorization review.
- Financial audit.
- Approval audit.
- Operational monitoring.
- Compliance assessment.

### 25.2 Security events

Security event logging shall include, as appropriate:

- Authentication events.
- Failed authentication.
- MFA events.
- Session creation.
- Session revocation.
- Authorization failures.
- Privilege changes.
- Tenant membership changes.
- Administrative actions.
- Approval requests.
- Approval decisions.
- Approval revocation.
- Deployment actions.
- Protected GitHub operations.
- Secret access.
- Financial events.
- Webhook processing.
- Security policy violations.
- Sandbox activity.
- Suspicious API activity.
- Security incidents.

### 25.3 Audit event content

Audit records shall include relevant fields such as:

- Event identifier.
- Event type.
- Timestamp.
- Actor.
- Actor type.
- Service identity where applicable.
- Tenant context.
- Resource.
- Action.
- Outcome.
- Correlation identifier.
- Approval reference where applicable.
- Security context where appropriate.

### 25.4 Sensitive information exclusion

Logs shall not unnecessarily include:

- Passwords.
- Authentication tokens.
- API secrets.
- Private keys.
- Full payment credentials.
- Sensitive personal data.
- Confidential source code.
- Private prompts.
- Full uploaded file contents.

### 25.5 Log protection

Logs shall be protected against unauthorized:

- Access.
- Modification.
- Deletion.
- Export.
- Disclosure.

Retention and access shall be governed by approved policies.

### 25.6 Monitoring

The platform shall establish security monitoring for:

- Suspicious authentication.
- Privilege escalation.
- Cross-tenant access attempts.
- Unauthorized data access.
- API abuse.
- Agent abuse.
- Prompt injection attempts.
- Sandbox escape indicators.
- Secret exposure.
- Financial anomalies.
- Webhook anomalies.
- Deployment anomalies.
- Unusual network activity.

### 25.7 Alerting

Security alerts shall be classified by severity and routed to designated responders.

Alerting shall include appropriate escalation, investigation and closure procedures.

---

## 26. Security Incident Response

### 26.1 Incident response framework

The platform shall establish an incident response process.

The process shall cover:

1. Preparation.
2. Detection.
3. Triage.
4. Investigation.
5. Containment.
6. Eradication.
7. Recovery.
8. Communication.
9. Post-incident review.
10. Corrective action.

### 26.2 Incident categories

Incident categories shall include, as appropriate:

- Account compromise.
- Credential exposure.
- Tenant data leakage.
- Unauthorized access.
- Privilege escalation.
- Prompt injection resulting in unauthorized action.
- Sandbox escape.
- Data exfiltration.
- Database compromise.
- Financial fraud.
- Payment compromise.
- API abuse.
- Infrastructure compromise.
- Malware.
- Denial of service.
- Supply-chain compromise.
- Insider threat.
- Unauthorized deployment.

### 26.3 Containment capabilities

The architecture shall support appropriate containment capabilities, including:

- Account suspension.
- Session revocation.
- Token revocation.
- Agent suspension.
- Tool revocation.
- Service isolation.
- Sandbox termination.
- Network restriction.
- Credential revocation.
- Secret rotation.
- Workflow cancellation.
- API throttling.
- Deployment suspension.
- Payment operation restriction.

### 26.4 Incident evidence

Incident evidence shall be protected and appropriately retained.

The platform shall preserve relevant:

- Logs.
- Audit events.
- Approval records.
- Workflow records.
- Artifact references.
- Security findings.
- Investigation notes.
- Relevant timestamps.

### 26.5 Incident notification

Notification procedures shall be established in accordance with applicable law, contractual requirements, approved incident policy and incident severity.

### 26.6 Post-incident review

Incident reviews shall identify:

- Root cause.
- Contributing factors.
- Impact.
- Containment effectiveness.
- Recovery effectiveness.
- Control failures.
- Corrective actions.
- Risk changes.
- Lessons learned.

---

## 27. Privacy, Data Protection and Regulatory Security

### 27.1 Privacy by design

Privacy shall be integrated into the platform architecture.

Controls shall address:

- Data minimization.
- Purpose limitation.
- Access control.
- Retention.
- Deletion.
- Consent where required.
- Data subject rights.
- Data classification.
- Privacy risk assessment.
- Third-party processing.
- Cross-border transfer.

### 27.2 Data classification

Data shall be classified according to its sensitivity and security requirements.

Classification shall govern access, storage, processing, transfer, retention, disclosure and deletion.

### 27.3 Personal data

Personal data shall be protected through appropriate technical and organizational measures.

The platform shall assess applicable data protection requirements, including Nigeria's NDPA and other relevant jurisdictions where the platform operates.

### 27.4 Cross-border processing

Cross-border data transfers shall not be assumed compliant merely because a cloud provider or AI provider offers a particular service.

The platform shall assess:

- Data categories.
- Purpose.
- Recipient.
- Location.
- Processing.
- Transfer mechanism.
- Applicable legal requirements.
- Contractual protections.
- Security.
- Retention.
- User rights.

### 27.5 AI provider data protection

AI provider integration shall be governed by appropriate data protection and security requirements.

The platform shall assess:

- Provider retention.
- Training use.
- Processing location.
- Access.
- Confidentiality.
- Data deletion.
- Data transfer.
- Contractual terms.
- Security incidents.

### 27.6 Data deletion

Deletion shall account for:

- Databases.
- Object storage.
- Git repositories.
- Artifacts.
- Embeddings.
- Cache.
- Search indexes.
- Logs where applicable.
- Replicas.
- Backups.
- External providers.
- Legal holds.

Deletion shall follow the approved retention and legal policy.

Restored backups shall not reintroduce records that must remain deleted or anonymized without an appropriate reconciliation process.

### 27.7 Privacy assessment

A formal privacy and data protection assessment shall be completed when required before processing relevant personal data at scale or introducing high-risk processing activities.

---

## 28. Business Continuity, Backup and Disaster Recovery Security

### 28.1 Backup protection

Backups shall be protected against:

- Unauthorized access.
- Modification.
- Deletion.
- Ransomware.
- Credential compromise.
- Tenant data exposure.

### 28.2 Backup controls

The platform shall establish:

- Backup encryption.
- Access restrictions.
- Backup retention.
- Backup integrity.
- Backup monitoring.
- Recovery procedures.
- Restore testing.
- Protection against destructive access.
- Appropriate separation of backup privileges.

### 28.3 Recovery architecture

Disaster recovery shall cover the full platform, including:

- PostgreSQL.
- Temporal persistence and workflow state.
- Object storage.
- Git repositories.
- Financial ledger.
- Identity.
- KMS.
- Secrets.
- Infrastructure.
- Configuration.
- Monitoring.
- Relevant integrations.

### 28.4 Recovery targets

RPO and RTO remain pending formal determination.

Targets shall be established through business impact assessment and validated through recovery testing.

### 28.5 Recovery testing

Recovery testing shall validate:

- Database restoration.
- Ledger integrity.
- Workflow recovery.
- Object storage recovery.
- Git recovery.
- Identity recovery.
- Key recovery.
- Secrets recovery.
- Infrastructure recovery.
- Tenant isolation after restoration.
- Deletion and anonymization reconciliation.

Cloud SQL HA shall not automatically be considered disaster recovery.

### 28.6 Business continuity

The platform shall define business continuity procedures for critical operations, including:

- Authentication.
- Financial services.
- Workflow orchestration.
- Production deployment.
- Incident response.
- Recovery.
- User communication.

---

## 29. Security Testing and Verification

### 29.1 Security testing approach

Security verification shall be integrated throughout implementation and release.

Testing shall assess the effectiveness of the security architecture, not merely the presence of security documentation.

### 29.2 Security testing categories

Testing shall include, as applicable:

- Authentication testing.
- Authorization testing.
- Tenant isolation testing.
- RLS testing.
- API security testing.
- Frontend security testing.
- SAST.
- SCA.
- Secret scanning.
- DAST.
- Container scanning.
- Infrastructure scanning.
- Penetration testing.
- Sandbox isolation testing.
- Prompt injection testing.
- Agent tool authorization testing.
- Financial security testing.
- Webhook verification testing.
- Privacy testing.
- Backup and recovery testing.
- Incident response testing.

### 29.3 Adversarial testing

Adversarial testing shall evaluate whether users, agents, tools, uploaded files, external content or malicious code can bypass security controls.

Testing shall include relevant threat scenarios, including:

- Cross-tenant access.
- Token manipulation.
- Unauthorized tool execution.
- Prompt injection.
- Data exfiltration.
- Privilege escalation.
- Sandbox escape.
- Approval replay.
- Approval bypass.
- Ledger manipulation.
- Webhook forgery.
- Credential exposure.
- Network bypass.
- RLS bypass.
- Unauthorized deployment.

### 29.4 Security acceptance criteria

Security acceptance shall require evidence that:

- Critical security boundaries are implemented.
- Required security tests pass.
- Security findings are reviewed.
- Critical and high-risk findings are appropriately resolved or formally risk-accepted.
- Security policies are enforced.
- Tenant isolation is validated.
- Approval mechanisms are validated.
- Secrets are appropriately protected.
- Sandbox controls are tested.
- Backup and recovery requirements are tested.
- Monitoring and incident response are operationally defined.
- Required security documentation is maintained.

### 29.5 Independent security review

Independent security review and penetration testing shall be planned at appropriate stages before production release.

### 29.6 Security certification

Security documentation or testing shall not be represented as certification.

SOC 2, ISO 27001 or other certification and compliance claims shall require the appropriate formal assessment, evidence, audit and certification process.

---

## 30. Security Risk Management

### 30.1 Security risk register

Security risks shall be managed through WLX-ARCH-011, RISK_REGISTER.md.

The risk register shall include applicable security risks, including:

- Cross-tenant leakage.
- Identity compromise.
- Privilege escalation.
- Prompt injection.
- Unauthorized tool execution.
- Sandbox escape.
- Database compromise.
- Backup failure.
- Approval bypass.
- Privacy noncompliance.
- Ledger inconsistency.
- Insider threats.
- Supply-chain compromise.
- Credential exposure.
- API abuse.
- Infrastructure compromise.

### 30.2 Risk ownership

Every material risk shall have:

- Risk owner.
- Control owner where applicable.
- Risk description.
- Impact.
- Likelihood.
- Score.
- Treatment.
- Status.
- Due date.
- Review date.
- Evidence.
- Escalation.
- Acceptance authority.

### 30.3 Risk acceptance

Risk acceptance shall be performed by an appropriately authorized person.

Project Owner authority and delegation shall be formally established.

Proposed controls shall not be assumed to reduce residual risk until implemented and verified.

### 30.4 Risk review

Security risks shall be reviewed:

- During architecture review.
- During implementation.
- Before production release.
- Following significant changes.
- Following security incidents.
- Following material vulnerability findings.
- Periodically during operations.

---

## 31. Security Responsibilities

Security responsibilities shall be assigned to defined roles.

### 31.1 Project Owner

The Project Owner shall be responsible for establishing or approving:

- Security priorities.
- Risk acceptance authority.
- Security policy.
- Approval authority.
- Architecture decisions.
- Security review requirements.
- Production readiness decisions.

The actual authority and delegation shall be formally documented.

### 31.2 Platform engineering

Platform engineering shall implement approved:

- Authentication integration.
- Authorization.
- Service security.
- Tenant isolation.
- Secure development.
- Infrastructure security.
- Deployment controls.
- Monitoring.
- Recovery controls.

### 31.3 Security function

A designated security function shall oversee:

- Security policy.
- Threat assessment.
- Vulnerability management.
- Security testing.
- Incident response.
- Risk review.
- Security monitoring.
- Security evidence.

The formal assignment of this function remains pending.

### 31.4 Service owners

Service owners shall be responsible for:

- Service-specific security.
- Authorization.
- Data access.
- Service identity.
- Security logging.
- Vulnerability remediation.
- Security testing.
- Secure integration.

### 31.5 Users

Users shall be responsible for:

- Protecting account credentials.
- Using MFA where required.
- Protecting API keys and personal integrations.
- Reviewing sensitive actions.
- Reporting suspicious activity.
- Following platform policies.

---

## 32. Human Decisions Pending

The following security-related decisions require formal resolution before the relevant implementation or production acceptance.

| ID | Decision | Status |
|---|---|---|
| HD-01 | Managed identity provider versus internally managed identity architecture | Pending |
| HD-02 | Temporal Cloud versus self-hosted Temporal | Pending |
| HD-03 | Primary and disaster-recovery regions | Pending |
| HD-04 | Final six-deployable topology and operational deployment model | Pending |
| HD-05 | Vector embedding dimension and pgvector implementation details | Pending |
| HD-06 | Final platform RPO and RTO | Pending |
| HD-07 | Risk acceptance authority and delegation | Pending |
| HD-08 | Final definitions and policies for GATE-01 through GATE-06 | Pending |

Additional security implementation decisions shall be recorded through the appropriate ADRs or controlled architecture decision process.

Pending decisions shall not be treated as approved.

---

## 33. Security Implementation Boundary

This document defines the Phase 0 security architecture baseline.

It does not authorize:

- Infrastructure provisioning.
- Cloud account modification.
- Kubernetes cluster creation.
- Database creation.
- Database migration execution.
- Security policy deployment.
- KMS provisioning.
- Secret provisioning.
- Production deployment.
- GitHub protected operations.
- Repository modification by automated agents.
- Production credential issuance.
- Security configuration execution.
- Penetration testing against live infrastructure.
- Phase 1 implementation.

Security implementation shall begin only after the appropriate Phase 0 review, authorization, implementation planning and applicable approvals.

---

## 34. Related Architecture Documents

| Document ID | Document |
|---|---|
| WLX-ARCH-001 | ARCHITECTURE_OVERVIEW.md |
| WLX-ARCH-002 | SYSTEM_ARCHITECTURE.md |
| WLX-ARCH-003 | TECHNOLOGY_STACK.md |
| WLX-ARCH-004 | REPOSITORY_STRUCTURE.md |
| WLX-ARCH-005 | AGENT_ECOSYSTEM.md |
| WLX-ARCH-006 | SERVICE_BOUNDARIES.md |
| WLX-ARCH-007 | DATABASE_ARCHITECTURE.md |
| WLX-ARCH-009 | DEPLOYMENT_ARCHITECTURE.md |
| WLX-ARCH-010 | DEVELOPMENT_ROADMAP.md |
| WLX-ARCH-011 | RISK_REGISTER.md |
| WLX-ARCH-012 | ADR_REGISTER.md |
| WLX-ARCH-013 | PHASE_0_INSPECTION_REPORT.md |
| WLX-ARCH-014 | TESTING_STRATEGY.md |
| WLX-ARCH-015 | MONITORING_AND_OBSERVABILITY.md |
| WLX-ARCH-016 | COST_AND_SCALABILITY.md |

---

## 35. Final Status

**Document ID:** WLX-ARCH-008  
**Document Name:** Security Architecture  
**Version:** 1.0  
**Status:** Phase 0 — Architecture Baseline  
**Implementation Status:** Not implemented  
**Verification Status:** Pending document save and targeted verification  
**Approval Status:** Pending formal review and approval

This document establishes the proposed security architecture baseline for the Worklexx AI Software Factory.

Security controls described herein are architectural requirements, design principles, proposed implementation controls or verification requirements. They are not evidence of implemented security, operational effectiveness, certification or formal approval.

The architecture shall undergo cross-document consistency review before Phase 1 implementation authorization.

**END OF DOCUMENT**