---
name: ycombinator-skills
description: Search 5,886 Y Combinator startups across 49 batches (2005–2026). Filter by industry, region, batch, status, team size, hiring status, and more.
---

# Y Combinator Startup Search API

## Base URL

```
https://45bwzj1sgc-dsn.algolia.net/1/indexes/*/queries
```

All requests are `POST` with `Content-Type: application/json`. The following query parameters are **required** on every request:

| Query Param                | Value                                                                                                                                                                                                                                                              |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `x-algolia-agent`          | `Algolia for JavaScript (3.35.1); Browser; JS Helper (3.16.1)`                                                                                                                                                                                                     |
| `x-algolia-application-id` | `45BWZJ1SGC`                                                                                                                                                                                                                                                       |
| `x-algolia-api-key`        | `NzllNTY5MzJiZGM2OTY2ZTQwMDEzOTNhYWZiZGRjODlhYzVkNjBmOGRjNzJiMWM4ZTU0ZDlhYTZjOTJiMjlhMWFuYWx5dGljc1RhZ3M9eWNkYyZyZXN0cmljdEluZGljZXM9WUNDb21wYW55X3Byb2R1Y3Rpb24lMkNZQ0NvbXBhbnlfQnlfTGF1bmNoX0RhdGVfcHJvZHVjdGlvbiZ0YWdGaWx0ZXJzPSU1QiUyMnljZGNfcHVibGljJTIyJTVE` |

URL-encode the `x-algolia-api-key` value. The key is pre-scoped to `YCCompany_production` and `YCCompany_By_Launch_Date_production` indexes with the `ycdc_public` tag filter — no additional auth needed.

---

## Indexes

Two indexes covering the same 5,886 companies. Choose based on sort order:

| Index                                 | Sort                         | Use When                                                          |
| ------------------------------------- | ---------------------------- | ----------------------------------------------------------------- |
| `YCCompany_production`                | Relevance (text match)       | Searching by name, keyword, filtering by batch/industry/region    |
| `YCCompany_By_Launch_Date_production` | Chronological (newest first) | "Most recent YC startups", "launched this year", timeline queries |

Both indexes have identical fields and support identical query parameters.

---

## Request Format

POST a JSON body with a `requests` array. Each request object targets one index:

```json
{
  "requests": [
    {
      "indexName": "YCCompany_production",
      "params": "query=<search>&hitsPerPage=<n>&page=<n>&facetFilters=%5B<filters>%5D&numericFilters=<filters>"
    }
  ]
}
```

The `params` string uses URL-encoded Algolia query syntax. All parameters are optional.

### Full Query Parameters

| Parameter        | Type       | Default          | Description                                                                             |
| ---------------- | ---------- | ---------------- | --------------------------------------------------------------------------------------- |
| `query`          | string     | `""` (match all) | Full-text search across `name`, `one_liner`, `long_description`, `tags`, `former_names` |
| `hitsPerPage`    | integer    | `20`             | Results per page. Max `100`                                                             |
| `page`           | integer    | `0`              | Page number (0-indexed)                                                                 |
| `facetFilters`   | JSON array | `[]`             | Filter by facet values. URL-encoded. See Facet Filters section                          |
| `numericFilters` | string     | none             | Filter by numeric fields. e.g. `team_size>=50`, `team_size:10 TO 100`                   |
| `facets`         | JSON array | none             | Request facet counts in response. e.g. `["batch","industries","regions","top_company"]` |

### Facet Filters

Format: URL-encoded JSON array. Each element is either:

- `"facetName:value"` — include only matches (AND within array, OR across arrays)
- `["facetName:value1", "facetName:value2"]` — OR within inner array

Examples (shown decoded; URL-encode before sending):

- Single: `["batch:Summer 2024"]`
- Multiple AND: `["batch:Summer 2024", "industries:Fintech"]`
- OR: `[["batch:Summer 2024", "batch:Summer 2023"]]`
- Negative: `["top_company:true", "isHiring:true"]`

String values with spaces or special chars must be URL-encoded. The full params string must be URL-encoded.

---

## Response Schema

```json
{
  "results": [
    {
      "hits": [
        {
          "id": 271,
          "objectID": "271",
          "name": "Airbnb",
          "slug": "airbnb",
          "former_names": [],
          "website": "http://airbnb.com",
          "all_locations": "San Francisco, CA, USA",
          "one_liner": "Book accommodations around the world.",
          "long_description": "Founded in August of 2008...",
          "team_size": 6132,
          "industry": "Consumer",
          "subindustry": "Consumer -> Travel, Leisure and Tourism",
          "industries": ["Consumer", "Travel, Leisure and Tourism"],
          "regions": ["United States of America", "America / Canada"],
          "tags": ["Marketplace", "Travel"],
          "batch": "Winter 2009",
          "status": "Public",
          "stage": "Growth",
          "top_company": true,
          "isHiring": false,
          "nonprofit": false,
          "launched_at": 1326790856,
          "small_logo_thumb_url": "https://bookface-images.s3.amazonaws.com/small_logos/...",
          "app_video_public": false,
          "demo_day_video_public": false,
          "app_answers": null,
          "question_answers": false,
          "tags_highlighted": [],
          "_highlightResult": {}
        }
      ],
      "nbHits": 5886,
      "page": 0,
      "nbPages": 295,
      "hitsPerPage": 20,
      "facets": {},
      "query": "airbnb",
      "index": "YCCompany_production",
      "params": "...",
      "processingTimeMS": 3
    }
  ]
}
```

