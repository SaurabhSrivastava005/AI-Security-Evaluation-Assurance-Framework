# 04 — Assurance and Release

## Assurance lifecycle

1. **Intake:** approve purpose, boundary, risk tier, owners, and threats.
2. **Design:** approve architecture, authorization matrix, safe states, policy points, approvals, network flows, and test plan.
3. **Build:** pass component tests, secure SDLC checks, secret scanning, SBOM, and artifact attestation.
4. **Integration:** pass production-like authorization, adversarial, privacy, side-effect, and audit tests.
5. **Operational readiness:** exercise load, failure injection, kill switch, credential revocation, recovery, and runbooks.
6. **Progressive release:** use shadow mode, restricted canary, quotas, feature flags, stop authority, and rollback rehearsal.
7. **Continuous assurance:** reassess material changes, drift, access, providers, incidents, and production samples.

## Release decision

A signed release record should include:

- Exact release manifest and environment
- Applicable risk tier and control register
- Test and retest evidence
- Open findings and approved exceptions
- Named approver and stop authority
- Monitoring, rollback, revocation, and recovery readiness
- Expiration or review date

## Mandatory gates

Stop release when authorization fails, sensitive data crosses its boundary, an unsafe action bypasses approval, an artifact is unverifiable, material telemetry is missing, recovery is untested, or a critical safety/security threshold fails.

Non-mandatory exceptions require bounded exposure, compensating controls, an owner, due date, remediation funding, and explicit expiry. An exception must never silently become a permanent control failure.
