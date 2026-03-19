---
description: "Email intelligence and lead enrichment skill powered by Hunter.io MCP — find professional email addresses by domain or name, verify email deliverability, enrich contacts and companies, discover target companies, and manage lead lists. Use this skill whenever a user mentions Hunter, email lookup, email finder, email verification, domain search for emails, contact enrichment, company enrichment, lead prospecting, email deliverability check, find someone's email, verify an email address, or build a prospect list. Also triggers on: 'find emails at [company]', 'verify this email', 'enrich this contact', 'who works at [domain]', 'get emails for [company]', 'look up email for [name]', 'check if email is valid', 'find decision makers at', or any B2B lead generation and outreach research task."
---

# Hunter Email Intelligence

Use the Hunter.io MCP service to find, verify, and enrich professional email addresses and company data. This skill provides structured workflows for every Hunter MCP tool.

## MCP Server Configuration

The Hunter MCP server must be configured in your Claude settings before use:

```json
{
  "type": "mcp",
  "server_label": "hunter-remote-mcp",
  "server_url": "https://mcp.hunter.io/mcp",
  "require_approval": "never",
  "headers": { "X-API-KEY": "e8008da94a1be08d315c874e308e888cbe0f8d16" }
}
```

## Available MCP Tools

The Hunter MCP server exposes these tools via the `hunter-remote-mcp` server label. Always use the MCP tool calls — never construct raw HTTP requests.

| Tool | Purpose | Key Parameters |
|------|---------|---------------|
| **Domain Search** | Find all emails at a company domain | `domain`, `company`, `type`, `seniority`, `department`, `limit` |
| **Email Finder** | Find a specific person's email | `domain`/`company`/`linkedin_handle`, `first_name`, `last_name` |
| **Email Verifier** | Check if an email is valid/deliverable | `email` |
| **Email Count** | Count available emails for a domain | `domain`/`company`, `type` |
| **Discover** | Find companies matching criteria | `query`, `industry`, `headcount`, `headquarters_location`, `technology` |
| **Email Enrichment** | Get person data from email/LinkedIn | `email`/`linkedin_handle` |
| **Company Enrichment** | Get company data from domain | `domain` |
| **Combined Enrichment** | Get person + company data together | `email` |
| **Leads — List** | List saved leads with filters | `leads_list_id`, `email`, `company`, `query` |
| **Leads — Create** | Save a new lead | `email`, `first_name`, `last_name`, `company`, `leads_list_id` |
| **Leads — Update** | Update an existing lead | `id`, fields to update |
| **Leads — Delete** | Remove a lead | `id` |
| **Leads Lists — List** | List all lead lists | `limit`, `offset` |
| **Leads Lists — Create** | Create a new lead list | `name` |
| **Account** | Check API usage and plan limits | — |

---

## Workflow 1 — Domain Search (Find All Emails at a Company)

Use when the user asks: "Find emails at [company]", "Who works at [domain]?", "Get contacts at [company]"

### Steps

1. **Call Domain Search** with the company domain. If only a company name is provided (no domain), pass the `company` parameter instead.
   - Set `limit` to control result count (default: 10, max: 100)
   - Optionally filter by `department` (executive, it, finance, management, communication, support, legal, hr, marketing, sales, engineering)
   - Optionally filter by `seniority` (junior, senior, executive)
   - Optionally filter by `type` (personal or generic)

2. **Parse the response** and extract for each email:
   - Email address
   - First name, last name
   - Position / job title
   - Department and seniority
   - Confidence score (0–100)
   - Verification status (valid, invalid, accept_all, webmail, unknown)
   - Sources (where the email was found)

3. **Present results** in a structured table:

| # | Name | Email | Position | Department | Confidence | Verified |
|---|------|-------|----------|------------|------------|----------|
| 1 | Jane Smith | jane@acme.com | VP Sales | sales | 95 | valid |
| 2 | John Doe | john@acme.com | CTO | engineering | 91 | valid |

4. **Summarize** below the table:
   - Total emails found vs. total available (from `email-count`)
   - Breakdown by department and seniority
   - Average confidence score
   - Verification status distribution

---

## Workflow 2 — Email Finder (Find a Specific Person's Email)

