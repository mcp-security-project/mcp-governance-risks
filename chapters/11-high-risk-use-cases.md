# Chapter 11: High-Risk MCP Use Cases

**Audience:** Security architects, AppSec, platform owners, and CISOs  
**Decision supported:** Understanding scenario-specific risks and mandatory controls for Tier 3–4 MCP servers  
**Reading time:** ~28 minutes

---

## When Generic Controls Are Not Enough

Tier 3 (Write-Capable) and Tier 4 (Privileged / Critical) MCP servers need more than the baseline matrix in [Chapter 10](10-minimum-security-baseline.md). Each high-risk scenario has distinct failure modes, attack paths, and compensating controls.

This chapter provides scenario-specific guidance for the most common Tier 3–4 use cases. For each scenario, assume:

- Formal threat modeling completed
- Risk scoring documented ([Chapter 6](06-risk-scoring.md))
- Full control baseline from Chapter 10 in place
- CISO approval for all Tier 4 servers

**Before approving any scenario below, ask:** Can this be done at a lower tier with narrower scope?

---

## Scenario 1: GitHub / Source Code Management

**Tier:** 3 (write) to 4 (admin)

### Capabilities at risk

- Create, merge, and close pull requests
- Modify branch protection rules
- Access repository secrets and settings
- Trigger CI/CD pipelines via webhook events
- Modify org-level permissions (Tier 4)

### Required controls

| Control | Implementation |
|---------|----------------|
| Separate read/write servers | Tier 1 read MCP + Tier 3 write MCP |
| HITL for merge and branch protection | No auto-merge without explicit approval |
| Scoped GitHub App | Not personal access tokens; repo-scoped permissions |
| Audit logging | MCP-level + GitHub audit log correlation |
| Rate limits | Cap PR creation and merges per hour |
| Rollback plan | Revert merge, restore branch protection documented |

### Attack path: prompt injection via PR description

1. Agent reads issue or PR with injected instructions
2. Instructions direct agent to merge unreviewed code or disable branch protection
3. Malicious code reaches production branch

**Mitigations:** HITL for all merges; branch protection changes prohibited via MCP or HITL-gated; prompt injection testing on Tier 2+ read paths feeding same agent.

### Approval note

Start with read-only MCP (Tier 1). Add write capabilities incrementally with pilot users. Never approve org-admin scope without Tier 4 review.

---

## Scenario 2: Cloud Infrastructure Admin (AWS / GCP / Azure)

**Tier:** 4

### Capabilities at risk

- Create, modify, delete cloud resources
- Modify IAM policies and roles
- Access secrets and key management services
- Modify security groups, firewalls, network ACLs

### Required controls

| Control | Implementation |
|---------|----------------|
| JIT access | No standing admin credentials |
| PAM integration | All admin actions through privileged access workflow |
| HITL per destructive action | Delete, IAM change, security group modification |
| Segregation of duties | Agent cannot create and approve resources |
| Full audit trail | CloudTrail / equivalent + MCP logs |
| Break-glass | Documented in [Chapter 14](14-incident-response.md) |
| Sandbox mandatory | Initial deployment only in non-prod account |
| CISO risk acceptance | Required before production |

### Common failure modes

- Agent deletes production resources from misinterpreted instruction
- Prompt injection via CloudWatch logs or resource tags triggers IAM changes
- Standing admin credentials in MCP configuration

### Approval note

**Strongly consider rejection.** Prefer scoped automation with predefined, reviewed action templates (Tier 3) over open-ended admin MCP. Most "cloud admin agent" use cases can be decomposed into specific approved actions.

---

## Scenario 3: Secrets Manager

**Tier:** 4

### Capabilities at risk

- Read production secrets, API keys, certificates
- Create and rotate secrets
- Modify access policies on secret stores

### Required controls

| Control | Implementation |
|---------|----------------|
| Path-scoped read | Specific secret paths only — no wildcards |
| No write via MCP | Unless explicitly justified and HITL-protected |
| Access logging | Every read logged with user/agent attribution |
| Secret redaction | Secret values never in MCP logs or tool responses |
| PAM integration | Secret access through privileged workflow |
| Tool chaining review | Block read-secret + send-email in same agent |

### Attack path: tool chaining exfiltration

1. Agent reads secrets via secrets MCP
2. Agent sends secrets via email or Slack MCP
3. Data exfiltrated without user awareness

**Mitigations:** Prohibit secrets MCP + communication MCP in same agent session; DLP on outbound tool parameters.

### Approval note

Prefer indirect access — MCP retrieves a short-lived token reference, not raw secret. Evaluate scoped service account instead of secrets MCP.

---

## Scenario 4: CI/CD Pipeline Trigger

**Tier:** 3

### Capabilities at risk

- Trigger production deployments
- Modify pipeline configurations
- Access build secrets and artifacts
- Bypass approval gates in deployment workflows

### Required controls

| Control | Implementation |
|---------|----------------|
| HITL before production deploy | No auto-deploy to prod |
| Approved branches/environments only | Block feature branch → production |
| Read-only pipeline config | MCP cannot modify pipeline YAML |
| Audit logging | Every trigger logged with user attribution |
| Rate limits | Max deploys per hour/day |
| Rollback tested | Documented and exercised quarterly |

### Common failure modes

