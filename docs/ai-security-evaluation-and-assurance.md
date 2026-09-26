# AI Security Evaluation and Assurance Framework

## 1. Purpose

This document defines how an organization evaluates, certifies, releases, and operates LLM, retrieval-augmented generation (RAG), and agentic systems that process enterprise, health, government, financial, and other sensitive data.

This is not a prompt-testing checklist. It is an assurance operating model for the complete system, including the model, application, retrieval stack, identity, policy enforcement, tool gateway, runtime, network, infrastructure, and human oversight.

The release authority must answer four questions with evidence:

1. What is the system allowed to do, for whom, and against which data and systems?
2. What happens when the model, user, retrieved content, tool, provider, network, policy service, or reviewer behaves unexpectedly?
3. How will the organization detect, contain, investigate, notify, recover, and learn from a failure?
4. Which exact model, prompt, policy, data, tool, runtime, evaluator, and infrastructure versions produced the evidence?

A model-quality score cannot compensate for a failed authorization, isolation, secret-management, privacy, supply-chain, or destructive-action control.

## 2. Scope and risk tiers

This framework applies to:

- Chat assistants and productivity copilots
- RAG systems
- Browser and web agents
- Coding and workflow agents
- Autonomous research systems
- Model gateways
- Fine-tuned or adapted models
- Agentic tool wrappers

Assess the use case before implementation. Classification is based on the highest applicable risk, not an average.

| Tier | Typical use | Required assurance |
|---|---|---|
| 1 | Low-impact drafting or search over approved public content | Regression, privacy, basic security, abuse, and operational tests |
| 2 | Internal workflow support or bounded reversible actions | Identity, permission-aware retrieval, tool gateway, adversarial tests, monitoring, and human sampling |
| 3 | Health, legal, financial, employment, benefits, government services, or autonomous external actions | Independent security review, mandatory gates, red team, resilience tests, and human approval |
| 4 | Unbounded access, irreversible high-impact decisions without accountable review, or operation where mandatory controls cannot be enforced | Do not deploy. Redesign or escalate to formal risk authorization |

A government services portal that exposes non-public aggregate statistics should be treated as Tier 3 when an agent can browse, enumerate, download, authenticate, or call APIs.

## 3. Control objectives

Use established security engineering practices alongside AI-specific testing. No single taxonomy is sufficient.

| Objective | Primary references | Evidence expected |
|---|---|---|
| AI threats and misuse | MITRE ATLAS, OWASP GenAI and Agentic guidance, abuse cases | Threat model, attack paths, mitigations, and residual risk |
| Application security | OWASP ASVS, API Security, secure SDLC | SAST, DAST, SCA, API tests, penetration findings, and remediation |
| Cybersecurity governance | NIST CSF 2.0, NIST AI RMF, ISO 27001 and ISO 27002 where applicable | Control mapping, owners, risk acceptance, and assurance record |
| Privacy | Privacy impact assessment and applicable privacy and health-data rules | Data inventory, purpose, minimization, retention, deletion, and access evidence |
| Cloud and runtime | CIS benchmarks, container and Kubernetes security, zero trust architecture | Hardened images, network policy, identity, runtime, and recovery tests |
| Software and model supply chain | SLSA-related controls, SBOM, signing, provenance, and dependency policy | Signed immutable artifacts, SBOM, attestation, and vulnerability disposition |
| Service operations | SRE, SLO, and incident-management practices | Alert tests, runbooks, restore, failover, rollback, and incident exercises |

Record the crosswalk in the project control register. A framework reference is not evidence of implementation.

## 4. Real-world system design

### 4.1 Independent enforcement

The model must not be the policy enforcement point. Every sensitive retrieval and tool call must pass through deterministic controls that receive the initiating identity, agent identity, business purpose, resource, action, and risk context.

The enforcement path must support:

- Deny by default
- Short-lived credentials
- Per-action authorization
- Rate and volume limits
- Destination allowlists
- Approval state
- Idempotency
- Correlation IDs
- Safe failure states
- Complete decision records

### 4.2 Agent authority model

Create an authority record for every agent.

| Field | Required decision |
|---|---|
| Agent identity | Workload identity, owner, environment, and lifecycle |
| Human initiator | How delegated identity and purpose are preserved |
| Allowed data | Datasets, fields, rows, documents, classification, and jurisdiction |
| Allowed tools | Versioned registry entry and risk class |
| Allowed actions | Read, draft, reversible write, irreversible write, or prohibited |
| Limits | Time, calls, concurrency, tokens, bytes, pages, transactions, and cost |
| Approval | Actions requiring one or two human approvals |
| Safe state | Behavior on uncertainty, timeout, denial, or telemetry loss |
| Evidence | Required trace fields and retention period |

Do not give an agent a general-purpose browser session, administrator token, unrestricted shell, broad database role, or the full permission set of the initiating user.

