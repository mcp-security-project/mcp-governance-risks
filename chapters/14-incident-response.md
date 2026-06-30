# Chapter 14: Incident Response Alignment

**Audience:** CISOs, security operations, incident responders, and MCP server owners  
**Decision supported:** Responding effectively when an MCP server is compromised, misused, or behaves unexpectedly  
**Reading time:** ~26 minutes

---

## MCP Incidents Are Different

Traditional security incidents often involve a human attacker or malware on an endpoint. MCP incidents add a third actor: **an AI agent** acting at machine speed, across multiple integrated systems, with **delegated user credentials** — sometimes triggered by prompt injection in content the agent read, not by a direct attacker login.

Organizations must extend incident response programs for MCP-specific scenarios while aligning with existing IR frameworks (NIST SP 800-61, SANS, internal playbooks).

This chapter provides an MCP incident response playbook covering detection, containment, investigation, recovery, and post-incident improvement.

---

## When to Trigger MCP Incident Response

| Trigger | Example |
|---------|---------|
| Unauthorized tool execution | Agent performs action outside approved scope |
| MCP server compromise | Server modified, backdoored, or wrong version running |
| Credential exposure | API keys or tokens in MCP config or logs |
| Data exfiltration via MCP | Sensitive data sent through communication MCP |
| Prompt injection exploit | Malicious wiki content triggers unauthorized write |
| High-risk shadow MCP discovered | Unapproved server with write/production access |
| Runaway agent | Hundreds of tool calls in rapid succession |
| HITL bypass | High-risk action executed without human approval |
| DLP alert on MCP tool parameters | Customer PII in outbound tool call |

**When in doubt, treat as incident.** Tier 3–4 events default to High severity minimum.

---

## Incident Response Playbook

### Phase 1: Detect and Triage

**Objective:** Confirm the incident and assess initial scope.

| Step | Action | Owner |
|------|--------|-------|
| 1 | Confirm alert/report is genuine MCP incident | SecOps |
| 2 | Identify affected MCP server(s) from inventory/risk register | SecOps + AppSec |
| 3 | Identify affected user(s) and agent session(s) | SecOps |
| 4 | Determine tier and risk score of affected server(s) | AppSec |
| 5 | Classify severity (Low / Medium / High / Critical) | SecOps + AppSec |
| 6 | Notify MCP server owner and AppSec lead | SecOps |
| 7 | Escalate to CISO for Tier 4 or Critical severity | AppSec |

**Severity classification:**

| Severity | Criteria | Example |
|----------|----------|---------|
| **Critical** | Active production data breach, privileged compromise, ongoing exfiltration | Secrets MCP + email MCP chaining |
| **High** | Unauthorized write actions, credential exposure, Tier 3–4 compromise | Unauthorized PR merge |
| **Medium** | Unauthorized sensitive read, moderate shadow MCP | Shadow CRM read MCP |
| **Low** | Policy violation, failed attack, Tier 0–1 anomaly | Failed auth spike |

---

### Phase 2: Contain

**Objective:** Stop ongoing damage; prevent spread.

| Step | Action | Notes |
|------|--------|-------|
| 1 | **Disconnect** affected MCP from AI platform | Remove from allowlist immediately |
| 2 | **Revoke** credentials — OAuth tokens, API keys, service accounts | Identity provider + downstream API |
| 3 | **Block** network access to MCP endpoint if self-hosted | Firewall / security group |
| 4 | **Disable** affected user/agent sessions | Prevent further tool calls |
| 5 | **Preserve** logs — do not delete; snapshot for forensics | Export MCP + SIEM + IdP logs |
| 6 | **Assess tool chaining** | Check other MCP in same agent session |
| 7 | **Contain related servers** | Disconnect chained MCP if attack used multiple |

**Break-glass (Tier 4):**

- Revoke all active JIT/PAM privileged sessions
- Activate break-glass only if needed for containment
- Document all break-glass usage for post-incident review

**Containment SLA:** Critical incidents — contain within 1 hour. High — within 4 hours.

---

### Phase 3: Investigate

**Objective:** Root cause, full scope, impact.

| Area | Key questions |
|------|---------------|
| Timeline | When did it start? First/last malicious tool call? |
| Attack vector | Prompt injection? Compromised creds? Vulnerable server? Shadow MCP? |
| Data impact | What data accessed, modified, exfiltrated? |
| Action impact | What actions performed? Reversible? |
| Scope | Which users, agents, systems affected? |
| Tool chaining | Multiple MCP servers used together? |
| Root cause | Config error? Missing control? Unpatched vulnerability? |

**Evidence sources:**