Use when the user asks: "Find email for [name] at [company]", "What's [person]'s work email?"

### Steps

1. **Call Email Finder** with:
   - `domain` (preferred) or `company` name or `linkedin_handle`
   - `first_name` and `last_name` (or `full_name`)

2. **Parse the response**:
   - Email address found
   - Confidence score (0–100)
   - Position and company
   - LinkedIn URL, Twitter handle, phone number (if available)
   - Verification status
   - Sources with URLs

3. **Present the result**:

| Field | Value |
|-------|-------|
| Email | jane.smith@acme.com |
| Confidence | 95/100 |
| Status | valid |
| Position | VP of Sales |
| Company | Acme Corp |
| LinkedIn | linkedin.com/in/janesmith |
| Sources | 3 public sources |

4. **Confidence guidance**:
   - **90–100**: High confidence — safe to use for outreach
   - **70–89**: Good confidence — consider verifying first
   - **Below 70**: Low confidence — verify before using

---

## Workflow 3 — Email Verification

Use when the user asks: "Is this email valid?", "Verify [email]", "Check deliverability"

### Steps

1. **Call Email Verifier** with the `email` parameter.

2. **Parse verification response**:
   - `status`: valid, invalid, accept_all, webmail, disposable, unknown
   - `score`: deliverability score (0–100)
   - `regexp`: syntax check passed
   - `gibberish`: email looks auto-generated
   - `disposable`: temporary/throwaway address
   - `webmail`: free email provider (Gmail, Yahoo, etc.)
   - `mx_records`: domain has mail servers
   - `smtp_server`: mail server responds
   - `smtp_check`: mailbox exists
   - `accept_all`: server accepts all addresses (catch-all)
   - `block`: email is on a blocklist
   - `sources`: number of public sources found

3. **Present the result**:

| Check | Result |
|-------|--------|
| Status | valid |
| Score | 95/100 |
| Syntax valid | Yes |
| MX records | Yes |
| SMTP server | Yes |
| Mailbox exists | Yes |
| Catch-all | No |
| Disposable | No |
| Webmail | No |
| Blocklisted | No |
| Public sources | 5 |

4. **Interpretation**:
   - **valid** (score >= 80): Email exists and is deliverable. Safe for outreach.
   - **accept_all**: Server accepts all emails — cannot confirm specific mailbox. Use with caution.
   - **webmail**: Personal email (Gmail, Yahoo). May not be appropriate for B2B outreach.
   - **disposable**: Temporary address. Do not use.
   - **invalid**: Email does not exist. Do not send.
   - **unknown**: Could not determine. Verify through alternative means.

---

## Workflow 4 — Contact & Company Enrichment

Use when the user asks: "Tell me about this person", "Enrich this contact", "Get company info for [domain]"

### Steps

1. **Choose the right enrichment endpoint**:
   - Person only → **Email Enrichment** (pass `email` or `linkedin_handle`)
   - Company only → **Company Enrichment** (pass `domain`)
   - Both → **Combined Enrichment** (pass `email`)

2. **For person enrichment**, extract:

| Field | Description |
|-------|-------------|
| Full name | First + last name |
| Email | Primary email |
| Location | City, state, country |
| Current role | Title, company, start date |
| LinkedIn | Profile URL |
| Twitter | Handle |
| Phone | If available |
| Previous roles | Employment history |

3. **For company enrichment**, extract:

| Field | Description |
|-------|-------------|
| Company name | Legal / display name |
| Domain | Primary website |
| Industry | Sector classification |
| Description | Company overview |
| Headcount | Employee range |
| Founded | Year established |
| Headquarters | Full address |
| Technologies | Tech stack detected |
| Funding | Total raised, last round |
| Social profiles | LinkedIn, Twitter, Facebook |

4. **Present findings** in structured sections with clear labels.

---

## Workflow 5 — Company Discovery

Use when the user asks: "Find companies like [company]", "Find SaaS companies in [location]", "Companies using [technology]"

### Steps

