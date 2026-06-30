# Chapter 8: Risk Ownership and RACI

**Audience:** CISOs, security architects, business owners, and program managers  
**Decision supported:** Assigning clear accountability for MCP risk across the organization  
**Reading time:** ~18 minutes

---

## Why RACI Matters for MCP

MCP governance fails in predictable ways when roles are ambiguous:

- Engineering deploys a server; security finds out months later
- An incident occurs; nobody knows who owns the server
- A vendor MCP processes customer data; legal was never consulted
- A Tier 4 server operates without CISO awareness
- Conditional approval conditions expire; nobody tracks remediation

A RACI matrix — **Responsible**, **Accountable**, **Consulted**, **Informed** — assigns unambiguous ownership for each governance activity. Every MCP server must have a named owner. Every approval must have a named approver.

**Golden rule:** Each activity has exactly **one Accountable** party. Multiple Responsible parties are acceptable.

---

## RACI Definitions

| Role | Meaning | MCP example |
|------|---------|-------------|
| **R — Responsible** | Does the work | Engineering deploys the MCP server |
| **A — Accountable** | Owns the outcome; final decision authority | AppSec assigns tier; CISO approves Tier 4 |
| **C — Consulted** | Provides input before decisions | Legal reviews sensitive data access |
| **I — Informed** | Notified of decisions and outcomes | CISO informed of Tier 2 approval |

---

## MCP Governance RACI Matrix

| Activity | Business Owner | Engineering | AppSec | CISO | Legal / Privacy | Procurement |
|----------|:-:|:-:|:-:|:-:|:-:|:-:|
| Define business need | A/R | C | C | I | I | I |
| Classify MCP server | C | R | **A** | C | C | I |
| Review data access | **A** | C | R | C | A (if sensitive) | I |
| Review technical risk | I | R | **A** | C | I | I |
| Review third-party vendor | C | C | C | I | C | **A/R** |
| Approve high-risk MCP | C | C | R | **A** | C | C |
| Monitor usage | I | R | **A** | C | I | I |
| Accept residual risk | **A** | C | C | A (critical) | C | I |

### How to read this matrix

**Define business need:** Business owner is Accountable and Responsible — they must articulate why the server exists. Engineering and AppSec are Consulted.

**Classify MCP server:** Engineering documents tools and data (Responsible). AppSec assigns tier (Accountable). Business owner confirms scope (Consulted).

**Approve high-risk MCP:** AppSec conducts review (Responsible). CISO makes final approval for Tier 3–4 (Accountable). Business owner confirms justification (Consulted).

**Accept residual risk:** Business owner accepts for Tier 0–2. CISO co-accepts for Tier 3–4 critical residual risk.

---

## Role Descriptions

### Business Owner

The person who can explain *why* this MCP server exists and accept consequences if it goes wrong.

**Responsibilities:**

- Define business need and use case
- Accountable for data access decisions in their domain
- Accept residual risk (Tier 0–2; consult on Tier 3–4)
- Ensure the server serves a legitimate, ongoing business purpose
- Participate in periodic review
- Notify AppSec of scope changes

**Who qualifies:** Product manager, engineering manager, department head — not a generic team alias.

---

### Engineering

Builds, deploys, and maintains MCP server infrastructure.

**Responsibilities:**

- Submit intake forms with accurate tool and data documentation
- Implement authentication, logging, scoping, HITL per approved controls
- Configure deployment per approval decision
- Monitor operational health
- Report changes (new tools, version upgrades) within 5 business days
- Execute rollback and containment during incidents

---

### AppSec (Application Security)

Leads security assessment and governance program execution.

**Responsibilities:**

- Accountable for classification decisions
- Lead technical security review (Stage 3)
- Define required controls per tier
- Maintain risk register and inventory accuracy
- Accountable for monitoring program effectiveness
- Escalate high-risk findings to CISO
- Track conditional approval remediation

---

### CISO

Sets policy, approves critical risk, and sponsors the governance program.

**Responsibilities:**

- Accountable for Tier 4 approvals and critical residual risk acceptance
- Set governance policy and minimum baselines
- Review monthly metrics ([Chapter 15](15-ciso-metrics.md))
- Own incident response escalation for MCP compromise
- Chair or delegate security risk board for exceptions

---

### Legal / Privacy

Ensures data handling complies with regulations and contracts.

**Responsibilities:**

- Accountable for data access review when sensitive or regulated data involved
- Review third-party data processing agreements
- Advise on GDPR, HIPAA, PCI, and sector-specific requirements
- Consulted on cross-border data flows
- Review AI usage policy language

---

### Procurement

Manages vendor relationships and contractual protections.

**Responsibilities:**

- Accountable for third-party vendor trust review
- Manage vendor contracts, SLAs, and security addenda
- Verify vendor security certifications (SOC 2, ISO 27001)
- Coordinate with Legal on data processing terms
- Maintain vendor inventory linked to MCP risk register

---