### Field Reference

| Field                   | Type    | Description                                       |
| ----------------------- | ------- | ------------------------------------------------- |
| `id`                    | integer | Unique company ID                                 |
| `name`                  | string  | Company name                                      |
| `slug`                  | string  | URL-safe name for ycombinator.com/launches/{slug} |
| `former_names`          | array   | Previous company names                            |
| `website`               | string  | Company website URL                               |
| `all_locations`         | string  | Primary location (city, region, country)          |
| `one_liner`             | string  | One-sentence pitch                                |
| `long_description`      | string  | Full company description                          |
| `team_size`             | integer | Number of employees                               |
| `industry`              | string  | Primary industry (broad category)                 |
| `subindustry`           | string  | Industry → Subindustry path                       |
| `industries`            | array   | All industry classifications                      |
| `regions`               | array   | Geographic regions                                |
| `tags`                  | array   | Technology and business model tags                |
| `batch`                 | string  | YC batch name (e.g. "Summer 2024")                |
| `status`                | string  | `Active` / `Inactive` / `Acquired` / `Public`     |
| `stage`                 | string  | `Growth` / `Early` / etc.                         |
| `top_company`           | boolean | YC top company designation                        |
| `isHiring`              | boolean | Currently hiring (self-reported)                  |
| `nonprofit`             | boolean | Nonprofit organization                            |
| `launched_at`           | integer | Unix timestamp of launch/public date              |
| `small_logo_thumb_url`  | string  | Logo image URL                                    |
| `app_video_public`      | boolean | Has public application video                      |
| `demo_day_video_public` | boolean | Has public Demo Day video                         |

### Note: No Founder Data

The public Algolia API does not expose founder names or bios. The `app_answers` field (which would contain YC application data) is `null` in all public records. For founder details, visit `https://www.ycombinator.com/launches/{slug}` directly.

---

## Facets and Canonical Values

### Batch Names

Exact strings for `facetFilters`:

Summer 2005 through Summer 2026 (every summer), Winter 2006 through Winter 2026 (every winter), plus `Unspecified`.

Full list: `Summer 2005`, `Summer 2006`, `Summer 2007`, `Summer 2008`, `Summer 2009`, `Summer 2010`, `Summer 2011`, `Summer 2012`, `Summer 2013`, `Summer 2014`, `Summer 2015`, `Summer 2016`, `Summer 2017`, `Summer 2018`, `Summer 2019`, `Summer 2020`, `Summer 2021`, `Summer 2022`, `Summer 2023`, `Summer 2024`, `Summer 2025`, `Summer 2026`, `Winter 2006`, `Winter 2007`, `Winter 2008`, `Winter 2009`, `Winter 2010`, `Winter 2011`, `Winter 2012`, `Winter 2013`, `Winter 2014`, `Winter 2015`, `Winter 2016`, `Winter 2017`, `Winter 2018`, `Winter 2019`, `Winter 2020`, `Winter 2021`, `Winter 2022`, `Winter 2023`, `Winter 2024`, `Winter 2025`, `Winter 2026`, `Fall 2024`, `Fall 2025`, `Fall 2026`, `Spring 2025`, `Spring 2026`, `Unspecified`

### Industries (73 values)

`B2B`, `Consumer`, `Healthcare`, `Fintech`, `Engineering, Product and Design`, `Industrials`, `Infrastructure`, `Productivity`, `Marketing`, `Real Estate and Construction`, `Operations`, `Healthcare IT`, `Sales`, `Finance and Accounting`, `Retail`, `Supply Chain and Logistics`, `Analytics`, `Education`, `Home and Personal`, `Payments`, `Consumer Health and Wellness`, `Content`, `Security`, `Social`, `Manufacturing and Robotics`, `Food and Beverage`, `Consumer Finance`, `Human Resources`, `Housing and Real Estate`, `Credit and Lending`, `Recruiting and Talent`, `Gaming`, `Healthcare Services`, `Banking and Exchange`, `Therapeutics`, `Aviation and Space`, `Insurance`, `Diagnostics`, `Legal`, `Drug Discovery and Delivery`, `Asset Management`, `Climate`, `Apparel and Cosmetics`, `Construction`, `Energy`, `Consumer Electronics`, `Medical Devices`, `Government`, `Travel, Leisure and Tourism`, `Industrial Bio`, `Agriculture`, `Transportation Services`, `Office Management`, `Automotive`, `Drones`, `Job and Career Services`, `Virtual and Augmented Reality`, `Unspecified`, `Defense`

