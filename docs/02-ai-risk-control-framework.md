# AI Risk and Control Framework

This document defines the control framework used to assess whether an AI system presents unacceptable operational, security, privacy, and compliance risk.

## 1. Objective

The goal is to create a repeatable risk model for AI systems based on actual exposure, not just model capability. The organization must assess both the user-facing behavior and the downstream system interactions.

## 2. Risk categories

| Category | Typical risk | Example controls |
|---|---|---|
| security | unauthorized access, privilege abuse, exfiltration | IAM, policy enforcement, sandboxing, egress restrictions |
| privacy | disclosure of protected data | PII minimization, access control, redaction, retention policy |
| operational | outages, denial of service, unreliable actions | quotas, retries, timeouts, rollback, kill switch |
| model behavior | harmful or incorrect outputs | red team, evals, safety checks, human review |
| supply chain | compromised dependencies or artifacts | SBOM, signed images, provenance, dependency policy |
| governance | unapproved use or unclear ownership | risk tiering, approval workflow, control register |

## 3. Risk assessment questions

The team should answer each question with evidence:

- What is the allowed purpose and prohibited purpose?
- What data can be accessed and by whom?
- What actions can the system take?
- What are the consequences of unsafe or incorrect behavior?
- What is the maximum blast radius of a failure?
- Which controls prevent unauthorized actions?
- How are failures detected, contained, and recovered?

## 4. Control framework

The organization should map each AI system to a control set spanning:

- identity and access
- prompt and model guardrails
- data classification and retrieval controls
- tool and API restrictions
- runtime isolation
- logging and traceability
- monitoring and incident response
- release governance

## 5. Mandatory control tests

The control framework should be validated with concrete tests, including:

- access denial and privilege boundary tests
- prompt injection and indirect instruction tests
- retrieval permission leak tests
- tool abuse, parameter injection, and approval bypass tests
- SSRF, egress, and network isolation tests
- secret handling and redaction tests
- artifact integrity and provenance tests
- forced failure and kill-switch tests

## 6. Stop-ship conditions

The organization should block release if any mandatory requirement fails, including:

- policy uncertainty defaults to allow
- a tool can bypass approval or access restrictions
- sensitive data can be retrieved outside scope
- logging cannot support reconstruction of material actions
- the system cannot be isolated or rolled back securely
- critical safety or security tests fail

## 7. Evidence expectations

The risk assessment must produce evidence supporting:

- threat model
- controls and residual risk
- decision owners and sign-off
- retest outcomes
- exceptions and time-bound remediation plans

## 8. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [AI Governance and Policy](01-ai-governance-policy.md)
- [Model and Prompt Assurance](03-model-and-prompt-assurance.md)

