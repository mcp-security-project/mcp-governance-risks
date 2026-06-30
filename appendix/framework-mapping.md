# Framework Mapping Appendix

**Purpose:** Map MCP Governance & Risk Model controls to established security and AI governance frameworks. Use this appendix for compliance audits, gap assessments, and alignment with existing organizational programs.

**Related guide chapters:** This mapping references controls defined in [Chapter 3](../chapters/03-governance-principles.md) through [Chapter 15](../chapters/15-ciso-metrics.md).

---

## OWASP MCP Top 10

The OWASP MCP Top 10 identifies the most critical security risks for MCP deployments. This table maps each risk category to guide controls.

| OWASP MCP Risk | Guide Section | Control / Implementation |
|----------------|---------------|--------------------------|
| MCP01 — Token Mismanagement & Audience Confusion | [Ch. 2](../chapters/02-why-mcp-needs-governance.md), [Ch. 9](../chapters/09-third-party-review.md), [Ch. 10](../chapters/10-minimum-security-baseline.md) | Enforce OAuth 2.1 with audience validation; reject token passthrough; verify during third-party review |
| MCP02 — Privilege Escalation | [Ch. 3](../chapters/03-governance-principles.md) (Principle 3), [Ch. 5](../chapters/05-server-classification.md), [Ch. 11](../chapters/11-high-risk-use-cases.md) | Least privilege per tool; separate read/write scopes; JIT access for Tier 4 |
| MCP03 — Lack of Audit and Telemetry | [Ch. 3](../chapters/03-governance-principles.md) (Principle 5), [Ch. 13](../chapters/13-continuous-monitoring.md) | Mandatory audit logging with user/agent/tool/action attribution; SIEM integration |
| MCP04 — Prompt Injection via Tool Output | [Ch. 2](../chapters/02-why-mcp-needs-governance.md), [Ch. 11](../chapters/11-high-risk-use-cases.md) | Prompt injection testing for Tier 2+; HITL for write actions; content sanitization |
| MCP05 — Tool Permission Smuggling | [Ch. 5](../chapters/05-server-classification.md), [Ch. 7](../chapters/07-approval-workflow.md) | Classify by highest-risk tool; re-classify when tools change; approval before new tools |
| MCP06 — Supply Chain / Dependency Risk | [Ch. 9](../chapters/09-third-party-review.md) | Vendor questionnaire; SBOM review; dependency CVE scanning; version pinning |
| MCP07 — Insufficient Input Validation | [Ch. 10](../chapters/10-minimum-security-baseline.md), [Ch. 11](../chapters/11-high-risk-use-cases.md) | Parameter validation; DLP on tool inputs; rate limits |
| MCP08 — Session Management Weaknesses | [Ch. 2](../chapters/02-why-mcp-needs-governance.md), [Ch. 10](../chapters/10-minimum-security-baseline.md) | Session binding, rotation, and timeout requirements in security review |
| MCP09 — Shadow MCP Deployments | [Ch. 4](../chapters/04-asset-inventory.md), [Ch. 12](../chapters/12-shadow-mcp-governance.md) | Inventory, discovery, prohibition policy, platform allowlists |
| MCP10 — Insecure Default Configurations | [Ch. 10](../chapters/10-minimum-security-baseline.md), [Ch. 7](../chapters/07-approval-workflow.md) | Minimum security baseline by tier; secure defaults verified during deployment |

---

## OWASP LLM Top 10

MCP governance intersects with LLM security risks because agents use LLMs to decide which tools to invoke.

