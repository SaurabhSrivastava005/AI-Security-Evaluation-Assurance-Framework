# Release, Change, and Continuous Assurance

This document defines how the organization manages deployment, change control, and the ongoing assurance of AI systems after release.

## 1. Objective

An AI system must not be treated as static after deployment. Model behavior, retrieval quality, user interaction patterns, provider changes, and policy drift can all create new risk over time.

## 2. Release readiness

A release should be approved only when:

- the intended use and risk tier are still valid
- evidence package is complete
- mandatory tests pass
- canary or shadow evaluation is acceptable
- rollback and suspension path is tested
- required approvals are recorded

## 3. Change control

Changes to the following require review and likely regression testing:

- model versions
- prompts and system instructions
- policy and access rules
- data sources and indexing logic
- tool registry and external APIs
- infrastructure, runtime, or egress configuration

## 4. Continuous assurance activities

The organization should operate a regular cadence:

- weekly or biweekly drift review
- monthly access recertification
- quarterly red-team validation
- incident-driven retesting after every material issue
- versioned change assessment and risk review

## 5. Evidence required

The organization should keep:

- release manifest
- signed decision record
- test evidence
- canary outcomes
- rollbacks and root-cause actions
- post-release monitoring reports

## 6. Checklist

- [ ] release manifest exists
- [ ] canary or shadow path defined
- [ ] rollback path tested
- [ ] post-release monitoring active
- [ ] drift review scheduled
- [ ] incident-to-regression linkage exists

## 7. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [AI Risk and Control Framework](02-ai-risk-control-framework.md)
- [Observability, Detection, and Incident Response](09-observability-detection-and-incident-response.md)

