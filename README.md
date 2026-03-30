# Robota.ua Scraper

Extract structured data from [robota.ua](https://robota.ua) — robota.ua job listings with salary, company, skills, and contact data. Supports keyword search, city/category filters, incremental tracking, and compact output for AI agents.

**[Robota.ua Scraper on Apify →](https://apify.com/blackfalcondata/robota-ua-scraper)**

---

## Key features



**Search with filters** — Search by keyword and location.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

---

## Use cases



**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from robota.ua on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from robota.ua.

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

---

## Related products by Black Falcon Data



- [StepStone Scraper](https://github.com/BlackFalconData-org/stepstone-scraper) — Job listings from 18 European portals
- [Indeed Job Scraper](https://github.com/BlackFalconData-org/indeed-job-scraper) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://github.com/BlackFalconData-org/glassdoor-job-scraper) — Glassdoor listings with company ratings

---

*Last updated: 2026 03*
