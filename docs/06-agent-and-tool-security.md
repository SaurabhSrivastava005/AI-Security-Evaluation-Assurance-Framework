# Agent and Tool Security

This document covers how agentic systems must safely invoke tools, APIs, and downstream services without exceeding their delegated authority.

## 1. Objective

AI agents must not be allowed to act directly on systems with unrestricted authority. Tool use must pass through a deterministic, policy-aware execution layer.

## 2. Core design requirements

The tool invocation path should enforce:

- structured request validation
- allowlist of permitted tools and destinations
- approved parameter schemas
- per-tool business rules
- approval for material side effects
- idempotency and reconcile-on-failure handling
- audit logs for every tool invocation

## 3. Agent safety principles

The organization should ensure that agents cannot:

- call unauthorized tools
- override restrictions through prompt manipulation
- enumerate unexpected destinations
- act with the full permissions of the initiating user
- retry unsafe or non-idempotent operations without control

## 4. Testing and validation

The system should be tested for:

- parameter tampering and payload abuse
- tool discovery abuse
- hidden or substituted destinations
- bulk export attempts
- repeated denial or recursion loops
- unsafe side effects and partial-commit failure states

## 5. Mandatory evidence

The tool gateway should retain:

- request and response metadata
- approval decision metadata
- tool version and destination information
- outcome classification
- reconciliation or rollback evidence

## 6. Checklist

- [ ] tool registry exists
- [ ] tool destinations are allowlisted
- [ ] schema validation is enforced
- [ ] approval required for irreversible actions
- [ ] replay and idempotency handling is tested
- [ ] unauthorized tool invocation is blocked

## 7. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [Identity, Access, and Authorization](05-identity-access-and-authorization.md)
- [Runtime, Network, and Isolation](07-runtime-network-and-isolation.md)

