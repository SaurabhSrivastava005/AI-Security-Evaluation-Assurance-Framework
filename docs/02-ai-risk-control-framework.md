# AI Risk and Control Framework

This document defines the control framework used to assess whether an AI system presents unacceptable operational, security, privacy, and compliance risk. It translates the governance principles established in the AI Governance and Policy document into concrete, testable controls that can be implemented and verified across different industry sectors.

## 1. Objective

The goal is to create a repeatable risk model for AI systems based on actual exposure, not just model capability. The organization must assess both the user-facing behavior and the downstream system impacts. This framework ensures that every AI deployment has documented ownership, defined boundaries, and measurable risk acceptance criteria that align with the organization's governance model.

Risk assessment is not a one-time gate; it is an ongoing process that adapts as the system, its data sources, external dependencies, and threat landscape evolve. This framework provides the structure for that continuous evaluation.

## 2. Risk Categories and Their Industry Implications

The following risk categories must be evaluated for every AI system, with specific attention to how each applies within your operational context.

### Security Risk

**Definition**: Unauthorized access, privilege abuse, credential compromise, or exploitation of system vulnerabilities that could allow an attacker to gain control of AI infrastructure or downstream systems.

**Industry-Specific Contexts**:
- **Financial Services**: Unauthorized access to trading systems, customer account data, or payment infrastructure. An AI system with broad API key access could expose transaction systems if compromised.
- **Healthcare**: Compromise of patient record access, medication ordering systems, or diagnostic equipment integration. A health AI with token-based authentication must prevent lateral movement to clinical workstations.
- **Manufacturing**: Access to industrial control systems, asset tracking, or production line orchestration. An AI monitoring system should not have permissions to modify equipment settings without explicit authorization.
- **Government**: Access to classified information systems, citizen databases, or policy decision platforms. AI agents in government must operate within strict air-gapped or federated trust models.

**Example Controls**: Role-based access control (RBAC) with time-limited tokens, API key rotation and auditing, network segmentation between AI workloads and sensitive systems, sandboxed execution environments with restricted outbound connectivity, secrets management systems with audit trails.

### Privacy Risk

**Definition**: Unauthorized disclosure, inference, or retention of protected personal data, regulated information, or commercially sensitive material. This includes both direct exposure through logs or outputs and indirect exposure through model memorization.

**Industry-Specific Contexts**:
- **Retail and E-Commerce**: Customer purchase history, browsing patterns, loyalty data, or payment information could be inferred from model responses or retained in logs. A recommendation AI must not reveal individual user preferences in aggregated analytics.
- **Legal and Professional Services**: Client names, case information, or privileged communications could be disclosed by an AI assistant if not properly redacted. An AI supporting legal discovery must enforce document-level access controls.
- **Education**: Student performance data, personal information, or family circumstances should not be accessible to all users of an educational AI platform. Role-based retrieval must enforce student privacy even in aggregated analytics.
- **Telecommunications**: Subscriber metadata, call patterns, or network behavior should remain confidential. AI systems analyzing network traffic must enforce data minimization.

**Example Controls**: PII detection and automatic redaction in logs and responses, data minimization (only retrieve what is needed), purpose-limited data access, retention policies with automatic deletion, encryption of data at rest and in transit, audit logging of all data access with alerts for anomalies.

### Operational Risk

**Definition**: System outages, denial of service, unreliable behavior, cascading failures, or inability to recover from errors. This includes both performance degradation and complete unavailability.

**Industry-Specific Contexts**:
- **Utilities and Energy**: An AI-assisted grid management or demand-response system that fails or hangs could lead to power outages. Operational risk includes response timeout, cascading model failures, or resource exhaustion.
- **Transportation**: An AI-assisted routing or dispatch system that becomes unavailable could disrupt logistics or public transit. Fallback to manual processes must be tested and maintained.
- **Hospitality**: An AI-driven reservation or guest services system that fails could impact revenue and customer experience. Graceful degradation and circuit breakers are essential.
- **Retail**: An AI-powered inventory or checkout system that crashes could halt operations. The system must be designed for automatic recovery without manual intervention.

**Example Controls**: Rate limiting and quota enforcement to prevent resource exhaustion, request timeouts and automatic retries with exponential backoff, circuit breakers to prevent cascading failures, health checks and automated restarts, failover to backup systems or manual processes, capacity planning and load testing, version rollback procedures tested and ready for quick deployment.