Additional: `Travel, Leisure and Tourism`, `Food and Beverage`, `Consumer -> Travel, Leisure and Tourism` etc. — use `subindustry` for granular filtering.

### Regions (100+ values)

Key regions: `America / Canada`, `United States of America`, `Remote`, `Partly Remote`, `Fully Remote`, `Europe`, `South Asia`, `Latin America`, `India`, `United Kingdom`, `Canada`, `Southeast Asia`, `Mexico`, `Africa`, `Middle East and North Africa`, `France`, `Nigeria`, `Singapore`, `Brazil`, `Germany`, and many more country-level values.

To get the full current region list, run a query with `facets=["regions"]`.

### Status Values

`Active` (4,051), `Inactive` (1,034), `Acquired` (778), `Public` (23)

### Additional Facets

| Facet             | Values                                     |
| ----------------- | ------------------------------------------ |
| `top_company`     | `true` (91), `false` (5,794)               |
| `isHiring`        | `true` (1,458), `false` (4,428)            |
| `nonprofit`       | `true` (42), `false` (5,844)               |
| `highlight_black` | `true` / `false` — Black-founded startups  |
| `highlight_latam` | `true` / `false` — Latin American startups |
| `highlight_women` | `true` / `false` — Women-founded startups  |

---

## Presentation Rules

When displaying results to users:

1. **Hyperlink company names** using `[name](website)` — never display raw URLs
2. **Show the one_liner** as a subtitle beneath each company name
3. **Show batch** badge for temporal context
4. **Show industry** and **team_size** as metadata
5. **Show status** only when `Acquired` or `Public`
6. **Show tags** as inline chips/badges
7. **Truncate long_description** to 2-3 sentences in lists; show full only when user requests detail
8. **Link to YC page**: `https://www.ycombinator.com/launches/{slug}` for more details
9. **For facet counts**, round to nearest whole number

Example display format:

> **Airbnb** — Book accommodations around the world.
> Batch W09 | Consumer · Travel | 6,132 employees | Public
> Tags: Marketplace, Travel
> [Website](http://airbnb.com) · [YC Page](https://www.ycombinator.com/launches/airbnb)

---

## Workflow Examples

### "Find Stripe in YC"

```bash
curl -s '<BASE_URL>?x-algolia-agent=...&x-algolia-application-id=45BWZJ1SGC&x-algolia-api-key=...' \
  -H 'Content-Type: application/json' \
  -d '{"requests":[{"indexName":"YCCompany_production","params":"query=stripe&hitsPerPage=3"}]}'
```

### "Show me YC Summer 2024 startups"

```bash
curl ... -d '{"requests":[{"indexName":"YCCompany_production","params":"query=&hitsPerPage=30&facetFilters=%5B%22batch%3ASummer%202024%22%5D"}]}'
```

### "Find fintech startups from recent batches"

```bash
curl ... -d '{"requests":[{"indexName":"YCCompany_production","params":"query=&hitsPerPage=20&facetFilters=%5B%22industries%3AFintech%22%5D"}]}'
```

### "AI startups in YC Winter 2024"

```bash
curl ... -d '{"requests":[{"indexName":"YCCompany_production","params":"query=AI&hitsPerPage=20&facetFilters=%5B%22batch%3AWinter%202024%22%5D"}]}'
```

### "Top YC companies that are hiring"

```bash
curl ... -d '{"requests":[{"indexName":"YCCompany_production","params":"query=&hitsPerPage=30&facetFilters=%5B%22top_company%3Atrue%22%2C%22isHiring%3Atrue%22%5D"}]}'
```

### "YC companies in India"

```bash
curl ... -d '{"requests":[{"indexName":"YCCompany_production","params":"query=&hitsPerPage=20&facetFilters=%5B%22regions%3AIndia%22%5D"}]}'
```

### "Large YC startups (100+ employees)"

```bash
curl ... -d '{"requests":[{"indexName":"YCCompany_production","params":"query=&hitsPerPage=20&numericFilters=team_size%3E%3D100"}]}'
```

---

## Tips

- **Use `hitsPerPage=0`** when you only need facet counts (count-by-batch, count-by-industry, etc.) — drastically reduces response size
- **Combine filters** for precise results: batch + industry + region + isHiring all work together
- **Search is fuzzy** — "stripe" matches "Stripe", "strip", etc. Use exact names when possible
- **URL-encode carefully** — `facetFilters=["batch:Summer 2024"]` becomes `facetFilters=%5B%22batch%3ASummer%202024%22%5D`
- **`industries` (plural)** is the multi-value field for filtering; `industry` (singular) is the primary value
- **No founder data** — if the user needs founder names, check `https://www.ycombinator.com/launches/{slug}` on the YC website

---

## Cross-References

- **YC Program FAQ**: See `YC_FAQ.md` in this directory for YC program details
- **Reference Data**: See `REFERENCE.md` for complete canonical lists of batches, industries, regions, and facets
