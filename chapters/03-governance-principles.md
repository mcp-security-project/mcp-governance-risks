# Chapter 3: MCP Governance Principles

**Audience:** Security architects, AppSec leaders, AI governance teams, and policy authors  
**Decision supported:** Establishing non-negotiable rules that govern every MCP approval decision  
**Reading time:** ~18 minutes

---

## Why Principles Matter

Chapters 1 and 2 explained *why* MCP needs governance. This chapter defines the *rules* that make governance work in practice. Every MCP governance program needs a small set of durable principles — not dozens of policies nobody reads, but five clear rules that apply regardless of risk tier, vendor, or deployment model.

These principles should be:

- **Embedded in policy** — referenced in your AI usage policy, acceptable use policy, and secure development lifecycle
- **Cited in approval decisions** — "Rejected per Principle 1: no named owner"
- **Used to resolve ambiguity** — when edge cases arise, principles provide the tiebreaker

If a proposed MCP deployment violates a principle, it must either be redesigned to comply or go through formal exception and risk acceptance ([Chapter 7](07-approval-workflow.md), [Exception Form](../templates/exception-risk-acceptance-form.md)).

---

## The Five Principles at a Glance

| # | Principle | One-line rule |
|---|-----------|---------------|
| 1 | No MCP Without Ownership | No owner = no approval |
| 2 | Classify Before You Connect | Know the risk tier before connecting |
| 3 | Least Privilege for Tools | Minimum permissions per tool, not per server name |
| 4 | Human Approval Must Be Meaningful | HITL must show what, where, who, and impact |
| 5 | Auditability Is Non-Negotiable | No logging = no production use |

The four governance rules from [Chapter 1](01-executive-summary.md) (no owner, no logging, no scope, no review) are operational expressions of these principles.

---

## Principle 1: No MCP Without Ownership

### The rule

Every MCP server must have a **named owner** — a specific person accountable for the server's purpose, scope, and risk. Not a team. Not a mailing list. A person.

| Condition | Rule | What it means in practice |
|-----------|------|---------------------------|
| No owner | No approval | Intake forms without a named owner are returned immediately |
| No logging | No production use | Servers without audit trails cannot operate in production |
| No scope definition | No access | Data and action scope must be documented before connection |
| No review | No enterprise deployment | Periodic review cadence is mandatory by risk tier |

### Why ownership is non-negotiable

When an MCP incident occurs at 2 a.m., the first question is: *Who owns this server?* If the answer is "the platform team" or "I'm not sure," containment slows down, accountability is unclear, and residual risk was never formally accepted.

The owner is typically a business or technical lead who:

- Understands the use case and can explain why the server exists
- Can accept residual risk for their domain (Tier 0–2) or escalate to CISO (Tier 3–4)
- Ensures security reviews happen and controls are maintained over time
- Reports changes — new tools, version upgrades, scope expansion

**Ownership does not mean the owner performs security reviews.** It means they are accountable for ensuring reviews happen, conditions are met, and the server is decommissioned when no longer needed.

### How to implement

1. **Intake gate:** The [Intake Form](../templates/intake-form.md) requires an owner field. Approval cannot proceed without it.
2. **Risk register:** Every approved server records business owner and technical owner in the [Risk Register](../templates/risk-register.md).
3. **Periodic review:** Owners participate in tier-based review ([Chapter 13](13-continuous-monitoring.md)).
4. **Offboarding:** When an owner leaves the organization, ownership must be reassigned within 30 days or the server is suspended.

**Guide reference:** [Chapter 8 — Risk Ownership and RACI](08-risk-ownership-raci.md)

---

## Principle 2: Classify Before You Connect

### The rule

Do not approve MCP servers generically. Classify them based on what they actually do — data accessed, actions permitted, identity used, exposure, vendor trust, business criticality, and blast radius — **before** they connect to enterprise AI systems.

### Why names are misleading

A server named "Slack MCP" could be:

- Read-only channel search (Tier 1) — low risk
- Posting to company-wide channels (Tier 3) — high risk
- Admin-level workspace configuration (Tier 4) — critical risk

The name tells you nothing. Classification must evaluate:

| Dimension | What to assess | Example |
|-----------|----------------|---------|
| **Data access** | Public, internal, confidential, regulated | CRM MCP → customer PII → Tier 2+ |
| **Action capability** | Read-only, write, delete, execute, deploy | PR merge → Tier 3 |
| **Identity scope** | Anonymous, standard user, privileged service account | Cloud admin SA → Tier 4 |
| **Deployment location** | Local laptop, internal network, internet-facing | Developer laptop + prod creds → higher exposure |
| **Vendor/source trust** | Internal, reviewed OSS, commercial, unknown | Unknown GitHub repo → reject or heavy review |
| **Business criticality** | Nice-to-have vs. production workflow dependency | CI/CD trigger → high criticality |
| **Blast radius** | Single user vs. enterprise-wide impact | IAM MCP → enterprise blast radius |