### Model Behavior Risk

**Definition**: The model producing harmful, biased, incorrect, or unexpectedly offensive outputs. This includes outputs that violate safety policies, produce misinformation, or exhibit harmful stereotypes.

**Industry-Specific Contexts**:
- **HR and Recruiting**: An AI screening candidates could exhibit bias based on protected characteristics (gender, race, national origin, age). Candidate decisions must be validated against adverse impact testing and alternative selection models.
- **Credit and Lending**: An AI evaluating creditworthiness could perpetuate disparate impact or unlawful discrimination. Model outputs must be validated against fair lending standards and explainability requirements.
- **Media and Content**: An AI generating or curating content could produce misinformation, hateful speech, or false information that harms public trust or individual reputations. Content safety checks and human review are required.
- **Cybersecurity and Fraud Detection**: An AI detecting fraudulent activity could misclassify legitimate transactions, causing customer friction. False positive rates and operational impact must be monitored.

**Example Controls**: Adversarial and jailbreak testing, bias and fairness evaluation against protected attributes, refusal behavior validation, output filtering and moderation, human review sampling, regression testing across diverse scenarios, red-teaming exercises by security professionals.

### Supply Chain Risk

**Definition**: Compromised model weights, malicious dependencies, altered prompts, tampered containers, or unsigned artifacts that could introduce malicious behavior or hidden capabilities into the AI system.

**Industry-Specific Contexts**:
- **Defense and Security**: A compromised model or dependency could introduce surveillance, data exfiltration, or backdoor capabilities. Supply chain verification through signed artifacts and attestation is non-negotiable.
- **Financial Compliance**: A tampered model used for regulatory reporting or audit could invalidate compliance evidence. Model and dependency versions must be locked and cryptographically verified.
- **Pharmaceuticals**: An AI involved in drug discovery or clinical trial analysis must use verified models and datasets; a compromised component could lead to unsafe drug approvals.
- **Critical Infrastructure**: An AI used in infrastructure monitoring or control must have fully traceable supply chain provenance; compromised components could enable sabotage.

**Example Controls**: Software Bill of Materials (SBOM) generation for all dependencies, cryptographic signing of model artifacts and containers, dependency vulnerability scanning with automated alerts, lockfiles preventing unintended updates, build attestation proving artifact origin and integrity, exception handling with time-bound expiration and mandatory review.

### Governance Risk

**Definition**: Unapproved use cases, unclear ownership, missing data authorization, bypassed approval workflows, or systems operating outside their defined boundaries. This includes drift where systems evolve beyond their intended use without re-evaluation.

**Industry-Specific Contexts**:
- **Public Sector and Government**: An AI system deployed for one specific purpose (e.g., processing license applications) that is later repurposed for a different function (e.g., fraud detection) without re-approval creates governance risk. Approval must be documented and accessible.
- **Financial Institutions**: An AI model used for internal risk assessment that is later shared with third parties or used for customer-facing decisions without proper re-certification violates governance controls.
- **Healthcare Systems**: An AI diagnostic assistant approved for one type of patient (e.g., outpatient) but used for another (e.g., intensive care) without re-validation creates liability and patient safety risk.
- **Regulated Industries Generally**: Lack of clear ownership or approval trail makes it impossible to hold anyone accountable when something goes wrong, and creates compliance violations during audits.

**Example Controls**: Documented use-case register with business justification, named and formally assigned owners for each system, risk tier classification with clear escalation criteria, authorized data and tool inventory with access controls, change management process requiring re-approval when use changes materially, periodic access reviews and recertification by business owners.

## 3. Risk Assessment Framework

Every AI system must be assessed against the risk categories above. The assessment should answer each of the following questions with documented evidence:

**Purpose and Scope**: What is the approved business purpose of the system, and what are the explicitly prohibited uses? Who is authorized to use it, and under what conditions?

**Data Access and Boundaries**: What data sources can the system access? What data classifications or sensitivities are included? Who is authorized to retrieve data through this system, and are there data scope limitations (e.g., only customer records you own)?

**System Authority and Actions**: What actions can the system take on downstream systems? What are the consequences if those actions fail, execute incorrectly, or are performed without authorization? Can the system modify data, initiate transactions, control equipment, or only read and report?

