# Supply Chain and Artifact Provenance

This document defines the requirements for secure build, release, and deployment of AI artifacts and dependencies.

## 1. Objective

AI systems are only as trustworthy as the components they run. The organization must ensure that model packages, prompts, adapters, containers, libraries, and infrastructure are signed, versioned, and provenance-verified.

## 2. Required controls

- SBOM generation for all software components
- dependency vulnerability scanning
- signed artifacts and build attestation
- provenance verification for models and containers
- lockfile and dependency pinning
- change control and pipeline approval
- exception handling with time-bound expiration

## 3. AI-specific supply chain risks

The organization should account for:

- altered model weights or adapters
- malicious prompt templates or evaluation assets
- compromised container images
- tampered retrieval indexes or embeddings
- unreviewed library additions in toolchains

## 4. Evidence required

The pipeline should retain evidence for:

- dependency inventory
- vulnerability disposition
- build provenance and signatures
- promotion approvals
- artifact and model version history

## 5. Checklist

- [ ] SBOM generated
- [ ] dependency scans completed
- [ ] signed artifacts used
- [ ] provenance verified
- [ ] exceptions tracked and expired
- [ ] rollback path exists

## 6. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [Runtime, Network, and Isolation](07-runtime-network-and-isolation.md)
- [Release, Change, and Continuous Assurance](11-release-change-and-continuous-assurance.md)

