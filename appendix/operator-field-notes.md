# Operator Field Notes

**Audience:** AppSec reviewers, security architects, governance leads, and MCP server owners  
**Purpose:** Practical guidance for running MCP governance reviews in the real world

---

## Why This Appendix Exists

The main guide defines the governance model: inventory, classification, scoring, approval, controls, monitoring, and incident response. This appendix covers the less formal part of the work: the questions experienced reviewers ask when an intake form looks acceptable on paper but still feels risky.

MCP governance is not only a paperwork exercise. A server can have an owner, a tier, a score, and an approval form and still be unsafe if the review misses how people will actually use it. These field notes are meant to help reviewers slow down in the right places.

---

## What Is Usually Missing from First Draft Reviews

Most early MCP reviews miss one or more of these details:

| Missing item | Why it matters | What to ask |
|--------------|----------------|-------------|
| Actual tool list | Server names hide risk | "Show every tool exposed, including disabled or experimental tools." |
| Agent configuration | Risk depends on what else the agent can access | "Which other MCP servers can run in the same agent session?" |
| Identity mapping | Audit logs need user, agent, and server attribution | "Can we tell whether Jane or the agent initiated this action?" |
| Negative test evidence | Teams often test only happy paths | "What happens when a token with the wrong audience is presented?" |
| Scope boundaries | "Read-only" is often broader than expected | "Read-only to which repos, channels, tenants, folders, or records?" |
| Human approval quality | HITL can become a blind click-through | "Does the prompt show action, target, identity, and impact?" |
| Rollback plan | Write-capable tools need recovery paths | "If the agent does the wrong thing, how do we reverse it?" |
| Change trigger | Servers drift after approval | "What specific changes force re-review?" |

If the review is moving quickly, use this table as a pause point before approval.

---

## Reviewer Questions That Surface Real Risk

Use these in review meetings or as comments on intake forms.

### Business and ownership

- What business process will break if this MCP server is not approved?
- Who can decide that the server should be turned off during an incident?
- Who will review access after the original requester changes teams?
- Is this a convenience tool, a productivity accelerator, or a production dependency?

### Data and scope

- What is the most sensitive record this server can read?
- Can the server return bulk data, or only narrowly scoped results?
- Can users change query filters to access data outside their normal role?
- Is any regulated data involved, including customer PII, employee data, payment data, secrets, or security findings?

### Tool behavior

- Which tools are read-only, write-capable, destructive, or privileged?
- Are write tools separated from read tools?
- Can tools call external URLs, send messages, create files, run commands, or trigger deployments?
- Are tool arguments constrained by allowlists, schemas, enums, or policy checks?

### Identity and authorization

- Does the MCP server validate token audience?
- Are OAuth scopes mapped to individual tools, or does one broad scope unlock everything?
- Is the server using user-delegated identity, a service account, or both?
- Can the server distinguish a human action from an agent-initiated action in logs?

### Operations and monitoring

- What alert fires if this server starts making 10 times its normal tool calls?
- Where do logs go, and who reads them?
- How quickly can credentials be revoked?
- What is the first containment action during a suspected prompt-injection incident?

---

## Evidence Pack for Approval

For Tier 2 and above, reviewers should ask for a small evidence pack. It does not need to be elaborate, but it should be concrete enough that another reviewer can reproduce the decision later.

| Evidence | Tier 2 | Tier 3 | Tier 4 |
|----------|--------|--------|--------|
| Completed intake form | Required | Required | Required |
| Tool inventory with action type | Required | Required | Required |
| Architecture or data-flow sketch | Recommended | Required | Required |
| Auth flow description | Required | Required | Required |
| Token audience validation test | Required | Required | Required |
| Audit log sample | Required | Required | Required |
| HITL screenshot or transcript | If write-like behavior exists | Required | Required |
| Threat model | Recommended | Required | Required |
| Rollback or recovery plan | Recommended | Required | Required |
| Vendor or OSS review | If external | Required if external | Required if external |
| CISO or risk board sign-off | Not usually | If required by policy | Required |

Good evidence is boring: screenshots, sample log lines, config snippets with secrets redacted, test results, and links to tickets. Avoid approving based only on verbal assurances.

---

## Sample Review Meeting Agenda

Use this for a 30-minute review of a Tier 2 or Tier 3 server.

| Time | Topic | Owner |
|------|-------|-------|
| 0-5 min | Business use case and owner confirmation | Requester / business owner |
| 5-10 min | Tool list, data accessed, and agent configuration | Engineering |
| 10-15 min | Classification and risk score | AppSec |
| 15-20 min | Auth, scope, logging, and HITL evidence | Engineering / AppSec |
| 20-25 min | Open gaps, conditions, and deadlines | AppSec / owner |
| 25-30 min | Decision path: approve, conditional, reject, or exception | Approver |

End the meeting with one of four outcomes. Do not end with "looks good, continue offline" unless someone owns the next step and due date.

---

## The Judgment Calls

Some MCP decisions will not fit cleanly into a table. These are common calls and how to handle them.

### "It is read-only, so it is low risk"