### 4.3 Controlled tool gateway

The agent submits a structured request to a gateway. The gateway validates the schema and business rules, evaluates policy independently, obtains approval where required, uses isolated short-lived credentials, executes only allowed operations, and records the outcome.

The gateway must distinguish rejected, retryable, accepted, completed, partial, and unknown outcomes. Non-idempotent operations must never be retried blindly. A successful HTTP response is not proof that the intended business operation completed.

### 4.4 Runtime and network isolation

Run the agent in an ephemeral, least-privileged sandbox with a read-only image, no production secrets, restricted filesystem access, CPU and memory quotas, constrained DNS, and restricted outbound destinations. Block metadata services, private network ranges, unauthorized protocols, and uncontrolled browser sessions.

### 4.5 Trace and evidence

Every material run must have one correlation ID connecting the initiator, purpose, risk tier, agent plan, model call, prompt and policy versions, memory access, retrieval filters and sources, policy decisions, tool requests, approvals, side effects, errors, and final outcome.

Evidence must be access-controlled, redacted where necessary, tamper-evident, retained according to policy, and usable for investigation and reconciliation.

## 5. Threat model and test objectives

Model threats using attack trees, STRIDE, MITRE ATT&CK, MITRE ATLAS, OWASP testing, and domain abuse cases.

| Threat path | Real-world failure | Test objective and expected control |
|---|---|---|
| Indirect prompt injection | A page, email, or PDF instructs the agent to ignore restrictions | Content remains untrusted; system policy and tool permissions remain unchanged |
| Excessive agency | The agent enumerates endpoints or retries after denial | Gateway blocks alternate paths, applies quotas, and records escalation |
| Confused deputy | The agent uses broad user access for a narrower task | Each call checks purpose, resource, and delegated scope |
| RAG permission leak | An index returns a document after source access is revoked | ACLs are enforced before retrieval and after cache and index operations |
| Tool abuse | Generated parameters cause an unsafe write or bulk export | Schema, policy, approval, transaction, and reconciliation controls block it |
| Secret disclosure | A token appears in content, memory, logs, or a browser session | Secrets are isolated, redacted, short-lived, and never returned to the model |
| Data poisoning | An untrusted document changes future agent behavior | Provenance, ingestion scanning, quarantine, and re-evaluation are enforced |
| SSRF or lateral movement | A browser or fetch tool reaches metadata or internal services | Egress, DNS, destination, and runtime controls prevent access |
| Supply-chain compromise | A package, model, adapter, prompt, or container is altered | Pinned, scanned, signed, and provenance-verified artifacts are promoted |
| Denial of service | Recursive delegation or context growth exhausts quota | Deadlines, loop limits, budgets, circuit breakers, and admission control work |
| Repudiation | The provider cannot prove which records were accessed | Tamper-evident, correlated, and access-controlled evidence is retained |

## 6. Evaluation program lifecycle

### Phase 0: Intake and boundary

Record intended use, prohibited use, affected parties, decisions, actions, data, jurisdictions, dependencies, providers, users, scale, and baseline process.

Exit evidence:

- Use-case record
- Data-flow diagram
- Authority record
- Risk tier
- Initial threat model
- Control register
- Named owners

### Phase 1: Design assurance

Define the allowed state machine, safe states, approval rules, tool registry, policy decision points, network flows, credential paths, retention, telemetry, service objectives, recovery objectives, and release thresholds.

Exit evidence:

- Architecture review
- Authorization matrix
- Tool contracts
- Policy tests
- Privacy assessment
- Resilience design
- Test plan

### Phase 2: Build and component testing

Run unit and contract tests for business rules, policy decisions, schemas, prompt templates, parsers, retrievers, memory, redaction, tool adapters, and output encoders. Scan code, dependencies, images, infrastructure, and secrets.

Exit evidence:

- Reproducible CI results
- SBOM
- Scan disposition
- Policy coverage
- Secret-scan result
- Artifact attestation

### Phase 3: Integration and adversarial testing

Use production-like identity, policy, network, data permissions, quotas, and tool behavior. Execute direct and indirect injection, encoded and multilingual attacks, jailbreaks, denial paths, privilege escalation, exfiltration, SSRF, poisoning, replay, and abuse cases.

Run attacks against the full system, not only the model endpoint. Assert actual downstream side effects and audit records.

Exit evidence:

- Attack inventory
- Reproducible traces
- Severity assessment
- Remediation
- Retest record
- Independent security sign-off

### Phase 4: Operational and human assurance

Load-test variable token and tool workloads. Inject identity, model, provider, network, policy, index, SIEM, approval, and target-system failures. Exercise the kill switch, credential revocation, egress blocking, rollback, restore, and reconciliation procedures.

Exit evidence:

