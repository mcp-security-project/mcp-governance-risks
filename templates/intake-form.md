# MCP Server Intake Form

**Instructions:** Complete this form before connecting any MCP server to enterprise AI systems. Submit to your AppSec team or MCP governance portal. Incomplete forms will be returned.

---

## Request Information

| Field | Value |
|-------|-------|
| **Date submitted** | |
| **Submitted by** | |
| **Requesting team** | |
| **Business owner** | |

## MCP Server Details

| Field | Value |
|-------|-------|
| **MCP server name** | |
| **Display name** | |
| **Version / commit** | |
| **Source / vendor** | [ ] Internal  [ ] Open-source  [ ] Commercial  [ ] Community |
| **Repository URL** (if applicable) | |
| **Deployment location** | [ ] Developer laptop  [ ] Internal network  [ ] Cloud (specify)  [ ] Vendor SaaS |

## Business Justification

| Field | Value |
|-------|-------|
| **Use case** | |
| **Business criticality** | [ ] Low  [ ] Medium  [ ] High  [ ] Critical |
| **Expected users** | |
| **Expected user count** | |
| **Alternative considered** | (Why is MCP needed vs. direct integration?) |

## Technical Details

| Field | Value |
|-------|-------|
| **Authentication model** | [ ] None  [ ] API key  [ ] OAuth 2.1  [ ] SSO  [ ] Other: ___ |
| **Identity used** | [ ] User OAuth  [ ] Service account  [ ] Shared credential  [ ] Other: ___ |

### Tools Exposed

List every tool the MCP server exposes:

| Tool Name | Action Type | Target System | Data Accessed |
|-----------|-------------|---------------|---------------|
| | [ ] Read  [ ] Write  [ ] Delete  [ ] Execute  [ ] Admin | | |
| | [ ] Read  [ ] Write  [ ] Delete  [ ] Execute  [ ] Admin | | |
| | [ ] Read  [ ] Write  [ ] Delete  [ ] Execute  [ ] Admin | | |
| | [ ] Read  [ ] Write  [ ] Delete  [ ] Execute  [ ] Admin | | |

### Data Access

| Field | Value |
|-------|-------|
| **Data types accessed** | |
| **Data classification** | [ ] Public  [ ] Internal  [ ] Confidential  [ ] Regulated |
| **Regulated data involved?** | [ ] No  [ ] Yes — specify: ___ |
| **Customer data involved?** | [ ] No  [ ] Yes |
| **Data sent to third party?** | [ ] No  [ ] Yes — specify: ___ |

## Security Self-Assessment

| Question | Yes | No | N/A |
|----------|-----|-----|-----|
| Does the server support scoped authorization? | | | |
| Does it avoid token passthrough? | | | |
| Does it validate token audience? | | | |
| Are secrets stored securely (no hardcoded credentials)? | | | |
| Does it provide audit logging? | | | |
| Does it restrict network egress? | | | |
| Does it avoid unsafe shell execution? | | | |

## Additional Information

| Field | Value |
|-------|-------|
| **Known risks or concerns** | |
| **Requested deployment date** | |
| **Pilot or full deployment?** | [ ] Pilot  [ ] Full |

---

**For AppSec use only (do not complete):**

| Field | Value |
|-------|-------|
| Intake received date | |
| Assigned reviewer | |
| Initial tier assessment | |
| Review status | [ ] In review  [ ] Complete |