Not always. Read-only access to customer data, HR records, security tickets, source code, or secrets metadata can still be Tier 2 or higher. Read-only also becomes more dangerous when the same agent session has write-capable tools.

**Reviewer move:** Ask what the data could enable if copied elsewhere. If the answer includes fraud, privacy harm, credential discovery, vulnerability exposure, or reputational damage, do not treat it as low risk.

### "The server is internal, so vendor review is not needed"

Internal servers still need source and maintenance review. The question changes from vendor trust to engineering ownership: who maintains it, how dependencies are patched, and whether it follows the minimum security baseline.

**Reviewer move:** Ask for repository owner, deployment owner, dependency scan status, and release process.

### "The tool is only for developers"

Developer tools can be high impact. Source code, CI/CD, cloud consoles, secrets managers, and production logs are often more sensitive than ordinary business applications.

**Reviewer move:** Classify by capability, not user population.

### "We will add logging later"

Logging later usually means no useful evidence during the first incident. For Tier 2 and above, production use should wait until minimum audit logs exist.

**Reviewer move:** Conditional approval may allow a limited pilot only if compensating controls exist and production data is not exposed.

### "The AI platform already approved the connector"

Platform availability is not enterprise approval. A vendor may make a connector available for general use while your organization still needs to evaluate data scope, identity, logging, and business risk.

**Reviewer move:** Treat platform-native connectors as pre-built software, not pre-approved risk.

---

## Practical Rollout Plan

Organizations rarely start with perfect MCP governance. A staged rollout works better than a large policy launch that teams ignore.

### First 30 days: visibility

- Publish the "no owner, no logging, no scope" rules.
- Create the initial MCP inventory.
- Ask engineering teams to self-report MCP usage without penalty for the first discovery window.
- Classify known servers using Tier 0-4.
- Block the most obvious unsafe patterns: hardcoded secrets, shell execution, broad filesystem access, and unknown third-party servers with sensitive data.

### Days 31-60: workflow

- Require intake for new MCP servers.
- Start approval meetings for Tier 2 and above.
- Add risk register fields to the system of record.
- Define SIEM fields for MCP tool call logs.
- Create a short list of pre-approved low-risk patterns, such as public read-only documentation search.

### Days 61-90: enforcement

- Enforce allowlists in AI platforms where possible.
- Require evidence packs for Tier 2+ approvals.
- Start periodic reviews for Tier 3 and Tier 4 servers.
- Report monthly metrics to the CISO.
- Convert repeated exceptions into backlog items with funded owners.

---

## Pre-Approved Pattern Examples

Pre-approved patterns reduce friction without weakening governance. They should be narrow, documented, and reviewed periodically.

| Pattern | Allowed when | Not allowed when |
|---------|--------------|------------------|
| Public documentation search | Public data only, no auth, no write tools | Combined with external send tools without review |
| Internal wiki search | Internal non-sensitive spaces only, user identity enforced | Includes HR, legal, security, or customer data |
| Read-only GitHub metadata | Repo list, issues, PR metadata, no code contents | Includes private source code or admin actions |
| Ticket search | Non-sensitive tickets, no comments with regulated data | Includes security incidents, customer records, HR issues |

Pre-approved does not mean untracked. These servers still belong in inventory.

---

## Language That Makes Decisions Clear

Use plain language in approval records. A future incident responder should be able to understand the decision quickly.

### Weak approval note

> Approved. Low risk.

### Stronger approval note

> Approved as Tier 1. Server can search internal engineering wiki pages only. No write tools, no HR/legal/security spaces, user OAuth required, tool calls logged to central logging. Re-review required if new spaces or write tools are added.

### Weak conditional approval

> Approved if logging is fixed.

### Stronger conditional approval

> Conditionally approved for 10 pilot users until 2026-09-30. Production rollout blocked until MCP tool call logs include user identity, agent session ID, server name, tool name, sanitized parameters, and outcome. Engineering owner: Alex Kim. AppSec verification required before status changes to approved.

---

## Signs the Program Is Working

You should see these changes within the first 90 days:

- Requesters ask about tier before building the server.
- Teams separate read tools from write tools earlier in design.
- Security review conversations become shorter because evidence is prepared.
- Shadow MCP count initially rises, then starts falling.
- Conditional approvals have real deadlines and fewer silent extensions.
- CISO reporting shifts from anecdotes to trends.

The best signal is cultural: teams stop asking "Can I use this MCP?" and start asking "What scope and controls would make this MCP acceptable?"

---

## Quick Reviewer Checklist

- [ ] Have I seen the actual tool list?
- [ ] Do I know what other MCP servers can run in the same agent session?
- [ ] Is the server classified by highest-risk tool?
- [ ] Is the owner a named person?
- [ ] Are data boundaries specific enough to enforce?
- [ ] Are write, delete, deploy, send, and execute actions controlled by HITL?
- [ ] Does the approval record say what would trigger re-review?
- [ ] Can logs reconstruct who did what, through which agent, and with what outcome?
- [ ] Is there a rollback or containment path?
- [ ] Would I be comfortable defending this decision during an audit or incident review?
