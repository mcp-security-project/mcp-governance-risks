# Chapter 15: Metrics for CISOs

**Audience:** CISOs, security leadership, and governance program managers  
**Decision supported:** Measuring MCP governance program health and identifying gaps  
**Reading time:** ~20 minutes

---

## What Gets Measured Gets Managed

MCP governance without metrics is invisible to leadership. Budget, staffing, and executive attention follow measurable risk. This chapter defines **15 monthly KPIs** that CISOs and security leadership should track to assess governance maturity, identify emerging risks, and report to executive stakeholders.

These metrics feed from:

- [Inventory](04-asset-inventory.md) and [risk register](../templates/risk-register.md)
- [Monitoring program](13-continuous-monitoring.md)
- [Incident response records](14-incident-response.md)
- Approval and exception forms

Capture a **baseline** in month one. Track trends, not just point-in-time snapshots.

---

## Monthly Dashboard KPIs

| # | Metric | Description | Target direction |
|---|--------|-------------|------------------|
| 1 | Total MCP servers discovered | All known servers (approved + shadow) | Stable or ↑ (better discovery) |
| 2 | Approved MCP servers | Formally approved count | ↑ as % of total |
| 3 | Unapproved / shadow MCP | Without approval | ↓ toward **zero** |
| 4 | MCP servers by risk tier | Count per Tier 0–4 | Tier 4 minimal |
| 5 | MCP servers with write access | Tier 3–4 count | Minimize to business need |
| 6 | MCP servers with privileged access | Tier 4 count | Minimize; CISO approved each |
| 7 | MCP servers accessing sensitive data | Tier 2+ count | Tracked; DLP required |
| 8 | MCP servers without audit logs | Missing required logging | **Zero** for Tier 2+ |
| 9 | Third-party MCP servers | External/OSS count | 100% vendor reviewed at Tier 2+ |
| 10 | MCP-related incidents | Security incidents involving MCP | ↓ |
| 11 | High-risk tool calls | Write/delete/deploy per month | Baseline + anomaly detection |
| 12 | Blocked tool calls | Denied by auth or DLP | Investigate spikes |
| 13 | Risk exceptions granted | Active exceptions | ↓; all time-bound |
| 14 | Open remediation items | Overdue conditional approvals | ↓ toward zero |
| 15 | Overdue periodic reviews | Past review due date | **Zero** |

---

## KPI Details and Data Sources

### Coverage metrics (1–3)

**Purpose:** How well do we know our MCP landscape?

| Metric | Data source | Healthy signal |
|--------|-------------|----------------|
| Total discovered | Inventory + discovery scans | Growing discovery = improving visibility |
| Approved | Risk register (status = approved) | High ratio to total |
| Shadow | Discovery minus inventory | Trending to zero |

**Key ratio:** `Approved ÷ Total Discovered` — target **>95%** after initial discovery phase (months 2–6).

**Executive narrative example:** *"We discovered 47 MCP servers this month, up from 32 — better visibility. 41 are approved (87%). Six shadow servers in remediation, down from 12."*

---

### Risk distribution metrics (4–7)

**Purpose:** What does our risk profile look like?

| Metric | Data source | Healthy signal |
|--------|-------------|----------------|
| By tier | Risk register (tier field) | Majority Tier 0–2; Tier 4 rare |
| Write access | Tier 3–4 count | Each has documented justification |
| Privileged | Tier 4 count | Minimal; CISO approval on file |
| Sensitive data | Tier 2+ count | All have DLP + full logging |

**Executive narrative example:** *"We have 3 Tier 4 servers, all with CISO sign-off and monthly review. No new Tier 4 approvals this quarter."*

---

### Control effectiveness metrics (8–9)

**Purpose:** Are required controls actually in place?

| Metric | Data source | Healthy signal |
|--------|-------------|----------------|
| Without audit logs | Compliance verification ([Ch. 10](10-minimum-security-baseline.md)) | Zero Tier 2+ |
| Third-party reviewed | Risk register + vendor questionnaires | 100% at Tier 2+ |

**Red flag:** Any Tier 2+ server without logging → suspend until remediated.

---

### Operational metrics (10–12)

**Purpose:** Active threats and operational health.