- Failure-injection results
- Alert-to-action timings
- Runbook execution
- Recovery evidence
- Human-factors assessment
- Incident report

### Phase 5: Progressive release

Start with shadow evaluation or a synthetic cohort. Then use a restricted canary with feature flags, quotas, cohort limits, and an explicit stop authority. Expand only when security, quality, operations, and evidence gates pass.

Exit evidence:

- Release manifest
- Signed decision
- Canary comparison
- Alert review
- Rollback rehearsal
- Post-release approval

### Phase 6: Continuous assurance

Monitor model, prompt, policy, tool, data, retrieval, identity, network, cost, usage, outcome, and attack drift. Re-run relevant tests after any material change to the model, provider, prompt, policy, tool, data, evaluator, runtime, or infrastructure.

Exit evidence:

- Change assessment
- Production sample review
- Drift report
- Access recertification
- Provider review
- Incident-to-test linkage

## 7. Production test catalog

### 7.1 Identity and authorization

Test token audience, issuer, expiry, replay, workload identity, delegated scopes, tenant isolation, object-level authorization, purpose binding, just-in-time privilege, emergency access, revocation, and fail-closed behavior.

### 7.2 Agent and tool behavior

Test discovery, allowlists, parameter substitution, destination substitution, pagination, bulk extraction, repeated denial, recursive delegation, memory contamination, deadlines, loop termination, approval binding, idempotency, reconciliation, and unknown outcomes.

### 7.3 RAG, data, and privacy

Test permission changes after indexing, row and document filtering, cache isolation, metadata leakage, stale data, deletion propagation, embedding and index provenance, poisoned content, inference from aggregates, retention, and data residency.

### 7.4 Application and API security

Apply secure SDLC controls including SAST, DAST, SCA, API contract tests, fuzzing, authentication and session tests, CSRF protection, file-upload validation, deserialization tests, output encoding, rate limits, and abuse controls.

### 7.5 Network, runtime, and supply chain

Test SSRF, DNS rebinding, unrestricted egress, metadata services, internal discovery, browser session theft, filesystem access, shell escape, container isolation, resource exhaustion, artifact tampering, signature validation, and dependency vulnerabilities.

### 7.6 Resilience and response

Inject provider timeouts, quota exhaustion, malformed outputs, policy-store unavailability, identity outage, index corruption, queue backlog, SIEM loss, target-system partial failure, and regional outage. Verify safe states, alerting, containment, recovery, and reconciliation.

## 8. Open-source framework selection

Open-source tools should be assembled as a control stack. They are not interchangeable, and none is a complete security product. Build a proof of value using representative data, identity, tools, policies, and operational conditions.

- **Promptfoo**: Declarative prompt and model comparisons, custom assertions, provider comparisons, and CI regression checks.
- **DeepEval**: Pytest-style tests and custom metrics around LLM applications, structured outputs, claims, and workflow behavior.
- **Ragas**: Retrieval and answer dimensions such as context relevance, faithfulness, and response relevance.
- **Giskard**: Quality, robustness, bias, and risk tests with collaborative scenario management.
- **garak**: Automated probes for unsafe completion, leakage, and jailbreak-oriented weaknesses.
- **Microsoft PyRIT**: Multi-turn adversarial testing and attack orchestration.
- **Inspect AI**: Reproducible, composable evaluations with tasks, solvers, scorers, and evidence.
- **OpenTelemetry**: Vendor-neutral traces, metrics, and logs for correlation across the system.
- **OPA and Cedar**: Deterministic policy-as-code enforcement independent of the model.
- **OWASP ZAP, Nuclei, Semgrep, CodeQL, Trivy, Syft, and Grype**: Web, API, code, infrastructure, container, and SBOM security.
- **k6, Locust, Chaos Mesh, and Litmus**: Load and failure testing across services and Kubernetes environments.

Make reproducible execution, version pinning, CI or API access, custom assertions, exportable evidence, data-egress control, redaction, and failure handling mandatory selection criteria.

## 9. Reference CI/CD assurance pipeline

```text
Pull request:
  secrets -> formatting -> unit and contract tests -> policy tests -> focused regression set

Build:
  locked dependencies -> SAST and SCA -> SBOM -> image scan -> signed artifact and provenance

Integration:
  identity -> ACL and RAG -> tool gateway -> network and egress -> secrets -> memory -> audit trace

Security campaign:
  injection -> jailbreak -> exfiltration -> poisoning -> SSRF -> privilege -> replay -> abuse

System assurance:
  end-to-end task -> approval -> side effect -> idempotency -> reconciliation -> safe state

Operations:
  load -> quota -> timeout -> provider outage -> policy outage -> restore -> rollback -> kill switch

Release:
  independent security, privacy, and domain review -> mandatory gates -> shadow or canary -> signed decision

Production:
  traces -> SIEM or SOAR -> drift -> attack replay -> access review -> incident-to-regression
```

