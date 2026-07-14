# Framework Review Feedback (v1.0)

**Date:** July 2026  
**Scope:** Four reviewer comments on `mcp-governance-risk-framework-v1.0.md`  
**Purpose:** Assess fit, recommend embed locations, and track implementation status

---

## Executive summary

All four comments are **embeddable in v1.0** without restructuring the guide. None require new chapters; each maps to one or two existing sections plus the control catalog. Recommended priority:

| # | Topic | Embed? | Effort | Priority |
|---|-------|--------|--------|----------|
| 1 | Output-path validation + MCP-13 | Yes | Small | **P0** — closes a real control gap |
| 2 | Critical-factor score floor | Yes | Trivial (one rule) | **P0** — fixes a scoring logic hole |
| 3 | GitHub worked example consistency | Yes | Medium | **P1** — people will copy the example |
| 4 | Paved road / pre-approved catalog | Yes | Medium–large | **P1** — strongest adoption argument |

---

## 1. Validate outputs, not just inputs (MCP-13)

### Reviewer comment

> Outputs need validation, not just inputs. Prompt injection is treated as input-side (poisoned wiki pages), but tool outputs re-enter the agent's context and become instructions on the next turn. Traditional appsec = validate inputs; agentic systems = validate inputs AND outputs. Add tool-output sanitization to Ch2 and MCP-13 ("tool output treated as untrusted input").

### Current state

**Partially covered, but the load-bearing shift is missing.**

- Ch2 already has a section titled **"Prompt Injection via Tool Output"** (~line 466), but the attack flow describes *poisoned content the agent reads* (wiki, tickets, email) — an **input-side** path. It does not explain the **output re-entry loop**: tool return values appended to context on the next turn, where they can function as instructions.
- Governance response mentions "content sanitization" once (~line 486) with no control ID, no evidence requirement, and no client/host responsibility.
- The control catalog ends at **MCP-12**; nothing covers output-path treatment.
- Ch2's "Four properties" table (~line 280) frames prompt injection as bridging trust boundaries via retrieved data — still input-framed.

### Assessment

**Strong agree.** This is the most important conceptual gap for AppSec readers. The doc already names the section correctly but under-delivers on the output-path mechanism and controls.

### Recommended embed locations

| Location | What to add |
|----------|-------------|
| **Ch2 → "MCP Changes the Security Model"** (~line 239–300) | One paragraph on the appsec paradigm shift: deterministic apps validate inputs at the boundary; agentic systems must treat **tool outputs as untrusted input on the next turn**. Tie to the multi-turn context window. |
| **Ch2 → "Prompt Injection via Tool Output"** (~line 466) | Split or extend into two sub-paths: (A) poisoned *resources* the agent reads, (B) poisoned or attacker-influenced *tool return values* that re-enter context. Add a simple turn diagram: `User → Agent → Tool → Output → Context → Agent (next turn)`. |
| **Ch2 → Governance response bullets** (~line 481) | Add: sanitize or structurally isolate tool outputs before re-injection; block instruction-like patterns in returns where feasible; log output hash/size for forensics. |
| **Appendix → Formal Control Catalog** (~line 1574) | **MCP-13: Tool output treated as untrusted input** — Required Tier 2+, Recommended Tier 0–1. Evidence: client/host output-handling policy or implementation review (delimiter tagging, output filtering, structured vs. free-text returns). |
| **Appendix → Evidence Pack** (~line 1592) | Optional artifact: output-handling review for Tier 2+ agents that chain read + write servers. |
| **Ch1 → Scenario 1** (~line 43) | One sentence: exfiltration can also originate from a *prior turn's tool output*, not only from poisoned wiki content. |

### Draft language (MCP-13)

```markdown
| MCP-13 | Tool output treated as untrusted input | Recommended | Required | Required | Required | Client/host output-handling review: outputs delimited or structured; no raw tool returns promoted to system instructions without validation |
```

### Draft language (paradigm shift, Ch2)

