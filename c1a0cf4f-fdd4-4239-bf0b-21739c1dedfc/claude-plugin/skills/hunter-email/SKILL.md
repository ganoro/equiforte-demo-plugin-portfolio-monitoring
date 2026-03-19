---
description: "Email intelligence and lead enrichment skill powered by Hunter.io API — find professional email addresses by domain or name, verify email deliverability, enrich contacts and companies, discover target companies, and manage lead lists. Use this skill whenever a user mentions Hunter, email lookup, email finder, email verification, domain search for emails, contact enrichment, company enrichment, lead prospecting, email deliverability check, find someone's email, verify an email address, or build a prospect list. Also triggers on: 'find emails at [company]', 'verify this email', 'enrich this contact', 'who works at [domain]', 'get emails for [company]', 'look up email for [name]', 'check if email is valid', 'find decision makers at', or any B2B lead generation and outreach research task."
---


# Hunter API (Simple Spec)

## Base URL

```
https://api.hunter.io/v2
```

## Auth

* Pass API key as query param:

```
?api_key=e8008da94a1be08d315c874e308e888cbe0f8d16
```

---

# 1. Discover Companies

### POST `/discover`

### Purpose

Search companies using filters or natural language.

### Request

```json
{
  "query": "Companies in Europe that specialize in software development"
}
```

OR

```json
{
  "organization": {
    "domain": ["hunter.io"]
  }
}
```

### Response (simplified)

```json
{
  "data": [
    {
      "domain": "hunter.io",
      "organization": "Hunter",
      "emails_count": {
        "total": 28
      }
    }
  ],
  "meta": {
    "results": 1
  }
}
```

---

# 2. Domain Search (List Emails)

### GET `/domain-search`

### Purpose

Get emails for a company/domain.

### Required

* `domain` OR `company` (domain preferred)

### Request

```
GET /domain-search?domain=intercom.com&api_key=KEY
```

### Optional Filters

* `limit` (default 10, max 100)
* `offset`
* `type` = `personal | generic`
* `seniority` = `junior | senior | executive`
* `department` = `sales, marketing, it, ...`
* `verification_status` = `valid | accept_all | unknown`

### Response (simplified)

```json
{
  "data": {
    "domain": "intercom.com",
    "organization": "Intercom",
    "emails": [
      {
        "value": "name@intercom.com",
        "type": "personal",
        "confidence": 92,
        "first_name": "Ciaran",
        "last_name": "Lee",
        "position": "Support Engineer",
        "verification": {
          "status": "valid"
        }
      }
    ]
  }
}
```

---

# 3. Email Finder

### GET `/email-finder`

### Purpose

Find a specific person’s email.

### Required

* One of: `domain | company | linkedin_handle`
* AND name:

  * `first_name + last_name` OR `full_name`

### Request

```
GET /email-finder?domain=reddit.com&first_name=Alexis&last_name=Ohanian&api_key=KEY
```

### Response

```json
{
  "data": {
    "email": "alexis@reddit.com",
    "score": 97,
    "position": "Cofounder",
    "company": "Reddit",
    "verification": {
      "status": "valid"
    }
  }
}
```

---

# 4. Email Verifier

### GET `/email-verifier`

### Purpose

Check if an email is deliverable.

### Request

```
GET /email-verifier?email=test@company.com&api_key=KEY
```

### Response

```json
{
  "data": {
    "email": "test@company.com",
    "status": "valid",
    "score": 100
  }
}
```

### Status Values

* `valid`
* `invalid`
* `accept_all`
* `webmail`
* `disposable`
* `unknown`

### Async Case

* `202` → still processing → retry same request

---

# 5. Email Enrichment

### GET `/people/find`

### Purpose

Get full profile from email or LinkedIn.

### Required

* `email` OR `linkedin_handle`

### Request

```
GET /people/find?email=matt@hunter.io&api_key=KEY
```

### Response

```json
{
  "data": {
    "name": {
      "fullName": "Matthew Tharp"
    },
    "email": "matt@hunter.io",
    "location": "United States",
    "employment": {
      "name": "Hunter",
      "title": "CEO"
    },
    "linkedin": {
      "handle": "matttharp"
    }
  }
}
```

---

# Common Rules

### Pagination

* Use `limit` + `offset`

### Rate Limits

* ~15 req/sec (most endpoints)
* Email verifier: 10 req/sec

### Errors (common)

* `400` → bad params
* `401` → invalid API key
* `202` → processing (retry)
* `451` → data restricted (do not use)

---
