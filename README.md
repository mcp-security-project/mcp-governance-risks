# MCP Governance & Risk Model

**A CISO Guide for Approving, Classifying, and Managing MCP Risk**

This guide helps organizations answer one central question: *Should this MCP server be allowed in our environment, and under what controls?*

Model Context Protocol (MCP) connects AI agents to tools, data, APIs, files, identity systems, cloud platforms, and business workflows. That connectivity spans security, engineering, legal, privacy, procurement, risk, and business ownership. This guide provides the governance framework to manage that risk systematically.

---

## How to Use This Guide

**First-time readers (CISO / security leadership):** Start with [Chapter 1](chapters/01-executive-summary.md) and [Chapter 2](chapters/02-why-mcp-needs-governance.md), then skim [Chapter 5](chapters/05-server-classification.md) and [Chapter 7](chapters/07-approval-workflow.md).

**Security architects / AppSec:** Read Chapters 3–10 in order. These chapters cover principles, inventory, classification, scoring, approval, ownership, third-party review, and minimum baselines.

**Operational teams:** Use Chapters 11–15 for high-risk scenarios, shadow MCP handling, monitoring, incident response, and metrics.

**Practitioners submitting requests:** Start with [Chapter 16](chapters/16-templates.md) and the [templates](templates/) folder.

**Compliance mapping:** See the [Framework Mapping Appendix](appendix/framework-mapping.md) for OWASP, NIST, ISO, and SOC 2 alignment.

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

| # | Chapter | Description |
|---|---------|-------------|
| 1 | [Executive Summary](chapters/01-executive-summary.md) | One-page CISO brief, ecosystem context, and guide overview |
| 2 | [Why MCP Needs Governance](chapters/02-why-mcp-needs-governance.md) | Threat landscape, MCP-specific risks, and why developer-only controls fail |
| 3 | [MCP Governance Principles](chapters/03-governance-principles.md) | Five foundational principles every organization should adopt |
| 4 | [MCP Asset Inventory](chapters/04-asset-inventory.md) | Discovery, intake fields, and inventory management |
| 5 | [MCP Server Classification Model](chapters/05-server-classification.md) | Tier 0–4 classification with examples and approval authority |
| 6 | [MCP Risk Scoring Model](chapters/06-risk-scoring.md) | Quantitative scoring worksheet and worked examples |
| 7 | [Approval Workflow](chapters/07-approval-workflow.md) | Intake through deployment: approve, conditionally approve, or reject |
| 8 | [Risk Ownership and RACI](chapters/08-risk-ownership-raci.md) | Roles, responsibilities, and accountability matrix |
| 9 | [Third-Party MCP Review](chapters/09-third-party-review.md) | Vendor checklist for external and open-source MCP servers |
| 10 | [Minimum Security Baseline](chapters/10-minimum-security-baseline.md) | Required controls by tier and sample policy language |
| 11 | [High-Risk MCP Use Cases](chapters/11-high-risk-use-cases.md) | Tier 3–4 scenarios and mandatory controls |
| 12 | [Shadow MCP Governance](chapters/12-shadow-mcp-governance.md) | Detection, prohibition, and remediation of unapproved servers |
| 13 | [Continuous Monitoring](chapters/13-continuous-monitoring.md) | Logging, alerting, and periodic review cadence |
| 14 | [Incident Response Alignment](chapters/14-incident-response.md) | Playbook for MCP compromise and break-glass procedures |
| 15 | [Metrics for CISOs](chapters/15-ciso-metrics.md) | Monthly dashboard KPIs and data sources |
| 16 | [Templates](chapters/16-templates.md) | How to use intake, risk register, and approval forms |

---

## Templates

| Template | Purpose |
|----------|---------|
| [Intake Form](templates/intake-form.md) | Initial request for a new MCP server |
| [Risk Register](templates/risk-register.md) | Ongoing inventory of approved MCP servers and their risk posture |
| [Vendor Questionnaire](templates/vendor-questionnaire.md) | Third-party and open-source MCP review |
| [Approval Decision Form](templates/approval-decision-form.md) | Document approve / conditional / reject decisions |
| [Exception / Risk Acceptance Form](templates/exception-risk-acceptance-form.md) | Formal risk acceptance for exceptions |

---

## Appendix

- [Framework Mapping](appendix/framework-mapping.md) — Alignment with OWASP MCP Top 10, OWASP LLM Top 10, NIST AI RMF, ISO 42001, SOC 2, and internal AI governance

---

## Related Resources

This guide sits within a broader MCP security ecosystem:

- **MCP Security Taxonomy** — Defines the risk language
- **MCP Governance & Risk Model** (this guide) — Decides what is allowed and who owns risk
- **MCP Testing Guide** — Validates whether controls actually work
- **Awesome MCP CVE** — Tracks real-world failure patterns
- **Awesome MCP Security List** — Curates resources, tools, research, and guidance