**Failure Impact and Blast Radius**: What is the maximum impact if the model produces incorrect output, if a component is compromised, or if authorization controls fail? Which business functions, customer segments, or compliance obligations would be affected?

**Control Enforcement Points**: Where are authorization checks performed—at the model layer, the tool gateway, the API layer, or the database layer? Can the model or user bypass controls through prompt manipulation or privilege escalation?

**Failure Detection and Recovery**: How would the organization detect that something has gone wrong (e.g., unauthorized data access, erratic model behavior, component compromise)? How would it contain the damage, notify affected parties, and recover to a safe state?

## 4. Comprehensive Control Framework

The organization must implement controls spanning the following domains. Each domain is addressed in detail in the supporting guidance documents, but they are presented here as an integrated whole.

### Identity, Credentials, and Access

The AI system must enforce authentication of all users and workloads, issue time-limited credentials, and validate every request against a policy database before granting access to data or tools. The model must not be the enforcement point for access control; enforcement must occur in a separate, deterministic service layer.

**Specific expectations**: Unique identity for each user and service agent; credentials that expire and are rotated regularly; least-privilege access by default (users can perform only their assigned role); time-bound or rate-limited access for sensitive operations; immediate revocation and emergency disablement paths.

### Prompt and Model Guardrails

The model's system instructions and safety filters must be versioned, reviewed, and tested. Output must be checked against safety policies before being returned to users. The system must include tests for adversarial inputs and jailbreak attempts.

**Specific expectations**: Prompt templates reviewed and approved before deployment; system instructions documented and version-controlled; output filters that detect and block harmful content; tests validating refusal behavior for out-of-policy inputs; regular re-evaluation of safety measures as new threats emerge.

### Data Classification and Retrieval Controls

Before retrieving data from databases, file systems, or knowledge repositories, the system must verify that the requesting user is authorized for that specific data. Access control must be enforced before the data is returned to the model and before the model incorporates it into an answer.

**Specific expectations**: Clear classification of all data sources (public, internal, confidential, regulated); row- or document-level access controls that prevent cross-tenant or cross-user retrieval; audit logging of all retrieval requests; detection of suspicious access patterns (e.g., a single user requesting thousands of records).

### Tool and API Restrictions

The system must maintain an allowlist of tools the agent is permitted to call. Each tool must be subject to parameter validation, business rule enforcement, and approval workflows for sensitive operations. The system must not allow tools to be enumerated or called based on model suggestions alone.

**Specific expectations**: Explicit allowlist of permitted tools and destination systems; parameter schema validation before execution; approval workflow for irreversible actions; audit logging of all tool invocations; inability to bypass allowlist through prompt manipulation.

### Runtime Isolation and Secrets Management

The AI workload must execute in a sandboxed environment with minimal permissions, no access to production secrets in environment variables, and restricted outbound network access. Secrets must be retrieved from a secure vault at runtime and never logged or exposed.

**Specific expectations**: Ephemeral or containerized execution environments; read-only base images; no production credentials in environment or logs; network policies restricting outbound connections to approved destinations only; secret retrieval from a vault without exposure in logs.

### Logging, Traceability, and Observability

Every significant operation must be logged in a way that allows reconstruction of what happened, who authorized it, and what the outcome was. Logs must be tamper-resistant and retained according to regulatory and operational requirements.

**Specific expectations**: Correlation IDs linking user request through all components; audit logs capturing identity, action, resource, outcome, and timestamp; alerts for policy violations, retries, or anomalies; log retention matching regulatory and operational needs; inability to delete or modify logs retroactively.

### Monitoring and Incident Response

The organization must actively monitor AI systems for signs of malfunction, unauthorized access, or drift from expected behavior. Incident response procedures must be documented, tested, and ready for rapid execution.

**Specific expectations**: Defined alert conditions and thresholds; incident runbooks describing detection, containment, evidence preservation, notification, and recovery steps; regular testing of incident response procedures; clear escalation paths and communication channels.

### Supply Chain and Artifact Provenance

All artifacts (model weights, containers, dependencies, prompts) must be signed and cryptographically verifiable. Dependencies must be scanned for known vulnerabilities, and exceptions must be tracked with risk acceptance.

