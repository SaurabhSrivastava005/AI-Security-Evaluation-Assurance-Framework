# Data, RAG, and Privacy

This document covers data access, retrieval controls, privacy safeguards, indexing, and governance for AI systems that interact with enterprise information.

## 1. Objective

The core control objective is simple: AI systems must only retrieve, summarize, or expose data that is authorized for the specific user, purpose, and context.

## 2. Data governance requirements

The organization must define:

- data classification and sensitivity
- lawful basis and use purpose
- allowed data sources and jurisdictions
- retention and deletion policies
- access control and authorization model
- indexing and embedding provenance

## 3. RAG safety controls

Required controls for RAG systems include:

- access checks before retrieval and after indexing
- source filtering and permission-aware retrieval
- row- and document-level authorization enforcement
- stale-data detection and invalidation
- provenance tracking for ingested content
- quarantine for suspicious or poisoned content
- secret masking and output filtering

## 4. Privacy and protection controls

The organization should implement:

- minimization and purpose limitation
- PII detection and redaction
- sensitive-data classification
- retention and deletion enforcement
- data residency controls
- DLP controls for outbound results
- audit logging for data access and exposure

## 5. Testing requirements

RAG systems should be tested for:

- unauthorized document retrieval
- tenant leakage or cross-scope access
- stale content appearing in retrieval
- metadata leakage and hidden instructions in content
- data poisoning and prompt influence via retrieved documents
- exfiltration via summarization or file export paths

## 6. Evidence needed

The system should retain:

- data sources and permission model
- retrieval filters and policy enforcement evidence
- ingestion provenance and quarantine records
- access logs and deletion actions
- privacy and compliance review evidence

## 7. Checklist

- [ ] data classification defined
- [ ] retention policy set
- [ ] access control matches use case
- [ ] retrieval policy enforced before response generation
- [ ] poisoning and hidden-instruction scenarios tested
- [ ] privacy redaction controls validated
- [ ] deletion and revocation flow tested

## 8. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [Identity, Access, and Authorization](05-identity-access-and-authorization.md)
- [Model and Prompt Assurance](03-model-and-prompt-assurance.md)

