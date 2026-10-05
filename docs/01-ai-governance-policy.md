# AI Governance and Policy

This document sets out a practical governance model for AI use across an organization. It is designed to help teams decide whether an AI use case is appropriate, who is accountable, what controls are required, and what evidence must be retained before the system is used in production.

The goal is simple: AI should be used only where there is clear business value, defined responsibility, approved data access, and enough controls to manage risk.

## 1. Objective

AI governance is not only about model quality. It is about controlling the full lifecycle of AI use:

- who can use it
- for what purpose
- what data it may access
- what decisions require human review
- what evidence must be retained
- what happens if the system fails or behaves unexpectedly

Every AI deployment should have a named accountable owner for:

- business purpose
- data access
- model selection and versioning
- operational reliability
- security and compliance
- release approval

## 2. Core policy principles

The organization should apply the following principles to all AI use cases:

- AI use must be aligned to an approved business purpose.
- AI systems must not access data outside the approved scope.
- Sensitive actions require explicit human approval.
- The system must be capable of suspension, rollback, and recovery.
- Evidence of model behavior, controls, and approvals must be retained and reviewable.
- A model score or output cannot override critical security, legal, or compliance failures.

## 3. Governance roles and responsibilities

| Role | Core responsibility |
|---|---|
| executive sponsor | approves risk tier, budget, and exceptions |
| product owner | confirms intended business use and operational workflow |
| model owner | selects and manages the model, prompt, and evaluation thresholds |
| data owner | approves data access, retention, and deletion |
| platform lead | oversees architecture, release readiness, and operational controls |
| security architect | reviews threat model and control coverage |
| compliance/privacy lead | verifies lawful use and policy alignment |
| SRE/operations | monitors system health, incidents, and recovery |
| approver/reviewer | approves high-risk actions and reviews evidence |

A single person may hold more than one role in a small organization, but accountability must still be clearly assigned.

## 4. Risk classification

AI systems should be classified by the highest applicable risk. A use case should be treated as higher risk when it:

- accesses regulated, confidential, or personal data
- can read or modify operational systems
- crosses trust boundaries or connects to external systems
- makes decisions with legal, financial, or safety impact
- operates with autonomy beyond human review

### Simple risk levels

| Risk level | Typical examples | Minimum expectation |
|---|---|---|
| low | internal productivity tools, document summarization, general knowledge support | basic approval, limited data access, monitoring |
| medium | customer support workflows, internal research assistants, workflow recommendations | formal owner, data approval, human review for sensitive outputs |
| high | credit decisions, hiring support, patient triage, operational control, access decisions | full governance review, explicit approval, audit trail, rollback plan |

If the system touches sensitive data or can affect people, it should not be treated as low risk by default.

## 5. Mandatory governance controls

Every approved AI system must have the following controls in place:

- approved use-case register
- named owners and accountability structure
- risk tier classification
- authorized data and tool inventory
- approval workflow for sensitive actions
- change and exception management
- periodic access review
- monitoring, alerting, and incident reporting
- rollback and recovery procedure

These controls should be implemented as a minimum standard for all business units.

## 6. Evidence required

The organization should require evidence showing that:

- the use case is approved and within scope
- data access is justified, restricted, and reviewed
- model and prompt versions are controlled
- tests and reviews are completed and retained
- exceptions are time-bound and assigned to an owner
- incidents are investigated and root causes are closed

Evidence should be accessible to the relevant governance owners and should be retained for the period required by law, policy, or operational need.

## 7. Minimum implementation checklist

Before a system is approved for production, confirm all items below:

- [ ] use case and risk tier are defined
- [ ] business owner is assigned
- [ ] technical owner is assigned
- [ ] data owner has approved access
- [ ] prohibited uses are documented
- [ ] data boundaries are approved
- [ ] approval path for sensitive actions is documented
- [ ] required evidence is retained
- [ ] human escalation path exists
- [ ] rollback and suspension path exists
- [ ] monitoring and alerting are configured
- [ ] incident reporting route is defined

## 8. Working example across industries

### Customer support chatbot
- Purpose: answer common customer questions
- Risk: usually low to medium
- Controls: approved knowledge base, human escalation, logging of customer interactions, no access to financial or identity data unless approved

### HR or hiring support
- Purpose: shortlist applicants or summarize applications
- Risk: medium to high
- Controls: human review of outcomes, no hidden decision authority, no use of sensitive personal data beyond approved scope, documented exception handling

### Operational decision support
- Purpose: detect anomalies, recommend maintenance, or support workflow routing
- Risk: medium to high depending on impact
- Controls: approved integration boundaries, override capability, alerting, audit log of decisions, recovery plan

The same governance model can be used across sectors; the main difference is the risk level and the strength of controls required.

## 9. Operational expectations

AI systems should not be treated as a one-time project. Governance is ongoing.

Organizations should review:

- whether the system remains within its approved purpose
- whether access still matches the approved scope
- whether model performance is acceptable
- whether incidents or close calls have been addressed
- whether controls still align to the latest risk level

The governance process should be repeatable, not ad hoc.

## 10. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [AI Risk and Control Framework](02-ai-risk-control-framework.md)
- [Release, Change, and Continuous Assurance](11-release-change-and-continuous-assurance.md)

## 11. Practical rule

If an AI system is handling sensitive data, making decisions that affect people, or operating without a clear human override, it should be treated as a governed business system, not an experimental tool.
