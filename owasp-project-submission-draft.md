---
title: OWASP MCP Governance and Risk Project — Submission Draft
draft: true
status: draft
project_name: OWASP MCP Governance and Risk
---

# OWASP MCP Governance and Risk Project — Submission Draft

> **Note:** This is a working draft for the OWASP project submission form. Review and customize before submitting.

---

## Problem space — Why are we doing this?

### Problem statement

Model Context Protocol (MCP) enables AI agents to connect directly to business systems — code repositories, cloud consoles, CRMs, ticketing platforms, identity systems, and production infrastructure — at machine speed, often without the same review channels used for traditional API integrations.

Organizations are adopting MCP faster than they can govern it. Common gaps include:

- **No inventory** — shadow MCP servers on developer laptops and AI platforms go undetected
- **No classification** — a public docs connector and a production Kubernetes admin server receive the same scrutiny (or none)
- **No approval workflow** — teams connect MCP servers ad hoc to meet deadlines
- **No ownership** — no one is accountable when something goes wrong
- **No audit requirements** — forensics after an incident is impossible
- **No vendor review** — third-party and open-source MCP servers access sensitive data without procurement or legal review

Existing security controls (API security, AppSec, LLM guardrails) are necessary but not sufficient. MCP introduces agent-driven tool selection, cross-system prompt injection, token passthrough, confused deputy issues, and tool-level privilege escalation that must be governed at the **organizational** level — not only by individual developers.

**The core question organizations cannot answer today:**

> *Should this MCP server be allowed in our environment, and under what controls?*

This project provides a repeatable, CISO-ready answer.

---

### Innovation

**How this differs from existing OWASP and FOSS solutions:**

| Existing resource | What it provides | Gap this project fills |
|-------------------|------------------|------------------------|
| **OWASP MCP Top 10** | Identifies the top MCP security risks (token mismanagement, shadow MCP, lack of audit, etc.) | Does not tell organizations *how to approve, classify, own, monitor, or remediate* MCP at enterprise scale |
| **OWASP LLM Top 10** | LLM application risks (prompt injection, excessive agency, supply chain) | Covers LLM risks broadly; does not provide MCP-specific governance lifecycle, tiering, or RACI |
| **MCP Security Taxonomy** (community) | Shared vocabulary for describing MCP risks | Defines language, not decision workflows |
| **MCP Testing Guide** (community) | Validates that technical controls work | Assumes governance decisions are already made |
| **MCP spec / security best practices** | Protocol and architectural guidance | Not an organizational governance program |

**This project is the missing operational layer:** it turns MCP risk awareness into **approval decisions, ownership assignments, policy language, metrics, and ongoing monitoring** — aligned with OWASP MCP Top 10, OWASP LLM Top 10, NIST AI RMF, ISO 42001, and SOC 2.

It is also **cross-functional by design**: security, engineering, legal, privacy, procurement, and business owners participate in MCP decisions — not just the team that installed the server.

---

## Ready to make it

### What is the purpose of this Project? / Describe your Project

**Purpose:** Provide the first open, vendor-neutral **MCP Governance & Risk Model** so CISOs, security architects, and AI governance teams can systematically decide which MCP servers are allowed, under what controls, and who owns residual risk.

**Description:**

The OWASP MCP Governance and Risk Project delivers a 16-chapter framework and practical templates that operationalize MCP security across the full lifecycle:

1. **Inventory** — discovery, intake, and shadow MCP detection
2. **Classify** — Tier 0–4 model based on data access, action capability, and blast radius
3. **Score** — eight-factor quantitative risk model for borderline decisions
4. **Approve** — structured workflow: approve, conditionally approve, or reject
5. **Assign ownership** — RACI across business, engineering, AppSec, CISO, legal, and procurement
6. **Monitor** — logging, alerting, periodic review, and CISO dashboard metrics
7. **Respond** — incident response alignment and break-glass procedures

Four non-negotiable governance rules anchor the model:

- No owner = no approval
- No logging = no production use
- No scope definition = no access
- No review = no enterprise deployment

**Primary audience:** CISOs, security architects, AppSec leaders, AI governance teams, risk/compliance, procurement, and engineering leaders adopting AI agents.

**Ecosystem position:** This project complements OWASP MCP Top 10 (risk identification) and community resources such as MCP Security Taxonomy and MCP Testing Guide (language and validation). Governance sits in the center: it decides what is allowed; testing validates that controls work.

---

### Project Deliverables

**Phase 1 — Core guide (current / near-term)**

- **16-chapter MCP Governance & Risk Model** (Markdown, OWASP-ready publication format):
  - Executive summary and threat landscape
  - Five governance principles
  - Asset inventory and shadow MCP governance
  - Tier 0–4 classification and eight-factor risk scoring
  - Approval workflow and RACI ownership model
  - Third-party / OSS vendor review
  - Minimum security baseline with sample policy language
  - High-risk use cases, continuous monitoring, incident response, CISO metrics

- **Operational templates** (ready to adopt):
  - MCP intake form
  - Risk register
  - Vendor questionnaire
  - Approval decision form
  - Exception / risk acceptance form

- **Framework mapping appendix** — crosswalk to OWASP MCP Top 10, OWASP LLM Top 10, NIST AI RMF, ISO 42001, and SOC 2

**Phase 2 — Community and adoption**

- OWASP project page and published documentation site
- Contributor guidelines and review process
- Community feedback loops (issues, discussions, working sessions)
- Case studies / implementation patterns from early adopters

