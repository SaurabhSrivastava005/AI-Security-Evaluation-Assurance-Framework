# Model and Prompt Assurance

This document defines the assurance required to select, evaluate, and operate the model layer, prompt configuration, routing policy, and evaluator pipeline. It is a technical and governance companion to the master AI assurance framework and the AI risk and control framework. The purpose is not to optimize for benchmark scores in isolation, but to ensure that the model behaves reliably within the organization’s approved purpose, risk tier, and operating controls.

A model that is highly capable but poorly governed remains a risk. The organization must validate not only what the model can generate, but also whether it follows policy, respects data boundaries, produces reliable tool calls, remains robust to adversarial input, and can be safely rolled back when evidence indicates failure.

## 1. Objective

The objective of model and prompt assurance is to establish a controlled and evidence-based method for deploying AI systems. The organization must be able to demonstrate that the selected model, prompt instructions, routing logic, retrieval integration, safety policies, and evaluator configuration are all aligned with the approved use case and the organization’s security and compliance requirements.

This includes confirming that the model has a defined owner, a clear deployment boundary, a versioned prompt, a recorded evaluation regime, and a known rollback path. It also requires proof that the model does not overstep permissions, leak sensitive data, treat untrusted content as instructions, or produce unsafe outputs during normal operations or adversarial conditions.

The model layer is not the enforcement point for access decisions. It is a decision-support component operating under policy, identity, retrieval, and tool controls that are enforced outside the model itself. Model assurance therefore focuses on verifying that the model behaves consistently within those boundaries and that any deviation is detected, contained, and remediated.

## 2. Model lifecycle controls

Model lifecycle control begins before deployment and continues through retirement. The organization must maintain a formal record of the model and configuration used in each environment, and must ensure that a production system is not using a model or prompt version that has not been reviewed and approved for that environment.

The model owner must define and document the approved model family, provider, region, deployment pattern, and version. This record should include the exact model identifier and whether the model is used through a managed API, self-hosted runtime, or a routed multi-model architecture. If a deployment must comply with data residency, legal processing restrictions, or regional constraints, these requirements must be enforced during model selection and operation.

The same discipline applies to prompt templates and system instructions. Prompt text is not a harmless design detail; it is part of the production control surface. The organization should maintain version control for prompts, store approval evidence for changes, and require documented review for any modification that affects behavior, safety, tool use, or retrieval handling. Prompt changes should be treated as release changes, not informal edits.

Safety and policy configuration must also be tracked as part of the production release record. This includes moderation settings, refusal rules, policy enforcement thresholds, output schema constraints, system instructions, guardrail logic, and any routing logic that chooses between models or policies. If the system uses a routing policy to select a model based on task, domain, or risk, the organization must test that policy under both expected and adversarial conditions.

Output handling must be governed as closely as input handling. The system should verify that the model returns the expected schema, uses the correct parameter names, obeys field constraints, and does not invent identifiers or actions when tool use is required. This is a core reliability issue because schema failure can create incorrect API calls, unsafe actions, or silent operational corruption.

The organization must also hold evidence for evaluator configuration and thresholds. This includes how tests are defined, which tasks are considered critical, what constitutes a failure, and what the release threshold is for each category of evaluation. A model that passes only a weak evaluator set is not suitably assured. In addition, the system must contain rollback and canary strategies so that a degraded model or prompt can be replaced quickly without causing uncontrolled service disruption.

## 3. Prompt assurance requirements

Prompt assurance is essential because prompts define the behavioral boundary of the model. The organization must assess both the explicit instructions and the hidden assumptions encoded in the prompt structure, retrieved context, and surrounding orchestration logic. A system prompt may appear safe in isolation but still fail when a user or retrieved document changes the context in a way that induces policy bypass or task confusion.

