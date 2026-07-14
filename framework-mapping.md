
# Framework Mapping Appendix

**Purpose:** Map MCP Governance & Risk Model controls to established security and AI governance frameworks. Use this appendix for compliance audits, gap assessments, and alignment with existing organizational programs.

**Related guide:** This mapping references the [MCP Governance & Risk Framework v1.0](mcp-governance-risk-framework-v1.0.md), which contains **six chapters** (Executive Summary through Risk Scoring) plus a **closing appendix** (control catalog, evidence pack, hardening, detection/IR, and checklists). There are no separate Chapters 7–15 in v1.0 — approval workflow, monitoring, incident response, and metrics content lives in Chapters 1, 3, 4, 6, and the appendix sections linked below.

---

## OWASP MCP Top 10

The OWASP MCP Top 10 identifies the most critical security risks for MCP deployments. This table maps each risk category to v1.0 guide controls.

| OWASP MCP Risk | Guide Section | Control / Implementation |
|----------------|---------------|--------------------------|
| MCP01: Token Mismanagement & Secret Exposure | [Ch. 2](mcp-governance-risk-framework-v1.0.md#authorization-design), [Ch. 6](mcp-governance-risk-framework-v1.0.md#authorization-hard-gates), [Appendix — Authorization Test Cases](mcp-governance-risk-framework-v1.0.md#authorization-test-cases) | For authenticated HTTP servers: OAuth 2.1-compatible authorization with audience validation; reject token passthrough. For STDIO: local hardening and credential handling |
| MCP02: Privilege Escalation via Scope Creep | [Ch. 3](mcp-governance-risk-framework-v1.0.md#principle-3-least-privilege-for-tools) (Principle 3), [Ch. 5](mcp-governance-risk-framework-v1.0.md#classification-rules) | Least privilege per tool; classify by highest-risk tool; re-classify when tools change |
| MCP03: Tool Poisoning | [Ch. 2](mcp-governance-risk-framework-v1.0.md#mcp-specific-attack-patterns), [Ch. 5](mcp-governance-risk-framework-v1.0.md#tier-decision-tree) | Tool chaining awareness; classify Tier 0+ with poisoning and intent-flow risks in mind |
| MCP04: Software Supply Chain Attacks & Dependency Tampering | [Appendix — Formal Control Catalog](mcp-governance-risk-framework-v1.0.md#formal-control-catalog) (MCP-09), [Appendix — Evidence Pack](mcp-governance-risk-framework-v1.0.md#evidence-pack-tier-2-approvals) | SBOM review; dependency CVE scanning; version pinning for external servers |
| MCP05: Command Injection & Execution | [Ch. 3](mcp-governance-risk-framework-v1.0.md#principle-3-least-privilege-for-tools), [Appendix — Local MCP Hardening](mcp-governance-risk-framework-v1.0.md#local-mcp-hardening-requirements) | Prohibit shell/command tools unless justified; sandboxing and command visibility on local servers |
| MCP06: Intent Flow Subversion / Prompt Injection | [Ch. 2 — Prompt Injection](mcp-governance-risk-framework-v1.0.md#1-prompt-injection-via-tool-output), [Ch. 3](mcp-governance-risk-framework-v1.0.md#principle-4-human-approval-must-be-meaningful) (Principle 4) | Tool chaining controls; HITL for write actions; separate read and write servers where possible |
| MCP07: Insufficient Authentication & Authorization | [Ch. 2](mcp-governance-risk-framework-v1.0.md#authorization-design), [Ch. 6](mcp-governance-risk-framework-v1.0.md#authorization-hard-gates), [Appendix — Authorization Test Cases](mcp-governance-risk-framework-v1.0.md#authorization-test-cases) | HTTP auth hard gates; session security review for Tier 2+ |
| MCP08: Lack of Audit and Telemetry | [Ch. 3](mcp-governance-risk-framework-v1.0.md#principle-5-auditability-requires-production-logging) (Principle 5), [Ch. 6 — Production Hard Gates](mcp-governance-risk-framework-v1.0.md#production-hard-gates), [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | Mandatory audit logging with user/agent/tool/action attribution; SIEM integration |
| MCP09: Shadow MCP Servers | [Ch. 4](mcp-governance-risk-framework-v1.0.md#approved-vs-shadow-mcp), [Ch. 4 — Discovery Methods](mcp-governance-risk-framework-v1.0.md#discovery-methods) | Inventory, discovery, prohibition policy, platform allowlists |

---

## OWASP LLM Top 10

MCP governance intersects with LLM security risks because agents use LLMs to decide which tools to invoke.

| OWASP LLM Risk | Guide Section | Control / Implementation |
|----------------|---------------|--------------------------|
| LLM01: Prompt Injection | [Ch. 2 — Prompt Injection](mcp-governance-risk-framework-v1.0.md#1-prompt-injection-via-tool-output), [Ch. 3](mcp-governance-risk-framework-v1.0.md#principle-4-human-approval-must-be-meaningful) | Tool chaining awareness; HITL for high-risk actions |
| LLM02: Insecure Output Handling | [Ch. 6](mcp-governance-risk-framework-v1.0.md#the-eight-risk-factors), [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | DLP on outbound tool parameters; monitor anomalous tool workflows |
| LLM03: Training Data Poisoning | [Appendix — Evidence Pack](mcp-governance-risk-framework-v1.0.md#evidence-pack-tier-2-approvals), [Appendix — Ten Questions](mcp-governance-risk-framework-v1.0.md#ten-questions-every-security-leader-should-be-able-to-answer) | Vendor review: confirm MCP data is not used for model training |
| LLM04: Model Denial of Service | [Ch. 2](mcp-governance-risk-framework-v1.0.md#four-properties-that-change-your-threat-model), [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | Rate limits on tool calls; volume anomaly alerting |
| LLM05: Supply Chain Vulnerabilities | [Appendix — Formal Control Catalog](mcp-governance-risk-framework-v1.0.md#formal-control-catalog) (MCP-09), [Appendix — Evidence Pack](mcp-governance-risk-framework-v1.0.md#evidence-pack-tier-2-approvals) | Third-party MCP review; SBOM; dependency scanning |
| LLM06: Sensitive Information Disclosure | [Ch. 5](mcp-governance-risk-framework-v1.0.md#chapter-5-mcp-server-classification-model), [Ch. 6 — The Eight Risk Factors](mcp-governance-risk-framework-v1.0.md#the-eight-risk-factors) | Data classification via tier and scoring; data minimization for Tier 2+ |
| LLM07: Insecure Plugin/Tool Design | [Ch. 3](mcp-governance-risk-framework-v1.0.md#chapter-3-mcp-governance-principles), [Ch. 5](mcp-governance-risk-framework-v1.0.md#classification-rules) | Tool-level classification; least privilege; threat modeling for Tier 3–4 |
| LLM08: Excessive Agency | [Ch. 3](mcp-governance-risk-framework-v1.0.md#principle-4-human-approval-must-be-meaningful) (Principle 4), [Ch. 2 — Tool chaining](mcp-governance-risk-framework-v1.0.md#tool-chaining-primary-risk) | HITL approval; scope limits; segregation of duties |
| LLM09: Overreliance | [Ch. 3](mcp-governance-risk-framework-v1.0.md#principle-1-no-mcp-without-ownership), [Ch. 1 — Step 4](mcp-governance-risk-framework-v1.0.md#step-4-assign-raci-owners) | Business owner accountability; human review of agent decisions |
| LLM10: Model Theft | [Appendix — Evidence Pack](mcp-governance-risk-framework-v1.0.md#evidence-pack-tier-2-approvals), [Appendix — Ten Questions](mcp-governance-risk-framework-v1.0.md#ten-questions-every-security-leader-should-be-able-to-answer) | Vendor data handling review; ensure MCP does not expose model weights |

---

## NIST AI Risk Management Framework (AI RMF)

| NIST AI RMF Function | Category | Guide Section | Implementation |
|----------------------|----------|---------------|----------------|
| **Govern** | GV-1 Policies | [Ch. 1 — Key Governance Rules](mcp-governance-risk-framework-v1.0.md#key-governance-rules), [Ch. 3](mcp-governance-risk-framework-v1.0.md#chapter-3-mcp-governance-principles) | MCP usage policy; shadow MCP prohibition |
| **Govern** | GV-2 Accountability | [Ch. 1 — Step 4](mcp-governance-risk-framework-v1.0.md#step-4-assign-raci-owners), [Ch. 3 — Principle 1](mcp-governance-risk-framework-v1.0.md#principle-1-no-mcp-without-ownership) | RACI guidance; named owners; risk acceptance |
| **Govern** | GV-6 Third-party risk | [Appendix — Evidence Pack](mcp-governance-risk-framework-v1.0.md#evidence-pack-tier-2-approvals), [Appendix — Formal Control Catalog](mcp-governance-risk-framework-v1.0.md#formal-control-catalog) (MCP-09) | Vendor/SBOM review for external servers |
| **Map** | MP-2 Categories of AI systems | [Ch. 5](mcp-governance-risk-framework-v1.0.md#chapter-5-mcp-server-classification-model) | Tier 0–4 classification model |
| **Map** | MP-5 Impact assessment | [Ch. 6](mcp-governance-risk-framework-v1.0.md#chapter-6-mcp-risk-scoring-model) | Eight-factor risk scoring |
| **Measure** | MS-2 Metrics | [Ch. 1 — Step 5](mcp-governance-risk-framework-v1.0.md#step-5-define-monthly-metrics), [Ch. 1 — Practical Rollout](mcp-governance-risk-framework-v1.0.md#practical-rollout-plan-90-days) | Monthly KPIs: inventory coverage, shadow MCP, overdue reviews |
| **Measure** | MS-2.7 Monitoring | [Ch. 4 — Inventory Maintenance](mcp-governance-risk-framework-v1.0.md#inventory-maintenance), [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | Audit logging, alerting, periodic review by tier |
| **Manage** | MG-2 Risk treatment | [Ch. 6 — Hard Gates](mcp-governance-risk-framework-v1.0.md#hard-gates-non-negotiable), [Ch. 6 — Using Scores in Decisions](mcp-governance-risk-framework-v1.0.md#using-scores-in-decisions) | Approve / conditional / reject decisions |
| **Manage** | MG-3 Third-party risk | [Appendix — Evidence Pack](mcp-governance-risk-framework-v1.0.md#evidence-pack-tier-2-approvals) | Vendor review outcomes and SBOM evidence |
| **Manage** | MG-4 Incident response | [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | MCP incident response phases and recovery criteria |

---

## ISO/IEC 42001 (AI Management System)

| ISO 42001 Area | Guide Section | Implementation |
|----------------|---------------|----------------|
| 6.1: Risk assessment | [Ch. 5](mcp-governance-risk-framework-v1.0.md#chapter-5-mcp-server-classification-model), [Ch. 6](mcp-governance-risk-framework-v1.0.md#chapter-6-mcp-risk-scoring-model) | Tier classification and quantitative scoring |
| 6.1: Risk treatment | [Ch. 6 — Using Scores in Decisions](mcp-governance-risk-framework-v1.0.md#using-scores-in-decisions), [Appendix — Formal Control Catalog](mcp-governance-risk-framework-v1.0.md#formal-control-catalog) | Approval decisions with required controls by tier |
| 7.4: Communication | [Ch. 1 — Step 4](mcp-governance-risk-framework-v1.0.md#step-4-assign-raci-owners), [Ch. 3 — Principle 1](mcp-governance-risk-framework-v1.0.md#principle-1-no-mcp-without-ownership) | RACI guidance; stakeholder notification |
| 8.1: Operational planning | [Ch. 4](mcp-governance-risk-framework-v1.0.md#chapter-4-mcp-asset-inventory), [Ch. 4 — Inventory Maintenance](mcp-governance-risk-framework-v1.0.md#inventory-maintenance) | Governance lifecycle from intake through decommission |
| 8.2: AI system impact assessment | [Ch. 2](mcp-governance-risk-framework-v1.0.md#mcp-specific-attack-patterns), [Ch. 5](mcp-governance-risk-framework-v1.0.md#worked-classification-examples) | Scenario-specific threat models for Tier 3–4 |
| 8.3: Data for AI systems | [Ch. 4 — Required fields](mcp-governance-risk-framework-v1.0.md#required-fields), [Ch. 6 — The Eight Risk Factors](mcp-governance-risk-framework-v1.0.md#the-eight-risk-factors) | Data scope documentation; DLP requirements by tier |
| 8.4: Third-party relationships | [Appendix — Evidence Pack](mcp-governance-risk-framework-v1.0.md#evidence-pack-tier-2-approvals), [Appendix — Formal Control Catalog](mcp-governance-risk-framework-v1.0.md#formal-control-catalog) (MCP-09) | Vendor questionnaire outcomes and SBOM evidence |
| 9.1: Monitoring and measurement | [Ch. 1 — Step 5](mcp-governance-risk-framework-v1.0.md#step-5-define-monthly-metrics), [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | Continuous monitoring and monthly KPIs |
| 9.2: Internal audit | [Ch. 4 — Inventory Maintenance](mcp-governance-risk-framework-v1.0.md#inventory-maintenance), [Appendix — Formal Control Catalog](mcp-governance-risk-framework-v1.0.md#formal-control-catalog) (MCP-07) | Periodic review cadence by tier |
| 10.1: Continual improvement | [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | Post-incident review; governance gap remediation |

---

## SOC 2 Trust Service Criteria

| SOC 2 Criteria | Guide Section | Implementation |
|----------------|---------------|----------------|
| **CC6.1**: Logical access | [Appendix — Formal Control Catalog](mcp-governance-risk-framework-v1.0.md#formal-control-catalog) (MCP-03, MCP-04), [Appendix — Authorization Test Cases](mcp-governance-risk-framework-v1.0.md#authorization-test-cases) | Authentication, scoped authorization, audience validation |
| **CC6.2**: Access removal | [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response), [Ch. 4 — Inventory Maintenance](mcp-governance-risk-framework-v1.0.md#inventory-maintenance) | Credential revocation during incident containment and decommission |
| **CC6.3**: Role-based access | [Ch. 1 — Step 4](mcp-governance-risk-framework-v1.0.md#step-4-assign-raci-owners), [Ch. 5 — Tier Summary](mcp-governance-risk-framework-v1.0.md#tier-summary-table) | RACI guidance; approval authority by tier |
| **CC6.6**: System boundaries | [Ch. 4](mcp-governance-risk-framework-v1.0.md#approved-vs-shadow-mcp), [Appendix — Client and Host Governance](mcp-governance-risk-framework-v1.0.md#client-and-host-governance) | Inventory; allowlists; shadow MCP prohibition |
| **CC6.7**: Data transmission | [Ch. 2](mcp-governance-risk-framework-v1.0.md#token-passthrough), [Appendix — Authorization Test Cases](mcp-governance-risk-framework-v1.0.md#authorization-test-cases) | Token handling; no passthrough; DLP |
| **CC6.8**: Malicious software | [Appendix — Formal Control Catalog](mcp-governance-risk-framework-v1.0.md#formal-control-catalog) (MCP-09) | Dependency scanning; SBOM review |
| **CC7.1**: Detection | [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | Alerting rules; anomaly detection |
| **CC7.2**: Monitoring | [Ch. 1 — Step 5](mcp-governance-risk-framework-v1.0.md#step-5-define-monthly-metrics), [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | Audit logging; monthly metrics |
| **CC7.3**: Incident response | [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | MCP incident response playbook |
| **CC7.4**: Recovery | [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | Eradicate and recover procedures; re-approval after hard gates pass |
| **CC8.1**: Change management | [Ch. 4 — Inventory Maintenance](mcp-governance-risk-framework-v1.0.md#inventory-maintenance), [Ch. 5 — Rule 2](mcp-governance-risk-framework-v1.0.md#rule-2-re-classify-when-tools-change) | Re-classification on tool changes; version pinning |
| **CC9.2**: Vendor risk | [Appendix — Evidence Pack](mcp-governance-risk-framework-v1.0.md#evidence-pack-tier-2-approvals), [Appendix — Formal Control Catalog](mcp-governance-risk-framework-v1.0.md#formal-control-catalog) (MCP-09) | Vendor review and SBOM evidence |

---

## Internal AI Governance Policies

Use this section to map guide controls to your organization's internal AI governance policies. Replace the placeholder rows with your actual policy references.

| Internal Policy | Guide Section | Alignment Notes |
|-----------------|---------------|-----------------|
| [Your AI Usage Policy] | [Ch. 1 — Key Governance Rules](mcp-governance-risk-framework-v1.0.md#key-governance-rules), [Ch. 3](mcp-governance-risk-framework-v1.0.md#chapter-3-mcp-governance-principles) | Adopt MCP-specific policy language from governance principles and four non-negotiable rules |
| [Your AI Risk Assessment Process] | [Ch. 5](mcp-governance-risk-framework-v1.0.md#chapter-5-mcp-server-classification-model), [Ch. 6](mcp-governance-risk-framework-v1.0.md#chapter-6-mcp-risk-scoring-model) | MCP tier classification and scoring as AI risk assessment |
| [Your Third-Party AI Vendor Policy] | [Appendix — Evidence Pack](mcp-governance-risk-framework-v1.0.md#evidence-pack-tier-2-approvals), [Appendix — Ten Questions](mcp-governance-risk-framework-v1.0.md#ten-questions-every-security-leader-should-be-able-to-answer) | Extend vendor review to include MCP architecture and auth evidence |
| [Your AI Incident Response Plan] | [Appendix — Detection and Incident Response](mcp-governance-risk-framework-v1.0.md#detection-and-incident-response) | Add MCP-specific playbook to existing IR plan |
| [Your Data Classification Standard] | [Ch. 5](mcp-governance-risk-framework-v1.0.md#tier-decision-tree), [Ch. 6 — The Eight Risk Factors](mcp-governance-risk-framework-v1.0.md#the-eight-risk-factors) | Map data classes to MCP tier requirements |
| [Your Privileged Access Policy] | [Ch. 5 — Tier 4](mcp-governance-risk-framework-v1.0.md#tier-summary-table), [Ch. 3 — Principle 3](mcp-governance-risk-framework-v1.0.md#principle-3-least-privilege-for-tools) | Tier 4 MCP servers follow PAM/JIT requirements |

---

## Using This Mapping

### For Compliance Audits

1. Identify the framework your auditor is assessing against
2. Locate the relevant mapping table in this appendix
3. Reference the guide chapter or appendix section that implements each control
4. Provide evidence: risk register entries, approval decisions, evidence packs, audit logs

### For Gap Assessments

1. Start with the OWASP MCP Top 10 mapping (most MCP-specific)
2. Cross-reference with NIST AI RMF Govern and Manage functions
3. Identify controls marked as "Recommended" or "Optional" in the [Formal Control Catalog](mcp-governance-risk-framework-v1.0.md#formal-control-catalog) that your organization has not implemented
4. Prioritize gaps by risk tier of affected MCP servers

### For Program Integration

If your organization already has an AI governance program:

- **Do not create a parallel process.** Map MCP governance lifecycle stages to existing AI system approval workflows
- **Extend existing templates** with MCP-specific fields from [Chapter 4 — Required fields](mcp-governance-risk-framework-v1.0.md#required-fields)
- **Add MCP metrics** to existing AI governance dashboards using [Chapter 1 — Step 5](mcp-governance-risk-framework-v1.0.md#step-5-define-monthly-metrics) KPIs

---

[MCP Governance & Risk Framework v1.0](mcp-governance-risk-framework-v1.0.md) · [Guide Home](README.md) · [Reference Links](reference.md)