**Specific expectations**: Software Bill of Materials (SBOM) for all software components; signed artifacts with verified signatures; dependency vulnerability scans with automated alerting; lockfiles pinning specific versions; change control requiring approval before updating dependencies.

### Release and Change Management

Changes to the model, prompts, data sources, policies, or infrastructure must be reviewed, approved, and tested before deployment. Rollback procedures must be tested and ready.

**Specific expectations**: Release manifest documenting all components and versions; evidence package showing test results and approvals; canary or staged rollout to detect issues early; rollback plan tested and ready; post-release monitoring for unexpected behavior.

## 5. Mandatory Control Testing and Validation

The control framework is only effective if it is tested and proven to work. The organization must perform concrete tests demonstrating that controls enforce their intended limits.

### Access Control Tests

- **Privilege Boundary Tests**: Attempt to use the system with insufficient permissions and verify denial. Confirm that privilege escalation attempts fail.
- **Cross-Tenant Leakage Tests**: In multi-tenant systems, attempt to retrieve data belonging to other tenants and verify that access is denied.
- **Approval Bypass Tests**: Attempt to trigger sensitive actions without completing the approval workflow and verify that execution is prevented.
- **Token Replay Tests**: Use an expired or revoked token and verify denial. Confirm that tokens cannot be reused after revocation.

### Model and Prompt Tests

- **Prompt Injection Tests**: Attempt to manipulate the model through embedded instructions in user input or retrieved content. Verify that the system follows its intended instructions, not instructions hidden in data.
- **Jailbreak and Refusal Tests**: Attempt to elicit harmful outputs or force the model to ignore safety guidelines. Validate that the model consistently refuses or redirects.
- **Output Filter Tests**: Pass harmful content through the output filter and verify that it is detected and blocked. Confirm filters are applied before returning results to users.

### Data Access Tests

- **Retrieval Permission Tests**: Attempt to retrieve data outside the user's authorization scope and verify denial. Confirm that row- and document-level controls function correctly.
- **Data Leakage Tests**: Check logs and audit records to confirm that no unauthorized data retrieval attempts expose sensitive information.
- **Stale Data Detection**: Verify that data is marked as stale after deletion or revocation and is not returned in subsequent retrievals.

### Tool and Agent Tests

- **Tool Enumeration Tests**: Attempt to discover tools not on the allowlist and verify that only approved tools are callable.
- **Parameter Injection Tests**: Attempt to pass malicious parameters to tools (e.g., SQL injection, command injection) and verify that parameters are validated and sanitized.
- **Approval Bypass Tests**: Attempt to trigger tool use without completing the approval workflow and verify that execution is prevented.
- **Idempotency Tests**: Execute the same tool call multiple times and verify that the system handles retries correctly without creating duplicate effects.

### Isolation and Network Tests

- **SSRF and DNS Rebinding Tests**: Attempt to use the AI system to access internal metadata services, private networks, or restricted infrastructure. Verify that egress policies block these attempts.
- **Container Escape Tests**: Attempt to break out of the sandbox or access the host filesystem. Verify that escape attempts fail and isolation holds.
- **Resource Exhaustion Tests**: Attempt to consume excessive CPU, memory, or disk through the AI system and verify that quotas and limits prevent denial of service.

### Supply Chain Tests

- **Artifact Integrity Tests**: Modify a signed artifact and verify that signature verification fails. Confirm that unsigned or incorrectly signed artifacts are rejected.
- **Dependency Vulnerability Tests**: Introduce a known vulnerable dependency and verify that scanning detects it and blocks deployment.

## 6. Stop-Ship Conditions and Release Gates

A production release cannot proceed if any of the following conditions are true. These are not optional guidelines; they are hard stops.

**Policy Enforcement Failure**: The system defaults to allowing access when policy is uncertain or unwritten. This violates the principle of deny-by-default and must be fixed before release.

**Tool Bypass Capability**: A tool can be called without passing through the approval gateway, or the tool gateway can be bypassed through the model. This creates unauthorized privilege escalation.

**Sensitive Data Outside Scope**: The system can retrieve data that is outside the user's authorized scope, or retrieval permissions are not enforced before the model incorporates data. This violates data governance.

**Untrackable Material Actions**: A significant action (data modification, external system call, approval decision) occurs without being logged or traceable to a user, policy, or approval. This prevents accountability and incident investigation.

