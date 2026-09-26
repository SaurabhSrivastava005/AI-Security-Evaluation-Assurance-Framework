# AI Governance and Policy

This document defines the governance structure required to evaluate, approve, deploy, and operate AI systems in an organization.

## 1. Objective

AI governance is not only about model quality. It is about establishing who can use AI, for what purpose, under which controls, with which evidence, and with what oversight.

Every AI deployment should have a named accountable owner for:

- business purpose
- data access
- model selection and versioning
- operational reliability
- security and compliance
- release approval

## 2. Policy principles

The organization should adopt the following principles:

- AI use must be aligned to approved business purpose.
- AI systems must not access data beyond approved scope.
- Sensitive actions require explicit human approval.
- Systems must be capable of suspension, rollback, and recovery.
- Evidence of behavior and controls must be retained and reviewable.
- No aggregate model score can override critical security or compliance failures.

## 3. Governance roles and responsibilities

| Role | Responsibilities |
|---|---|
| executive sponsor | approves risk tier, budget, and exceptions |
| product owner | confirms intended business use and workflow |
| model owner | manages model choice, prompts, evaluation thresholds |
| data owner | approves data access, retention, and deletion |
| platform lead | oversees architecture, controls, and release readiness |
| security architect | validates threat model and control coverage |
| compliance/privacy lead | ensures lawful use and alignment to policy |
| SRE/operations | manages alerts, recovery, and incident response |
| approver/reviewer | authorizes high-risk actions and reviews evidence |

## 4. Risk classification

AI systems must be classified by highest applicable risk. A use case should be treated as higher risk when:

- it accesses regulated, confidential, or personal data
- it has the ability to read or modify operational systems
- it can cross trust boundaries or external networks
- it makes decisions with legal, financial, or safety impact
- it acts with autonomy beyond human review

## 5. Mandatory governance controls

- approved use-case register
- named owners and accountability structure
- risk tier classification
- authorized data and tool inventory
- approval workflow for sensitive actions
- change and exception management
- periodic access review
- incident reporting and learning loops

## 6. Evidence required

The governing body should require evidence that:

- the use case is approved and within scope
- data access is justified and restricted
- model and prompt versions are controlled
- test and review records are retained
- exceptions are owned and time-bound
- incidents are investigated and root causes are closed

## 7. Organization-level checklist

Before a system is approved for production, confirm:

- [ ] use case and risk tier are defined
- [ ] ownership is assigned
- [ ] prohibited use is documented
- [ ] data boundaries are approved
- [ ] approval paths are documented
- [ ] required evidence is retained
- [ ] human escalation path exists
- [ ] rollback and suspension path exists

## 8. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [AI Risk and Control Framework](02-ai-risk-control-framework.md)
- [Release, Change, and Continuous Assurance](11-release-change-and-continuous-assurance.md)

