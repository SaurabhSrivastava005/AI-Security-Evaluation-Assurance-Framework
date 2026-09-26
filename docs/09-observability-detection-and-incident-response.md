# Observability, Detection, and Incident Response

This document defines what is required to monitor AI systems, detect unsafe behavior, and respond quickly to incidents.

## 1. Objective

Organizations need the ability to detect, reconstruct, and investigate AI-driven behavior before, during, and after execution.

## 2. Monitoring requirements

The organization should monitor:

- model and prompt version use
- tool and API invocation paths
- retrieval and access patterns
- identity and approval events
- unusual volume, latency, or output anomalies
- policy denials and retries
- cost and operational drift

## 3. Log and trace standards

Every material run should include:

- correlation ID
- user and agent identity
- business purpose and risk tier
- model and prompt versions
- retrieval source and filters
- tool and API results
- approval and policy decisions
- outcome and side effects

## 4. Incident response flow

When unsafe behavior is detected, the organization should:

- isolate the affected workload or identity
- preserve evidence
- revoke credentials or tool privileges if needed
- assess blast radius and impacted data
- notify required stakeholders
- perform root-cause review and corrective action

## 5. Checklist

- [ ] trace model is defined
- [ ] alert conditions are established
- [ ] incident runbooks exist
- [ ] evidence is retained
- [ ] notification pathway is defined
- [ ] containment steps are tested

## 6. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [AI Risk and Control Framework](02-ai-risk-control-framework.md)
- [Release, Change, and Continuous Assurance](11-release-change-and-continuous-assurance.md)

