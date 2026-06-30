# Chapter 9: Third-Party MCP Review

**Audience:** AppSec, procurement, vendor risk teams, and security architects  
**Decision supported:** Whether an external, open-source, or community MCP server can be trusted with enterprise data  
**Reading time:** ~22 minutes

---

## Why Third-Party Review Is Different

Internally built MCP servers are reviewed for security controls — authentication, logging, scoping. Third-party servers add **vendor risk** on top of technical risk:

- Who maintains the code?
- What happens to your data when it passes through their server?
- Will they patch vulnerabilities?
- Do you have contractual recourse if something goes wrong?

A popular GitHub repository is not a security review. Stars, forks, and README quality do not answer whether the server validates OAuth audience, avoids token passthrough, or logs tool calls.

Before approving any external MCP server, conduct a structured review covering **vendor trust**, **security controls**, **data handling**, and **operational risk**. Use the [Vendor Questionnaire](../templates/vendor-questionnaire.md) to document findings.

**Procurement leads vendor trust review. AppSec leads security controls review.**

---

## When Third-Party Review Is Required

| Source | Review type | When required |
|--------|-------------|---------------|
| Internally built | Security review only | Always |
| Internal fork of OSS | Security review + verify fork maintenance | Always |
| Open-source (community) | Full third-party review | Tier 0+ recommended; **required Tier 2+** |
| Commercial vendor | Full review + procurement | Tier 0+ recommended; **required Tier 2+** |
| Unknown / unverified | **Reject** until source verified | Cannot approve |

Minimum tier requirements from [Chapter 10](10-minimum-security-baseline.md):

| Tier | Vendor review |
|------|---------------|
| 0–1 | Optional (recommended for OSS) |
| 2 | Required if external |
| 3–4 | Required |

---

## Review Process: Step by Step

### Step 1: Identify source and maintainer

| Question | What to look for | Red flag |
|----------|------------------|----------|
| Who maintains it? | Named maintainers, org affiliation, responsive to issues | Anonymous account, no activity 6+ months |
| OSS, commercial, internal, community? | Determines contract and review depth | No license file |
| Is the repository active? | Commits in last 90 days; issues addressed | Abandoned with open CVEs |
| Are releases signed? | GPG, Sigstore, or equivalent | Unsigned binaries from unknown source |

### Step 2: Assess supply chain

| Question | What to look for | Red flag |
|----------|------------------|----------|
| Dependencies maintained? | No critical CVEs; dependabot or equivalent | Transitive deps with known exploits |
| Vulnerability disclosure process? | SECURITY.md, responsible disclosure | No way to report vulnerabilities |
| SBOM available? | Dependency list for analysis | Opaque dependency tree |
| Version pinning supported? | Specific versions, not `latest` | Floating tags only |

