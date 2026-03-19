# Hunter.io API Reference

Complete parameter reference for all Hunter.io MCP tools. Use this when you need exact parameter names or want to understand response fields.

## Domain Search

**Purpose:** Find all email addresses associated with a company domain.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `domain` | Yes (or `company`) | Target domain (e.g., "stripe.com") |
| `company` | Yes (or `domain`) | Company name (e.g., "Stripe") |
| `limit` | No | Results per page (default: 10, max: 100) |
| `offset` | No | Pagination offset (default: 0) |
| `type` | No | `personal` or `generic` |
| `seniority` | No | `junior`, `senior`, or `executive` |
| `department` | No | See department list below |
| `required_field` | No | `full_name`, `position`, `phone_number` |
| `verification_status` | No | `valid`, `accept_all`, `webmail`, `unknown` |
| `location` | No | Geographic filter |
| `job_titles` | No | Filter by job title keywords |

**Departments:** executive, it, finance, management, communication, support, legal, hr, marketing, sales, engineering

**Response fields:** `emails[]` (email, type, confidence, first_name, last_name, position, seniority, department, linkedin, twitter, phone_number, verification.status, verification.date, sources[])

---

## Email Finder

**Purpose:** Find the most probable email for a specific person.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `domain` | One of domain/company/linkedin_handle | Target domain |
| `company` | One of domain/company/linkedin_handle | Company name |
| `linkedin_handle` | One of domain/company/linkedin_handle | LinkedIn profile handle |
| `first_name` | Yes (unless linkedin_handle) | Person's first name |
| `last_name` | Yes (unless linkedin_handle) | Person's last name |
| `full_name` | Alternative to first+last | Full name |
| `max_duration` | No | Max wait time in seconds |

**Response fields:** email, score, position, company, first_name, last_name, twitter, linkedin_url, phone_number, verification.status, verification.date, sources[]

---

## Email Verifier

**Purpose:** Verify an email address's deliverability.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `email` | Yes | Email address to verify |

**Response fields:** status (valid/invalid/accept_all/webmail/disposable/unknown), score, email, regexp, gibberish, disposable, webmail, mx_records, smtp_server, smtp_check, accept_all, block, sources

---

## Email Count

**Purpose:** Count available emails for a domain without consuming search credits.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `domain` | Yes (or `company`) | Target domain |
| `company` | Yes (or `domain`) | Company name |
| `type` | No | `personal` or `generic` |

**Response fields:** total, personal_emails, generic_emails, department[] (department, count), seniority[] (seniority, count)

---

## Discover (Company Search)

**Purpose:** Find companies matching criteria. Premium feature.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `query` | No | Free-text search |
| `organization` | No | Company name |
| `similar_to` | No | Domain to find similar companies |
| `headquarters_location` | No | Location filter |
| `industry` | No | Industry classification |
| `headcount` | No | Range: "1-10", "11-50", "51-200", "201-500", "501-1000", "1001-5000", "5001-10000", "10001+" |
| `company_type` | No | public, private, nonprofit |
| `year_founded` | No | Year range |
| `keywords` | No | Descriptive keywords |
| `technology` | No | Tech stack filter |
| `funding` | No | Funding range |
| `limit` | No | Max results (default: 10, max: 100) |
| `offset` | No | Pagination offset |

**Response fields:** companies[] (domain, name, industry, headcount, email_count, location, description)

---

## Email Enrichment (People Find)

**Purpose:** Get comprehensive person data from email or LinkedIn.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `email` | Yes (or `linkedin_handle`) | Email address |
| `linkedin_handle` | Yes (or `email`) | LinkedIn profile handle |

**Response fields:** first_name, last_name, email, location (city, state, country), employment (domain, company, title, start_date, end_date, current), linkedin, twitter, facebook, phone, timezone, activity_dates

---

## Company Enrichment

**Purpose:** Get comprehensive company data from domain.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `domain` | Yes | Company domain |

**Response fields:** name, domain, industry, description, headcount, year_founded, location (street, city, state, country, postal_code), metrics (raised, annual_revenue, employees_range), technologies[], social (linkedin, twitter, facebook), founders[], parent_domain

---

## Combined Enrichment

**Purpose:** Get person + company data in a single call.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `email` | Yes | Email address |

**Response fields:** person (same as Email Enrichment), company (same as Company Enrichment)

---

## Leads CRUD

### List Leads
**Parameters:** `leads_list_id`, `email`, `first_name`, `last_name`, `position`, `company`, `industry`, `website`, `country_code`, `company_size`, `source`, `verification_status[]`, `query`, `limit`, `offset`

### Create Lead
**Required:** `email`
**Optional:** `first_name`, `last_name`, `position`, `company`, `company_industry`, `company_size`, `confidence_score`, `website`, `country_code`, `linkedin_url`, `phone_number`, `twitter`, `notes`, `source`, `leads_list_id`, `leads_list_ids`

### Update Lead
**Parameters:** `id` (required) + any fields from Create

### Delete Lead
**Parameters:** `id` (required)

---

## Leads Lists CRUD

### List All Lists
**Parameters:** `limit`, `offset`

### Create List
**Parameters:** `name` (required)

### Update List
**Parameters:** `id` (required), `name` (required)

### Delete List
**Parameters:** `id` (required)

---

## Account Information

**Purpose:** Check plan limits and current usage.

**Parameters:** None

**Response fields:** email, first_name, last_name, plan_name, plan_level, reset_date, team_id, calls (used, available — broken down by type: searches, verifications, email_count)
