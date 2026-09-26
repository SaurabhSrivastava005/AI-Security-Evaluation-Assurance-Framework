# AI Security Evaluation and Assurance Framework

A production-oriented framework for evaluating, certifying, releasing, and operating LLM, retrieval-augmented generation (RAG), and agentic AI systems with enterprise-grade security controls and assurance processes.

This repository provides a pragmatic, organization-ready AI governance and assurance model. It is structured as a master guide plus domain-specific guidance that teams can apply in real deployments.

## Start here

- [Master guide](docs/ai-security-evaluation-and-assurance.md)
- [Documentation map](docs/ai-security-evaluation-and-assurance.md#document-map)

## What this framework answers

The release authority must be able to answer these questions with evidence:

1. What is the system allowed to do, for whom, and against which data and systems?
2. What happens when the model, user, retrieved content, tool, provider, network, policy service, or reviewer behaves unexpectedly?
3. How will the organization detect, contain, investigate, notify, recover, and learn from a failure?
4. Which exact model, prompt, policy, data, tool, runtime, evaluator, and infrastructure versions produced the evidence?

A model-quality score cannot compensate for failed authorization, isolation, secret management, privacy, supply-chain, or destructive-action controls.

## Documentation structure

- [01 AI Governance and Policy](docs/01-ai-governance-policy.md)
- [02 AI Risk and Control Framework](docs/02-ai-risk-control-framework.md)
- [03 Model and Prompt Assurance](docs/03-model-and-prompt-assurance.md)
- [04 Data, RAG, and Privacy](docs/04-data-rag-and-privacy.md)
- [05 Identity, Access, and Authorization](docs/05-identity-access-and-authorization.md)
- [06 Agent and Tool Security](docs/06-agent-and-tool-security.md)
- [07 Runtime, Network, and Isolation](docs/07-runtime-network-and-isolation.md)
- [08 Supply Chain and Artifact Provenance](docs/08-supply-chain-and-artifact-provenance.md)
- [09 Observability, Detection, and Incident Response](docs/09-observability-detection-and-incident-response.md)
- [10 Human Oversight and Approvals](docs/10-human-oversight-and-approvals.md)
- [11 Release, Change, and Continuous Assurance](docs/11-release-change-and-continuous-assurance.md)

## Coverage

- chat assistants, copilots, RAG systems, browser and web agents
- coding, workflow, autonomous research, and tool-using agents
- model gateways and fine-tuned or adapted models
- identity and authorization, permission-aware retrieval, and tenant isolation
- tool safety, approval, idempotency, reconciliation, and bounded side effects
- prompt injection, excessive agency, confused deputy, secret disclosure, poisoning, SSRF, and supply-chain threats
- runtime isolation, egress control, observability, incident response, and recovery
- progressive release, mandatory stop-ship gates, and continuous assurance

## Risk tiers

| Tier | Typical use | Required assurance |
|---|---|---|
| 1 | Low-impact drafting or search over approved public content | regression, privacy, basic security, abuse, and operational tests |
| 2 | Internal workflow support or bounded reversible actions | identity, permission-aware retrieval, tool gateway, adversarial tests, monitoring, and human sampling |
| 3 | Health, legal, financial, employment, benefits, government services, or autonomous external actions | independent review, mandatory gates, red team, resilience tests, and human approval for material actions |
| 4 | Unbounded access, irreversible high-impact decisions without accountable review, or unenforceable mandatory controls | do not deploy; redesign or escalate to formal risk authorization |

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

## Contributing

Contributions that improve threat models, evaluation methods, implementation guidance, or real-world examples are welcome. Adapt the framework to the organization's risk profile, regulatory obligations, and deployment model.

## License

This framework is provided as a reference for enterprise AI security assurance. Organizations should review and adapt it for their specific legal, regulatory, privacy, and security requirements.