## 10. Medicare-style public-sector scenario

Assume an autonomous research agent is asked to find Medicare statistics. The intended task is read-only, but the agent can browse, follow links, download files, and call APIs.

A safe design publishes an approved dataset catalog and machine-readable API. The agent identity receives read-only, field-level, time-bound, and volume-limited access to those datasets only. The gateway validates every request, applies policy, blocks alternate destinations, and records the complete trace.

The test plan must include public and private boundary cases, changed permissions after indexing, non-public metadata, aggregate inference, hidden instructions in documents, alternate URL attempts, rate exhaustion, and endpoint enumeration.

An incident exercise simulates endpoint enumeration. The response team suspends the agent, revokes its credentials, blocks egress, preserves tamper-evident evidence, identifies accessed resources, notifies accountable owners, restores the safe state, and adds the attack to regression testing.

## 11. Mandatory release gates and scorecard

| Domain | Required evidence | Stop-ship condition |
|---|---|---|
| Identity | Authority record, access matrix, denial and revocation tests | Agent accesses a resource outside delegated purpose or scope |
| Authorization | Versioned policy, fail-closed test, and decision logs | Policy uncertainty defaults to allow |
| Agent and tools | Registry, schemas, approval, side-effect, replay, and reconciliation tests | Model bypasses gateway or approval |
| Data and privacy | Permission propagation, deletion, retention, DLP, and negative retrieval tests | Cross-tenant, unauthorized, or irreversible data exposure |
| Runtime and network | Sandbox, egress, SSRF, metadata, and lateral-movement tests | Unapproved destination or runtime escape |
| Supply chain | SBOM, scan, signature, provenance, and exception register | Unverified artifact or unresolved critical exposure |
| Detection | Complete trace, alert injection, runbook, and timing evidence | Material action cannot be reconstructed or detected |
| Resilience | Failure injection, restore, rollback, kill switch, and reconciliation | Security control failure permits unsafe continuation |
| Human control | Reviewer authority, workload, evidence, and binding approval tests | Approval is cosmetic, bypassable, or unauditable |
| Quality and safety | Versioned regression, adversarial, domain, and segment results | Critical safety or prohibited-action threshold fails |
| Governance | Risk decision, owners, expiry, and change triggers | Mandatory failure is waived through aggregate scoring |

Mandatory failures cannot be converted into a conditional release. Non-mandatory conditions require bounded exposure, compensating controls, an owner, funded remediation, a due date, and an expiry.

## 12. Operational cadence and ownership

The product owner owns the intended outcome and workflow. The model owner owns model, prompt, routing, and evaluator evidence. The data owner owns rights, quality, lineage, and retrieval evidence. Security owns threat modeling, security testing, incident readiness, and control assurance. The platform owner owns runtime, identity integration, network, and deployment evidence. The risk or compliance owner owns the decision record and exceptions.

Every pull request runs deterministic, policy, secret, and focused regression tests. Every release runs the complete applicable security, adversarial, resilience, and evidence gates. Weekly or risk-based reviews assess drift, incidents, access, provider changes, and open exceptions.

## 13. Required artifacts

- Use-case, risk, and prohibited-use record
- System, data-flow, and trust-boundary diagrams
- Agent authority, tool registry, and authorization matrix
- Threat model, abuse cases, and control register
- Privacy, data classification, retention, and residency assessment
- Versioned datasets, rubrics, attack corpus, evaluator configuration, and thresholds
- SBOM, dependency decisions, artifact signatures, and provenance
- Security, privacy, adversarial, resilience, and human-oversight reports
- Trace schema, redaction design, dashboards, alert rules, and runbooks
- Release manifest, signed decision, and exception register
- Kill switch, revocation, rollback, restore, reconciliation, and incident evidence
- Post-incident root cause, corrective action, and regression result

## 14. Exit criteria

The system is production-ready only when its exact release boundary is reproducible, mandatory controls pass, representative attacks fail safely, downstream side effects are bounded and reconciled, telemetry supports investigation, human controls are binding, recovery procedures have been exercised, and accountable owners have signed the release decision.

## 15. Recommended implementation approach

For a real-world enterprise deployment, build the minimum operating stack in this order:

1. Identity and access control
2. Tool gateway with explicit authorization and approval
3. Policy-as-code enforcement for data and action restrictions
4. Logging and trace correlation with redaction
5. Model and retrieval evaluation with representative adversarial datasets
6. RAG permission and retrieval validation
7. Runtime isolation and network egress controls
8. Secret scanning and artifact provenance checks
9. Red-team and adversarial campaigns
10. Automated regression and incident replay

Do not start by buying or deploying a broad evaluation platform. Start by proving the secure path for one real workflow, then add the corresponding automation, controls, and evidence.

This is the practical production standard for AI security assurance.