**Isolation or Rollback Failure**: The system cannot be isolated from production infrastructure, the model cannot be rolled back to a previous version, or secrets cannot be revoked. This prevents rapid response to security issues.

**Critical Test Failures**: Mandatory tests (privilege denial, approval enforcement, data access boundaries, SSRF/escape prevention, artifact integrity) fail. These are evidence that controls do not work.

**Unresolved Exceptions**: Time-bound risk exceptions expire without resolution or remediation plan. This violates the governance principle that exceptions are not permanent.

## 7. Evidence Requirements

Every AI system must produce an evidence package demonstrating control implementation and testing. This package is the basis for risk acceptance and release approval.

**Threat Model Documentation**: A documented analysis of what could go wrong, including attack scenarios, insider threats, supply-chain compromise, and model failures. The threat model should be specific to the system, its data, its users, and its industry.

**Control Mapping**: A clear mapping of each threat to one or more controls that mitigate it. This should show that every significant threat has at least one mitigating control, and that critical threats have multiple controls (defense in depth).

**Test Evidence and Results**: Documentation of all mandatory tests performed, their results, and any issues found and remediated. Test results must be tied to specific versions of the system being released.

**Risk Assessment and Decision**: A summary of residual risks (risks that cannot be fully eliminated), the organization's acceptance of those risks, and the signature of the accountable decision maker (typically the executive sponsor and security architect).

**Retest and Remediation Records**: Evidence that issues found in testing were remediated and re-tested. If issues could not be resolved, documentation of compensating controls and risk acceptance.

**Configuration and Version Records**: Exact versions of the model, prompts, evaluators, infrastructure, dependencies, and data sources used in the release. This allows reproduction of the evidence package and investigation of production incidents.

## 8. Continuous and Evolving Risk Assessment

Risk assessment does not end at release. The organization must continuously monitor and re-assess.

**Quarterly Control Review**: Revisit the threat model and control framework. Confirm that controls remain effective and that new threats (e.g., new attack techniques, new model vulnerabilities) are addressed.

**Incident-Driven Assessment**: When an incident occurs or a close call is detected, perform root-cause analysis and determine whether controls were missing or ineffective. Update controls accordingly.

**Dependency and Provider Updates**: When underlying models, libraries, or infrastructure services are updated, reassess risk. New vulnerabilities might be introduced; new capabilities might require new controls.

**Data and Use Evolution**: As the system's data sources or use cases expand, reassess data access controls and retrieval scope.

**Regulatory and Compliance Changes**: As regulations evolve (e.g., AI Act, algorithmic accountability laws), reassess whether the control framework remains aligned with legal requirements.

## 9. Alignment with AI Governance Policy

This risk and control framework operationalizes the governance principles established in the AI Governance and Policy document. The framework is not independent; it is tightly coupled to governance:

**Risk Tier Classification** maps to governance roles and approval authority. A high-risk system (Tier 3 or 4) requires executive sponsor review and sign-off, full security architect involvement, and mandatory gates. A low-risk system (Tier 1) may proceed with less formal review but still requires documented risk assessment.

**Control Ownership** aligns with governance roles. The data owner approves data access controls. The security architect reviews the threat model and control coverage. The compliance/privacy lead validates privacy controls. The platform lead ensures architecture and operational controls are sound.

**Approval Workflows** defined in governance are enforced through controls described in this framework. If governance says "high-risk actions require executive approval," the control framework must include an approval gateway that enforces this requirement.

**Evidence Retention** required by governance is produced by the control framework. Every governance decision (use-case approval, risk tier assignment, control sign-off) is supported by evidence from this framework.

**Exception Management** defined in governance applies to control testing. If a control cannot be implemented (e.g., data access control is not technically feasible), the exception must be documented, risk-accepted by the appropriate governance owner, and time-bound.

## 10. Sector-Specific Implementations

While this framework is universal, its application varies by sector based on regulatory requirements, data sensitivity, and operational impact.

### Financial Services

The control framework must support regulatory requirements (GDPR, CCPA for customer data; Dodd-Frank for transparency; fair lending laws for credit decisions). Risk tiers should be elevated for any system that touches transaction data, credit decisions, or customer financial data. Supply chain controls must be especially rigorous due to third-party model/data dependencies.

### Healthcare

