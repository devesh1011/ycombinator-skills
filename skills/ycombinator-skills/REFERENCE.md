# YC Reference Data

Canonical lists for filtering. Use exact strings in `facetFilters`.

---

## Batches (49 values)

| Batch | Era |
|---|---|
| Summer 2005 | First YC batch |
| Winter 2006 | |
| Summer 2006 | |
| Winter 2007 | |
| Summer 2007 | |
| Winter 2008 | |
| Summer 2008 | |
| Winter 2009 | Airbnb batch |
| Summer 2009 | Stripe batch |
| Winter 2010 | |
| Summer 2010 | |
| Winter 2011 | |
| Summer 2011 | |
| Winter 2012 | |
| Summer 2012 | Coinbase, Instacart batch |
| Winter 2013 | |
| Summer 2013 | DoorDash batch |
| Winter 2014 | |
| Summer 2014 | |
| Winter 2015 | |
| Summer 2015 | |
| Winter 2016 | |
| Summer 2016 | |
| Winter 2017 | |
| Summer 2017 | |
| Winter 2018 | |
| Summer 2018 | |
| Winter 2019 | |
| Summer 2019 | |
| Winter 2020 | |
| Summer 2020 | |
| Winter 2021 | |
| Summer 2021 | |
| Winter 2022 | |
| Summer 2022 | |
| Winter 2023 | |
| Summer 2023 | |
| Winter 2024 | |
| Summer 2024 | |
| Fall 2024 | First Fall batch |
| Winter 2025 | |
| Spring 2025 | First Spring batch |
| Summer 2025 | |
| Fall 2025 | |
| Winter 2026 | |
| Spring 2026 | |
| Summer 2026 | |
| Fall 2026 | |
| Unspecified | Unknown batch |

Pattern: YC runs 4 batches/year from 2024 onward (Winter, Spring, Summer, Fall). Pre-2024: Winter and Summer only.

---

## Industries (73 values)

```
Agriculture
Analytics
Apparel and Cosmetics
Asset Management
Automotive
Aviation and Space
B2B
Banking and Exchange
Climate
Construction
Consumer
Consumer Electronics
Consumer Finance
Consumer Health and Wellness
Content
Credit and Lending
Defense
Diagnostics
Drug Discovery and Delivery
Drones
Education
Energy
Engineering, Product and Design
Finance and Accounting
Fintech
Food and Beverage
Gaming
Government
Healthcare
Healthcare IT
Healthcare Services
Home and Personal
Housing and Real Estate
Human Resources
Industrial Bio
Industrials
Infrastructure
Insurance
Job and Career Services
Legal
Manufacturing and Robotics
Marketing
Medical Devices
Office Management
Operations
Payments
Productivity
Real Estate and Construction
Recruiting and Talent
Retail
Sales
Security
Social
Supply Chain and Logistics
Therapeutics
Transportation Services
Travel, Leisure and Tourism
Unspecified
Virtual and Augmented Reality
```

### Subindustry Format

Subindustries follow the pattern `{Industry} -> {Subcategory}`. Examples:
- `Consumer -> Travel, Leisure and Tourism`
- `Consumer -> Food and Beverage`
- `Fintech -> Banking and Exchange`
- `Healthcare -> Therapeutics`
- `Healthcare -> Diagnostics`

Filter on `industries` (plural) for subindustry-level precision. Filter on `industry` (singular) for broad category matching.

---

## Regions (100+ values)

### Major Regions

```
America / Canada (4,383)
Remote (3,006)
Partly Remote (1,858)
Fully Remote (1,148)
Europe (426)
Unspecified (294)
South Asia (221)
Latin America (214)
Southeast Asia (105)
Africa (85)
Middle East and North Africa (69)
East Asia (21)
Oceania (14)
```

### Countries

```
United States of America (4,252)
India (209)
United Kingdom (200)
Canada (142)
Mexico (88)
France (62)
Nigeria (58)
Singapore (53)
Brazil (50)
Germany (50)
Colombia (32)
Indonesia (31)
Israel (31)
Argentina (20)
Chile (20)
Spain (19)
Denmark (16)
Australia (12)
Egypt (12)
Netherlands (12)
Sweden (12)
United Arab Emirates (11)
Kenya (10)
Pakistan (10)
Peru (10)
Philippines (10)
Switzerland (10)
Ireland (8)
China (7)
Hong Kong (7)
Malaysia (7)
Panama (6)
South Korea (6)
Vietnam (6)
Ghana (5)
Norway (5)
Poland (5)
Saudi Arabia (5)
Turkey (5)
Austria (4)
Finland (4)
Slovenia (4)
Belgium (3)
Estonia (3)
Italy (3)
Morocco (3)
Portugal (3)
Senegal (3)
New Zealand (2)
Puerto Rico (2)
Romania (2)
South Africa (2)
Uganda (2)
Ukraine (2)
Algeria (1)
Bahrain (1)
Bangladesh (1)
Belarus (1)
Costa Rica (1)
Croatia (1)
Cyprus (1)
Czechia (1)
Democratic Republic of the Congo (1)
Ecuador (1)
Ethiopia (1)
Georgia (1)
Greece (1)
Hungary (1)
Iceland (1)
Iraq (1)
Ivory Coast (1)
Japan (1)
Kyrgyzstan (1)
Latvia (1)
Lithuania (1)
Namibia (1)
Nepal (1)
Russia (1)
Seychelles (1)
Tanzania (1)
Thailand (1)
Uruguay (1)
Venezuela (1)
Zambia (1)
```

Parenthetical counts approximate as of May 2026.

---

## Status Values

```
Active (4,051)    — Currently operating
Inactive (1,034)  — No longer operating
Acquired (778)    — Acquired by another company
Public (23)       — IPO / publicly traded
```

---

## Additional Boolean Facets

```
top_company: true (91) / false (5,794)
isHiring: true (1,458) / false (4,428)
nonprofit: true (42) / false (5,844)
highlight_black: true / false
highlight_latam: true / false
highlight_women: true / false
```

---

## Numeric Filter Reference

| Field | Example | Description |
|---|---|---|
| `team_size` | `team_size>=100` | Companies with 100+ employees |
| `team_size` | `team_size:10 TO 100` | Companies with 10–100 employees |
| `team_size` | `team_size<10` | Companies with fewer than 10 employees |
| `launched_at` | `launched_at>=1700000000` | Launched after Unix timestamp |

---

## Tags (common values)

```
AI, API, Analytics, B2B, Banking as a Service, Blockchain,
Climate, Consumer, Crypto, Database, Developer Tools,
DevOps, E-commerce, Education, Enterprise, Fintech,
Generative AI, Healthcare, Infrastructure, Insurance,
Machine Learning, Marketplace, Mobile, Open Source,
Payments, Productivity, Robotics, SaaS, Security,
Social, Supply Chain, Travel, Web3
```

Tags are free-form. Use the `tags` field for fuzzy technology/business-model matching. For structured categorization, prefer `industries`.