### How to implement

1. **Before connection:** Complete classification as Stage 2 of the [approval workflow](07-approval-workflow.md).
2. **Use highest-risk tool:** If a server has one read tool and one admin tool, classify as Tier 4 ([Chapter 5](05-server-classification.md)).
3. **Re-classify on change:** Adding a write tool to a Tier 1 server triggers re-classification — not optional.
4. **Document rationale:** Record why a tier was assigned in the [Approval Decision Form](../templates/approval-decision-form.md).

**Guide reference:** [Chapter 5 — Classification](05-server-classification.md), [Chapter 6 — Risk Scoring](06-risk-scoring.md)

---

## Principle 3: Least Privilege for Tools

### The rule

MCP tools should receive the **minimum permissions** required for the business use case. Evaluate each tool individually, not the server as a monolith.

### Why this matters

Organizations routinely over-provision MCP access because it is faster. "Give the GitHub MCP admin scope so we don't have permission issues later" is a common pattern — and a common source of Tier 4 risk where Tier 1 would suffice.

| Comparison | Risk difference | Governance action |
|------------|-----------------|-------------------|
| Calendar-read MCP vs. calendar-write MCP | Read is Tier 1; write is Tier 3 | Separate servers or disable write tools |
| GitHub read MCP vs. GitHub admin MCP | Read is Tier 1–2; admin is Tier 4 | Never combine in one server if avoidable |
| Local file search MCP vs. shell execution MCP | Search is Tier 1–2; shell is Tier 3–4 | Prohibit shell unless formally justified |
| Jira read MCP vs. Jira ticket update MCP | Read is Tier 1–2; write is Tier 3 | HITL for ticket updates |

### Implementation guidance