- Agent triggers production deploy from feature branch
- Prompt injection in build logs modifies deployment target
- Agent disables approval gates before triggering deploy

### Approval note

MCP should **trigger** pipelines, not **control** pipeline logic. Approval gates must remain outside MCP reach.

---

## Scenario 5: Communication (Email / Slack / Teams)

**Tier:** 3

### Capabilities at risk

- Send messages to internal or external recipients
- Post to company-wide channels
- Forward sensitive data to unauthorized recipients
- Phishing via agent-sent messages (attacker-controlled content)

### Required controls

| Control | Implementation |
|---------|----------------|
| HITL for external / broad channels | `#general`, external email domains |
| DLP on outbound content | Scan message body and attachments |
| Rate limits | Messages per minute/hour |
| Recipient allowlists | For automated messages |
| Audit logging | Sanitized content + recipient list |
| Separate read/write servers | Tier 1 read + Tier 3 post |

### Attack path: data exfiltration via Slack

1. Agent reads confidential data from CRM or wiki MCP
2. Agent posts data to public or external Slack channel
3. Sensitive information exposed

**Mitigations:** DLP; prohibit read-sensitive + write-communication in same agent; HITL for external posts.

---

## Scenario 6: Finance / Payment Workflows

**Tier:** 4

### Capabilities at risk

- Initiate payments or financial transactions
- Modify billing configurations
- Access financial records and PII
- Approve invoices or purchase orders

### Required controls

| Control | Implementation |
|---------|----------------|
| Segregation of duties | Agent cannot initiate and approve |
| HITL for every financial action | No exceptions |
| Transaction amount limits | Configurable thresholds |
| Full audit trail | Financial compliance retention periods |
| PAM for financial system access | |
| CISO + finance leadership sign-off | Dual accountability |
| Formal threat model | Required |

### Approval note

Financial MCP should be **last resort**. Prefer predefined, reviewed automation workflows over agent-driven financial actions. Many organizations should **reject** open-ended finance MCP entirely.

---

## Scenario 7: Kubernetes Admin

**Tier:** 4 (cluster-admin) or 3 (namespace-scoped)

### Capabilities at risk

- Deploy, scale, delete workloads
- Modify RBAC and network policies
- Access pod logs and secrets
- Execute commands inside containers

### Required controls

| Control | Implementation |
|---------|----------------|
| Namespace-scoped access | Default; cluster-admin requires Tier 4 justification |
| HITL for destructive ops | Delete deployment, scale-to-zero, RBAC change |
| No shell exec in production | Prohibit `kubectl exec` via MCP in prod |
| K8s audit policy | API server audit logs + MCP correlation |
| PAM / JIT | Elevated access time-bound |
| CISO approval | For cluster-admin scope |

### Common failure modes

- Agent deletes production deployments
- Prompt injection via pod logs triggers RBAC change
- Agent exec into pod and exfiltrates data

### Approval note

Namespace-scoped read + limited write (restart deployment) may be Tier 3. Cluster-admin is Tier 4.

---

## Cross-Scenario Controls

All Tier 3–4 servers require regardless of use case:

| Control | Reference |
|---------|-----------|
| Formal threat model | [Chapter 10](10-minimum-security-baseline.md) |
| Risk scoring with rationale | [Chapter 6](06-risk-scoring.md) |
| HITL for sensitive actions | [Chapter 3](03-governance-principles.md) |
| Full audit trail | [Chapter 13](13-continuous-monitoring.md) |
| Incident response playbook | [Chapter 14](14-incident-response.md) |
| CISO approval (Tier 4) | [Chapter 8](08-risk-ownership-raci.md) |
| Periodic review per tier | [Chapter 13](13-continuous-monitoring.md) |
| Tool chaining assessment | [Chapter 2](02-why-mcp-needs-governance.md) |

---

## Threat Modeling Template for High-Risk MCP

Use this structure for Tier 3–4 threat models:

```
1. Server name, tier, owner
2. Tools and data flows (diagram)
3. Trust boundaries (agent, MCP, downstream API)
4. Threat actors (external attacker, malicious insider, prompt injection)
5. STRIDE analysis per tool
6. Tool chaining scenarios (combined MCP blast radius)
7. Mitigations mapped to each threat
8. Residual risk and acceptor
9. Review date and next refresh
```

---

## References

| Source | Relevance |
|--------|-----------|
| [OWASP MCP04: Prompt Injection](https://owasp.org/www-project-mcp-top-10/) | Cross-scenario attack path |
| [OWASP LLM08: Excessive Agency](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | HITL justification |
| [Chapter 5 — Tier 3–4 definitions](05-server-classification.md) | Classification |

---

## Practitioner Checklist

- [ ] Each Tier 3–4 server mapped to scenario in this chapter
- [ ] Scenario-specific controls implemented and verified
- [ ] Threat model completed for each high-risk server
- [ ] Tool chaining risk evaluated (combined MCP blast radius)
- [ ] HITL tested with meaningful approval prompts
- [ ] Rollback plan documented and tested for write-capable servers
- [ ] CISO risk acceptance obtained for all Tier 4 servers

---

**Next:** [Chapter 12 — Shadow MCP Governance](12-shadow-mcp-governance.md) addresses detection and remediation of unapproved MCP servers.
