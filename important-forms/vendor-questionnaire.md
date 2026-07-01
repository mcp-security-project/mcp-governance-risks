# Third-Party MCP Vendor Questionnaire

**Part of:** [MCP Governance & Risk Framework](../mcp-governance-risk-framework.md) — see [Chapter 9: Third-Party MCP Review](../mcp-governance-risk-framework.md#chapter-9-third-party-mcp-review) and [Chapter 16: Templates](../mcp-governance-risk-framework.md#chapter-16-templates).

**Instructions:** Complete this questionnaire for all external, open-source, and community MCP servers before approval. Procurement leads vendor trust review; AppSec leads security controls review.

**MCP Server Name:** _________________________  
**Vendor / Maintainer:** _________________________  
**Reviewer:** _________________________  
**Review Date:** _________________________

---

## Section 1: Vendor / Source Trust

| # | Question | Response | Pass/Fail/N/A |
|---|----------|----------|---------------|
| 1.1 | Who maintains this MCP server? | | |
| 1.2 | Is it open-source, commercial, internal, or community-built? | | |
| 1.3 | Is the repository active (commits within 90 days)? | | |
| 1.4 | Are releases signed (GPG, Sigstore, or equivalent)? | | |
| 1.5 | Are dependencies maintained (no critical CVEs)? | | |
| 1.6 | Is there a vulnerability disclosure process (SECURITY.md)? | | |
| 1.7 | Is an SBOM (Software Bill of Materials) available? | | |
| 1.8 | What license applies? Is it compatible with enterprise use? | | |

**Section 1 outcome:** [ ] Pass  [ ] Pass with conditions  [ ] Fail

**Conditions (if applicable):**

---

## Section 2: Security Controls

| # | Question | Response | Pass/Fail/N/A |
|---|----------|----------|---------------|
| 2.1 | Does it support authentication? (OAuth 2.1 preferred) | | |
| 2.2 | Does it support scoped authorization? | | |
| 2.3 | Does it avoid token passthrough? | | |
| 2.4 | Does it validate token audience per MCP authorization spec? | | |
| 2.5 | Does it store secrets securely (no hardcoded credentials)? | | |
| 2.6 | Does it expose audit logs for tool calls? | | |
| 2.7 | Does it restrict network egress? | | |
| 2.8 | Does it avoid unsafe shell execution? | | |

**Section 2 outcome:** [ ] Pass  [ ] Pass with conditions  [ ] Fail

**Conditions (if applicable):**

---

## Section 3: Data Handling

| # | Question | Response | Pass/Fail/N/A |
|---|----------|----------|---------------|
| 3.1 | What data does it access? | | |
| 3.2 | Where is data processed? (region, infrastructure) | | |
| 3.3 | Is data sent to a third party? | | |
| 3.4 | Is data retained? For how long? | | |
| 3.5 | Is data used for model training? | | |
| 3.6 | Is customer data involved? | | |
| 3.7 | Is regulated data involved (GDPR, HIPAA, PCI)? | | |
| 3.8 | Is a Data Processing Agreement (DPA) in place? | | |

**Section 3 outcome:** [ ] Pass  [ ] Pass with conditions  [ ] Fail

**Conditions (if applicable):**

---

## Section 4: Operational Risk

| # | Question | Response | Pass/Fail/N/A |
|---|----------|----------|---------------|
| 4.1 | Can it write, delete, deploy, or send? | | |
| 4.2 | Can actions be reversed? | | |
| 4.3 | Are rate limits available? | | |
| 4.4 | Is there health monitoring? | | |
| 4.5 | Is there an incident response / security contact? | | |
| 4.6 | What happens if the MCP server is unavailable? | | |
| 4.7 | What is the vendor's SLA (if commercial)? | | |

**Section 4 outcome:** [ ] Pass  [ ] Pass with conditions  [ ] Fail

**Conditions (if applicable):**

---

## Overall Review Outcome

| Field | Value |
|-------|-------|
| **Overall outcome** | [ ] Pass  [ ] Pass with conditions  [ ] Fail  [ ] Insufficient information |
| **Reviewer (Procurement)** | |
| **Reviewer (AppSec)** | |
| **Date** | |

### Summary of Findings

---

### Required Remediation (if conditional)

| # | Item | Owner | Deadline |
|---|------|-------|----------|
| 1 | | | |
| 2 | | | |
| 3 | | | |
