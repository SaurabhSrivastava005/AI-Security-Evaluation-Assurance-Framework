# 02 — Security Controls

## Control principle

The model is never the enforcement point. Deterministic controls must independently enforce identity, authorization, data boundaries, tool permissions, approval state, quotas, and safe failure.

## Control domains

### Identity and authorization

Use workload identity, delegated user context, short-lived credentials, least privilege, purpose binding, tenant isolation, object-level authorization, revocation, and deny-by-default behavior.

### Data and RAG

Enforce source permissions before retrieval and after index or cache operations. Test deletion propagation, stale permissions, cross-tenant isolation, metadata leakage, poisoning, retention, residency, and redaction.

### Tool gateway

All tool calls should pass through a versioned gateway that validates schemas, destinations, authorization, approval state, rate limits, idempotency, and transaction reconciliation. Never grant unrestricted shell, browser, database, or administrative access.

### Runtime and network

Use ephemeral least-privileged execution, read-only images, resource quotas, restricted filesystem access, egress and DNS controls, destination allowlists, SSRF defenses, and no production secrets in model-visible context.

### Supply chain

Pin and verify models, prompts, adapters, dependencies, containers, datasets, and evaluators. Maintain SBOMs, signatures, provenance, vulnerability disposition, and reproducible promotion records.

### Evidence and observability

Correlate initiator, purpose, model, prompt, policy, retrieval, tool calls, approvals, outcomes, and side effects. Protect, redact, retain, and make evidence tamper-evident according to policy.

## Stop-ship examples

- Policy uncertainty fails open.
- An agent bypasses the tool gateway or approval requirement.
- Unauthorized or cross-tenant data is retrieved.
- An artifact cannot be verified or its provenance is unknown.
- A material action cannot be reconstructed or safely reconciled.
