# Human Oversight and Approvals

This document defines how organizations ensure that high-risk AI actions remain under appropriate human control and evidence-based review.

## 1. Objective

Human oversight must be meaningful, auditable, and tied to actual system behavior. Approval cannot be cosmetic or bypassable.

## 2. Approval model

The organization should define which actions require:

- no approval
- one-step approval
- two-step approval
- exception-based approval with documented risk

Approval should be required for:

- irreversible writes
- access to regulated or sensitive data
- external system actions
- privileged or high-impact operations
- material changes to model, data, or policy

## 3. Human review design requirements

- approval decisions must be tied to context and purpose
- approvers need the relevant evidence and risk summary
- approval records must be retained and reviewable
- override paths must require explicit accountability
- approval fatigue and bypass risks must be considered

## 4. Testing expectations

Validate:

- approval prompts are not bypassed
- approval scope matches the intended action
- approval metadata is preserved in traces
- role limitations are enforced
- stale or invalid approvals are rejected

## 5. Checklist

- [ ] approval workflow defined
- [ ] trigger conditions documented
- [ ] approver roles assigned
- [ ] evidence is presented to approver
- [ ] override and emergency path defined
- [ ] approval records are retained

## 6. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [Identity, Access, and Authorization](05-identity-access-and-authorization.md)
- [Agent and Tool Security](06-agent-and-tool-security.md)

