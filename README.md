# AI Security Evaluation and Assurance Framework

A production-oriented framework for evaluating, certifying, releasing, and operating LLM, retrieval-augmented generation (RAG), and agentic AI systems with enterprise-grade security controls and assurance processes.

This repository separates the security assurance implementation guide from the broader enterprise AI and data strategy repository. It covers the complete system: model, application, retrieval stack, identity, policy enforcement, tool gateway, runtime, network, human oversight, and infrastructure.

## Start here

- [AI Security Evaluation and Assurance Framework](docs/ai-security-evaluation-and-assurance.md)

## What this framework answers

The release authority must be able to answer these questions with evidence:

1. What is the system allowed to do, for whom, and against which data and systems?
2. What happens when the model, user, retrieved content, tool, provider, network, policy service, or reviewer behaves unexpectedly?
3. How will the organization detect, contain, investigate, notify, recover, and learn from a failure?
4. Which exact model, prompt, policy, data, tool, runtime, evaluator, and infrastructure versions produced the evidence?

A model-quality score cannot compensate for a failed authorization, isolation, secret-management, privacy, supply-chain, or destructive-action control.

## Coverage

- Chat assistants, copilots, RAG systems, browser and web agents
- Coding, workflow, autonomous research, and tool-using agents
- Model gateways and fine-tuned or adapted models
- Identity and authorization, permission-aware retrieval, and tenant isolation
- Tool safety, approval, idempotency, reconciliation, and bounded side effects
- Prompt injection, excessive agency, confused deputy, secret disclosure, poisoning, SSRF, and supply-chain threats
- Runtime isolation, egress control, observability, incident response, and recovery
- Progressive release, mandatory stop-ship gates, and continuous assurance

## Risk tiers

| Tier | Typical use | Required assurance |
|---|---|---|
| 1 | Low-impact drafting or search over approved public content | Regression, privacy, basic security, abuse, and operational tests |
| 2 | Internal workflow support or bounded reversible actions | Identity, permission-aware retrieval, tool gateway, adversarial tests, monitoring, and human sampling |
| 3 | Health, legal, financial, employment, benefits, government services, or autonomous external actions | Independent security review, mandatory gates, red team, resilience tests, and human approval |
| 4 | Unbounded access, irreversible high-impact decisions without accountable review, or unenforceable mandatory controls | Do not deploy; redesign or escalate to formal risk authorization |

## Evaluation lifecycle

1. **Intake and boundary** — use case, data flows, authority, risk tier, threat model, and owners
2. **Design assurance** — state machine, safe states, approvals, policy points, network flows, and test plan
3. **Build and component testing** — unit, contract, policy, code, dependency, secret, SBOM, and attestation checks
4. **Integration and adversarial testing** — production-like identity, permissions, quotas, tools, attacks, side effects, and audit records
5. **Operational and human assurance** — load, failure injection, kill switch, revocation, recovery, and human-factors exercises
6. **Progressive release** — shadow evaluation, restricted canary, explicit stop authority, and rollback rehearsal
7. **Continuous assurance** — drift monitoring, production sampling, access recertification, provider review, and incident-to-regression linkage

## Recommended control stack

- Promptfoo, DeepEval, Ragas, Giskard, garak, Microsoft PyRIT, and Inspect AI for evaluation and adversarial testing
- OpenTelemetry for correlated traces, metrics, and logs
- OPA or Cedar for deterministic policy-as-code enforcement
- OWASP ZAP, Nuclei, Semgrep, CodeQL, Trivy, Syft, and Grype for application and supply-chain security
- k6, Locust, Chaos Mesh, and Litmus for load and failure testing

These tools are components of a control stack, not substitutes for authorization, isolation, privacy, governance, or operational controls.

## Mandatory release principle

Mandatory failures cannot be converted into a conditional release through aggregate scoring. Any non-mandatory exception must have bounded exposure, compensating controls, an owner, funded remediation, a due date, and an expiry.

## Implementation order

1. Identity and access control
2. Tool gateway with explicit authorization and approval
3. Policy-as-code enforcement
4. Redacted logging and trace correlation
5. Model and retrieval evaluation with representative adversarial data
6. RAG permission and retrieval validation
7. Runtime isolation and network egress controls
8. Secret scanning and artifact provenance
9. Red-team and adversarial campaigns
10. Automated regression and incident replay

Start by proving the secure path for one real workflow; then add automation, controls, and evidence.

## Contributing

Contributions that improve threat models, evaluation methods, implementation guidance, or real-world examples are welcome. Adapt the framework to the organization’s risk profile, regulatory obligations, and operational context.

## License

This framework is provided as a reference for enterprise AI security assurance. Organizations should review and adapt it for their specific legal, regulatory, privacy, and security requirements.