| OWASP LLM Risk | Guide Section | Control / Implementation |
|----------------|---------------|--------------------------|
| LLM01 — Prompt Injection | [Ch. 2](../chapters/02-why-mcp-needs-governance.md), [Ch. 11](../chapters/11-high-risk-use-cases.md) | Prompt injection testing; HITL for high-risk actions; tool chaining awareness |
| LLM02 — Insecure Output Handling | [Ch. 13](../chapters/13-continuous-monitoring.md) | DLP on outbound tool parameters; output sanitization before downstream use |
| LLM03 — Training Data Poisoning | [Ch. 9](../chapters/09-third-party-review.md) | Vendor review: confirm MCP data is not used for model training |
| LLM04 — Model Denial of Service | [Ch. 11](../chapters/11-high-risk-use-cases.md), [Ch. 13](../chapters/13-continuous-monitoring.md) | Rate limits on tool calls; volume anomaly alerting |
| LLM05 — Supply Chain Vulnerabilities | [Ch. 9](../chapters/09-third-party-review.md) | Third-party MCP review; SBOM; dependency scanning |
| LLM06 — Sensitive Information Disclosure | [Ch. 5](../chapters/05-server-classification.md), [Ch. 10](../chapters/10-minimum-security-baseline.md) | Data classification; DLP; data minimization for Tier 2+ |
| LLM07 — Insecure Plugin/Tool Design | [Ch. 3](../chapters/03-governance-principles.md), [Ch. 5](../chapters/05-server-classification.md) | Tool-level classification; least privilege; threat modeling for Tier 3–4 |
| LLM08 — Excessive Agency | [Ch. 3](../chapters/03-governance-principles.md) (Principle 4), [Ch. 11](../chapters/11-high-risk-use-cases.md) | HITL approval; scope limits; segregation of duties |
| LLM09 — Overreliance | [Ch. 8](../chapters/08-risk-ownership-raci.md) | Business owner accountability; human review of agent decisions |
| LLM10 — Model Theft | [Ch. 9](../chapters/09-third-party-review.md) | Vendor data handling review; ensure MCP does not expose model weights |

---

## NIST AI Risk Management Framework (AI RMF)

| NIST AI RMF Function | Category | Guide Section | Implementation |
|----------------------|----------|---------------|----------------|
| **Govern** | GV-1 Policies | [Ch. 10](../chapters/10-minimum-security-baseline.md) | MCP usage policy; shadow MCP prohibition |
| **Govern** | GV-2 Accountability | [Ch. 8](../chapters/08-risk-ownership-raci.md) | RACI matrix; named owners; risk acceptance |
| **Govern** | GV-6 Third-party risk | [Ch. 9](../chapters/09-third-party-review.md) | Vendor questionnaire; procurement review |
| **Map** | MP-2 Categories of AI systems | [Ch. 5](../chapters/05-server-classification.md) | Tier 0–4 classification model |
| **Map** | MP-5 Impact assessment | [Ch. 6](../chapters/06-risk-scoring.md) | Eight-factor risk scoring |
| **Measure** | MS-2 Metrics | [Ch. 15](../chapters/15-ciso-metrics.md) | 15 monthly KPIs |
| **Measure** | MS-2.7 Monitoring | [Ch. 13](../chapters/13-continuous-monitoring.md) | Audit logging, alerting, periodic review |
| **Manage** | MG-2 Risk treatment | [Ch. 7](../chapters/07-approval-workflow.md) | Approve / conditional / reject decisions |
| **Manage** | MG-3 Third-party risk | [Ch. 9](../chapters/09-third-party-review.md) | Vendor review outcomes |
| **Manage** | MG-4 Incident response | [Ch. 14](../chapters/14-incident-response.md) | MCP incident response playbook |

---

## ISO/IEC 42001 (AI Management System)

| ISO 42001 Area | Guide Section | Implementation |
|----------------|---------------|----------------|
| 6.1 — Risk assessment | [Ch. 5](../chapters/05-server-classification.md), [Ch. 6](../chapters/06-risk-scoring.md) | Tier classification and quantitative scoring |
| 6.1 — Risk treatment | [Ch. 7](../chapters/07-approval-workflow.md), [Ch. 10](../chapters/10-minimum-security-baseline.md) | Approval decisions with required controls |
| 7.4 — Communication | [Ch. 8](../chapters/08-risk-ownership-raci.md) | RACI matrix; stakeholder notification |
| 8.1 — Operational planning | [Ch. 4](../chapters/04-asset-inventory.md), [Ch. 7](../chapters/07-approval-workflow.md) | Governance lifecycle (intake through deployment) |
| 8.2 — AI system impact assessment | [Ch. 11](../chapters/11-high-risk-use-cases.md) | Scenario-specific threat models for Tier 3–4 |
| 8.3 — Data for AI systems | [Ch. 9](../chapters/09-third-party-review.md) (Section 3) | Data handling review; DLP requirements |
| 8.4 — Third-party relationships | [Ch. 9](../chapters/09-third-party-review.md) | Vendor questionnaire and review outcomes |
| 9.1 — Monitoring and measurement | [Ch. 13](../chapters/13-continuous-monitoring.md), [Ch. 15](../chapters/15-ciso-metrics.md) | Continuous monitoring and monthly KPIs |
| 9.2 — Internal audit | [Ch. 13](../chapters/13-continuous-monitoring.md) | Periodic review cadence by tier |
| 10.1 — Continual improvement | [Ch. 14](../chapters/14-incident-response.md) (Phase 5) | Post-incident review; governance gap remediation |

