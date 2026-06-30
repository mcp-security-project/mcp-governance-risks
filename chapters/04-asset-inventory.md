# Chapter 4: MCP Asset Inventory

**Audience:** Security architects, AppSec, platform engineering, and AI governance teams  
**Decision supported:** Knowing which MCP servers exist in your environment — approved and unapproved  
**Reading time:** ~18 minutes

---

## Why Inventory Comes First

You cannot classify, score, approve, or monitor what you cannot see. MCP asset inventory is the foundation of the entire governance model described in this guide. Without it:

- Shadow MCP servers proliferate undetected
- Duplicate integrations go unnoticed (three teams each running their own GitHub MCP)
- Incident response has no starting point ("What MCP servers did this user have connected?")
- Monthly metrics are meaningless ([Chapter 15](15-ciso-metrics.md))
- Auditors ask a simple question — "List all MCP integrations" — and nobody can answer

The inventory answers one essential question:

> **Which MCP servers are connected to our AI systems, who owns them, and what is their approval status?**

[Chapter 1](01-executive-summary.md) lists standing up an inventory as the first recommended step. This chapter explains how to do it — thoroughly, practically, and in a way that scales from a spreadsheet to a CMDB integration.

---

## What to Inventory

Every MCP server — regardless of source, tier, or deployment model — must be recorded with consistent metadata. These fields align with the [Intake Form](../templates/intake-form.md) and feed directly into the [Risk Register](../templates/risk-register.md).

### Required fields

| Field | Description | Example | Why it matters |
|-------|-------------|---------|----------------|
| MCP server name | Unique identifier | `github-repo-management` | Distinct from display name; used in logs and allowlists |
| Display name | Human-readable name | GitHub Repo Management MCP | For reports and dashboards |
| Use case | Business purpose | Enable agents to create PRs for engineering teams | Justifies existence; drives classification |
| Owner | Named accountable person | jane.smith@company.com | Principle 1 — no owner, no approval |
| Requesting team | Team that requested access | Platform Engineering | Escalation and communication |
| Source / vendor | Internal, OSS, commercial, community | Internal fork of `@modelcontextprotocol/server-github` | Determines vendor review depth |
| Deployment location | Where the server runs | Internal K8s cluster, developer laptop, vendor SaaS | Affects exposure scoring |
| Authentication model | How the server authenticates | OAuth 2.1 with corporate GitHub App | Baseline compliance check |
| Data accessed | Classification of data touched | Internal source code (confidential) | Drives tier assignment |
| Tools / actions exposed | Tool names and capabilities | `search_repos` (read), `create_pr` (write) | Classify by highest-risk tool |
| Expected users | Who will use this server | Engineering (200 users) | Blast radius assessment |
| Approval status | Approved / conditional / rejected / unapproved | Conditionally approved | Governance state |
| Risk tier | Tier 0–4 | Tier 3 | Drives controls and review cadence |
| Version | Pinned version or commit | v1.2.0 | Supply chain tracking |
| Last review date | Most recent security review | 2026-06-15 | Compliance tracking |
| Next review date | Scheduled next review | 2026-09-15 | Prevents review decay |

### Optional but valuable fields

- Agent platforms using this server (Cursor, Claude Desktop, internal agent platform)
- Connected MCP servers in same agent config (tool chaining risk)
- Data processing location (region, cloud provider)
- Incident history (linked IR tickets)
- Conditional approval items and deadlines

---

## Discovery Methods

MCP servers appear in environments through multiple channels. No single discovery method finds everything. Use all applicable methods and reconcile results into one inventory.

### Method 1: Configuration scanning

**What it finds:** MCP entries in config files on endpoints and in repositories.

**Where to look:**

| Location | Config pattern |
|----------|----------------|
| Cursor | `.cursor/mcp.json` or user settings |
| Claude Desktop | `claude_desktop_config.json` |
| VS Code / IDE extensions | Extension settings, workspace configs |
| Custom agent platforms | Platform-specific MCP registry |
| CI/CD pipelines | Pipeline YAML referencing MCP servers |
| Container images | Dockerfile, Helm charts, docker-compose |
| Infrastructure-as-code | Terraform, Pulumi manifests deploying MCP servers |

**How to run:**

1. Deploy configuration scanning via endpoint management (MDM, EDR config inspection) or repository scanning (GitHub Advanced Security, GitLab secret/detection scans adapted for MCP patterns).
2. Search for common MCP indicators: `"mcpServers"`, `modelcontextprotocol`, MCP transport URLs, known MCP package names.
3. Deduplicate findings — the same server may appear on many developer laptops.
4. Compare against inventory; unmatched entries are candidate shadow MCP.

