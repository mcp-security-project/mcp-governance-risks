# Chapter 10: Minimum Security Baseline

**Audience:** CISOs, security architects, policy authors, and AppSec teams  
**Decision supported:** Defining the minimum controls every MCP server must meet based on its risk tier  
**Reading time:** ~22 minutes

---

## Non-Negotiable Baselines

This chapter defines the **minimum security requirements** for each risk tier. These are floors, not ceilings:

- Organizations **may add** controls beyond the baseline
- Organizations **must not remove** required controls for a tier
- **Exceptions** require formal risk acceptance ([Exception Form](../templates/exception-risk-acceptance-form.md))

Use this matrix during security review (Stage 3) and deployment (Stage 5) of the [approval workflow](07-approval-workflow.md). During periodic review ([Chapter 13](13-continuous-monitoring.md)), verify each control is still in place.

---

## Controls by Risk Tier

| Control | Tier 0 | Tier 1 | Tier 2 | Tier 3 | Tier 4 |
|---------|:------:|:------:|:------:|:------:|:------:|
| Inventory | Required | Required | Required | Required | Required |
| Named owner | Required | Required | Required | Required | Required |
| Authentication | Optional | Required | Required | Required | Required |
| Scoped authorization | Optional | Recommended | Required | Required | Required |
| Audit logging | Basic | Basic | Required | Required | Required |
| Human approval (HITL) | Optional | Optional | Recommended | Required | Required |
| Threat model | Optional | Optional | Recommended | Required | Required |
| Vendor review | Optional | If external | Required if external | Required | Required |
| DLP | Optional | Optional | Required | Required | Required |
| Incident playbook | Optional | Optional | Recommended | Required | Required |
| CISO approval | No | No | Sometimes | Sometimes | **Required** |

**Legend:**

- **Required** — must be in place before production use
- **Recommended** — should be in place; mandatory for conditional approvals
- **Optional** — apply based on risk assessment
- **Sometimes** — required when risk score ≥ 28 or sensitive data at scale

---

## Control Definitions

### Inventory

Server recorded in MCP asset inventory with all required fields ([Chapter 4](04-asset-inventory.md)). No production use without inventory entry.

**Verify:** Cross-reference live connections against risk register.

---

### Named Owner

Specific person accountable for purpose, scope, and risk ([Chapter 3 — Principle 1](03-governance-principles.md), [Chapter 8](08-risk-ownership-raci.md)).

**Verify:** Owner field populated; owner confirms accountability annually.

---

### Authentication

| Tier | Requirement |
|------|-------------|
| 0 | Optional (no sensitive data) |
| 1+ | SSO or OAuth 2.1 required |
| 3–4 | MFA for privileged access; no shared credentials |