The control framework must enforce HIPAA privacy controls (minimum necessary, purpose limitation, audit logging). Risk tiers should be elevated for any system supporting diagnosis, treatment, or patient triage. Model bias testing must address known health disparities. Approval workflows must include clinical review.

### Government and Public Sector

The control framework must support transparency and accountability to citizens. Identity and access controls should follow government security standards (NIST, FedRAMP). High-risk tiers should require formal Authority to Operate (ATO). Data residency and sovereignty constraints may apply (data must remain within specific jurisdictions).

### Retail and E-Commerce

The control framework must protect customer privacy and prevent fraud. Data access controls must enforce customer data segmentation (a customer can only see their own order history). Approval workflows for price changes, discounts, or refunds must be auditable.

### Manufacturing and Logistics

The control framework must protect trade secrets and intellectual property. Tool and API restrictions must prevent unauthorized access to equipment control systems. Operational continuity is critical; fallback to manual processes must be well-defined.

## 11. Checklist for Control Framework Implementation

Before a system advances to production release, verify the following:

- [ ] **Threat Model Complete**: A documented threat model specific to this system, data, and use case exists and has been reviewed by security personnel.
- [ ] **Risk Tier Assigned**: The system is classified into a risk tier (1-4) aligned with governance policy and approved by the executive sponsor.
- [ ] **Controls Mapped**: For each threat, at least one control mitigates it. Critical threats have multiple controls (defense in depth).
- [ ] **Access Control Tests Passed**: Privilege boundary, approval bypass, and token revocation tests all pass.
- [ ] **Data Access Tests Passed**: Retrieval permission, cross-user leakage, and stale data detection tests all pass.
- [ ] **Model Safety Tests Passed**: Prompt injection, jailbreak, and output filter tests all pass.
- [ ] **Tool and Agent Tests Passed**: Enumeration, parameter injection, and approval bypass tests all pass.
- [ ] **Isolation Tests Passed**: SSRF, container escape, and resource exhaustion tests all pass.
- [ ] **Supply Chain Verified**: Artifacts are signed, dependencies are scanned, SBOMs are generated, and exceptions are tracked.
- [ ] **Logging and Alerting Configured**: All material operations are logged with correlation IDs and timestamps. Alert thresholds are defined and tested.
- [ ] **Incident Response Runbooks Exist**: Detection procedures, containment steps, and recovery processes are documented and tested.
- [ ] **Rollback Procedure Tested**: The system can be rolled back to a known-good state without data loss or cascading failures.
- [ ] **Evidence Package Complete**: All test results, approvals, and threat model documentation are collected and accessible.
- [ ] **Governance Alignment Verified**: The risk tier, data access, approval workflow, and ownership match what was approved in governance.

## 12. Related Guidance

- [Master Guide: AI Security Evaluation and Assurance](ai-security-evaluation-and-assurance.md)
- [AI Governance and Policy](01-ai-governance-policy.md) — Defines roles, risk tiers, and approval authority.
- [Model and Prompt Assurance](03-model-and-prompt-assurance.md) — Defines model evaluation and safety testing.
- [Data, RAG, and Privacy](04-data-rag-and-privacy.md) — Defines data access controls and privacy safeguards.
- [Identity, Access, and Authorization](05-identity-access-and-authorization.md) — Defines authentication and authorization controls.
- [Agent and Tool Security](06-agent-and-tool-security.md) — Defines tool invocation safety and approval workflows.
- [Runtime, Network, and Isolation](07-runtime-network-and-isolation.md) — Defines execution sandbox and egress controls.
- [Supply Chain and Artifact Provenance](08-supply-chain-and-artifact-provenance.md) — Defines artifact signing and dependency management.
- [Observability, Detection, and Incident Response](09-observability-detection-and-incident-response.md) — Defines monitoring, alerting, and response procedures.

## 13. Final Note

The risk and control framework is not a compliance checkbox. It is a practical tool for identifying where things can go wrong and ensuring that the organization has concrete measures to prevent or detect those failures. Effective implementation requires discipline, clear ownership, and ongoing commitment to testing and refinement. Organizations that treat this framework as a one-time gate or a paper exercise will inevitably miss risks and experience preventable incidents. Organizations that implement it as a living, evolving system will be better positioned to deploy AI safely and maintain stakeholder trust.