> In traditional application security, the trust boundary is the request: validate inputs, authorize actions, log results. In agentic systems, **tool outputs cross back into the trust boundary** on the next turn. A CRM query result, a wiki excerpt, or a webhook response becomes part of the prompt the model reasons over — and can carry embedded instructions the user never saw. Security teams must extend validation and monitoring to the **output path**, not only the input path.

---

## 2. Critical-factor score floor

### Reviewer comment

> A straight 1–5 sum lets seven low scores hide one critical one (e.g., Action Capability 5 + everything else low → Medium). Fix: any single factor scoring 5 sets a floor of High. Also, Ch6 says "weighted" but there are no weights.

### Current state

**Hole confirmed.**

Example: Action Capability = 5, all other factors = 1 → **Total = 12 → Low** (band 8–15). Same for Identity Scope = 5 with admin/IAM credentials.

- Risk Rating Bands (~line 1372) use total score only; no floor rule.
- Line 1249 still says **"Weighted scoring applies after all hard gates pass"** but no weights exist anywhere in Ch6.
- The GitHub worked example (~line 1425) totals 26 (High) because multiple factors are elevated — it does not demonstrate the floor problem, but the AWS example (~line 1480) correctly lands Critical at 36.

### Assessment

**Strong agree.** One-sentence fix. Also fix the "weighted" mislabel (reviewer already renamed to "scoring model" in a PR — align main doc).

### Recommended embed locations

| Location | What to add |
|----------|-------------|
| **Ch6 → Risk Rating Bands** (~line 1372) | New subsection **"Critical factor floor"** immediately after the bands table: *If any single factor scores 5, the risk rating floor is **High**, regardless of total score. Total score still determines whether Critical (33–40) applies.* |
| **Ch6 → Scoring Worksheet** (~line 1395) | Add checkbox/note: `[ ] Any factor = 5 → floor High` |
| **Ch6 → line 1249** | Replace "Weighted scoring" with **"Scoring applies"** or **"The scoring model applies"** |
| **Ch1 → "Score: quantify risk"** (~line 86) | If weights are deferred to v1.1, say "eight-factor scoring model" (already correct there) — ensure Ch6 matches |
| **Ch6 → Common Scoring Mistakes** (~line 1522) | Add row: "Averaging out a critical factor" → "One factor at 5 can mean IAM/admin capability even if total looks Low" |

### Draft language (floor rule)

> **Critical factor floor:** If **any** risk factor scores **5**, the risk rating cannot be lower than **High**, regardless of total score. Total score still determines approval path within High and Critical bands. Example: Action Capability 5 with all other factors at 1 (total 12) → **High**, not Low. Reject or scope-down unless CISO-level exception applies.

### v1.1 note (optional footnote)

> v1.1 may introduce explicit factor weights (e.g., Action Capability and Identity Scope weighted higher). v1.0 uses equal 1–5 factors plus the critical-factor floor.

---

## 3. GitHub worked example vs. hard gates / Principle 3

### Reviewer comment

> The GitHub example uses a corporate GitHub App with **repository admin scope** for PR create/merge. That looks like a "broad token acceptance" gate failure and Principle 3 violation, yet it passes gates and gets conditionally approved. Either clarify the gate scope, or — better — have the reviewer catch admin scope and force scope-down before resubmission.

### Current state

**Internal inconsistency — example undermines its own rules.**

- Scenario (~line 1427): admin scope for search + PR create + merge.
- Identity Scope scored 4 with rationale "Corporate GitHub App with admin scope."
- Hard gate **"Broad token acceptance"** (~line 1231): *"Server accepts tokens with scopes or audiences broader than the approved use case → Reject."*
- Principle 3 (~line 659): least privilege; admin scope for PR workflow is explicitly called out as a red-flag pattern (~line 663–669).
- Decision (~line 1448): conditional approval removes **merge** but leaves **admin scope** unaddressed. Action Capability drops to 3; Identity Scope stays 4.

