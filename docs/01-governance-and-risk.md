# 01 — Governance and Risk

## Objective

Ensure every AI system has a defined purpose, accountable owners, risk classification, prohibited uses, and an approved operating boundary before implementation.

## Required records

- Use-case and business-purpose record
- System boundary and data-flow diagram
- Intended and prohibited use
- Affected users, populations, and jurisdictions
- Data classification, retention, residency, and deletion requirements
- Named business, model, data, platform, security, privacy, and operations owners
- Agent authority record and human approval requirements
- Threat model and residual-risk decision

## Risk tiers

| Tier | Example | Minimum posture |
|---|---|---|
| 1 | Low-impact drafting or approved public search | Regression, privacy, abuse, and basic security tests |
| 2 | Internal workflow support or reversible actions | Identity, permission-aware retrieval, gateway controls, adversarial tests, monitoring |
| 3 | Regulated decisions or autonomous external actions | Independent review, red team, resilience testing, mandatory gates, human oversight |
| 4 | Unbounded access or irreversible high-impact action without accountable review | Do not deploy; redesign or escalate |

Classification uses the highest applicable risk, not an average score.

## Accountability

The release authority must be able to identify who owns business purpose, model behavior, data access, policy enforcement, operational response, and risk acceptance. Exceptions must be time-bound, approved by an accountable authority, backed by compensating controls, and tracked to closure.

## Exit criteria

Do not proceed to design assurance until the risk tier, owners, boundary, authority model, prohibited uses, initial threat model, and control register are approved.