The first requirement is a formal review of system instructions and their interaction with retrieved content, tool instructions, and user policy. This review should answer whether the prompt clearly distinguishes trusted instructions from user-controlled content, whether refusal behavior is specific and policy-consistent, and whether the model is told to defer to system policy when conflicting instructions appear. The review must cover hidden assumptions that could cause the model to over-trust untrusted inputs, omit required verification steps, or misinterpret user intent.

The second requirement is evidence that prompt injection susceptibility is assessed in a realistic way. This includes both direct prompt attacks and indirect prompt injection through retrieved emails, documents, web content, tickets, or user-generated artifacts. The model must not treat untrusted content as authoritative instructions, nor should it allow external sources to override the organization’s intended policy or approved tool workflow.

A prompt should also be validated for safety, refusal, and escalation behavior. The model must refuse disallowed requests in a consistent and explainable manner, and it must know when to ask for clarification instead of fabricating a response or acting without required authority. In workflows involving external systems, the model must not assume that a user’s request is permitted simply because it is phrased as a valid task. It must check the boundary of delegated authority.

The output format and parameter correctness must be validated as part of prompt assurance. If the model is expected to produce structured fields, tool arguments, or decision labels, tests should verify that the output is valid, complete, and within the allowed domain. In domains involving automation, this is not an optional quality check; it is a control requirement. A model that invents fields, mislabels actions, or produces invalid parameters creates security and operational risk even if the textual answer appears plausible.

Prompt assurance also requires adversarial and multilingual robustness checks. Models often fail under cross-language prompts, code-switching, obfuscated instructions, or subtle manipulations that are not visible in standard evaluation data. The organization must verify that the prompt design remains robust under these conditions and that refusal and safety behavior remains stable when the user’s phrasing changes but the underlying intent does not.

Finally, prompt changes must be controlled through versioning and formal review. Prompt modifications should be tracked with change justification, test evidence, and approval from the accountable owner. A prompt that is changed without evidence is effectively a new system and must be treated as such.

## 4. Evaluation program

A production evaluation program is not a single benchmark run. It is an evidence set that measures whether the model can operate safely and reliably in the context it is actually deployed. The evaluation strategy should combine deterministic testing, domain task validation, adversarial testing, and production-like monitoring.

Deterministic regression tests should be used to capture known-good behavior and confirm that previously fixed issues do not recur. These tests should cover expected prompts, refusal scenarios, output schemas, tool arguments, retrieval-grounded reasoning, and standard business flows. If a change to a prompt or model causes an existing regression, the release should not proceed without a documented remediation and retest.

Domain-focused task tests should reflect the actual business workflow for which the system is approved. This includes use cases, edge cases, and policy-sensitive scenarios relevant to the real deployment. A generic intelligence benchmark is insufficient evidence for a regulated or high-impact function. The evaluation set must be representative of the organization’s actual operating conditions and user population.

Adversarial and abuse cases are mandatory. These include prompt injection, jailbreak attempts, maliciously crafted retrieval content, deceptive user requests, misleading attachments, and manipulative tool-use instructions. The testing program must verify both the model’s direct output and the surrounding control stack. If the system behaves safely in isolation but fails when a malicious or benign user manipulates context, the risk is still present and must be treated as a product issue.

Tool-call correctness tests should verify that the model chooses the correct tool, passes valid arguments, uses approved parameters, and does not exceed its delegated permission set. This includes validation of parameter names, data types, required fields, and prohibited values. Tool call assessment is especially important for systems that can create records, submit workflows, trigger outbound calls, or modify business data.

Retrieval-grounded answer tests are required when the system depends on documents, enterprise knowledge, or a retrieval pipeline. These tests should confirm that answers are grounded in the correct data source, do not expose data outside the user’s authorization scope, and do not generate unsupported conclusions from partially retrieved or stale content. A model can produce a confident answer while silently ignoring retrieval boundaries, which is a governance and privacy failure.

Safety and refusal tests must be run against the model and its prompt configuration under realistic conditions. The organization should validate that harmful requests are refused, unsafe actions are blocked, inappropriate disclosures are not generated, and safety policies do not degrade under multilingual or adversarial prompting. These tests must be tied to release evidence and reviewed by the system owner.