1. **Separate read and write** into distinct MCP servers where possible — easier to approve, monitor, and revoke.
2. **Scope OAuth tokens** to minimum required permissions; avoid org-wide admin scopes.
3. **Disable or remove tools** not needed for the approved use case — do not leave dormant write tools "just in case."
4. **Re-evaluate on tool addition** — new tools require re-classification per [OWASP MCP05: Tool Permission Smuggling](https://owasp.org/www-project-mcp-top-10/).
5. **Prefer predefined action templates** over open-ended admin access for Tier 4 scenarios ([Chapter 11](11-high-risk-use-cases.md)).

### Red flags during review

- Personal access tokens instead of scoped OAuth apps
- Wildcard permissions (`*`, `admin`, `cluster-admin`)
- Filesystem MCP with write access to home directory or `/`
- Shell/command execution without sandboxing
- "Temporary" elevated permissions with no expiration date

---

## Principle 4: Human Approval Must Be Meaningful

### The rule

Human-in-the-loop (HITL) approval is a control for high-risk actions — but only if the approval screen gives the user enough information to make an informed decision. A meaningless approval prompt is worse than no prompt: it creates false confidence.

### Bad vs. good approval

**Bad approval screen:**

> "Allow assistant to continue?"

The user has no idea what will happen. They click "Allow" to continue their work. This is security theater.

**Good approval screen:**

> "Allow MCP server `github-admin` to create a new branch protection rule in repository `payments-api` using your corporate GitHub identity?"

The user can make an informed decision because they see the server, tool, action, target, and identity.

### Meaningful approval must show

| Element | What to display | Example |
|---------|-----------------|---------|
| **What tool** | Tool name and MCP server | `create_pull_request` on `github-repo-management` |
| **What data** | Parameters and target resources | `repo=payments-api`, `branch=feature-x` |
| **What action** | Create, delete, deploy, send | "Merge pull request #142" |
| **What identity** | User OAuth, service account | "Using your corporate GitHub identity" |
| **What impact** | Affected systems, reversibility | "This will merge code to the production branch. Revert is possible but requires manual intervention." |

### HITL requirements by tier

| Tier | HITL requirement |
|------|------------------|
| 0–1 | Optional |
| 2 | Recommended for sensitive data access patterns |
| 3 | Required for write, delete, deploy, send actions |
| 4 | Required for every privileged action; consider dual approval |

**Guide reference:** [Chapter 10 — Minimum Security Baseline](10-minimum-security-baseline.md), [Chapter 11 — High-Risk Use Cases](11-high-risk-use-cases.md)

### Testing HITL

During security review, trigger a write action and verify:

- Approval prompt appears before execution
- Prompt contains all five elements above
- Denying the prompt blocks the action
- Approval/denial is logged with user attribution

---

## Principle 5: Auditability Is Non-Negotiable

### The rule

Servers without audit logging cannot be used in production. Period.

The [OWASP MCP Top 10](https://owasp.org/www-project-mcp-top-10/) identifies **lack of audit and telemetry (MCP03)** as a major risk. Without logging, organizations lose visibility into what agents did, what data they accessed, what actions they performed, which identity was used, and whether authorization succeeded or failed.

### Minimum audit fields for every tool call

| Field | Required | Example |
|-------|----------|---------|
| Timestamp | Yes | `2026-06-29T14:32:01Z` |
| User / agent identity | Yes | `jane.smith@company.com` / `agent-session-abc123` |
| MCP server name | Yes | `github-repo-management` |
| Tool name | Yes | `create_pull_request` |
| Parameters (sanitized) | Yes | `repo=payments-api`, `branch=feature-x` |
| Outcome | Yes | `success` / `denied` / `error` |
| Authorization result | Tier 2+ | `HITL-approved` / `denied` |
| Source IP / client | Recommended | `10.0.1.45` |
| Data classification touched | Tier 2+ | `confidential` |

**Sanitization rule:** Never log secret values, tokens, passwords, or raw PII in parameter fields. Redact or hash sensitive values.

### What good logging enables

- **Incident response** — reconstruct what happened during a compromise
- **Compliance audits** — demonstrate who accessed regulated data and when
- **Abuse detection** — identify runaway agents, prompt injection attempts, or credential abuse
- **Periodic review** — verify servers operate within approved scope

### How to implement

1. **Deployment gate:** Logging must be active before first production use ([Chapter 7](07-approval-workflow.md), Stage 5).
2. **SIEM integration:** Forward logs to centralized platform ([Chapter 13](13-continuous-monitoring.md)).
3. **Compliance verification:** Execute test tool call during periodic review; verify log entry appears with all required fields.
4. **Reject servers that cannot log:** If a third-party MCP server cannot produce audit trails, reject or limit to non-production pilot with compensating controls.

---

## Applying Principles to Edge Cases

| Scenario | Principle | Resolution |
|----------|-----------|------------|
| Developer wants to test OSS MCP locally | 2 — Classify | Allow local Tier 0–1 testing without production data; prohibit production credentials |
| Urgent production need, no time for review | 1 — Ownership | Exception process with CISO awareness; time-bound risk acceptance |
| Vendor MCP has no logging API | 5 — Auditability | Reject for Tier 2+; or wrap with proxy that logs tool calls |
| Team adds new tool to approved server | 2 — Classify | Re-classify; may require re-approval |
| User complains HITL prompts are annoying | 4 — Meaningful HITL | Reduce scope so fewer actions require approval; do not weaken prompt content |
| Business owner on extended leave | 1 — Ownership | Reassign owner within 30 days or suspend server |

---

## Glossary

| Term | Definition |
|------|------------|
| **MCP server** | A service that exposes tools and/or resources to AI agents via the Model Context Protocol |
| **Tool** | An action an agent can invoke through an MCP server (e.g., `create_ticket`, `search_files`) |
| **Resource** | Data an agent can read through an MCP server (e.g., a document, configuration file) |
| **Shadow MCP** | An MCP server connected without formal inventory, classification, or approval |
| **HITL** | Human-in-the-loop — requiring explicit user approval before high-risk actions |
| **Token passthrough** | Forwarding a client token to downstream APIs without independent validation |
| **Confused deputy** | A server performing actions with a token not intended for that service |
| **Blast radius** | The scope of impact if an MCP server is compromised or misused |

---

## References

| Source | Relevance |
|--------|-----------|
| [MCP Authorization Specification](https://spec.modelcontextprotocol.io/specification/2025-03-26/basic/authorization/) | OAuth 2.1, audience validation — supports Principles 3 and 5 |
| [OWASP MCP Top 10](https://owasp.org/www-project-mcp-top-10/) | MCP03 (audit), MCP05 (tool smuggling) — supports Principles 3 and 5 |
| [OWASP LLM08: Excessive Agency](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | Supports Principle 4 (meaningful HITL) |
| [Chapter 2 — Why MCP Needs Governance](02-why-mcp-needs-governance.md) | Threat landscape justification for these principles |

---

## Practitioner Checklist

**Policy adoption**

- [ ] Five principles adopted in organizational MCP / AI usage policy
- [ ] Four governance rules (no owner, no logging, no scope, no review) published alongside principles
- [ ] Principles communicated to engineering and AI platform teams

**Operational enforcement**

- [ ] Ownership requirement enforced in intake process — incomplete forms returned
- [ ] Classification performed before any new MCP connection
- [ ] Least-privilege review conducted per tool, not per server name
- [ ] HITL approval screens reviewed and tested for meaningful content
- [ ] Audit logging mandated and verified for all production MCP servers at Tier 2+

**Edge case readiness**

- [ ] Exception process defined when principles cannot be fully met
- [ ] Re-classification process defined for tool additions and scope changes
- [ ] Owner reassignment process defined for role changes and departures

---

**Next:** [Chapter 4 — MCP Asset Inventory](04-asset-inventory.md) explains how to discover, catalog, and maintain an inventory of all MCP servers — the foundation everything else depends on.
