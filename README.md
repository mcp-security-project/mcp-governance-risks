# MCP Governance & Risk Model

**A CISO Guide for Approving, Classifying, and Managing MCP Risk**

This guide helps organizations answer one central question: *Should this MCP server be allowed in our environment, and under what controls?*

**Full framework (all 16 chapters):** [MCP Governance & Risk Framework](mcp-governance-risk-framework.md)

Model Context Protocol (MCP) connects AI agents to tools, data, APIs, files, identity systems, cloud platforms, and business workflows. That connectivity spans security, engineering, legal, privacy, procurement, risk, and business ownership. This guide provides the governance framework to manage that risk systematically.

---

## How to Use This Guide

**First-time readers (CISO / security leadership):** Start with [Chapter 1](mcp-governance-risk-framework.md#chapter-1-executive-summary) and [Chapter 2](mcp-governance-risk-framework.md#chapter-2-why-mcp-needs-governance), then skim [Chapter 5](mcp-governance-risk-framework.md#chapter-5-mcp-server-classification-model) and [Chapter 7](mcp-governance-risk-framework.md#chapter-7-approval-workflow). Or read the [full framework](mcp-governance-risk-framework.md) in one document.

**Security architects / AppSec:** Read Chapters 3–10 in the [framework](mcp-governance-risk-framework.md). These chapters cover principles, inventory, classification, scoring, approval, ownership, third-party review, and minimum baselines.

**Operational teams:** Use Chapters 11–15 in the [framework](mcp-governance-risk-framework.md) for high-risk scenarios, shadow MCP handling, monitoring, incident response, and metrics.

**Practitioners submitting requests:** Start with [Chapter 16](mcp-governance-risk-framework.md#chapter-16-templates) and the [Important Forms](important-forms/) folder.

**Compliance mapping:** See [Framework Mapping](framework-mapping.md) for OWASP, NIST, ISO, and SOC 2 alignment.

---

## Audience

- CISOs and delegated security risk boards
- Security architects and AppSec leaders
- AI governance teams
- Enterprise architecture teams
- Risk and compliance teams
- Procurement and vendor review teams
- Engineering leaders adopting AI agents

---

## Ten Questions This Guide Answers

1. Which MCP servers are allowed?
2. Who approved them?
3. What data can they access?
4. What actions can they perform?
5. Are they internal, third-party, open-source, or shadow MCP servers?
6. What authentication and authorization model do they use?
7. Are tool calls logged and auditable?
8. Can the MCP server write, delete, execute, deploy, or exfiltrate data?
9. What happens if the MCP server is compromised?
10. Who owns the risk?

---

## Chapters

All chapters are available in the single [MCP Governance & Risk Framework](mcp-governance-risk-framework.md) document.

| # | Chapter | Description |
|---|---------|-------------|
| 1 | [Executive Summary](mcp-governance-risk-framework.md#chapter-1-executive-summary) | One-page CISO brief, ecosystem context, and guide overview |
| 2 | [Why MCP Needs Governance](mcp-governance-risk-framework.md#chapter-2-why-mcp-needs-governance) | Threat landscape, MCP-specific risks, and why developer-only controls fail |
| 3 | [MCP Governance Principles](mcp-governance-risk-framework.md#chapter-3-mcp-governance-principles) | Five foundational principles every organization should adopt |
| 4 | [MCP Asset Inventory](mcp-governance-risk-framework.md#chapter-4-mcp-asset-inventory) | Discovery, intake fields, and inventory management |
| 5 | [MCP Server Classification Model](mcp-governance-risk-framework.md#chapter-5-mcp-server-classification-model) | Tier 0–4 classification with examples and approval authority |
| 6 | [MCP Risk Scoring Model](mcp-governance-risk-framework.md#chapter-6-mcp-risk-scoring-model) | Quantitative scoring worksheet and worked examples |
| 7 | [Approval Workflow](mcp-governance-risk-framework.md#chapter-7-approval-workflow) | Intake through deployment: approve, conditionally approve, or reject |
| 8 | [Risk Ownership and RACI](mcp-governance-risk-framework.md#chapter-8-risk-ownership-and-raci) | Roles, responsibilities, and accountability matrix |
| 9 | [Third-Party MCP Review](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) | Vendor checklist for external and open-source MCP servers |
| 10 | [Minimum Security Baseline](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) | Required controls by tier and sample policy language |
| 11 | [High-Risk MCP Use Cases](mcp-governance-risk-framework.md#chapter-11-high-risk-mcp-use-cases) | Tier 3–4 scenarios and mandatory controls |
| 12 | [Shadow MCP Governance](mcp-governance-risk-framework.md#chapter-12-shadow-mcp-governance) | Detection, prohibition, and remediation of unapproved servers |
| 13 | [Continuous Monitoring](mcp-governance-risk-framework.md#chapter-13-continuous-monitoring) | Logging, alerting, and periodic review cadence |
| 14 | [Incident Response Alignment](mcp-governance-risk-framework.md#chapter-14-incident-response-alignment) | Playbook for MCP compromise and break-glass procedures |
| 15 | [Metrics for CISOs](mcp-governance-risk-framework.md#chapter-15-metrics-for-cisos) | Monthly dashboard KPIs and data sources |
| 16 | [Templates](mcp-governance-risk-framework.md#chapter-16-templates) | How to use intake, risk register, and approval forms |

---

## Important Forms

| Form | Purpose |
|------|---------|
| [Intake Form](important-forms/intake-form.md) | Initial request for a new MCP server |
| [Risk Register](important-forms/risk-register.md) | Ongoing inventory of approved MCP servers and their risk posture |
| [Vendor Questionnaire](important-forms/vendor-questionnaire.md) | Third-party and open-source MCP review |
| [Approval Decision Form](important-forms/approval-decision-form.md) | Document approve / conditional / reject decisions |
| [Exception / Risk Acceptance Form](important-forms/exception-risk-acceptance-form.md) | Formal risk acceptance for exceptions |

---

## Framework Mapping

- [Framework Mapping](framework-mapping.md) — Alignment with OWASP MCP Top 10, OWASP LLM Top 10, NIST AI RMF, ISO 42001, SOC 2, and internal AI governance

---

## Related Resources

This guide sits within a broader MCP security ecosystem:

- **MCP Security Taxonomy** — Defines the risk language
- **MCP Governance & Risk Model** (this guide) — Decides what is allowed and who owns risk
- **MCP Testing Guide** — Validates whether controls actually work
- **Awesome MCP CVE** — Tracks real-world failure patterns
- **Awesome MCP Security List** — Curates resources, tools, research, and guidance