**Limitations:** Does not find SaaS-hosted MCP with no local config. May miss personal machines not under MDM.

---

### Method 2: Network and endpoint monitoring

**What it finds:** Live MCP traffic and processes not visible in static configs.

**Techniques:**

| Technique | What it detects |
|-----------|-----------------|
| Outbound connection monitoring | Agent hosts connecting to MCP server endpoints |
| Process monitoring | New processes listening on MCP transport ports (stdio, SSE, HTTP) |
| API gateway logs | MCP protocol traffic patterns through corporate proxies |
| DNS logs | Lookups for known MCP hosting domains |
| Cloud network flow logs | MCP servers in VPCs talking to internal APIs |

**How to run:**

1. Baseline normal agent traffic for 2–4 weeks before alerting.
2. Alert on connections to unknown MCP endpoints.
3. Correlate with inventory — approved servers should match; others trigger shadow MCP workflow ([Chapter 12](12-shadow-mcp-governance.md)).

**Limitations:** Encrypted traffic may hide payload details. Requires tuning to reduce false positives.

---

### Method 3: Developer surveys and self-reporting

**What it finds:** Servers developers know about but scanners miss — especially new or personal setups.

**How to run:**

1. Publish the [Intake Form](../templates/intake-form.md) with a clear, low-friction submission path.
2. Include MCP usage attestation in developer onboarding: "List all MCP servers you use."
3. Run periodic campaigns (quarterly): "Self-report MCP usage by [date] — amnesty for shadow MCP submitted voluntarily."
4. Link from internal developer documentation and AI platform admin consoles.

**Limitations:** Relies on honesty and awareness. Use alongside automated methods, not instead of them.

---

### Method 4: Platform integration

**What it finds:** Everything connected through a centralized AI platform — the most controllable surface.

**How to run:**

1. Require MCP server registration before connection on enterprise AI platforms.
2. Enforce allowlists — only inventoried and approved servers can connect.
3. Integrate inventory with CMDB or software asset management (SAM) tools.
4. Log all connection events (user, server, timestamp) to SIEM.

**Why this is the strongest control:** Prevention beats detection. If the platform blocks unlisted servers, shadow MCP cannot connect — though local-only configs on unmanaged devices may still exist.

**Guide reference:** [Chapter 12 — Shadow MCP Governance](12-shadow-mcp-governance.md)

---

## Approved vs. Shadow MCP

Every discovered MCP server must have a status. Status drives action.

| Status | Definition | Action required |
|--------|------------|-----------------|
| **Approved** | Inventoried, classified, reviewed, formally approved | Monitor per tier cadence |
| **Conditionally approved** | Approved with documented conditions and remediation timeline | Track conditions; escalate if overdue |
| **Pending** | Submitted via intake; review not complete | Block production use until approved |
| **Shadow** | Discovered without inventory entry or approval | Remediate per [Chapter 12](12-shadow-mcp-governance.md) |
| **Rejected** | Formally rejected; must not be connected | Block and monitor for reconnection |
| **Decommissioned** | Retired; credentials revoked | Archive record; remove from allowlists |

### Shadow MCP priority

Shadow MCP is one of the highest-priority governance gaps ([Chapter 2](02-why-mcp-needs-governance.md)). Prioritize remediation by risk:

| Shadow MCP profile | Priority | Immediate action |
|--------------------|----------|------------------|
| Write access + production data + hardcoded secrets | Critical | Disconnect immediately; investigate |
| Write access + internal data | High | Disconnect or restrict; fast-track intake |
| Read-only + sensitive data | Medium | Fast-track intake; enhanced monitoring during review |
| Read-only + public/non-sensitive data | Low | Fast-track intake; may remain connected during review |

Monthly metrics should track the ratio of approved to shadow servers. Target: shadow trending toward zero ([Chapter 15](15-ciso-metrics.md)).

---

## Inventory Maintenance

Inventory is not a one-time exercise. It decays without active maintenance.

### Six maintenance activities

**1. Intake on creation**

Every new MCP server request starts with the [Intake Form](../templates/intake-form.md). No exceptions. Make the intake path faster than shadow installation — if formal approval takes 6 weeks and `npm install` takes 6 minutes, shadow MCP wins.

**2. Change notification**

Owners must report within 5 business days:

- New tools added to an existing server
- Version upgrades (especially major versions)
- Scope changes (new data sources, new user groups)
- Authentication model changes
- Deployment location changes

Changes trigger re-classification ([Chapter 5](05-server-classification.md)) and may require re-approval.

