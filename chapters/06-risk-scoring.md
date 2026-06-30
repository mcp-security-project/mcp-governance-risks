# Chapter 6: MCP Risk Scoring Model

**Audience:** Security architects, risk analysts, and approval authorities  
**Decision supported:** Quantifying MCP risk to inform approve / conditionally approve / reject decisions  
**Reading time:** ~20 minutes

---

## Why Score When You Already Have Tiers?

Classification (Tier 0–4) provides a categorical risk label. It answers: *What class of controls and approval authority applies?*

Risk scoring adds a **quantitative dimension** that helps you:

- **Compare servers within the same tier** — two Tier 3 servers are not equally risky
- **Prioritize remediation** — which conditional approvals to fix first
- **Document risk acceptance** — defensible numbers for audit and board reporting
- **Detect misclassification** — a Tier 1 label with a score of 30 warrants investigation

Scoring complements but does not replace tier classification. Use both together during security review (Stage 3 of the [approval workflow](07-approval-workflow.md)).

**Typical alignment:**

| Tier | Typical score range |
|------|---------------------|
| 0 | 8–12 |
| 1 | 12–18 |
| 2 | 18–26 |
| 3 | 22–32 |
| 4 | 30–40 |

Discrepancies between tier and score should be investigated — they may indicate misclassification or missing context.

---

## The Eight Risk Factors

Use a simple **1–5 score** for each factor. Total scores range from 8 (minimum) to 40 (maximum).

| Risk Factor | 1 = Low | 3 = Medium | 5 = Critical |
|-------------|---------|------------|--------------|
| **Data Sensitivity** | Public | Internal confidential | Regulated / customer PII / secrets |
| **Action Capability** | Read-only | Write / modify | Delete / deploy / admin |
| **Identity Scope** | Anonymous / public | Standard corporate user | Privileged user / broad service account |
| **Exposure** | Local only | Internal network | Internet-facing / third-party hosted |
| **Vendor Trust** | Internal, reviewed | Known OSS / established vendor | Unknown / unverified |
| **Auditability** | Full logs with attribution | Partial logs | No logs |
| **Reversibility** | Easy rollback | Partial rollback | Irreversible action |
| **Blast Radius** | Single user | Team / department | Enterprise / production-wide |

### How to score each factor

**Data Sensitivity** — What is the most sensitive data any tool can touch?

| Score | Criteria |
|-------|----------|
| 1 | Public data only |
| 2 | Internal non-sensitive (engineering docs) |
| 3 | Internal confidential (source code, business strategy) |
| 4 | Customer PII, employee data |
| 5 | Regulated data (HIPAA, PCI, GDPR special category), secrets, credentials |

**Action Capability** — What is the most dangerous action any tool can perform?

| Score | Criteria |
|-------|----------|
| 1 | Read public data |
| 2 | Read internal data |
| 3 | Create or modify non-production resources |
| 4 | Write to production, send communications, trigger deployments |
| 5 | Delete, admin, IAM changes, financial transactions |

**Identity Scope** — What identity does the MCP server operate under?

| Score | Criteria |
|-------|----------|
| 1 | No auth / anonymous |
| 2 | Per-user OAuth with minimal scope |
| 3 | Per-user OAuth with broad scope |
| 4 | Shared service account with write access |
| 5 | Privileged service account, admin credentials, standing root access |

**Exposure** — Where does the MCP server run and who can reach it?

| Score | Criteria |
|-------|----------|
| 1 | Local developer machine, offline |
| 2 | Internal network, VPN required |
| 3 | Internal network, broadly accessible |
| 4 | Internet-facing with authentication |
| 5 | Third-party SaaS, internet-facing, multi-tenant |

**Vendor Trust** — How well do you trust the MCP server source?

| Score | Criteria |
|-------|----------|
| 1 | Built internally, full code review |
| 2 | Internal fork of known OSS, maintained |
| 3 | Established OSS or commercial vendor, partially reviewed |
| 4 | Community OSS, limited review |
| 5 | Unknown source, no review, anonymous maintainer |

**Auditability** — Can you see what the server did?

| Score | Criteria |
|-------|----------|
| 1 | Full MCP-level logs with user/agent/tool/action, SIEM integrated |
| 2 | Full MCP-level logs, not yet in SIEM |
| 3 | Partial logs (tool name only, no user attribution) |
| 4 | Downstream system logs only (e.g., GitHub audit log, no MCP layer) |
| 5 | No logs |