## Accountable vs. Responsible in Practice

### Example 1: Classifying a new Jira MCP server

| Role | Action |
|------|--------|
| Engineering (R) | Submits intake form; documents tools: `search_issues` (read), `create_issue` (write) |
| AppSec (A) | Assigns Tier 3 (write capability); scores 24 (Medium-High); defines HITL requirement |
| Business Owner (C) | Confirms use case: "Auto-create bugs from agent triage" |
| Legal (C) | Reviews because security project tickets may contain vulnerability details |
| CISO (I) | Notified of Tier 3 approval |

### Example 2: Approving a Kubernetes admin MCP (Tier 4)

| Role | Action |
|------|--------|
| Engineering (R) | Proposes server; documents cluster-admin tools |
| AppSec (R) | Conducts threat model; recommends namespace-scoped alternative |
| Business Owner (C) | Provides business justification or accepts deferral |
| Platform Owner (C) | Confirms infrastructure impact |
| CISO (A) | Approves or rejects; signs risk acceptance if approved |
| Legal (C) | Reviews if production customer data accessible via cluster |

### Example 3: Third-party OSS Slack MCP

| Role | Action |
|------|--------|
| Engineering (R) | Requests OSS server; provides repo URL |
| Procurement (A/R) | Reviews maintainer, license, support model |
| AppSec (R) | Reviews security controls, token handling, logging |
| Legal (C) | Reviews if messages contain customer data |
| Business Owner (A) | Accepts residual risk for Tier 3 write (posting) |

---

## Risk Ownership Model

Every MCP server in the risk register must have four named roles:

| Field | Who | Purpose |
|-------|-----|---------|
| Business risk owner | Business owner who requested server | Accepts business residual risk |
| Technical risk owner | Engineering lead for deployment | Maintains controls and reports changes |
| Security risk owner | AppSec analyst who conducted review | Owns security assessment currency |
| Residual risk acceptor | Business owner (Tier 0–2) or CISO (Tier 3–4) | Signed acceptance on file |

Residual risk acceptance must be documented in the [Risk Register](../templates/risk-register.md) or [Exception / Risk Acceptance Form](../templates/exception-risk-acceptance-form.md).

---

## Escalation Path

```
Engineering identifies MCP need
        ↓
Business Owner defines use case + accepts ownership
        ↓
AppSec classifies and reviews (Stage 2–3)
        ↓
┌─────────────────────────────────────────────┐
│ Tier 0–1: AppSec + business owner approve   │
│ Tier 2: AppSec + data owner (+ legal)       │
│ Tier 3: Security arch + business + platform │
│ Tier 4: CISO / risk board approves          │
└─────────────────────────────────────────────┘
        ↓
Exception needed? → Exception form + CISO sign-off
        ↓
Deploy with controls → Monitor → Periodic review
        ↓
Incident? → Owner + AppSec + CISO (Tier 4) per Chapter 14
```

### Escalation triggers

| Trigger | Escalate to |
|---------|-------------|
| Tier 3+ server requested | Security architecture + platform owner |
| Tier 4 server requested | CISO immediately |
| Regulated data involved | Legal / privacy before approval |
| Third-party OSS at Tier 2+ | Procurement + AppSec |
| Conditional approval overdue | AppSec → CISO |
| Shadow MCP with write access | AppSec → incident response |
| Score ≥ 33 | CISO before approval |

---

## Ownership Lifecycle Events

| Event | Required action | Timeline |
|-------|-----------------|----------|
| Owner changes role / departs | Reassign ownership | 30 days |
| Server scope expands | Owner notifies AppSec | 5 business days |
| Server decommissioned | Owner initiates decommission | Immediate |
| Incident occurs | Owner participates in IR | Per IR SLA |
| Periodic review due | Owner attends review | Per tier cadence |

Orphaned servers (no valid owner) are **suspended** until ownership reassigned.

---

## References

| Source | Relevance |
|--------|-----------|
| [Chapter 3 — Principle 1: Ownership](03-governance-principles.md) | Foundation for RACI |
| [Chapter 7 — Approval Workflow](07-approval-workflow.md) | Stage ownership |
| [Risk Register](../templates/risk-register.md) | Record ownership fields |
| [NIST AI RMF — Govern function](../appendix/framework-mapping.md) | Accountability alignment |

---

## Practitioner Checklist

- [ ] RACI matrix adopted and communicated to all stakeholders
- [ ] Every MCP server has named business and technical risk owner
- [ ] AppSec accountable for classification on every server
- [ ] CISO approval required and enforced for Tier 4
- [ ] Legal/privacy consulted for sensitive data access
- [ ] Procurement engaged for all third-party MCP servers
- [ ] Residual risk acceptance documented with named acceptor
- [ ] Escalation path published and understood
- [ ] Owner reassignment process defined for departures

---

**Next:** [Chapter 9 — Third-Party MCP Review](09-third-party-review.md) provides the vendor checklist for external and open-source MCP servers.
