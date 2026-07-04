# Framework Mapping Appendix

**Purpose:** Map MCP Governance & Risk Model controls to established security and AI governance frameworks. Use this appendix for compliance audits, gap assessments, and alignment with existing organizational programs.

**Related guide:** This mapping references controls defined in the [MCP Governance & Risk Framework](mcp-governance-risk-framework.md) ([MCP Governance Principles](mcp-governance-risk-framework.md#chapter-3-mcp-governance-principles) through [Metrics for CISOs](mcp-governance-risk-framework.md#chapter-15-metrics-for-cisos)).

---

## OWASP MCP Top 10

The OWASP MCP Top 10 identifies the most critical security risks for MCP deployments. This table maps each risk category to guide controls.

| OWASP MCP Risk | Guide Section | Control / Implementation |
|----------------|---------------|--------------------------|
| MCP01 — Token Mismanagement & Audience Confusion | [Ch. 2](mcp-governance-risk-framework.md#chapter-2-why-mcp-needs-governance), [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review), [Ch. 10](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) | Enforce OAuth 2.1 with audience validation; reject token passthrough; verify during third-party review |
| MCP02 — Privilege Escalation | [Ch. 3](mcp-governance-risk-framework.md#chapter-3-mcp-governance-principles) (Principle 3), [Ch. 5](mcp-governance-risk-framework.md#chapter-5-mcp-server-classification-model), [Ch. 11](mcp-governance-risk-framework.md#chapter-11-high-risk-mcp-use-cases) | Least privilege per tool; separate read/write scopes; JIT access for Tier 4 |
| MCP03 — Lack of Audit and Telemetry | [Ch. 3](mcp-governance-risk-framework.md#chapter-3-mcp-governance-principles) (Principle 5), [Ch. 13](mcp-governance-risk-framework.md#chapter-13-continuous-monitoring) | Mandatory audit logging with user/agent/tool/action attribution; SIEM integration |
| MCP04 — Prompt Injection via Tool Output | [Ch. 2](mcp-governance-risk-framework.md#chapter-2-why-mcp-needs-governance), [Ch. 11](mcp-governance-risk-framework.md#chapter-11-high-risk-mcp-use-cases) | Prompt injection testing for Tier 2+; HITL for write actions; content sanitization |
| MCP05 — Tool Permission Smuggling | [Ch. 5](mcp-governance-risk-framework.md#chapter-5-mcp-server-classification-model), [Ch. 7](mcp-governance-risk-framework.md#chapter-7-approval-workflow) | Classify by highest-risk tool; re-classify when tools change; approval before new tools |
| MCP06 — Supply Chain / Dependency Risk | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Vendor questionnaire; SBOM review; dependency CVE scanning; version pinning |
| MCP07 — Insufficient Input Validation | [Ch. 10](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline), [Ch. 11](mcp-governance-risk-framework.md#chapter-11-high-risk-mcp-use-cases) | Parameter validation; DLP on tool inputs; rate limits |
| MCP08 — Session Management Weaknesses | [Ch. 2](mcp-governance-risk-framework.md#chapter-2-why-mcp-needs-governance), [Ch. 10](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) | Session binding, rotation, and timeout requirements in security review |
| MCP09 — Shadow MCP Deployments | [Ch. 4](mcp-governance-risk-framework.md#chapter-4-mcp-asset-inventory), [Ch. 12](mcp-governance-risk-framework.md#chapter-12-shadow-mcp-governance) | Inventory, discovery, prohibition policy, platform allowlists |
| MCP10 — Insecure Default Configurations | [Ch. 10](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline), [Ch. 7](mcp-governance-risk-framework.md#chapter-7-approval-workflow) | Minimum security baseline by tier; secure defaults verified during deployment |

---

## OWASP LLM Top 10

MCP governance intersects with LLM security risks because agents use LLMs to decide which tools to invoke.

| OWASP LLM Risk | Guide Section | Control / Implementation |
|----------------|---------------|--------------------------|
| LLM01 — Prompt Injection | [Ch. 2](mcp-governance-risk-framework.md#chapter-2-why-mcp-needs-governance), [Ch. 11](mcp-governance-risk-framework.md#chapter-11-high-risk-mcp-use-cases) | Prompt injection testing; HITL for high-risk actions; tool chaining awareness |
| LLM02 — Insecure Output Handling | [Ch. 13](mcp-governance-risk-framework.md#chapter-13-continuous-monitoring) | DLP on outbound tool parameters; output sanitization before downstream use |
| LLM03 — Training Data Poisoning | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Vendor review: confirm MCP data is not used for model training |
| LLM04 — Model Denial of Service | [Ch. 11](mcp-governance-risk-framework.md#chapter-11-high-risk-mcp-use-cases), [Ch. 13](mcp-governance-risk-framework.md#chapter-13-continuous-monitoring) | Rate limits on tool calls; volume anomaly alerting |
| LLM05 — Supply Chain Vulnerabilities | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Third-party MCP review; SBOM; dependency scanning |
| LLM06 — Sensitive Information Disclosure | [Ch. 5](mcp-governance-risk-framework.md#chapter-5-mcp-server-classification-model), [Ch. 10](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) | Data classification; DLP; data minimization for Tier 2+ |
| LLM07 — Insecure Plugin/Tool Design | [Ch. 3](mcp-governance-risk-framework.md#chapter-3-mcp-governance-principles), [Ch. 5](mcp-governance-risk-framework.md#chapter-5-mcp-server-classification-model) | Tool-level classification; least privilege; threat modeling for Tier 3–4 |
| LLM08 — Excessive Agency | [Ch. 3](mcp-governance-risk-framework.md#chapter-3-mcp-governance-principles) (Principle 4), [Ch. 11](mcp-governance-risk-framework.md#chapter-11-high-risk-mcp-use-cases) | HITL approval; scope limits; segregation of duties |
| LLM09 — Overreliance | [Ch. 8](mcp-governance-risk-framework.md#chapter-8-risk-ownership-and-raci) | Business owner accountability; human review of agent decisions |
| LLM10 — Model Theft | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Vendor data handling review; ensure MCP does not expose model weights |

---

## NIST AI Risk Management Framework (AI RMF)

| NIST AI RMF Function | Category | Guide Section | Implementation |
|----------------------|----------|---------------|----------------|
| **Govern** | GV-1 Policies | [Ch. 10](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) | MCP usage policy; shadow MCP prohibition |
| **Govern** | GV-2 Accountability | [Ch. 8](mcp-governance-risk-framework.md#chapter-8-risk-ownership-and-raci) | RACI matrix; named owners; risk acceptance |
| **Govern** | GV-6 Third-party risk | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Vendor questionnaire; procurement review |
| **Map** | MP-2 Categories of AI systems | [Ch. 5](mcp-governance-risk-framework.md#chapter-5-mcp-server-classification-model) | Tier 0–4 classification model |
| **Map** | MP-5 Impact assessment | [Ch. 6](mcp-governance-risk-framework.md#chapter-6-mcp-risk-scoring-model) | Eight-factor risk scoring |
| **Measure** | MS-2 Metrics | [Ch. 15](mcp-governance-risk-framework.md#chapter-15-metrics-for-cisos) | 15 monthly KPIs |
| **Measure** | MS-2.7 Monitoring | [Ch. 13](mcp-governance-risk-framework.md#chapter-13-continuous-monitoring) | Audit logging, alerting, periodic review |
| **Manage** | MG-2 Risk treatment | [Ch. 7](mcp-governance-risk-framework.md#chapter-7-approval-workflow) | Approve / conditional / reject decisions |
| **Manage** | MG-3 Third-party risk | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Vendor review outcomes |
| **Manage** | MG-4 Incident response | [Ch. 14](mcp-governance-risk-framework.md#chapter-14-incident-response-alignment) | MCP incident response playbook |

---

## ISO/IEC 42001 (AI Management System)

| ISO 42001 Area | Guide Section | Implementation |
|----------------|---------------|----------------|
| 6.1 — Risk assessment | [Ch. 5](mcp-governance-risk-framework.md#chapter-5-mcp-server-classification-model), [Ch. 6](mcp-governance-risk-framework.md#chapter-6-mcp-risk-scoring-model) | Tier classification and quantitative scoring |
| 6.1 — Risk treatment | [Ch. 7](mcp-governance-risk-framework.md#chapter-7-approval-workflow), [Ch. 10](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) | Approval decisions with required controls |
| 7.4 — Communication | [Ch. 8](mcp-governance-risk-framework.md#chapter-8-risk-ownership-and-raci) | RACI matrix; stakeholder notification |
| 8.1 — Operational planning | [Ch. 4](mcp-governance-risk-framework.md#chapter-4-mcp-asset-inventory), [Ch. 7](mcp-governance-risk-framework.md#chapter-7-approval-workflow) | Governance lifecycle (intake through deployment) |
| 8.2 — AI system impact assessment | [Ch. 11](mcp-governance-risk-framework.md#chapter-11-high-risk-mcp-use-cases) | Scenario-specific threat models for Tier 3–4 |
| 8.3 — Data for AI systems | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) (Section 3) | Data handling review; DLP requirements |
| 8.4 — Third-party relationships | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Vendor questionnaire and review outcomes |
| 9.1 — Monitoring and measurement | [Ch. 13](mcp-governance-risk-framework.md#chapter-13-continuous-monitoring), [Ch. 15](mcp-governance-risk-framework.md#chapter-15-metrics-for-cisos) | Continuous monitoring and monthly KPIs |
| 9.2 — Internal audit | [Ch. 13](mcp-governance-risk-framework.md#chapter-13-continuous-monitoring) | Periodic review cadence by tier |
| 10.1 — Continual improvement | [Ch. 14](mcp-governance-risk-framework.md#chapter-14-incident-response-alignment) (Phase 5) | Post-incident review; governance gap remediation |

---

## SOC 2 Trust Service Criteria

| SOC 2 Criteria | Guide Section | Implementation |
|----------------|---------------|----------------|
| **CC6.1** — Logical access | [Ch. 10](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) | Authentication, scoped authorization, SSO/OAuth |
| **CC6.2** — Access removal | [Ch. 14](mcp-governance-risk-framework.md#chapter-14-incident-response-alignment) | Credential revocation during incident containment |
| **CC6.3** — Role-based access | [Ch. 8](mcp-governance-risk-framework.md#chapter-8-risk-ownership-and-raci) | RACI matrix; approval authority by tier |
| **CC6.6** — System boundaries | [Ch. 4](mcp-governance-risk-framework.md#chapter-4-mcp-asset-inventory), [Ch. 12](mcp-governance-risk-framework.md#chapter-12-shadow-mcp-governance) | Inventory; allowlists; shadow MCP prohibition |
| **CC6.7** — Data transmission | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Token handling; no passthrough; DLP |
| **CC6.8** — Malicious software | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Dependency scanning; SBOM review |
| **CC7.1** — Detection | [Ch. 13](mcp-governance-risk-framework.md#chapter-13-continuous-monitoring) | Alerting rules; anomaly detection |
| **CC7.2** — Monitoring | [Ch. 13](mcp-governance-risk-framework.md#chapter-13-continuous-monitoring), [Ch. 15](mcp-governance-risk-framework.md#chapter-15-metrics-for-cisos) | Audit logging; monthly metrics |
| **CC7.3** — Incident response | [Ch. 14](mcp-governance-risk-framework.md#chapter-14-incident-response-alignment) | MCP incident response playbook |
| **CC7.4** — Recovery | [Ch. 14](mcp-governance-risk-framework.md#chapter-14-incident-response-alignment) (Phase 4) | Eradicate and recover procedures |
| **CC8.1** — Change management | [Ch. 7](mcp-governance-risk-framework.md#chapter-7-approval-workflow) | Approval workflow before deployment; version pinning |
| **CC9.2** — Vendor risk | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Vendor questionnaire and review |

---

## Internal AI Governance Policies

Use this section to map guide controls to your organization's internal AI governance policies. Replace the placeholder rows with your actual policy references.

| Internal Policy | Guide Section | Alignment Notes |
|-----------------|---------------|-----------------|
| [Your AI Usage Policy] | [Ch. 10](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) | Adopt MCP-specific policy language from [Minimum Security Baseline](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) |
| [Your AI Risk Assessment Process] | [Ch. 5](mcp-governance-risk-framework.md#chapter-5-mcp-server-classification-model), [Ch. 6](mcp-governance-risk-framework.md#chapter-6-mcp-risk-scoring-model) | MCP tier classification and scoring as AI risk assessment |
| [Your Third-Party AI Vendor Policy] | [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Extend vendor review to include MCP vendor questionnaire |
| [Your AI Incident Response Plan] | [Ch. 14](mcp-governance-risk-framework.md#chapter-14-incident-response-alignment) | Add MCP-specific playbook to existing IR plan |
| [Your Data Classification Standard] | [Ch. 5](mcp-governance-risk-framework.md#chapter-5-mcp-server-classification-model) | Map data classes to MCP tier requirements |
| [Your Privileged Access Policy] | [Ch. 11](mcp-governance-risk-framework.md#chapter-11-high-risk-mcp-use-cases) | Tier 4 MCP servers follow PAM/JIT requirements |

---

## Using This Mapping

### For Compliance Audits

1. Identify the framework your auditor is assessing against
2. Locate the relevant mapping table in this appendix
3. Reference the guide chapter that implements each control
4. Provide evidence: completed templates, risk register entries, approval decisions, audit logs

### For Gap Assessments

1. Start with the OWASP MCP Top 10 mapping (most MCP-specific)
2. Cross-reference with NIST AI RMF Govern and Manage functions
3. Identify controls marked as "Recommended" or "Optional" in [Chapter 10](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) that your organization has not implemented
4. Prioritize gaps by risk tier of affected MCP servers

### For Program Integration

If your organization already has an AI governance program:

- **Do not create a parallel process.** Map MCP governance lifecycle stages to existing AI system approval workflows
- **Extend existing templates** with MCP-specific fields from the [Intake Form](important-forms/intake-form.md)
- **Add MCP metrics** to existing AI governance dashboards using [Chapter 15](mcp-governance-risk-framework.md#chapter-15-metrics-for-cisos) KPIs

---

[MCP Governance & Risk Framework](mcp-governance-risk-framework.md) · [Guide Home](README.md)