**Reversibility** — Can you undo the damage if something goes wrong?

| Score | Criteria |
|-------|----------|
| 1 | Read-only; no state change |
| 2 | Write with trivial rollback (draft, unshared doc) |
| 3 | Reversible with effort (revert PR, restore file) |
| 4 | Difficult rollback (sent email, posted to Slack) |
| 5 | Irreversible (deleted data, financial transaction, IAM change) |

**Blast Radius** — If compromised, how wide is the impact?

| Score | Criteria |
|-------|----------|
| 1 | Single user, single resource |
| 2 | Single team |
| 3 | Department or business unit |
| 4 | Multiple systems, production-adjacent |
| 5 | Enterprise-wide, all customers, production core |

---

## Risk Rating Bands

| Total Score | Risk Rating | Typical Decision |
|-------------|-------------|------------------|
| 8–15 | **Low** | Approve with standard controls |
| 16–25 | **Medium** | Approve with tier-appropriate controls |
| 26–32 | **High** | Conditional approval with enhanced controls |
| 33–40 | **Critical** | CISO approval required; formal risk acceptance |

### What each band means for approvers

**Low (8–15):** Standard path. Verify tier-appropriate controls from [Chapter 10](10-minimum-security-baseline.md). Annual review.

**Medium (16–25):** Normal approval workflow. Ensure all tier controls are in place. No shortcuts on authentication or logging.

**High (26–32):** Conditional approval is likely. Identify specific gaps — logging, scope, HITL, vendor review — and set remediation deadlines. Enhanced monitoring. Quarterly review minimum.

**Critical (33–40):** CISO or risk board approval mandatory. Formal threat model and risk acceptance document required. Ask whether the use case justifies the risk. Monthly or continuous review.

---

## Scoring Worksheet

Use this worksheet during security review. Record scores in the [Approval Decision Form](../templates/approval-decision-form.md).

```
MCP Server Name: _________________________
Reviewer: _________________________  Date: _____________

Risk Factor              Score (1-5)    Notes
─────────────────────────────────────────────────
Data Sensitivity         [   ]          
Action Capability        [   ]          
Identity Scope           [   ]          
Exposure                 [   ]          
Vendor Trust             [   ]          
Auditability             [   ]          
Reversibility            [   ]          
Blast Radius             [   ]          
─────────────────────────────────────────────────
TOTAL                    [   ]          

Risk Rating:  [ ] Low  [ ] Medium  [ ] High  [ ] Critical
Tier Assigned: [ ] 0  [ ] 1  [ ] 2  [ ] 3  [ ] 4
Decision:      [ ] Approve  [ ] Conditional  [ ] Reject
```

**Rule:** Every score must have a one-line rationale in the Notes column. Scores without rationale are not auditable.

---

## Worked Example: GitHub Repo Management MCP

**Scenario:** An engineering team requests an MCP server that can search repositories, create pull requests, and merge PRs to protected branches. It uses the team's corporate GitHub App with repository admin scope.

### Factor-by-factor scoring

| Risk Factor | Score | Rationale |
|-------------|-------|-----------|
| Data Sensitivity | 3 | Internal source code (confidential) |
| Action Capability | 4 | Can create and merge PRs (write + deploy-like) |
| Identity Scope | 4 | Corporate GitHub App with admin scope |
| Exposure | 2 | Internal K8s cluster, not internet-facing |
| Vendor Trust | 3 | Internal fork of known OSS project |
| Auditability | 3 | GitHub audit log exists; MCP-level logging partial |
| Reversibility | 3 | PR merges can be reverted but not trivially |
| Blast Radius | 4 | Can affect production repositories |

**Total Score: 26 → High Risk**

**Tier: 3** (Write-Capable) — consistent with score.

**Decision:** Conditional approval with:

- Remove merge capability initially (reduces Action Capability to 3, score to ~23)
- Full MCP-level audit logging within 30 days
- HITL required for all write actions
- Re-score after conditions met

---

## Worked Example: Internal Wiki Search MCP

**Scenario:** Read-only MCP searching internal engineering wiki. Per-user SSO. No write tools. Hosted internally.

