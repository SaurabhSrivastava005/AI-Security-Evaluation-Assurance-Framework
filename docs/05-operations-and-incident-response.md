# 05 — Operations and Incident Response

## Operational controls

Monitor model behavior, prompt and policy changes, retrieval quality, identity, tool calls, egress, costs, latency, quotas, safety signals, and downstream side effects. Use correlation IDs and redaction so material runs can be investigated without exposing unnecessary sensitive data.

## Required response capabilities

- Kill switch and feature disablement
- Credential and delegated-scope revocation
- Agent, tenant, tool, and provider isolation
- Alert-to-action runbooks
- Evidence preservation and access control
- Rollback, restore, and transaction reconciliation
- User, regulator, customer, and provider notification paths where applicable
- Root-cause analysis and corrective-action tracking

## Incident triggers

Treat unauthorized access, data leakage, unsafe or irreversible action, policy bypass, secret disclosure, sandbox escape, supply-chain compromise, material loss of auditability, or uncontrolled availability impact as security incidents.

## Response lifecycle

1. Detect and validate.
2. Contain access, execution, and propagation.
3. Preserve traces, artifacts, prompts, policies, and downstream records.
4. Assess scope, affected parties, and reporting obligations.
5. Eradicate the cause and rotate or revoke compromised authority.
6. Recover through verified rollback, restore, and reconciliation.
7. Review root cause, update controls and tests, and verify the corrective action.

## Operating cadence

Run focused checks on pull requests, full applicable gates at release, drift and sample reviews weekly or biweekly, access recertification monthly, red-team and control-effectiveness reviews quarterly, and incident-to-regression updates after every material incident.
