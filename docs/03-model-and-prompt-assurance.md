# Model and Prompt Assurance

This document addresses the assurance required for selecting, evaluating, and operating the model layer, prompts, routing policy, and evaluator pipelines.

## 1. Objective

The model alone is not sufficient for safe deployment. The organization must validate the model, prompt design, system instructions, retrieval integration, routing logic, and evaluation process together.

## 2. Model lifecycle controls

The organization should control:

- model version and provider selection
- regional and data-residency constraints
- prompt template versioning
- safety and policy configuration
- output schema handling
- evaluator configuration and thresholds
- rollback and canary strategy

## 3. Prompt assurance requirements

Prompt assurance should include:

- review of system instructions and hidden assumptions
- tests for prompt injection susceptibility
- validation of safety and refusal behaviors
- verification of output format and tool parameter correctness
- adversarial and multilingual robustness checks
- control over prompt changes via versioning and review

## 4. Evaluation program

A production evaluation program should include:

- deterministic regression tests
- domain-focused task tests
- adversarial and abuse cases
- prompt injection and jailbreak tests
- tool-call correctness tests
- retrieval-grounded answer tests
- safety and refusal tests

## 5. Mandatory evidence

The model owner should retain:

- model name, provider, and version
- prompt template version
- evaluator configuration and thresholds
- regression test results
- attack cases and remediations
- deployment history and rollback evidence

## 6. Release considerations

A model should not advance to broader deployment without:

- representative evaluation in production-like conditions
- safety evidence tied to release version
- consistent prompt and policy versions
- no unresolved critical failures in adversarial or policy tests

## 7. Checklist

- [ ] model version recorded
- [ ] prompt version recorded
- [ ] evaluator thresholds defined
- [ ] adversarial set included
- [ ] refusal behavior validated
- [ ] output schema controls tested
- [ ] rollback and canary path exists

## 8. Related guidance

- [Master guide](ai-security-evaluation-and-assurance.md)
- [AI Risk and Control Framework](02-ai-risk-control-framework.md)
- [Agent and Tool Security](06-agent-and-tool-security.md)