- MCP audit logs (tool calls, parameters, outcomes)
- AI platform connection logs
- SIEM alerts and correlated events
- MCP server configuration (current + git history)
- OAuth/token audit logs from identity provider
- Downstream system logs (GitHub, AWS, Slack, etc.)
- Retrieved content that may have contained injection payload

---

### Phase 4: Eradicate and Recover

**Objective:** Remove threat; restore safe operations.

| Step | Action |
|------|--------|
| 1 | Patch or replace compromised MCP server |
| 2 | Rotate **all** credentials associated with affected server |
| 3 | Reverse unauthorized actions where possible (revert merge, delete created resources) |
| 4 | Re-classify and re-score if scope changed |
| 5 | Implement missing controls identified in investigation |
| 6 | Re-approve through formal workflow before reconnection |
| 7 | Enhanced monitoring for 30 days post-recovery |

**Do not reconnect** until formal re-approval complete ([Chapter 7](07-approval-workflow.md)).

---

### Phase 5: Review and Improve

**Objective:** Learn and strengthen governance.

| Step | Action | SLA |
|------|--------|-----|
| 1 | Post-incident review (PIR) | Within 5 business days |
| 2 | Document timeline, root cause, impact, remediation | |
| 3 | Identify governance gaps (inventory, controls, policy) | |
| 4 | Update threat model for affected server | |
| 5 | Update risk register with lessons learned | |
| 6 | Communicate findings to stakeholders | |
| 7 | Track remediation items to completion | |

---

## MCP-Specific Incident Scenarios

### Scenario A: Prompt injection via retrieved content

**Flow:** Agent reads poisoned wiki → executes write MCP tool → unauthorized action.

**Response:**

1. Disconnect write MCP server
2. Preserve agent session logs and retrieved content
3. Identify injection payload source; quarantine or sanitize content
4. Implement HITL for write actions if missing
5. Review agent MCP configuration for tool chaining
6. Re-test prompt injection before re-approval

### Scenario B: Compromised MCP server binary

**Flow:** Supply chain attack or unauthorized code modification → hidden tools or exfiltration.

**Response:**

1. Disconnect immediately
2. Compare running binary/hash against approved version in risk register
3. Review all tool calls since last known-good version
4. Full vendor/source re-review ([Chapter 9](09-third-party-review.md))
5. Re-approve only after code review and version pinning verified

### Scenario C: Credential exposure in MCP config

**Flow:** API key in config committed to repo → attacker uses credentials directly.

**Response:**

1. Rotate credentials immediately
2. Scan repos and endpoints for exposed secrets
3. Review all actions taken with compromised credentials (MCP and direct API)
4. Implement secret scanning in CI/CD
5. Reject MCP configs with inline secrets going forward

### Scenario D: Runaway agent

**Flow:** Agent executes hundreds of tool calls — bug, injection, or misconfiguration.

**Response:**

1. Disable agent session and disconnect MCP server
2. Rate limit analysis — were limits configured?
3. Review tool call log for unauthorized actions amid noise
4. Implement or tighten rate limits before re-approval

---

## Integration with Existing IR Program

| Existing IR element | MCP extension |
|---------------------|---------------|
| Incident classification | Add MCP-specific severity criteria above |
| Escalation matrix | Include MCP server owner + AppSec lead |
| Communication plan | Template for MCP stakeholder notification |
| Forensics procedures | MCP audit log preservation and analysis |
| Playbook library | This chapter as MCP-specific playbook |
| Tabletop exercises | Include MCP compromise scenario annually |

### Suggested tabletop scenario

*"An engineer's AI assistant has GitHub read, Slack write, and internal wiki MCP connected. A wiki page contains injected instructions. The agent posts internal source code snippets to a public Slack channel. Walk through detect, contain, investigate, recover."*

---

## References

| Source | Relevance |
|--------|-----------|
| [Chapter 12 — Shadow MCP](12-shadow-mcp-governance.md) | Discovery during IR |
| [Chapter 13 — Monitoring](13-continuous-monitoring.md) | Detection sources |
| [NIST SP 800-61](https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final) | IR framework alignment |

---

## Practitioner Checklist

- [ ] MCP incident response playbook documented and accessible to SecOps
- [ ] Severity classification includes MCP-specific criteria
- [ ] Containment procedures tested (disconnect, revoke, preserve logs)
- [ ] Break-glass procedure documented for Tier 4 servers
- [ ] Investigation procedures include MCP audit log analysis
- [ ] Post-incident review process defined with 5-day SLA
- [ ] MCP compromise scenario in annual tabletop exercise
- [ ] Integration with existing IR program documented
- [ ] MCP server owners know their escalation role

---

**Next:** [Chapter 15 — Metrics for CISOs](15-ciso-metrics.md) defines the monthly dashboard KPIs for MCP governance program health.
