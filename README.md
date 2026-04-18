# Robota.ua Scraper

Extract structured data from [robota.ua](https://robota.ua) — robota.ua job listings with salary, company, skills, and contact data. Supports keyword search, city/category filters, incremental tracking, and compact output for AI agents.

**[Robota.ua Scraper - Ukraine Job Listings on Apify →](https://apify.com/blackfalcondata/robota-ua-scraper?fpr=1h3gvi)**

---

## Key features





**Search with filters** — Search by keyword and location.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 5.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases





**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from robota.ua on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from robota.ua.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on robota.ua to inform pricing decisions, hiring plans, or candidate negotiations.

**Lead generation**
Extract employer contact details alongside listings to build outreach lists for recruiters, staffing agencies, or B2B sales teams.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "developer",
  "maxResults": 50,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Job search keywords (e.g. 'developer', 'marketing manager'). Use JSON array for multi-query: ["python", "javascript"]. |
| `cityId` | integer | — | Filter by city. Common IDs: 1 = Kyiv, 2 = Odesa, 3 = Dnipro, 4 = Kharkiv, 5 = Lviv. Full list: GET https://api.robota.ua/dictionary/city |
| `rubricIds` | array | — | Filter by job category. JSON array of rubric IDs. Full list: GET https://api.robota.ua/dictionary/rubric |
| `scheduleId` | integer | — | Filter by work schedule. IDs: 1=Full-time, 2=Part-time, 3=Remote, 4=Internship, 5=Project, 6=Seasonal, 7=Shift work, 8=Hybrid, 9=Office. |
| `salary` | integer | — | Filter jobs with salary at or above this amount in Ukrainian hryvnia. |
| `experienceIds` | array | — | Filter by experience. JSON array. IDs: 4 = No experience, 5 = Up to 1 year, 1 = 1-2 years, 2 = 2-5 years, 3 = 5+ years. |
| `maxResults` | integer | `25` | Maximum total job listings to return (0 = unlimited). |
| `maxPages` | integer | `5` | Maximum search result pages to fetch per query. |
| `includeDetails` | boolean | `true` | Fetch each job's detail page for full description, skills, contact info, and company data. |
| `descriptionMaxLength` | integer | `0` | Truncate description to this many characters. 0 = no truncation. |
| `compact` | boolean | `false` | Output only core fields (jobId, title, company, location, salary, employmentType, isRemote, portalUrl, postedDate). Ideal for AI-agent and MCP workflows. |
| `incrementalMode` | boolean | `false` | Track changes across runs. Only emits NEW and UPDATED jobs. Requires stateKey. |
| `stateKey` | string | — | Stable identifier for the tracked search universe (e.g. 'kyiv-developer'). |
| `emitUnchanged` | boolean | `false` | In incremental mode, also emit records that haven't changed since last run. |
| `emitExpired` | boolean | `false` | In incremental mode, emit records no longer found in search results. |

---

## FAQ

<!-- WRITE: 4-6 Q&A pairs relevant to this product -->

**Is it legal to scrape robota.ua?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check the target site's terms of service for your specific use case.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

---

## Known limitations

<!-- WRITE: 4-6 honest limitations -->

- <!-- WRITE: limitation 1 -->
- <!-- WRITE: limitation 2 -->


## Output fields

Every listing returns the same 42-field schema. Missing values are `null` — never omitted.

- `jobId`
- `jobKey`
- `title`
- `company`
- `companyId`
- `companyUrl`
- `companyVerified`
- `isAgency`
- `location`
- `cityId`
- `cityName`
- `districtName`
- `metroName`
- `address`
- `latitude`
- `longitude`
- `salaryMin`
- `salaryMax`
- `salaryComment`
- `salaryCurrency`
- `description`
- `descriptionHtml`
- `descriptionLength`
- `shortDescription`
- `employmentType`
- `experienceLevel`
- `industry`
- `isRemote`
- `isHot`
- `skills`
- `badges`
- `contactPerson`
- `contactPhone`
- `contactEmail`
- `applyUrl`
- `postedDate`
- `portalUrl`
- `source`
- `scrapedAt`
- `searchQuery`
- `detailFetched`
- `contentQuality`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "3d7734eabf8fcf72f07d61df89b23eb5b6fc031af366464d8ba9bcc4fb7fd691",
  "jobKey": "11046596",
  "title": "Middle Fullstack (Java + Angular) developer",
  "company": "Агропросперіс",
  "companyId": 2451400,
  "companyUrl": "http://www.agroprosperis.com/",
  "companyVerified": true,
  "isAgency": false,
  "location": "Киев",
  "cityId": 1,
  "cityName": "Киев",
  "districtName": null
}
```

*Truncated — full records contain 42 fields. See Output fields for the complete schema.*


**[Try Robota.ua Scraper - Ukraine Job Listings now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/robota-ua-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.002 |

See the [actor on Apify](https://apify.com/blackfalcondata/robota-ua-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data





- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal


## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---
---

*Last updated: 2026 03*
