# MCP Risk Register

**Instructions:** Maintain this register as the single source of truth for all approved and conditionally approved MCP servers. Update upon approval, re-classification, periodic review, or decommissioning.

---

## Register Entries

| # | MCP Server Name | Owner | Source | Risk Tier | Data Accessed | Actions Allowed | Identity Used | Approval Status | Residual Risk | Risk Owner | Required Controls | Last Review | Next Review |
|---|----------------|-------|--------|-----------|---------------|-----------------|---------------|-----------------|---------------|------------|-------------------|-------------|-------------|
| 1 | | | | | | | | | | | | | |
| 2 | | | | | | | | | | | | | |
| 3 | | | | | | | | | | | | | |
| 4 | | | | | | | | | | | | | |
| 5 | | | | | | | | | | | | | |

## Field Definitions

| Field | Description | Values |
|-------|-------------|--------|
| MCP Server Name | Unique identifier | e.g., `github-repo-management` |
| Owner | Named accountable person | Email address |
| Source | Origin of the server | Internal, OSS, vendor, community |
| Risk Tier | Classification tier | Tier 0, 1, 2, 3, 4 |
| Data Accessed | Classification of data | Public, internal, confidential, regulated |
| Actions Allowed | Capabilities | Read, write, delete, admin, execute |
| Identity Used | Authentication identity | User, service account, privileged token |
| Approval Status | Current governance status | Approved, conditional, rejected, decommissioned |
| Residual Risk | Remaining risk after controls | Low, medium, high, critical |
| Risk Owner | Person accepting residual risk | Email address |
| Required Controls | Active controls | e.g., Logging, auth, DLP, HITL, sandboxing |
| Last Review | Most recent security review | Date |
| Next Review | Scheduled next review | Date (per tier cadence) |

## Review Cadence Reference

| Tier | Review Frequency |
|------|-----------------|
| 0 | Annually |
| 1 | Annually |
| 2 | Every 6 months |
| 3 | Quarterly |
| 4 | Monthly or continuous |

## Summary Metrics (update monthly)

| Metric | Count |
|--------|-------|
| Total approved servers | |
| Conditionally approved | |
| Tier 0 | |
| Tier 1 | |
| Tier 2 | |
| Tier 3 | |
| Tier 4 | |
| Overdue reviews | |
| Active exceptions | |
