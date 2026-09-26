# 03 — Evaluation and Testing

## Objective

Produce reproducible evidence that the system is secure, safe, reliable, useful, and bounded under representative normal, adversarial, and failure conditions.

## Test layers

1. **Component:** policy decisions, schemas, parsers, retrievers, redaction, prompt templates, and adapters.
2. **Application:** authentication, authorization, API contracts, output handling, file uploads, rate limits, and secure SDLC checks.
3. **AI security:** direct and indirect prompt injection, jailbreaks, data poisoning, secret disclosure, excessive agency, confused deputy, SSRF, and tool abuse.
4. **Data and privacy:** permission propagation, deletion, retention, leakage, inference, and tenant isolation.
5. **Runtime and supply chain:** sandbox escape, egress, metadata access, resource exhaustion, artifact integrity, and dependency exposure.
6. **Resilience:** provider timeouts, quota exhaustion, policy-store failure, identity outage, index corruption, queue backlog, and partial downstream failure.
7. **Human oversight:** reviewer workload, approval binding, escalation, decision quality, and bypass resistance.

## Evidence requirements

Each result should identify the exact system version, model, prompt, policy, dataset, evaluator, environment, timestamp, test inputs, expected outcome, observed outcome, severity, remediation, and retest status.

## Quality is not a security waiver

Aggregate model or quality scores cannot compensate for failed authorization, isolation, privacy, secret management, supply-chain, or destructive-action controls. Mandatory failures remain release blockers.

## Recommended tooling

Prompt/model evaluation, adversarial testing, tracing, policy-as-code, SAST/DAST/SCA, SBOM, container scanning, load testing, and chaos tooling may be combined, but tools are evidence generators—not substitutes for control ownership or judgment.