**3. Automated discovery**

Run configuration and network scans on a defined cadence:

| Cadence | Activity |
|---------|----------|
| Weekly | Repository and CI/CD config scans |
| Monthly | Endpoint configuration scans |
| Quarterly | Full reconciliation — inventory vs. live environment |

**4. Periodic review**

Reconcile inventory against live environment per tier cadence ([Chapter 13](13-continuous-monitoring.md)):

| Tier | Review frequency |
|------|------------------|
| 0–1 | Annually |
| 2 | Every 6 months |
| 3 | Quarterly |
| 4 | Monthly |

**5. Decommissioning**

When a server is retired:

1. Remove from AI platform allowlists
2. Revoke credentials (OAuth tokens, API keys, service accounts)
3. Update risk register status to "decommissioned"
4. Archive approval records per retention policy
5. Verify no active connections via discovery scan

**6. Owner validation**

Quarterly: verify every server still has a valid, reachable owner. Orphaned servers are suspended until ownership is reassigned.

---

## Intake Process (Stage 1)

The governance lifecycle begins with intake. This is Stage 1 of the [approval workflow](07-approval-workflow.md).

### Step-by-step intake flow

```
Requester identifies MCP need
        ↓
Complete Intake Form (all required fields)
        ↓
Gate: Named owner? → No → Return to requester
        ↓ Yes
Submit to AppSec / governance queue
        ↓
AppSec acknowledges receipt (SLA: 2 business days)
        ↓
Proceed to Classification (Chapter 5)
```

### Minimum intake capture

- MCP server name and use case
- Owner and requesting team
- Data accessed and tools/actions exposed
- Deployment location and source/vendor
- Authentication model and expected users

Full fields are in the [Intake Form](../templates/intake-form.md). Completed intake feeds classification ([Chapter 5](05-server-classification.md)) and risk scoring ([Chapter 6](06-risk-scoring.md)).

### Intake SLAs (recommended)

| Stage | Target SLA |
|-------|------------|
| Intake acknowledgment | 2 business days |
| Tier 0–1 approval | 5 business days |
| Tier 2 approval | 10 business days |
| Tier 3 approval | 15 business days |
| Tier 4 approval | 20 business days (includes threat model) |

Fast, predictable SLAs reduce shadow MCP incentive.

---

## Starting from Zero: First 30 Days

If you have no inventory today, follow this sequence:

| Week | Activity | Outcome |
|------|----------|---------|
| 1 | Stand up spreadsheet or risk register; publish intake form | Inventory container exists |
| 1 | Survey engineering and AI teams | Initial server list (incomplete is OK) |
| 2 | Run first config scan on repos and sample endpoints | Shadow MCP candidates identified |
| 2 | Classify all known servers (rough tier) | Tier column populated |
| 3 | Prioritize shadow MCP remediation | High-risk shadow disconnected or fast-tracked |
| 4 | Publish inventory to security leadership | Baseline metrics captured |

---

## References

| Source | Relevance |
|--------|-----------|
| [OWASP MCP09: Shadow MCP Deployments](https://owasp.org/www-project-mcp-top-10/) | Inventory and discovery as primary control |
| [Chapter 3 — Governance Principles](03-governance-principles.md) | Principle 1 (ownership) enforced at intake |
| [Chapter 12 — Shadow MCP Governance](12-shadow-mcp-governance.md) | Remediation when discovery finds unapproved servers |
| [Intake Form](../templates/intake-form.md) | Standardized capture |
| [Risk Register](../templates/risk-register.md) | Ongoing inventory record |

---

## Practitioner Checklist

**Inventory foundation**

- [ ] MCP inventory exists (spreadsheet, GRC tool, or CMDB entry)
- [ ] Required fields defined and enforced via intake form
- [ ] Risk register established as single source of truth
- [ ] Decommissioning process documented

**Discovery**

- [ ] At least one automated discovery method active (config scan, network monitor, or platform allowlist)
- [ ] Discovery cadence defined (weekly/monthly/quarterly)
- [ ] Shadow MCP detection process defined with priority matrix
- [ ] Reconciliation process: inventory vs. live environment

**Operations**

- [ ] Inventory review cadence assigned to responsible team (AppSec or governance PM)
- [ ] Change notification process communicated to MCP owners
- [ ] Intake SLAs published to engineering teams
- [ ] Owner validation process defined (quarterly)

---

**Next:** [Chapter 5 — MCP Server Classification Model](05-server-classification.md) explains how to assign Tier 0–4 based on data access and action capability — the decision that drives everything downstream.