Per [MCP Authorization Specification](https://spec.modelcontextprotocol.io/specification/2025-03-26/basic/authorization/): audience validation mandatory for OAuth deployments.

**Verify:** Connection without valid credentials fails.

---

### Scoped Authorization

OAuth tokens or API keys scoped to minimum required permissions. Separate read and write scopes. Reject token passthrough architectures.

**Verify:** Attempt out-of-scope action; should fail and log denial.

---

### Audit Logging

| Level | Fields |
|-------|--------|
| **Basic** (Tier 0–1) | Server name, tool name, timestamp, outcome |
| **Required** (Tier 2+) | Above plus user/agent identity, sanitized parameters, authorization result, source IP |

Never log secrets, tokens, or raw PII in parameters.

**Verify:** Execute test tool call; confirm log entry in SIEM with all required fields.

---

### Human Approval (HITL)

Explicit user confirmation before high-risk tool invocations. Approval screen must be meaningful ([Chapter 3 — Principle 4](03-governance-principles.md)).

| Tier | HITL |
|------|------|
| 0–1 | Optional |
| 2 | Recommended for sensitive data patterns |
| 3–4 | Required for write, delete, deploy, admin actions |

**Verify:** Trigger write action; confirm prompt shows tool, action, target, identity, impact.

---

### Threat Model

Documented analysis of attack vectors, trust boundaries, and mitigations. STRIDE or similar applied to MCP tool chains.

| Tier | Requirement |
|------|-------------|
| 3–4 | Required before approval |
| 2 | Recommended for score ≥ 22 |

**Verify:** Threat model document exists, dated, and references specific tools and data flows.

---

### Vendor Review

Third-party review per [Chapter 9](09-third-party-review.md) for external and OSS servers.

**Verify:** Completed Vendor Questionnaire on file; token audience validation tested.

---

### DLP (Data Loss Prevention)

Detect and block sensitive data exfiltration through MCP tool parameters and responses. Required when server accesses confidential or regulated data.

**Verify:** Attempt to pass test PII/secret in tool parameter; DLP blocks or alerts.

---

### Incident Playbook

Documented response for MCP compromise ([Chapter 14](14-incident-response.md)). Tier 3–4 servers must have server-specific escalation contacts.

**Verify:** Playbook exists; owner and SecOps have reviewed it.

---

### CISO Approval

Formal sign-off by CISO or delegated security risk board.

| Tier | CISO |
|------|------|
| 4 | Required |
| 3 | Required if score ≥ 28 |
| 2 | Required if regulated data + external vendor |

**Verify:** Signed Approval Decision Form or risk acceptance on file.

---

## Sample Policy Language

Adopt or adapt for your AI usage policy, acceptable use policy, or secure development lifecycle.

### MCP Usage Policy

> **MCP Server Approval**
>
> All MCP servers connected to enterprise AI systems must be inventoried, classified, and approved before use. Connecting an unapproved MCP server to enterprise AI systems is prohibited.
>
> **Classification and Review**
>
> MCP servers that access sensitive data, perform write actions, execute code, access production systems, or interact with identity, security, or financial systems require formal security review and risk scoring.
>
> **Prohibited Practices**
>
> The following are prohibited:
> - Unapproved MCP servers ("shadow MCP")
> - MCP servers using hardcoded credentials or API keys in configuration
> - MCP servers with excessive permissions beyond documented business need
> - MCP servers without audit logging in production environments
> - Token passthrough that bypasses audience validation
>
> **Logging and Attribution**
>
> All MCP tool calls at Tier 2 and above must be logged and attributable to a user, agent, tool, identity, and action. Logs must be retained per organizational log retention policy.
>
> **Human Approval**
>
> MCP servers at Tier 3 and above must require explicit human approval before executing write, delete, deploy, or administrative actions. Approval prompts must describe the specific tool, action, target, and identity being used.
>
> **Periodic Review**
>
> Approved MCP servers must be reviewed at the cadence defined by their risk tier: annually (Tier 0–1), every 6 months (Tier 2), quarterly (Tier 3), or monthly (Tier 4).
>
> **Risk Acceptance**
>
> Exceptions to minimum security requirements require formal risk acceptance documented by the business risk owner and approved by the CISO for Tier 3–4 servers.

### MCP Connection Policy (for AI Platforms)

> Only MCP servers listed in the approved MCP inventory may be connected to enterprise AI platforms. Platform administrators must enforce allowlists and block connections to unlisted servers. New MCP server requests must be submitted through the MCP intake process before connection.

### Shadow MCP Policy (excerpt)

> Connecting unapproved MCP servers to enterprise AI systems, corporate devices, or networks accessing internal resources is prohibited. Violations may result in removal of MCP access and mandatory security review. See [Chapter 12](12-shadow-mcp-governance.md).

---

## Verifying Compliance

During periodic review, verify each control with evidence:

| Control | Verification method | Pass criteria |
|---------|---------------------|---------------|
| Inventory | Cross-reference live vs. register | Server listed, fields complete |
| Authentication | Test without credentials | Connection rejected |
| Scoped authorization | Review scopes; test OOS action | Denied and logged |
| Audit logging | Test tool call | Log entry with all required fields |
| HITL | Trigger write action | Meaningful prompt; deny works |
| DLP | Test sensitive data in parameter | Blocked or alerted |
| Threat model | Document review | Current, covers all tools |
| Vendor review | Questionnaire on file | Complete, not expired |
| CISO approval | Approval form | Signed for Tier 4 |

Document verification date and reviewer in risk register.

---

## Gap Remediation

When a server fails compliance verification:

| Gap severity | Action | Timeline |
|--------------|--------|----------|
| Critical (no auth, no logs on Tier 2+) | Suspend production use | Immediate |
| High (missing HITL on Tier 3) | Conditional status; remediate | 30 days |
| Medium (DLP not configured) | Track in risk register | 60 days |
| Low (documentation outdated) | Update at next review | Next review cycle |

Unresolved critical gaps → escalate to CISO. Repeated gaps → re-evaluate approval.

---

## References

| Source | Relevance |
|--------|-----------|
| [Chapter 5 — Classification](05-server-classification.md) | Tier drives baseline |
| [OWASP MCP Top 10](../appendix/framework-mapping.md) | Control mapping |
| [MCP Security Best Practices](https://modelcontextprotocol.io/specification/draft/basic/security_best_practices) | Technical requirements |

---

## Practitioner Checklist

- [ ] Tier × control matrix adopted as organizational baseline
- [ ] Policy language published in AI/MCP usage policy
- [ ] Platform allowlists enforce approved-only connections
- [ ] Compliance verification methods defined per control
- [ ] Gap remediation process defined with timelines
- [ ] CISO approval gate enforced for Tier 4
- [ ] Policy communicated to engineering and AI teams
- [ ] Annual policy review scheduled

---

**Next:** [Chapter 11 — High-Risk MCP Use Cases](11-high-risk-use-cases.md) covers Tier 3–4 scenarios with scenario-specific controls.
