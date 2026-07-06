---
title: MCP Governance & Risk — Reference Links
draft: true
status: draft
description: Curated URLs for MCP governance, risk, security, and compliance resources
---

# MCP Governance & Risk — Reference Links

This document consolidates external references for the **MCP Governance & Risk Model** guide — including every URL cited in the guide chapters, related resources from the broader MCP security and AI governance ecosystem, and additional links useful for threat modeling, vendor review, compliance mapping, and control validation.

---

## URLs Cited in This Guide

These links appear in the [MCP Governance & Risk Framework](mcp-governance-risk-framework.md) and related documents.

| Resource | URL | Used in |
|----------|-----|---------|
| MCP Specification | https://spec.modelcontextprotocol.io/ | [Ch. 1](mcp-governance-risk-framework.md#chapter-1-executive-summary), [Ch. 2](mcp-governance-risk-framework.md#chapter-2-why-mcp-needs-governance) |
| MCP Authorization Specification (2025-11-25) | https://spec.modelcontextprotocol.io/specification/2025-11-25/basic/authorization/ | [Ch. 1](mcp-governance-risk-framework-v1.0.md#chapter-1-executive-summary), [Ch. 2](mcp-governance-risk-framework-v1.0.md#chapter-2-why-mcp-needs-governance), [Ch. 3](mcp-governance-risk-framework-v1.0.md#chapter-3-mcp-governance-principles), [Ch. 6](mcp-governance-risk-framework-v1.0.md#chapter-6-mcp-risk-scoring-model), [Appendix](mcp-governance-risk-framework-v1.0.md#formal-control-catalog) |
| MCP Security Best Practices | https://modelcontextprotocol.io/specification/draft/basic/security_best_practices | [Ch. 1](mcp-governance-risk-framework.md#chapter-1-executive-summary), [Ch. 2](mcp-governance-risk-framework.md#chapter-2-why-mcp-needs-governance), [Ch. 10](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) |
| OWASP MCP Top 10 | https://owasp.org/www-project-mcp-top-10/ | [Ch. 1](mcp-governance-risk-framework.md#chapter-1-executive-summary)–[Ch. 5](mcp-governance-risk-framework.md#chapter-5-mcp-server-classification-model), [Ch. 9](mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review), [Ch. 11](mcp-governance-risk-framework.md#chapter-11-high-risk-mcp-use-cases)–[Ch. 13](mcp-governance-risk-framework.md#chapter-13-continuous-monitoring) |
| OWASP Top 10 for LLM Applications | https://owasp.org/www-project-top-10-for-large-language-model-applications/ | [Ch. 1](mcp-governance-risk-framework.md#chapter-1-executive-summary), [Ch. 2](mcp-governance-risk-framework.md#chapter-2-why-mcp-needs-governance), [Ch. 3](mcp-governance-risk-framework.md#chapter-3-mcp-governance-principles), [Ch. 11](mcp-governance-risk-framework.md#chapter-11-high-risk-mcp-use-cases) |
| NIST AI Risk Management Framework (AI RMF 1.0) | https://www.nist.gov/itl/ai-risk-management-framework | [Ch. 1](mcp-governance-risk-framework.md#chapter-1-executive-summary) |
| ISO/IEC 42001:2023 | https://www.iso.org/standard/81230.html | [Ch. 1](mcp-governance-risk-framework.md#chapter-1-executive-summary) |
| Awesome MCP Security List | https://github.com/awesome-mcp-security/awesome-mcp-security | [Ch. 1](mcp-governance-risk-framework.md#chapter-1-executive-summary), [Ch. 2](mcp-governance-risk-framework.md#chapter-2-why-mcp-needs-governance) |
| Awesome MCP CVE | https://github.com/awesome-mcp-security/awesome-mcp-cve | [Ch. 1](mcp-governance-risk-framework.md#chapter-1-executive-summary), [Ch. 2](mcp-governance-risk-framework.md#chapter-2-why-mcp-needs-governance) |
| NIST SP 800-61 Rev. 2 (Incident Response) | https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final | [Ch. 14](mcp-governance-risk-framework.md#chapter-14-incident-response-alignment) |

---

## Internal Guide Documents

| Document | Path | Purpose |
|----------|------|---------|
| MCP Governance & Risk Framework | [mcp-governance-risk-framework.md](mcp-governance-risk-framework.md) | Complete 16-chapter guide in one document |
| README / guide index | [README.md](README.md) | Navigation and audience routing |
| Framework Mapping Appendix | [framework-mapping.md](framework-mapping.md) | OWASP, NIST AI RMF, ISO 42001, SOC 2 alignment |
| OWASP Project Submission Draft | [owasp-project-submission-draft.md](owasp-project-submission-draft.md) | Project charter and ecosystem positioning |
| Intake Form | [important-forms/intake-form.md](important-forms/intake-form.md) | New MCP server request |
| Risk Register | [important-forms/risk-register.md](important-forms/risk-register.md) | Approved server inventory |
| Vendor Questionnaire | [important-forms/vendor-questionnaire.md](important-forms/vendor-questionnaire.md) | Third-party / OSS review |
| Approval Decision Form | [important-forms/approval-decision-form.md](important-forms/approval-decision-form.md) | Approve / conditional / reject |
| Exception / Risk Acceptance Form | [important-forms/exception-risk-acceptance-form.md](important-forms/exception-risk-acceptance-form.md) | Formal risk acceptance |

---

## MCP Official Protocol & Security

| Resource | URL |
|----------|-----|
| Model Context Protocol (main site) | https://modelcontextprotocol.io/ |
| MCP documentation index (`llms.txt`) | https://modelcontextprotocol.io/llms.txt |
| MCP Specification (spec site) | https://spec.modelcontextprotocol.io/ |
| MCP Specification (2025-11-25) | https://spec.modelcontextprotocol.io/specification/2025-11-25/ |
| MCP Authorization (2025-11-25) | https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization |
| MCP Authorization (spec site, 2025-11-25) | https://spec.modelcontextprotocol.io/specification/2025-11-25/basic/authorization/ |
| MCP Specification (2025-03-26) | https://spec.modelcontextprotocol.io/specification/2025-03-26/ |
| MCP Authorization (2025-03-26, historical) | https://modelcontextprotocol.io/specification/2025-03-26/basic/authorization |
| MCP Authorization (spec site, 2025-03-26, historical) | https://spec.modelcontextprotocol.io/specification/2025-03-26/basic/authorization/ |
| MCP Security Best Practices (draft spec path) | https://modelcontextprotocol.io/specification/draft/basic/security_best_practices |
| MCP Security Best Practices (2025-11-25) | https://modelcontextprotocol.io/specification/2025-11-25/basic/security_best_practices |
| MCP Security Best Practices (docs tutorial) | https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices |
| Anthropic — Introducing MCP | https://www.anthropic.com/news/model-context-protocol |
| MCP GitHub organization | https://github.com/modelcontextprotocol |
| MCP specification repository | https://github.com/modelcontextprotocol/modelcontextprotocol |
| Official MCP Registry | https://registry.modelcontextprotocol.io/ |
| MCP Registry — about | https://modelcontextprotocol.io/registry/about |
| MCP Registry — charter | https://modelcontextprotocol.io/community/registry/charter |
| MCP Registry — GitHub | https://github.com/modelcontextprotocol/registry |
| MCP Registry launch announcement | https://blog.modelcontextprotocol.io/posts/2025-09-08-mcp-registry-preview/ |

### OAuth & Transport Standards (referenced by MCP auth spec)

| Resource | URL |
|----------|-----|
| OAuth 2.1 (IETF draft) | https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-11 |
| OAuth 2.0 Security Best Current Practice (RFC 9700) | https://datatracker.ietf.org/doc/html/rfc9700 |
| OAuth 2.0 Authorization Server Metadata (RFC 8414) | https://datatracker.ietf.org/doc/html/rfc8414 |
| OAuth 2.0 Dynamic Client Registration (RFC 7591) | https://datatracker.ietf.org/doc/html/rfc7591 |
| OAuth 2.0 Token Exchange (RFC 8693) | https://datatracker.ietf.org/doc/html/rfc8693 |
| IETF Internet-Draft — Secure MCP (message signing & tool integrity) | https://datatracker.ietf.org/doc/draft-secure-mcp/ |

---

## OWASP MCP Top 10

| Resource | URL |
|----------|-----|
| OWASP MCP Top 10 (project page) | https://owasp.org/www-project-mcp-top-10/ |
| OWASP MCP Top 10 (GitHub repository) | https://github.com/OWASP/www-project-mcp-top-10/ |

### Individual Risk Categories (2025 v0.1)

| ID | Risk | URL |
|----|------|-----|
| MCP01 | Token Mismanagement & Secret Exposure | https://owasp.org/www-project-mcp-top-10/2025/MCP01-2025-Token-Mismanagement-and-Secret-Exposure |
| MCP02 | Privilege Escalation via Scope Creep | https://owasp.org/www-project-mcp-top-10/2025/MCP02-2025-%E2%80%93Privilege-Escalation-via-Scope-Creep |
| MCP03 | Tool Poisoning | https://owasp.org/www-project-mcp-top-10/2025/MCP03-2025-%E2%80%93Tool-Poisoning |
| MCP04 | Software Supply Chain Attacks & Dependency Tampering | https://owasp.org/www-project-mcp-top-10/2025/MCP04-2025-%E2%80%93Software-Supply-Chain-Attacks&Dependency-Tampering |
| MCP05 | Command Injection & Execution | https://owasp.org/www-project-mcp-top-10/2025/MCP05-2025-%E2%80%93Command-Injection&Execution |
| MCP06 | Intent Flow Subversion / Prompt Injection via Contextual Payloads | https://owasp.org/www-project-mcp-top-10/2025/MCP06-2025-%E2%80%93Prompt-InjectionviaContextual-Payloads |
| MCP07 | Insufficient Authentication & Authorization | https://owasp.org/www-project-mcp-top-10/2025/MCP07-2025-%E2%80%93Insufficient-Authentication&Authorization |
| MCP08 | Lack of Audit and Telemetry | https://owasp.org/www-project-mcp-top-10/2025/MCP08-2025-%E2%80%93Lack-of-Audit-and-Telemetry |
| MCP09 | Shadow MCP Servers | https://owasp.org/www-project-mcp-top-10/2025/MCP09-2025-%E2%80%93Shadow-MCP-Servers |
| MCP10 | Context Injection & Over-Sharing | https://owasp.org/www-project-mcp-top-10/2025/MCP10-2025-%E2%80%93ContextInjection&OverSharing |

---

## OWASP LLM, GenAI & Agentic Security

| Resource | URL |
|----------|-----|
| OWASP Top 10 for LLM Applications (project page) | https://owasp.org/www-project-top-10-for-large-language-model-applications/ |
| OWASP Top 10 for LLM Applications (GitHub) | https://github.com/OWASP/Top10LLMForLLMApp |
| OWASP GenAI Security Project | https://genai.owasp.org/ |
| OWASP LLM Top 10 (latest) | https://genai.owasp.org/llm-top-10/ |
| OWASP Top 10 for Agentic Applications (2026) | https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/ |
| OWASP GenAI — Contribute | https://genai.owasp.org/contribute/ |
| OWASP GenAI — Meetings | https://genai.owasp.org/meetings/ |
| OWASP MCP Security Cheat Sheet | https://cheatsheetseries.owasp.org/cheatsheets/MCP_Security_Cheat_Sheet.html |
| OWASP AI Security Verification Standard (AISVS) | https://owasp.org/www-project-ai-security-verification-standard/ |
| OWASP AISVS — C10 MCP Security | https://github.com/OWASP/AISVS/blob/main/1.0/en/0x10-C10-MCP-Security.md |
| OWASP SSRF Prevention Cheat Sheet | https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html |

---

## AI Governance & Risk Frameworks

| Resource | URL | Relevance |
|----------|-----|-----------|
| NIST AI Risk Management Framework (AI RMF 1.0) | https://www.nist.gov/itl/ai-risk-management-framework | Govern, Map, Measure, Manage — [Framework Mapping Appendix](framework-mapping.md) |
| NIST AI RMF Playbook | https://www.nist.gov/itl/ai-risk-management-framework/nist-ai-rmf-1-0 | Implementation guidance |
| NIST AI RMF — Generative AI Profile | https://www.nist.gov/itl/ai-risk-management-framework/generative-artificial-intelligence-profile | GenAI-specific RMF guidance |
| NIST Cybersecurity Framework 2.0 | https://www.nist.gov/cyberframework | Mapped in COMPEL MCP baseline |
| NIST SP 800-61 Rev. 2 — Incident Response | https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final | [Ch. 14](mcp-governance-risk-framework.md#chapter-14-incident-response-alignment) IR alignment |
| NIST SP 800-207 — Zero Trust Architecture | https://csrc.nist.gov/pubs/sp/800/207/final | OWASP AISVS MCP controls |
| ISO/IEC 42001:2023 — AI management systems | https://www.iso.org/standard/81230.html | Formal AI governance programs |
| EU AI Act (official text) | https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689 | Regulated AI system obligations |

---

## Standards, Baselines & Certification

Testable control frameworks useful for tier alignment, vendor questionnaires, and audit evidence.

| Resource | URL | Notes |
|----------|-----|-------|
| MCP Server Security Standard (MSSS) | https://github.com/mcp-security-standard/mcp-server-security-standard | 24 controls, 4 levels (L1–L4), deployment profiles |
| COMPEL — MCP 12-Control Hardening Baseline | https://www.compelframework.org/articles/model-context-protocol-security-standards | Maps to NIST CSF 2.0 and ISO 42001 |
| SlowMist MCP Security Checklist | https://github.com/slowmist/MCP-Security-Checklist | Server, client, host, multi-MCP scenarios |
| Appsecco — Pentesting MCP Servers Checklist | https://github.com/appsecco/pentesting-mcp-servers-checklist | Traffic, auth, tool behavior, injection |
| SAF-MCP — Secure Agentic Framework | https://github.com/safe-agentic-framework/safe-mcp | MITRE ATT&CK-style MCP TTP taxonomy |
| MCPSEC — MCP Security Benchmark | https://github.com/paolovella/vellaveto/tree/main/mcpsec | 10 properties, 105 attack test cases |

---

## Cloud & Enterprise Governance Guides

| Resource | URL | Focus |
|----------|-----|-------|
| AWS — MCP Strategies (introduction) | https://docs.aws.amazon.com/prescriptive-guidance/latest/mcp-strategies/introduction.html | Tool design, hosting, governance pillars |
| AWS — MCP Governance Strategy | https://docs.aws.amazon.com/prescriptive-guidance/latest/mcp-strategies/mcp-governance-strategy.html | Auth, rate limits, metrics, distribution |
| AWS — MCP Hosting Strategy | https://docs.aws.amazon.com/prescriptive-guidance/latest/mcp-strategies/mcp-hosting-strategy.html | Local vs remote, registries, gateways |
| AWS — MCP Strategies (PDF) | https://docs.aws.amazon.com/pdfs/prescriptive-guidance/latest/mcp-strategies/mcp-strategies.pdf | Full guide download |
| AWS — AgentCore OBO Token Exchange | https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/on-behalf-of-token-exchange.html | Confused-deputy mitigation pattern |
| Microsoft — MCP Azure Security Guide | https://github.com/microsoft/mcp-azure-security-guide | OWASP MCP Top 10 on Azure |
| Microsoft — MCP Azure Security Guide (site) | https://microsoft.github.io/mcp-azure-security-guide/ | Published controls and architectures |
| Microsoft — Agent Governance Toolkit | https://github.com/microsoft/agent-governance-toolkit | MCP OWASP compliance mapping |
| Microsoft — MCP for Beginners (Security module) | https://github.com/microsoft/mcp-for-beginners/tree/main/02-Security | Learning path with OWASP mapping |
| Microsoft — State of MCP Security in 2026 | https://techcommunity.microsoft.com/blog/microsoft-security-blog/the-state-of-mcp-security-in-2026/4531327 | Industry threat landscape summary |
| Microsoft — APIM as MCP Auth Gateway | https://techcommunity.microsoft.com/blog/integrationsonazureblog/azure-api-management-your-auth-gateway-for-mcp-servers/4402690 | Gateway enforcement pattern |

---

## Research, Taxonomies & Threat Models

Academic and formal frameworks that inform classification, threat modeling, and vendor review.

| Resource | URL | Notes |
|----------|-----|-------|
| MCP Landscape, Security Threats & Future Research (Hou et al.) | https://arxiv.org/abs/2503.23278 | Lifecycle threat taxonomy; 16 scenarios |
| MCP Landscape — HTML version | https://arxiv.org/html/2503.23278v3 | Same paper, web format |
| MCP Landscape — data repository | https://github.com/security-pride/MCP_Landscape | Case studies and implementation examples |
| SoK: Security and Safety in the MCP Ecosystem | https://arxiv.org/html/2512.08290 | Security vs safety taxonomy; context weaponization |
| MCPShield — Formal Security Framework for MCP Agents | https://arxiv.org/abs/2604.05969 | 7 categories, 23 attack vectors, verification model |
| Simplified and Secure MCP Gateways (enterprise integration) | https://arxiv.org/abs/2504.19997 | Gateway architecture for enterprise AI |
| Wiz — MCP Security Research Briefing | https://www.wiz.io/blog/mcp-security-research-briefing | Remote server risk analysis |
| Invariant Labs — Tool Poisoning Attacks | https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks | Rug pulls and description injection |

---

## Security Testing, Audit & Discovery Tools

Tools that support governance evidence collection, third-party review, and continuous monitoring.

| Resource | URL | Use in governance |
|----------|-----|-------------------|
| mcp-scan (Invariant Labs) | https://github.com/invariantlabs-ai/mcp-scan | Tool poisoning / shadowing detection |
| MCP Tool Poisoning Experiments | https://github.com/invariantlabs-ai/mcp-injection-experiments | Prompt injection via tool output research |
| SecureMCP | https://github.com/makalin/SecureMCP | Vulnerability and misconfiguration auditing |
| MCP Audit Extension (VS Code / Copilot) | https://github.com/Agentity-com/mcp-audit-extension | Tool call logging for review evidence |
| ToolHive (Stacklok) | https://github.com/StacklokLabs/toolhive | MCP server isolation and lifecycle |
| MCP Defender | https://github.com/MCP-Defender/MCP-Defender | MCP-specific defense tooling |
| AI-Infra-Guard (Tencent) | https://github.com/Tencent/AI-Infra-Guard | AI infrastructure security scanning |

---

## MCP Security Community Resources

| Resource | URL |
|----------|-----|
| Awesome MCP Security List | https://github.com/awesome-mcp-security/awesome-mcp-security |
| Awesome MCP CVE | https://github.com/awesome-mcp-security/awesome-mcp-cve |
| Awesome MCP Security (Puliczek — actively maintained) | https://github.com/Puliczek/awesome-mcp-security |
| Awesome MCP Security — contributing guide | https://github.com/Puliczek/awesome-mcp-security/blob/main/CONTRIBUTING.md |

---

## Industry Analysis & Practitioner Articles

Selected articles useful for executive briefings, threat modeling, and reviewer education. For exhaustive lists, see Awesome MCP Security.

| Resource | URL | Topic |
|----------|-----|-------|
| Trail of Bits — MCP servers attack before first use | https://blog.trailofbits.com/2025/04/21/jumping-the-line-how-mcp-servers-can-attack-you-before-you-ever-use-them/ | Supply chain / install-time risk |
| Trail of Bits — MCP conversation history theft | https://blog.trailofbits.com/2025/04/23/how-mcp-servers-can-steal-your-conversation-history | Data exfiltration |
| Trail of Bits — Insecure credential storage in MCP | https://blog.trailofbits.com/2025/04/30/insecure-credential-storage-plagues-mcp/ | MCP01 token mismanagement |
| Trail of Bits — Security layer MCP needed | https://blog.trailofbits.com/2025/07/28/we-built-the-security-layer-mcp-always-needed/ | Gateway / policy enforcement |
| Block Goose — Securing MCP | https://block.github.io/goose/blog/2025/03/31/securing-mcp/ | Enterprise MCP hardening |
| Simon Willison — MCP prompt injection | https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/ | Cross-tool injection demo |
| Auth0 — MCP and Authorization intro | https://auth0.com/blog/an-introduction-to-mcp-and-authorization/ | OAuth patterns for MCP |
| Aaron Parecki — OAuth for MCP | https://aaronparecki.com/2025/04/03/15/oauth-for-model-context-protocol | Authorization design |
| Obot — MCP Security Best Practices (2026 guide) | https://obot.ai/resources/learning-center/mcp-security/ | Defense-in-depth framework |
| Cisco — MCP and Security | https://community.cisco.com/t5/security-blogs/ai-model-context-protocol-mcp-and-security/ba-p/5274394 | Enterprise security perspective |
| Windows — Securing MCP on Windows | https://blogs.windows.com/windowsexperience/2025/05/19/securing-the-model-context-protocol-building-a-safer-agentic-future-on-windows/ | Platform-level controls |

---

## Related Ecosystem (Referenced in This Project)

The [README](README.md) and [OWASP submission draft](owasp-project-submission-draft.md) describe a broader MCP security ecosystem:

| Resource | Status | URL / Notes |
|----------|--------|-------------|
| **MCP Governance & Risk Model** (this guide) | In development | This repository |
| **MCP Security Taxonomy** | URL TBD | Shared risk language — see [MCP Landscape paper](https://arxiv.org/abs/2503.23278) and [SAF-MCP](https://github.com/safe-agentic-framework/safe-mcp) for interim taxonomies |
| **MCP Testing Guide** | URL TBD | Validates whether controls work — see [MCPSEC](https://github.com/paolovella/vellaveto/tree/main/mcpsec) and [Appsecco checklist](https://github.com/appsecco/pentesting-mcp-servers-checklist) |
| **OWASP MCP Top 10** | Published (beta v0.1) | Defines *what* can go wrong |
| **Awesome MCP CVE / Awesome MCP Security** | Published | Threat models and vendor review inputs |
| **MSSS** | Published (v0.1) | Certifiable control standard for MCP servers |

---

## Quick Reference by Guide Topic

| Guide topic | Primary URLs |
|-------------|--------------|
| Approval & authorization | [MCP Authorization Spec (2025-11-25)](https://spec.modelcontextprotocol.io/specification/2025-11-25/basic/authorization/), [MCP Security Best Practices](https://modelcontextprotocol.io/specification/2025-11-25/basic/security_best_practices), [OWASP MCP Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/MCP_Security_Cheat_Sheet.html) |
| Classification & risk scoring | [OWASP MCP Top 10](https://owasp.org/www-project-mcp-top-10/), [MSSS levels](https://github.com/mcp-security-standard/mcp-server-security-standard), [Framework Mapping Appendix](framework-mapping.md) |
| Asset inventory & registry | [Official MCP Registry](https://registry.modelcontextprotocol.io/), [MCP Registry about](https://modelcontextprotocol.io/registry/about) |
| Third-party / supply chain review | [OWASP MCP04](https://owasp.org/www-project-mcp-top-10/2025/MCP04-2025-%E2%80%93Software-Supply-Chain-Attacks&Dependency-Tampering), [Awesome MCP CVE](https://github.com/awesome-mcp-security/awesome-mcp-cve), [Vendor Questionnaire](important-forms/vendor-questionnaire.md) |
| Shadow MCP & inventory | [OWASP MCP09](https://owasp.org/www-project-mcp-top-10/2025/MCP09-2025-%E2%80%93Shadow-MCP-Servers), [Ch. 12](mcp-governance-risk-framework.md#chapter-12-shadow-mcp-governance) |
| Audit & monitoring | [OWASP MCP08](https://owasp.org/www-project-mcp-top-10/2025/MCP08-2025-%E2%80%93Lack-of-Audit-and-Telemetry), [MCP Audit Extension](https://github.com/Agentity-com/mcp-audit-extension) |
| High-risk / HITL scenarios | [OWASP MCP06](https://owasp.org/www-project-mcp-top-10/2025/MCP06-2025-%E2%80%93Prompt-InjectionviaContextual-Payloads), [OWASP LLM Top 10](https://genai.owasp.org/llm-top-10/) |
| Incident response | [NIST SP 800-61](https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final), [Ch. 14](mcp-governance-risk-framework.md#chapter-14-incident-response-alignment) |
| Compliance mapping | [Framework Mapping Appendix](framework-mapping.md), [COMPEL baseline](https://www.compelframework.org/articles/model-context-protocol-security-standards), [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) |
| Enterprise rollout | [AWS MCP Governance Strategy](https://docs.aws.amazon.com/prescriptive-guidance/latest/mcp-strategies/mcp-governance-strategy.html), [Microsoft MCP Azure Security Guide](https://microsoft.github.io/mcp-azure-security-guide/) |
| Reviewer prompts & evidence | [Ch. 7 — Approval Workflow](mcp-governance-risk-framework.md#chapter-7-approval-workflow) |

---

## Maintenance Notes

- **Draft status:** This file is not yet linked from the main guide navigation. Review before promoting to published status.
- **OWASP MCP Top 10:** Currently in beta (v0.1). Risk names and URLs may change at final release. Note: published OWASP MCP risk names differ slightly from some internal guide chapter mappings — reconcile during final release.
- **Current spec version:** This guide targets MCP Specification **2025-11-25** as the current authorization reference. Older versions (2025-03-26, 2025-06-18) remain listed for historical comparison.
- **Dual spec hosts:** MCP documentation appears on both `modelcontextprotocol.io` and `spec.modelcontextprotocol.io`. Verify which version your deployment targets.
- **Link rot:** Community awesome lists and blog posts change frequently. Prefer standards bodies, official MCP docs, and GitHub repos as canonical sources.
- **Contributions:** Add new URLs via pull request. Prefer governance, risk, compliance, and MCP-specific security sources over general AI news.

---

## Internet Review Additions — 2026-06-30

These references were identified during an internet review and are recommended additions before publishing. They emphasize official protocol documentation, governance/community process, security-relevant SEPs, current NIST incident response guidance, and platform implementation references.

### Official MCP Documentation Gaps

| Resource | URL | Why add it |
|----------|-----|------------|
| MCP Specification (2025-06-18) | https://modelcontextprotocol.io/specification/2025-06-18 | Official intermediate spec version between 2025-03-26 and 2025-11-25 |
| MCP Key Changes (2025-06-18) | https://modelcontextprotocol.io/specification/2025-06-18/changelog | Helps reviewers understand version-specific behavior changes |
| MCP Authorization (2025-06-18) | https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization | Versioned auth reference for OAuth and audience validation |
| MCP Transports (2025-06-18) | https://modelcontextprotocol.io/specification/2025-06-18/basic/transports | Useful for local vs. remote server risk review |
| MCP Tools (2025-06-18) | https://modelcontextprotocol.io/specification/2025-06-18/server/tools | Canonical tool behavior reference for classification and HITL review |
| MCP Sampling (2025-06-18) | https://modelcontextprotocol.io/specification/2025-06-18/client/sampling | Important for server-initiated model calls and recursive agent behavior |
| MCP Elicitation (2025-06-18) | https://modelcontextprotocol.io/specification/2025-06-18/client/elicitation | Relevant to user data collection and consent review |
| MCP Roots (2025-06-18) | https://modelcontextprotocol.io/specification/2025-06-18/client/roots | Relevant to filesystem and workspace boundary review |
| MCP Logging utility (2025-11-25) | https://modelcontextprotocol.io/specification/2025-11-25/server/utilities/logging | Useful for audit and monitoring discussions |
| Understanding Authorization in MCP | https://modelcontextprotocol.io/docs/tutorials/security/authorization | Practical auth implementation guide |
| MCP Client Best Practices | https://modelcontextprotocol.io/docs/develop/clients/client-best-practices | Useful for host/client-side governance, tool filtering, and multi-server risk |
| Connect to remote MCP servers | https://modelcontextprotocol.io/docs/develop/connect-remote-servers | Remote server deployment and connection guidance |
| MCP Inspector | https://modelcontextprotocol.io/docs/tools/inspector | Useful for testing, debugging, and review evidence |
| MCP SDKs | https://modelcontextprotocol.io/docs/sdk | Official SDK reference for implementation and vendor review |

### MCP Governance, Community, and Security Process

| Resource | URL | Why add it |
|----------|-----|------------|
| MCP Governance and Stewardship | https://modelcontextprotocol.io/community/governance | Official governance model for the protocol project |
| MCP Security Policy | https://modelcontextprotocol.io/community/security | Vulnerability reporting and disclosure process |
| MCP Security Interest Group Charter | https://modelcontextprotocol.io/community/interest-groups/security | Official security group scope |
| MCP Authorization Interest Group Charter | https://modelcontextprotocol.io/community/interest-groups/auth | Useful for tracking authorization evolution |
| MCP Enterprise-Managed Authorization Charter | https://modelcontextprotocol.io/community/interest-groups/enterprise-managed-authorization | Enterprise auth governance direction |
| MCP Working and Interest Groups | https://modelcontextprotocol.io/community/working-interest-groups | How MCP governance groups operate |
| MCP Feature Lifecycle and Deprecation Policy | https://modelcontextprotocol.io/community/feature-lifecycle | Helps organizations track spec feature maturity |
| MCP Roadmap | https://modelcontextprotocol.io/development/roadmap | Useful for governance planning and version monitoring |
| MCP SEPs index | https://modelcontextprotocol.io/seps/index | Canonical list of Specification Enhancement Proposals |

### Security-Relevant MCP SEPs

| Resource | URL | Why add it |
|----------|-----|------------|
| SEP-932: Model Context Protocol Governance | https://modelcontextprotocol.io/seps/932-model-context-protocol-governance | Official governance SEP for MCP project process |
| SEP-1024: MCP Client Security Requirements for Local Server Installation | https://modelcontextprotocol.io/seps/1024-mcp-client-security-requirements-for-local-server- | Directly relevant to shadow MCP, local install risk, and client trust |
| SEP-414: OpenTelemetry Trace Context Propagation Conventions | https://modelcontextprotocol.io/seps/414-request-meta | Useful for monitoring, traceability, and audit correlation |
| SEP-985: Align OAuth 2.0 Protected Resource Metadata with RFC 9728 | https://modelcontextprotocol.io/seps/985-align-oauth-20-protected-resource-metadata-with-rf | Important for OAuth metadata and resource-server security |
| SEP-990: Enterprise IdP Policy Controls During MCP OAuth Flows | https://modelcontextprotocol.io/seps/990-enable-enterprise-idp-policy-controls-during-mcp-o | Enterprise identity policy enforcement |
| SEP-991: URL-Based Client Registration Using OAuth Client ID Metadata Documents | https://modelcontextprotocol.io/seps/991-enable-url-based-client-registration-using-oauth-c | Relevant to dynamic registration and client trust |
| SEP-1046: OAuth Client Credentials Flow in Authorization | https://modelcontextprotocol.io/seps/1046-support-oauth-client-credentials-flow-in-authoriza | Relevant to service-account and machine-to-machine MCP use |
| SEP-2207: OIDC-Flavored Refresh Token Guidance | https://modelcontextprotocol.io/seps/2207-oidc-refresh-token-guidance | Relevant to token lifecycle governance |
| SEP-2243: HTTP Header Standardization for Streamable HTTP Transport | https://modelcontextprotocol.io/seps/2243-http-standardization | Useful for gateway and transport security reviews |
| SEP-2468: Recommend Issuer Claim for Auth | https://modelcontextprotocol.io/seps/2468-recommend-issuer-claim-for-auth | Relevant to token issuer validation |
| SEP-2577: Deprecate Roots, Sampling, and Logging | https://modelcontextprotocol.io/seps/2577-deprecate-roots-sampling-and-logging | Important lifecycle note for governance documents referencing these features |

### OWASP and AppSec References Worth Adding

| Resource | URL | Why add it |
|----------|-----|------------|
| OWASP AI Agent Security Cheat Sheet | https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html | Agentic security guidance adjacent to MCP governance |
| OWASP LLM Prompt Injection Prevention Cheat Sheet | https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html | Useful for prompt/tool-output injection controls |
| OWASP RAG Security Cheat Sheet | https://cheatsheetseries.owasp.org/cheatsheets/RAG_Security_Cheat_Sheet.html | Relevant when MCP servers expose retrieval and knowledge-base tools |
| OWASP Logging Cheat Sheet | https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html | Supports audit log design in [Minimum Security Baseline](mcp-governance-risk-framework.md#chapter-10-minimum-security-baseline) and [Continuous Monitoring](mcp-governance-risk-framework.md#chapter-13-continuous-monitoring) |
| OWASP Secrets Management Cheat Sheet | https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html | Supports MCP01/token and secret handling controls |
| OWASP Software Supply Chain Security Cheat Sheet | https://cheatsheetseries.owasp.org/cheatsheets/Software_Supply_Chain_Security_Cheat_Sheet.html | Supports third-party and OSS MCP review |

### Updated Governance and Incident Response References

| Resource | URL | Why add it |
|----------|-----|------------|
| NIST SP 800-61 Rev. 3 — Incident Response Recommendations and Considerations for Cybersecurity Risk Management | https://csrc.nist.gov/pubs/sp/800/61/r3/final | Current final incident response guidance; supersedes Rev. 2 |
| NIST SP 800-61 Rev. 3 DOI | https://doi.org/10.6028/NIST.SP.800-61r3 | Stable DOI for citation |
| NIST AI RMF Playbook | https://airc.nist.gov/airmf-resources/playbook/ | Official implementation suggestions for AI RMF outcomes |
| NIST AI RMF Crosswalk Documents | https://airc.nist.gov/airmf-resources/crosswalks/ | Useful for compliance mappings |
| NIST Cybersecurity Framework 2.0 | https://www.nist.gov/cyberframework | Useful because SP 800-61 Rev. 3 is framed as a CSF 2.0 Community Profile |

### Platform Implementation References

| Resource | URL | Why add it |
|----------|-----|------------|
| OpenAI API — MCP and Connectors | https://developers.openai.com/api/docs/guides/tools-connectors-mcp | Platform implementation reference for hosted MCP and connectors |
| OpenAI Agents SDK — MCP | https://openai.github.io/openai-agents-python/mcp/ | SDK reference including transports, approvals, filtering, and tracing |
| OpenAI Apps SDK examples | https://developers.openai.com/apps-sdk/build/examples | Useful where MCP Apps or interactive components are in scope |
| Microsoft Semantic Kernel — MCP concept sample | https://learn.microsoft.com/semantic-kernel/concepts/plugins/adding-mcp-plugins | Platform implementation reference for MCP plugins |

### Research References Worth Considering

| Resource | URL | Why add it |
|----------|-----|------------|
| Breaking the Protocol: Security Analysis of MCP Specification and Prompt Injection Vulnerabilities | https://arxiv.org/abs/2601.17549 | Protocol-level security analysis and MCPBench / MCPSec discussion |
| SMCP: Secure Model Context Protocol | https://arxiv.org/abs/2602.01129 | Proposed secure MCP variant with identity, policy, and audit concepts |
| MCPShield: Security Cognition Layer for Adaptive Trust Calibration | https://arxiv.org/abs/2602.14281 | Runtime trust and tool validation research |
| Making REST APIs Agent-Ready: From OpenAPI to MCP Servers | https://arxiv.org/abs/2507.16044 | Useful for API-to-MCP governance and generated server review |
| Making OpenAPI Documentation Agent-Ready | https://arxiv.org/abs/2605.14312 | Useful for API documentation quality and tool-readiness governance |

### Suggested Existing-Reference Updates

| Existing reference | Suggested update |
|--------------------|------------------|
| NIST SP 800-61 Rev. 2 | Keep Rev. 2 only for historical compatibility; add Rev. 3 as the current primary IR reference |
| MCP Security Best Practices draft path | Prefer the docs tutorial URL for general readers: `https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices`; keep versioned spec paths when citing a specific protocol version |
| MCP individual OWASP links | Re-check before publishing; OWASP MCP Top 10 remains beta and individual URLs may change |
| MCP Specification (2025-11-25) | Keep as current/later version reference, but add 2025-06-18 because many ecosystem docs and implementations still refer to it |

# Framework Mapping Appendix

**Purpose:** Map MCP Governance & Risk Model controls to established security and AI governance frameworks. Use this appendix for compliance audits, gap assessments, and alignment with existing organizational programs.

**Related guide:** This mapping references controls defined in the [MCP Governance & Risk Framework](mcp-governance-risk-framework.md) ([MCP Governance Principles](mcp-governance-risk-framework.md#chapter-3-mcp-governance-principles) through [Metrics for CISOs](mcp-governance-risk-framework.md#chapter-15-metrics-for-cisos)).

---

## OWASP MCP Top 10

The OWASP MCP Top 10 identifies the most critical security risks for MCP deployments. This table maps each risk category to guide controls.

| OWASP MCP Risk | Guide Section | Control / Implementation |
|----------------|---------------|--------------------------|
| MCP01 — Token Mismanagement & Audience Confusion | [Ch. 2](mcp-governance-risk-framework-v1.0.md#chapter-2-why-mcp-needs-governance), [Appendix](mcp-governance-risk-framework-v1.0.md#authorization-test-cases) | For authenticated HTTP servers: enforce OAuth 2.1-compatible authorization with audience validation; reject token passthrough; verify during third-party review. For STDIO: enforce local hardening and credential handling |
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