## 5. Model owner evidence and recordkeeping

The model owner must retain evidence sufficient to explain and reproduce the behavior of the production system. This evidence is not optional documentation; it is required to support governance decisions, incident investigation, release approvals, and post-deployment review.

The record should include the exact model name, provider, model version, region or deployment location, and the conditions under which it is approved for use. It should also include the prompt template version, policy configuration, evaluator configuration, thresholds, and traceability to the release that used them. If the system includes a router, these routing rules and their testing evidence must also be recorded.

The evidence package must contain the regression, adversarial, and task-specific evaluation results used to support the release. It must also retain examples of attack cases, failed prompts, and the remediation measures applied. The organization should be able to show how its test set evolved when new failure patterns were discovered, and what remediation was applied before the model was reapproved.

The deployment history must be preserved with time-based records showing when each model or prompt version entered production, what approval was granted, and whether any rollback or containment action was taken. This record allows the organization to answer not only whether a model was safe at the time of release, but also what changed when a later issue was identified.

## 6. Release considerations and stop-ship criteria

A model should not advance to broader deployment without representative evaluation in the environment that approximates the production operating model. A pilot environment that does not include the actual retrieval sources, safety stack, tool controls, routing policy, and deployment constraints is insufficient assurance. The organization must test the full path from user prompt to retrieval, model reasoning, policy checks, and action execution.

Release decisions should be tied to versioned evidence. The decision to approve a broader rollout must be supported by current model and prompt versions, policy configuration, evaluator thresholds, and test outcomes from the same release candidate. If the system configuration differs from the evaluated build, the release evidence is no longer sufficient.

A release must not proceed if there are unresolved critical failures in adversarial, policy, or tool validation tests. The same is true when safety behavior is inconsistent under prompt manipulation, retrieval poisoning, or edge-case user requests. The organization must prioritize prevention of harmful or unauthorized behavior over nominal model quality.

The risk and control framework defines hard-stop conditions for production release. If a model or agent can act outside its delegated purpose, ignore access boundaries, generate unsafe outputs without review, or rely on an untracked or unauthorized tool path, the release should be refused. A governance model without enforcement is not assurance.

## 7. Governance alignment

This document operates within the broader governance structure set out in the master guide and the AI risk and control framework. The model owner is accountable for model selection, prompt integrity, evaluator evidence, and release readiness. The security architect reviews the control surface and validates whether the model is protected by independent policy checks. The data owner confirms that retrieval boundaries, data residency, and data governance constraints are properly enforced. The platform lead ensures that routing, runtime, logging, and rollback requirements are satisfied.

This division of responsibility is necessary because model quality and operational safety are separate concerns. A model may be technically strong yet still fail governance due to unauthorized data access, missing approval workflow, weak retrieval enforcement, or absent evidence retention. The control and governance structure exists to prevent those failures from being treated as acceptable trade-offs.

## 8. Related guidance

This document should be read together with the master guide, the risk and control framework, and the domain-specific security guidance for data, identity, runtime isolation, tool use, and deployment assurance. The relevant references are the AI Security Evaluation and Assurance Framework master guide, the AI Risk and Control Framework, and the Agent and Tool Security guidance, which together define the operational and governance basis for model deployment.

The organization should treat model and prompt assurance as a continuous operating discipline rather than a one-time approval exercise. The model, prompt, and evaluator pipeline must evolve with the system, the data, the threat landscape, and the organization’s risk posture. A production AI system is only as safe as the evidence behind the version currently running.

The final requirement is straightforward: the organization must be able to show that the deployment is authorized, bounded, tested, observable, and reversible. If it cannot show that, it does not have sufficient assurance for release.

[Master guide](ai-security-evaluation-and-assurance.md)
[AI Risk and Control Framework](02-ai-risk-control-framework.md)
[Agent and Tool Security](06-agent-and-tool-security.md)