| Risk Factor | Score | Rationale |
|-------------|-------|-----------|
| Data Sensitivity | 2 | Internal non-sensitive engineering docs |
| Action Capability | 2 | Read internal data only |
| Identity Scope | 2 | Per-user SSO, read scope |
| Exposure | 2 | Internal network |
| Vendor Trust | 1 | Built internally |
| Auditability | 2 | Full logs, SIEM integrated |
| Reversibility | 1 | Read-only |
| Blast Radius | 2 | Single team primary users |

**Total Score: 14 → Low Risk**

**Tier: 1** — consistent. Approve with standard Tier 1 controls.

---

## Worked Example: AWS Admin MCP

**Scenario:** MCP with ability to create/delete EC2 instances, modify security groups, and read secrets from Secrets Manager. Standing IAM role with `AdministratorAccess`. Third-party OSS server.

| Risk Factor | Score | Rationale |
|-------------|-------|-----------|
| Data Sensitivity | 5 | Secrets, infrastructure credentials |
| Action Capability | 5 | Delete, deploy, admin |
| Identity Scope | 5 | Standing admin IAM role |
| Exposure | 3 | Internal host but broad API reach |
| Vendor Trust | 4 | Community OSS, limited review |
| Auditability | 4 | CloudTrail only, no MCP-level logs |
| Reversibility | 5 | Resource deletion, IAM changes irreversible |
| Blast Radius | 5 | Enterprise production infrastructure |

**Total Score: 36 → Critical**

**Tier: 4** — consistent. CISO approval required. Strongly recommend decomposing into scoped automation (Tier 3 max) or rejecting.

---

## Using Scores in Decisions

### When score and tier disagree

| Situation | Action |
|-----------|--------|
| Tier 1, score 28 | Investigate — likely misclassified; probably Tier 2 or 3 |
| Tier 3, score 16 | Investigate — controls may be over-scoped; or score is missing exposure context |
| Tier 4, score 30 | Acceptable — Tier 4 with relatively contained blast radius |
| Tier 2, score 32 | Escalate — sensitive read with critical-scoring factors (e.g., no logs, unknown vendor) |

### Tool chaining adjustment

When multiple MCP servers are connected to the same agent, consider adjusting **Blast Radius** and **Action Capability** upward by 1 point each if a read server and write server are combined — unless documented business need and compensating controls exist.

---

## Common Scoring Mistakes

| Mistake | Why it is wrong | Correction |
|---------|-----------------|------------|
| Scoring based on server name, not tools | "Slack MCP" could be Tier 1 or Tier 3 | Evaluate each tool; use highest scores |
| Ignoring blast radius of tool chaining | Read + write in same agent multiplies risk | Adjust scores or prohibit combination |
| Auditability 4–5 when only partial logs exist | Downstream logs ≠ MCP attribution | If MCP-level attribution missing, score 3–4 |
| Vendor trust 1–2 for "popular" OSS | Popularity ≠ your review status | Score based on *your* organization's review |
| Not re-scoring after changes | New tools change the risk profile | Re-score on any material change |
| Scoring without written rationale | Unauditable decisions | Require Notes column for every factor |

---

## References

| Source | Relevance |
|--------|-----------|
| [Chapter 5 — Classification](05-server-classification.md) | Tier assignment alongside scoring |
| [Chapter 7 — Approval Workflow](07-approval-workflow.md) | Stage 3 security review |
| [Approval Decision Form](../templates/approval-decision-form.md) | Record scores and rationale |
| [NIST AI RMF — Measure function](../appendix/framework-mapping.md) | Risk quantification alignment |

---

## Practitioner Checklist

- [ ] Risk scoring worksheet used for every MCP server at or above Tier 2
- [ ] All eight factors scored with documented rationale
- [ ] Total score mapped to risk rating band
- [ ] Score compared to tier assignment for consistency
- [ ] Scores recorded in risk register and approval decision form
- [ ] Re-scoring triggered by material changes (new tools, scope expansion)
- [ ] Critical scores (33–40) escalated to CISO
- [ ] Tool chaining considered in blast radius and action capability scores

---

**Next:** [Chapter 7 — Approval Workflow](07-approval-workflow.md) defines how scoring and classification feed into formal approve, conditional, or reject decisions.