---

## SOC 2 Trust Service Criteria

| SOC 2 Criteria | Guide Section | Implementation |
|----------------|---------------|----------------|
| **CC6.1** — Logical access | [Ch. 10](../chapters/10-minimum-security-baseline.md) | Authentication, scoped authorization, SSO/OAuth |
| **CC6.2** — Access removal | [Ch. 14](../chapters/14-incident-response.md) | Credential revocation during incident containment |
| **CC6.3** — Role-based access | [Ch. 8](../chapters/08-risk-ownership-raci.md) | RACI matrix; approval authority by tier |
| **CC6.6** — System boundaries | [Ch. 4](../chapters/04-asset-inventory.md), [Ch. 12](../chapters/12-shadow-mcp-governance.md) | Inventory; allowlists; shadow MCP prohibition |
| **CC6.7** — Data transmission | [Ch. 9](../chapters/09-third-party-review.md) | Token handling; no passthrough; DLP |
| **CC6.8** — Malicious software | [Ch. 9](../chapters/09-third-party-review.md) | Dependency scanning; SBOM review |
| **CC7.1** — Detection | [Ch. 13](../chapters/13-continuous-monitoring.md) | Alerting rules; anomaly detection |
| **CC7.2** — Monitoring | [Ch. 13](../chapters/13-continuous-monitoring.md), [Ch. 15](../chapters/15-ciso-metrics.md) | Audit logging; monthly metrics |
| **CC7.3** — Incident response | [Ch. 14](../chapters/14-incident-response.md) | MCP incident response playbook |
| **CC7.4** — Recovery | [Ch. 14](../chapters/14-incident-response.md) (Phase 4) | Eradicate and recover procedures |
| **CC8.1** — Change management | [Ch. 7](../chapters/07-approval-workflow.md) | Approval workflow before deployment; version pinning |
| **CC9.2** — Vendor risk | [Ch. 9](../chapters/09-third-party-review.md) | Vendor questionnaire and review |

---

## Internal AI Governance Policies

Use this section to map guide controls to your organization's internal AI governance policies. Replace the placeholder rows with your actual policy references.

| Internal Policy | Guide Section | Alignment Notes |
|-----------------|---------------|-----------------|
| [Your AI Usage Policy] | [Ch. 10](../chapters/10-minimum-security-baseline.md) | Adopt MCP-specific policy language from Chapter 10 |
| [Your AI Risk Assessment Process] | [Ch. 5](../chapters/05-server-classification.md), [Ch. 6](../chapters/06-risk-scoring.md) | MCP tier classification and scoring as AI risk assessment |
| [Your Third-Party AI Vendor Policy] | [Ch. 9](../chapters/09-third-party-review.md) | Extend vendor review to include MCP vendor questionnaire |
| [Your AI Incident Response Plan] | [Ch. 14](../chapters/14-incident-response.md) | Add MCP-specific playbook to existing IR plan |
| [Your Data Classification Standard] | [Ch. 5](../chapters/05-server-classification.md) | Map data classes to MCP tier requirements |
| [Your Privileged Access Policy] | [Ch. 11](../chapters/11-high-risk-use-cases.md) | Tier 4 MCP servers follow PAM/JIT requirements |

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
3. Identify controls marked as "Recommended" or "Optional" in [Chapter 10](../chapters/10-minimum-security-baseline.md) that your organization has not implemented
4. Prioritize gaps by risk tier of affected MCP servers

### For Program Integration

If your organization already has an AI governance program:

- **Do not create a parallel process.** Map MCP governance lifecycle stages to existing AI system approval workflows
- **Extend existing templates** with MCP-specific fields from the [Intake Form](../templates/intake-form.md)
- **Add MCP metrics** to existing AI governance dashboards using [Chapter 15](../chapters/15-ciso-metrics.md) KPIs

---

[Back to Guide Home](../README.md)
