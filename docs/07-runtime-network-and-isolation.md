# Runtime, Network, and Isolation

This document covers the runtime controls required for AI workloads, including sandboxing, network segmentation, secret handling, and egress restrictions.

## 1. Objective

The model and agent environment must be isolated from production systems and sensitive credentials. Runtime controls reduce the risk of lateral movement, data exposure, or control bypass.

## 2. Core controls

The environment should include:

- ephemeral execution containers
- least-privilege service identity
- read-only base image and minimized attack surface
- no production secrets in environment variables or logs
- restricted filesystem and process access
- constrained CPU, memory, and execution time
- controlled DNS and egress policy
- private networking and destination allowlists

## 3. Network protections

The organization should enforce:

- egress allowlisting
- DNS filtering and no broad outbound access
- blocklist of metadata endpoints and internal services
- segmentation between user-facing and internal systems
- no direct access to critical infrastructure without approval

## 4. Testing expectations

Test for:

- SSRF and DNS rebinding attempts
- metadata service access
- lateral movement through container escapes
- filesystem tampering
- unrestricted outbound access
- resource exhaustion and loop-based DoS

## 5. Evidence required

The environment should retain:

- runtime configuration records
- network policy decisions
- security scan and image hardening evidence
- incident response and rollback evidence

## 6. Checklist

- [ ] isolated runtime defined
- [ ] secret handling is validated
- [ ] egress is restricted
- [ ] metadata endpoints are blocked
- [ ] runtime escape tests pass
- [ ] recovery flow is tested

## 7. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [Agent and Tool Security](06-agent-and-tool-security.md)
- [Supply Chain and Artifact Provenance](08-supply-chain-and-artifact-provenance.md)