A reader copying this example will over-provision OAuth scopes and still get a "conditional approve" narrative.

### Assessment

**Strong agree.** The better story is a **two-pass review**: first submission fails scope review; resubmission with `contents:write` + `pull_requests:write` (or equivalent minimal scopes) proceeds to conditional approval on merge/HITL/logging.

Alternative (weaker): footnote that "broad token acceptance" gate applies only to audience/passthrough, not OAuth scope fit — but that **weakens** the gate and contradicts Principle 3. Prefer fixing the example.

### Recommended embed locations

| Location | What to add |
|----------|-------------|
| **Ch6 → Authorization Hard Gates** (~line 1231) | Clarify **"Broad token acceptance"** definition: includes OAuth/API scopes exceeding documented action scope (not only wrong audience). Cross-ref Principle 3. |
| **Ch6 → Worked Example: GitHub Repo Management MCP** (~line 1425) | Restructure as **Submission 1 (rejected)** → **Submission 2 (conditional approve)** |
| **Ch3 → Principle 3 → Red flags** (~line 682) | Add: "Repository admin scope for PR-only use case" as explicit red flag (may already be implied — make explicit) |

### Suggested revised example narrative

**Submission 1 — Rejected at hard gate / Principle 3**

- Request: search repos, create PRs, merge to protected branches.
- Identity: GitHub App with **repository admin** scope.
- Reviewer finding: admin scope exceeds approved action scope → **Reject per broad token acceptance gate and Principle 3**. Required remediation: scope down to read + PR write; split merge to separate review or require HITL-only merge tool.

**Submission 2 — Conditional approval**

- Same tools, GitHub App with **read + pull_request** scopes (no admin).
- Identity Scope: 2 or 3 (not 4).
- Merge capability: disabled initially OR HITL-gated.
- Total score drops; conditional approval focuses on MCP-level logging and HITL evidence — consistent with catalog.

---

## 4. "Approved path faster than shadow IT" / pre-approved catalog

### Reviewer comment

> "Make the approved path faster than shadow IT" is the best idea and it's buried. The 6 weeks vs 6 minutes line in Ch4 is great. Promote to a sixth principle (or dedicated section) and grow the pre-approved low-risk patterns bullet into a starter catalog. This is the answer to eng-leader pushback.

### Current state

**Idea present, structure absent.**

- Ch4 intake (~line 966): *"if formal approval takes 6 weeks and npm install takes 6 minutes, shadow MCP wins"* — excellent, but one sentence inside maintenance activities.
- Ch2 Shadow MCP (~line 519): bullet *"Provide an approved path that is faster than shadow IT,"* — **sentence appears truncated** (trailing comma, no continuation).
- Ch1 rollout (~line 223): *"Create a short list of pre-approved low-risk patterns, such as public read-only documentation search"* — single bullet, no catalog.
- Five principles (~line 594); nothing about paved-road / enablement.

### Assessment

**Strong agree.** This is the adoption mechanism that makes the rest of the framework stick. Prohibition + discovery are cleanup; **pre-approved catalog + fast intake SLA** are prevention.

### Recommended embed locations

| Location | What to add |
|----------|-------------|
| **Ch3 → New Principle 6** (after Principle 5, ~line 742) | **Principle 6: The Approved Path Must Beat Shadow IT** — One-line rule: *"Pre-approved patterns and SLAs must be faster than unofficial install."* Expand: catalog, intake SLA, self-service for Tier 0–1 patterns, escalation not blockage for Tier 2+. |
| **Ch3 → "The Five Principles at a Glance"** | Rename to **"The Six Principles at a Glance"** and add row 6. Update Ch1 cross-refs if any say "five principles." |
| **Ch4 → New section: "Pre-Approved MCP Catalog (Paved Road)"** (~after intake flow, ~line 990) | Starter catalog table + how to add patterns + review cadence. Link from Principle 6. |
| **Ch1 → Practical Rollout Plan, Days 31–60** (~line 223) | Replace single bullet with pointer to catalog section. |
| **Ch2 → Shadow MCP governance response** (~line 519) | Complete the truncated bullet; link to Principle 6 and catalog. |
| **Ch1 → Executive Summary** (~line 70+) | Add **"Enable"** capability alongside Inventory / Classify / Score — one short paragraph on paved road. |
| **README.md** | Add Principle 6 and catalog to quick-start for engineering audience. |