**Phase 3 — Extended outputs (roadmap)**

- Maturity model for MCP governance programs
- Quick-start playbooks by organization size
- Integration guidance with GRC and SIEM tooling
- Alignment updates as MCP spec and OWASP MCP Top 10 evolve

**License:** Open source (recommend **Creative Commons BY-SA 4.0** or **Apache 2.0**, consistent with other OWASP documentation projects).

---

### Project Roadmap — First year as an OWASP Project

**Q1 — Foundation and launch**

- Complete OWASP project onboarding and publish project page
- Finalize v1.0 of the 16-chapter guide and templates
- Publish framework mapping appendix
- Announce project; recruit core contributors and reviewers from AppSec, AI governance, and MCP practitioner communities
- Establish GitHub repository, issue templates, and contribution guidelines

**Q2 — Validation and refinement**

- Run **pilot reviews** with 3–5 organizations implementing the model
- Collect feedback on classification tiers, scoring worksheet, and approval workflow
- Release **v1.1** with clarifications from pilot feedback
- Host community working session(s) on shadow MCP and third-party review
- Coordinate with **OWASP MCP Top 10** maintainers on cross-references and control mapping

**Q3 — Adoption enablement**

- Release **Quick Start Guide** (30/60/90-day implementation path for CISOs)
- Publish **role-based reading paths** (CISO, AppSec, engineering, compliance)
- Add worked examples for Tier 3–4 scenarios (GitHub admin, cloud admin, CI/CD)
- Develop **maturity model** draft (Level 1–4 governance maturity)
- Present at OWASP chapter meetings and relevant conferences

**Q4 — Scale and sustain**

- Release **v2.0** incorporating community contributions and spec updates
- Publish **implementation case studies** (anonymized where needed)
- Evaluate companion artifacts (checklist PDF, GRC integration notes)
- Annual review against MCP authorization spec, OWASP MCP Top 10 updates, and NIST AI RMF
- Plan Year 2: training materials, assessment checklist, and deeper integration with MCP Testing Guide ecosystem

---

### Anything else?

**Relationship to the MCP security ecosystem**

This project is intentionally designed as the **governance hub** in a broader MCP security ecosystem:

- **OWASP MCP Top 10** → defines *what* can go wrong
- **This project** → defines *what is allowed* and *who owns risk*
- **MCP Testing Guide** → validates *whether controls work*
- **MCP Security Taxonomy** → provides shared *risk language*
- **Awesome MCP CVE / Awesome MCP Security List** → inform threat models and vendor review

**Neutrality and scope**

- Vendor-neutral; no product endorsements
- Focuses on **governance and risk management**, not MCP server implementation
- Complements — does not duplicate — OWASP MCP Top 10 or OWASP LLM Top 10

**Why now**

MCP adoption is accelerating across AI platforms (Cursor, Claude, Copilot, custom agents). Organizations that wait for an incident or audit to discover shadow MCP will pay a high cost. A published OWASP governance model gives security leaders a credible, community-maintained starting point before the gap becomes a breach.

**Suggested project leaders / contacts** *(fill in before submitting)*

- Project Leader: [Name, affiliation]
- Core contributors: [Names]
- Liaison to OWASP MCP Top 10: [Name, if applicable]

---

### Project Policy & Procedures

**Openness**

- All project content maintained in a **public GitHub repository** under an OSI-approved license
- Documentation published on the **OWASP project site**
- Decisions, roadmap, and release notes documented transparently

**Neutrality**

- No vendor or product endorsements
- Examples use generic or hypothetical scenarios; no preferential treatment of commercial MCP servers or AI platforms
- Contributors disclose affiliations per OWASP contributor guidelines

**Contribution model**

- Contributions via GitHub pull requests with maintainer review
- Issues used for bugs, gaps, and enhancement requests
- Major changes (new tiers, scoring factors, policy language) discussed in GitHub Discussions or scheduled working sessions before merge
- Subject matter experts (CISO, AppSec, legal, engineering) invited for structured review of sensitive chapters

**Quality and accuracy**

- Content aligned with official MCP specification and authorization requirements (OAuth 2.1, audience validation)
- Framework mappings reviewed when OWASP MCP Top 10, OWASP LLM Top 10, or NIST AI RMF receive updates
- Versioned releases (semver-style: v1.0, v1.1, v2.0) with changelog

**Release cadence**

- **Minor releases** (clarifications, template updates): quarterly or as needed
- **Major releases** (structural changes, new chapters): annually or when MCP ecosystem shifts materially
- **Emergency updates** for factual errors or spec misalignment: as soon as practicable

**Community engagement**

- Respond to GitHub issues and PRs within a defined SLA (e.g., 14 days for initial response)
- Quarterly community sync (virtual) for roadmap and feedback
- Encourage chapter presentations and conference talks citing the project

**Conflict of interest**

- Maintainers and leaders follow OWASP conflict-of-interest policies
- Commercial MCP vendors may contribute but may not control project direction

**Security of the project itself**

- No secrets or organization-specific data in the repository
- Templates are generic; organizations customize locally

---

## Submission checklist

- [ ] Fill in project leader and contributor names
- [ ] Confirm license choice (CC BY-SA 4.0 or Apache 2.0)
- [ ] Verify GitHub repository URL for submission form
- [ ] Trim sections to fit OWASP form character limits if needed
- [ ] Set `draft: false` when ready to publish internally