**Reference:** [OWASP MCP06: Supply Chain / Dependency Risk](https://owasp.org/www-project-mcp-top-10/)

### Step 3: Verify security controls

| Question | Requirement | How to verify |
|----------|-------------|---------------|
| Authentication supported? | Required Tier 1+ | Test unauthenticated access fails |
| Scoped authorization? | Minimum OAuth scopes | Review token scope configuration |
| Avoids token passthrough? | Must not forward client tokens blindly | Test with wrong-audience token |
| Validates token audience? | Per [MCP Authorization Specification](https://spec.modelcontextprotocol.io/specification/2025-03-26/basic/authorization/) | Present token for different audience; expect rejection |
| Secrets stored securely? | No hardcoded credentials | Source code review, config scan |
| Exposes logs? | Audit trail for tool calls | Execute test call; verify log output |
| Restricts network egress? | No unnecessary outbound connections | Network monitoring in test deploy |
| Avoids unsafe shell execution? | Sandboxed or prohibited | Review tool list and implementation |

**Testing approach:**

1. Deploy in **isolated environment** — no production data or credentials
2. Attempt token passthrough with token scoped for different audience
3. Verify rejection and logging of unauthorized attempts
4. Review source code for hardcoded secrets, `eval`, unrestricted file access
5. Run dependency scanner (Snyk, Dependabot, OSV)

### Step 4: Review data handling

| Question | Implication |
|----------|-------------|
| What data does it access? | Maps to classification tier |
| Where is data processed? | On-prem, cloud region, vendor infra — legal implications |
| Is data sent to a third party? | Requires DPA and legal review |
| Is data retained? | Retention period and deletion capability |
| Is data used for training? | Must be prohibited for enterprise data without consent |
| Customer data involved? | Privacy review + contractual protections |
| Regulated data involved? | HIPAA, GDPR, PCI — may prohibit third-party processing |

**Policy:** Third-party MCP servers must not process regulated data unless a data processing agreement (DPA) is in place and the vendor meets compliance requirements.

### Step 5: Assess operational risk

| Question | Consideration |
|----------|---------------|
| Can it write, delete, deploy, or send? | Determines tier (3–4) |
| Can actions be reversed? | Rollback for write actions |
| Rate limits available? | Prevents runaway agents |
| Monitoring / health checks? | Operational visibility |
| Incident response contact? | Vendor security email or maintainer |
| Unavailability impact? | Business continuity if server goes down |

### Step 6: Document outcome

| Outcome | Action |
|---------|--------|
| **Pass** | Proceed to approval workflow with findings attached |
| **Pass with conditions** | Approve with remediation (enable logging, reduce scope, internal fork) |
| **Fail** | Reject; document findings; notify requester |
| **Insufficient information** | Return questionnaire to vendor/maintainer; hold approval |

---

## Red Flags — Automatic Escalation or Reject

| Red flag | Typical action |
|----------|----------------|
| No commits in 6+ months + open security issues | Reject or require internal fork |
| Hardcoded credentials in source | Reject until remediated |
| Token passthrough confirmed | Reject for Tier 1+ |
| No authentication option | Reject for Tier 1+ |
| Anonymous maintainer, no disclosure process | Reject for Tier 2+ |
| License incompatible with enterprise use | Legal review; likely reject |
| Undocumented tools discovered in testing | Reject per [OWASP MCP05](https://owasp.org/www-project-mcp-top-10/) |
| Data sent to vendor cloud without DPA | Hold until legal completes |

---

## Open-Source Specific Guidance

Open-source MCP servers require **additional** scrutiny beyond commercial vendors:

1. **Review the source code** — do not trust popularity alone. Read the implementation of auth, logging, and tool handlers.
2. **Check dependency tree** — `npm audit`, `pip audit`, or equivalent on all transitive dependencies.
3. **Prefer internal forks** — maintain an internal fork with controlled updates and your own security patches.
4. **Pin versions** — never use `latest` or floating tags in production. Document exact version in risk register.
5. **Monitor upstream** — subscribe to GitHub security advisories, RSS, or OSV alerts for the project.
6. **Contribute fixes** — if you find issues, contribute patches upstream or maintain private fork.
7. **Assume no SLA** — community projects have no uptime or incident response guarantee; plan accordingly.

### Internal fork strategy

| Approach | When to use |
|----------|-------------|
| Direct OSS use | Tier 0–1, well-maintained, full code review completed |
| Internal fork | Tier 2+; need controlled updates and patch management |
| Wrap with proxy | OSS lacks logging; your proxy adds audit trail |
| Reject | Cannot meet controls; no resources to fork and maintain |

---

## Commercial Vendor Considerations

| Requirement | Document to request |
|-------------|-------------------|
| Security certifications | SOC 2 Type II, ISO 27001 |
| Data processing agreement | DPA with subprocessors listed |
| Breach notification | SLA for notification (e.g., 72 hours) |
| Audit rights | Right to assess or receive pen test results |
| Data residency | Where data is processed and stored |
| AI/training use | Confirmation data is not used for model training |
| Incident contact | security@vendor.com or equivalent |
| SLA and support | Uptime, support response times |

Procurement owns contractual review; AppSec owns technical control verification.

---

## Worked Example: Community GitHub MCP

**Request:** Engineering wants `@community/github-mcp` from npm for PR automation.

| Review area | Finding | Result |
|-------------|---------|--------|
| Maintainer | Single contributor, last commit 4 months ago | Yellow |
| Dependencies | 2 transitive deps with medium CVEs | Yellow |
| Auth | OAuth supported; audience validation implemented | Green |
| Logging | No MCP-level logging; GitHub audit only | Yellow |
| Token passthrough | Not observed in testing | Green |
| Data | Internal source code | Tier 2–3 |

**Outcome:** Pass with conditions

- Internal fork required within 30 days
- MCP-level logging proxy before Tier 3 production use
- Pin version v2.1.0; no auto-update
- Re-review in 6 months

---

## References

| Source | Relevance |
|--------|-----------|
| [MCP Authorization Specification](https://spec.modelcontextprotocol.io/specification/2025-03-26/basic/authorization/) | Audience validation requirement |
| [OWASP MCP06](https://owasp.org/www-project-mcp-top-10/) | Supply chain risk |
| [Vendor Questionnaire](../templates/vendor-questionnaire.md) | Standardized capture |
| [Chapter 7 — Approval Workflow](07-approval-workflow.md) | Stage 3 integration |
| [Chapter 8 — RACI](08-risk-ownership-raci.md) | Procurement + AppSec roles |

---

## Practitioner Checklist

- [ ] Third-party review required for all external MCP at Tier 2+
- [ ] Vendor Questionnaire completed and filed for each external server
- [ ] Token audience validation verified (no passthrough)
- [ ] Data handling reviewed by legal/privacy if sensitive data involved
- [ ] SBOM or dependency analysis performed for OSS
- [ ] Source code reviewed for OSS servers (not just README)
- [ ] Version pinned and update process defined
- [ ] Vendor/maintainer incident contact documented
- [ ] Review outcome recorded in approval decision

---

**Next:** [Chapter 10 — Minimum Security Baseline](10-minimum-security-baseline.md) defines required controls by tier and provides sample policy language.
