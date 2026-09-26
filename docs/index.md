# AI Security Evaluation & Assurance Framework

## Purpose

This is the master navigation document for an enterprise AI security assurance program. It applies to LLM, RAG, copilot, and agentic systems across design, release, and operations.

## How to use this repository

1. Classify the use case and assign accountable owners.
2. Define the system boundary, data flows, authority model, and threats.
3. Implement deterministic controls outside the model.
4. Produce evaluation and security evidence.
5. Pass mandatory release gates before production.
6. Operate continuous monitoring, response, recovery, and re-evaluation.

## Domain guides

| Area | Guide | Primary outcome |
|---|---|---|
| Governance and risk | [01 Governance and Risk](01-governance-and-risk.md) | Accountable ownership, risk tier, scope, and exceptions |
| Security controls | [02 Security Controls](02-security-controls.md) | Enforced identity, data, tool, runtime, and supply-chain controls |
| Evaluation and testing | [03 Evaluation and Testing](03-evaluation-and-testing.md) | Reproducible quality, safety, security, and adversarial evidence |
| Assurance and release | [04 Assurance and Release](04-assurance-and-release.md) | Stage gates, approval records, stop-ship criteria, and rollback |
| Operations and incidents | [05 Operations and Incident Response](05-operations-and-incident-response.md) | Monitoring, containment, recovery, and learning |
| Implementation roadmap | [06 Implementation Roadmap](06-implementation-roadmap.md) | Practical adoption sequence and maturity progression |

## Existing reference standard

The complete reference text remains available in [AI Security Evaluation and Assurance](ai-security-evaluation-and-assurance.md). The domain guides make that material easier to implement and assign.

## Enterprise readiness statement

This repository is an enterprise-oriented framework and evidence model, not a turnkey security product or compliance certification. Each organization must adapt it to its architecture, legal obligations, risk appetite, and control environment.