| Metric | Data source | Healthy signal |
|--------|-------------|----------------|
| MCP incidents | IR tickets tagged MCP | Low and decreasing |
| High-risk tool calls | SIEM / MCP audit logs | Stable baseline |
| Blocked tool calls | Auth/DLP denial logs | Spikes investigated |

---

### Governance process metrics (13–15)

**Purpose:** Program discipline.

| Metric | Data source | Healthy signal |
|--------|-------------|----------------|
| Risk exceptions | Exception forms | Few; all with expiration |
| Open remediation | Conditional approval tracking | None overdue |
| Overdue reviews | Risk register (next review date) | Zero |

---

## Sample Monthly Report Template

```
MCP Governance Monthly Report — [Month Year]
Prepared by: [Governance PM]  |  Reviewed by: [CISO]

EXECUTIVE SUMMARY
- Total MCP servers: [X] (approved: [Y], shadow: [Z])
- Approval ratio: [Y/X]%
- New servers approved: [N]
- Shadow MCP remediated: [N]
- MCP incidents: [N]
- Active risk exceptions: [N] (expiring within 30 days: [N])

RISK DISTRIBUTION
  Tier 0: [N]  |  Tier 1: [N]  |  Tier 2: [N]  |  Tier 3: [N]  |  Tier 4: [N]

CONTROL GAPS (require action)
- Servers without audit logs: [N] → [server names]
- Overdue periodic reviews: [N] → [server names]
- Open remediation items: [N] → [details]

INCIDENTS
- [Summary or "None this month"]

TRENDS (vs. prior month)
- Shadow MCP: [↑/↓/→]
- Tier 4 count: [↑/↓/→]
- Incidents: [↑/↓/→]

ACTION ITEMS
1. [Action] — Owner — Due date
2. [Action] — Owner — Due date
```

---

## Maturity Progression

Use metrics to track governance maturity over 12–24 months:

| Level | Indicators |
|-------|------------|
| **Initial** | No inventory; shadow unknown; no metrics |
| **Developing** | Inventory exists; approval process defined; basic KPIs tracked |
| **Defined** | All servers classified; workflow operational; monthly reporting |
| **Managed** | Shadow near zero; controls verified; exceptions time-bound |
| **Optimized** | Automated discovery/monitoring; continuous Tier 4 review; metrics-driven decisions |

**Realistic timeline:** Most organizations reach **Defined** within 6–9 months; **Managed** within 12–18 months with executive sponsorship.

---

## Reporting Cadence

| Audience | Frequency | Content |
|----------|-----------|---------|
| CISO | Monthly | Full dashboard (all 15 KPIs) |
| Security leadership | Monthly | Executive summary + incidents + gaps |
| Engineering leadership | Quarterly | Tier distribution + approvals + policy updates |
| Executive / board | Quarterly | Summary metrics + incidents + risk trends |
| Audit / compliance | Annually | Full risk register + control verification |

---

## Setting Targets (first 90 days)

| Metric | Day 30 target | Day 90 target |
|--------|---------------|---------------|
| Total discovered | Baseline captured | +20% visibility acceptable |
| Approval ratio | >50% | >85% |
| Shadow count | Known and prioritized | <5% of total |
| Tier 2+ without logs | Identified | Zero |
| Overdue reviews | Identified | Zero |

Adjust targets after baseline month based on organizational size and MCP adoption rate.

---

## References

| Source | Relevance |
|--------|-----------|
| [Chapter 4 — Inventory](04-asset-inventory.md) | Coverage metrics |
| [Chapter 13 — Monitoring](13-continuous-monitoring.md) | Operational metrics |
| [Risk Register](../templates/risk-register.md) | Primary data source |
| [NIST AI RMF — Measure](../appendix/framework-mapping.md) | Framework alignment |

---

## Practitioner Checklist

- [ ] All 15 KPIs defined with data sources
- [ ] Monthly data collection process established
- [ ] Dashboard or report template created
- [ ] Reporting cadence assigned to governance program owner
- [ ] Baseline measurements captured
- [ ] Targets defined for key ratios
- [ ] Monthly report reviewed by CISO or security leadership
- [ ] Quarterly executive summary scheduled

---

**Next:** [Chapter 16 — Templates](16-templates.md) provides the forms and worksheets used throughout this guide.
