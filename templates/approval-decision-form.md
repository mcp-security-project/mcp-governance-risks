# MCP Approval Decision Form

**Instructions:** Complete this form after security review. Record the approval decision and required controls. File in the risk register.

---

## Server Information

| Field | Value |
|-------|-------|
| **MCP server name** | |
| **Intake form reference** | |
| **Vendor questionnaire reference** (if applicable) | |
| **Business owner** | |
| **Requesting team** | |

## Classification and Scoring

| Field | Value |
|-------|-------|
| **Risk tier assigned** | [ ] Tier 0  [ ] Tier 1  [ ] Tier 2  [ ] Tier 3  [ ] Tier 4 |
| **Tier rationale** | |

### Risk Scoring

| Risk Factor | Score (1–5) | Notes |
|-------------|-------------|-------|
| Data Sensitivity | | |
| Action Capability | | |
| Identity Scope | | |
| Exposure | | |
| Vendor Trust | | |
| Auditability | | |
| Reversibility | | |
| Blast Radius | | |
| **Total Score** | | |
| **Risk Rating** | [ ] Low (8–15)  [ ] Medium (16–25)  [ ] High (26–32)  [ ] Critical (33–40) |

## Security Review Summary

| Review Area | Finding | Pass/Fail |
|-------------|---------|-----------|
| AuthN / AuthZ | | |
| Secrets handling | | |
| Token handling | | |
| Tool permissions | | |
| Prompt injection exposure | | |
| Command execution | | |
| Logging | | |
| Network access | | |
| Dependencies | | |
| Vendor posture | | |

## Decision

| Field | Value |
|-------|-------|
| **Decision** | [ ] Approved  [ ] Conditionally Approved  [ ] Rejected |
| **Approver name** | |
| **Approver role** | |
| **Approval date** | |
| **Next review date** | |

### Required Controls

| Control | Required | In Place | Notes |
|---------|----------|----------|-------|
| Inventory | | | |
| Named owner | | | |
| Authentication | | | |
| Scoped authorization | | | |
| Audit logging | | | |
| Human approval (HITL) | | | |
| Threat model | | | |
| Vendor review | | | |
| DLP | | | |
| Incident playbook | | | |
| CISO approval | | | |

### Conditions (if conditionally approved)

| # | Condition | Owner | Deadline | Status |
|---|-----------|-------|----------|--------|
| 1 | | | | [ ] Open  [ ] Met |
| 2 | | | | [ ] Open  [ ] Met |
| 3 | | | | [ ] Open  [ ] Met |

### Rejection Rationale (if rejected)

---

## Deployment Authorization

| Field | Value |
|-------|-------|
| **Approved user group** | |
| **Approved environment** | [ ] Dev  [ ] Staging  [ ] Production |
| **Version pinned** | |
| **Deployment date** | |
| **Deployed by** | |

---

**Signatures:**

| Role | Name | Date |
|------|------|------|
| Approver | | |
| Business owner (acknowledged) | | |
| AppSec reviewer | | |
