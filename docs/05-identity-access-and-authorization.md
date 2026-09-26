# Identity, Access, and Authorization

This document defines how AI systems should authenticate users and workloads, enforce access boundaries, and apply authorization consistently.

## 1. Objective

AI systems must not rely on the model to decide what a user or agent is allowed to do. Authorization must be enforced at deterministic policy points.

## 2. Identity principles

The organization should enforce:

- unique workload identity for agents and services
- delegated user identity where appropriate
- short-lived credentials
- least-privilege access by default
- approval-sensitive authorization for material actions
- revocation and emergency disablement paths

## 3. Authorization model

Every user, service, and agent should have a clear authority model covering:

- purpose and business context
- allowed systems and resources
- allowed actions and data scope
- rate limits and time bounds
- approval requirements
- safe failure behavior

## 4. Controls required

- token validation and audience checks
- issuer and expiry handling
- tenant isolation
- object-level authorization
- user-to-agent purpose binding
- just-in-time privilege patterns
- explicit deny conditions and elevated approval paths

## 5. Testing expectations

The organization must test for:

- privilege escalation attempts
- confused deputy behavior
- unauthorized tool calls
- approval bypass
- token replay or session misuse
- cross-tenant access
- stale permission propagation

## 6. Evidence required

The system should keep:

- identity and credential lifecycle records
- access decisions and policy traces
- approval metadata
- access reviews and recertification records
- revocation and failed-attempt evidence

## 7. Checklist

- [ ] workload identity defined
- [ ] delegated purpose is preserved
- [ ] resource and action scope set
- [ ] approval path exists for material actions
- [ ] denial and revocation tests pass
- [ ] access reviews are scheduled

## 8. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [AI Governance and Policy](01-ai-governance-policy.md)
- [Agent and Tool Security](06-agent-and-tool-security.md)