1. **Call Discover** with filter criteria:
   - `query`: Free-text search
   - `organization`: Company name
   - `similar_to`: Domain of a company to find similar ones
   - `headquarters_location`: City, state, or country
   - `industry`: Industry classification
   - `headcount`: Employee count range (e.g., "11-50", "51-200")
   - `company_type`: public, private, nonprofit, etc.
   - `year_founded`: Founding year range
   - `keywords`: Descriptive keywords
   - `technology`: Technologies used (e.g., "Salesforce", "React")
   - `funding`: Funding range

2. **Parse results** into a discovery table:

| # | Company | Domain | Industry | Headcount | Location | Emails Available |
|---|---------|--------|----------|-----------|----------|-----------------|
| 1 | Acme Corp | acme.com | SaaS | 51-200 | SF, CA | 142 |
| 2 | Beta Inc | beta.io | SaaS | 11-50 | NYC, NY | 38 |

3. **Follow-up options**: Offer to drill into any company with Domain Search or Company Enrichment.

---

## Workflow 6 — Lead Management

Use when the user asks: "Save these leads", "Add to my lead list", "Create a prospect list"

### Steps

1. **List existing lead lists** using Leads Lists — List to check for duplicates.

2. **Create a new list** if needed using Leads Lists — Create with a descriptive `name`.

3. **Add leads** using Leads — Create for each contact:
   - Required: `email`
   - Recommended: `first_name`, `last_name`, `position`, `company`, `website`
   - Optional: `linkedin_url`, `phone_number`, `twitter`, `notes`, `source`
   - Assign to list: `leads_list_id`

4. **Present confirmation**:

| # | Name | Email | Company | List | Status |
|---|------|-------|---------|------|--------|
| 1 | Jane Smith | jane@acme.com | Acme Corp | Q1 Prospects | Added |
| 2 | John Doe | john@beta.io | Beta Inc | Q1 Prospects | Added |

---

## Workflow 7 — Bulk Prospecting Pipeline

Use when the user asks: "Build a prospect list for [criteria]", "Find decision makers at companies like [X]"

### Steps

1. **Discover companies** matching target criteria (Workflow 5)
2. **Domain search** each company for relevant contacts (Workflow 1), filtering by `seniority` and `department`
3. **Verify** top prospect emails (Workflow 3)
4. **Enrich** key contacts (Workflow 4)
5. **Save** verified prospects to a lead list (Workflow 6)
6. **Present the pipeline summary**:

| Metric | Count |
|--------|-------|
| Companies discovered | 25 |
| Contacts found | 87 |
| Emails verified (valid) | 62 |
| Contacts enriched | 15 |
| Leads saved | 62 |

---

## Rate Limits & Usage

| Endpoint | Rate Limit |
|----------|-----------|
| Domain Search | 15 req/sec, 500 req/min |
| Email Finder | 15 req/sec, 500 req/min |
| Email Verifier | 15 req/sec, 500 req/min |
| Enrichment | 15 req/sec, 500 req/min |
| Discover | 15 req/sec, 500 req/min |

**Check account usage** before large batch operations by calling the Account tool. This returns your plan limits and current consumption.

---

## Critical Rules

1. **Always use MCP tool calls** — never construct raw API URLs or use curl/fetch. The MCP server handles authentication via the configured `X-API-KEY` header.
2. **Respect confidence scores** — clearly communicate score meaning to the user. Never present a low-confidence email (< 70) without a warning.
3. **Verify before outreach** — always recommend or perform email verification before the user sends emails, especially for email-finder results with confidence < 90.
4. **Label verification status** — every email presented must include its verification status (valid/invalid/accept_all/unknown). Never omit this.
5. **Handle errors gracefully** — if Hunter returns no results or an error, inform the user clearly and suggest alternatives (different domain spelling, company name, LinkedIn handle).
6. **Rate limit awareness** — for bulk operations (> 50 lookups), pace requests and inform the user of expected duration. Check account limits first.
7. **Never fabricate emails** — if Hunter returns no result, say so. Do not guess email patterns or construct emails manually.
8. **Privacy and compliance** — remind users that email data should be used in compliance with applicable laws (GDPR, CAN-SPAM, etc.) when performing bulk lookups or building outreach lists.
9. **Prefer domain over company name** — when both are available, use `domain` as the primary identifier; it produces more accurate results.
10. **Present sources** — when Hunter provides source URLs for found emails, include them so the user can verify provenance.