### Draft Principle 6

> **Principle 6: The Approved Path Must Beat Shadow IT**  
> Governance fails when unofficial install is faster than official approval. Organizations must maintain a **pre-approved catalog** of low-risk MCP patterns (Tier 0–1) with self-service or sub-48-hour intake, publish intake SLAs, and reserve full review for Tier 2+. Prohibition and discovery manage residual shadow MCP; the catalog prevents it.

### Starter catalog (seed content for Ch4)

| Pattern ID | Pattern | Tier | Max tools | Identity | Approval path | Typical SLA |
|------------|---------|------|-----------|----------|---------------|-------------|
| CAT-01 | Public read-only docs / API (weather, public RFCs) | 0 | Read only | None or API key (public) | Self-service register | Same day |
| CAT-02 | Internal wiki/docs search (read-only) | 1 | Read only | Per-user SSO, read scope | Lightweight intake | 2 business days |
| CAT-03 | Issue tracker read (Jira/Linear search) | 1–2 | Read only | Per-user OAuth, read scope | Standard intake | 3–5 business days |
| CAT-04 | GitHub/GitLab repo read (no write) | 1–2 | Read only | GitHub App, contents:read | Standard intake | 3–5 business days |
| CAT-05 | Slack channel read / search | 1–2 | Read only | Bot token, channel-scoped | Standard intake | 3–5 business days |
| CAT-06 | Calendar read (availability only) | 1 | Read only | Per-user OAuth, calendar.read | Lightweight intake | 2 business days |

*Patterns above CAT-03 require data-owner sign-off if sensitive data classes apply.*

Also document **intake SLAs** in Ch4 (~line 979 already mentions 2-day ack): e.g., Tier 0–1 complete in 5 business days; Tier 2 in 10; Tier 3+ scheduled review.

---

## Cross-cutting implementation checklist

Use this when embedding feedback into `mcp-governance-risk-framework-v1.0.md`:

- [ ] **Ch2:** Output-path validation paragraph + expanded prompt-injection section
- [ ] **Ch3:** Principle 6 + fix "five" → "six" references
- [ ] **Ch4:** Complete shadow IT bullet; add Pre-Approved Catalog section; keep 6-weeks/6-minutes line (prominent)
- [ ] **Ch6:** Critical-factor floor rule; fix "weighted" wording; rewrite GitHub example (two-pass); clarify broad-token gate
- [ ] **Appendix:** MCP-13 in control catalog; optional evidence pack row
- [ ] **Ch1 / README:** Enable/paved-road mention; principle count
- [ ] **reference.md:** Optional link to OWASP LLM01 / MCP06 output-handling resources if added during embed

---

## What not to do in v1.0

- **Do not** add real factor weights in the same release as the floor rule — floor fixes the immediate hole; weights need calibration and examples (v1.1 design conversation).
- **Do not** weaken the broad-token gate to save the old GitHub example — fix the example instead.
- **Do not** create a separate "policy" document for the catalog — keep it in Ch4 so engineers find it during intake.

---

## File map (this repo)

| File | Role |
|------|------|
| `mcp-governance-risk-framework-v1.0.md` | Primary embed target |
| `framework-review-feedback.md` | This file — reviewer comments, assessment, placement map |
| `README.md` | Update after embed: Principle 6, catalog pointer |
| `reference.md` | Optional: output-validation and paved-road references |

---

*Generated from structured review of four feedback items. Implement embeds via focused PR; this file can remain as audit trail or be linked from CONTRIBUTING.*
