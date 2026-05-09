# YC Skills

Agent skills for Y Combinator startup data. One command gives AI coding agents access to:

- **5,886 YC startups** across 49 batches (2005–2026)
- **All finalists + top companies** with details
- **Rich filtering**: industry, region, batch, status, team size, hiring, and more

## Install

```bash
npx skills add ycombinator-skills
```

Then tell your agent: `use ycombinator-skills`

## What It Does

Teaches agents how to query the YC public Algolia search API. No backend, no API keys — just the documented query format. Agents who read the skill can:

- Search companies by name, keyword, or description
- Filter by batch (Summer 2024, Winter 2025, etc.)
- Filter by industry (Fintech, Healthcare, AI, Consumer, etc.)
- Filter by region (India, Europe, Remote, USA, etc.)
- Filter by status (Active, Acquired, Public)
- Find top companies, hiring startups, nonprofits
- Get facet counts for overview analysis
- Sort by launch date for "newest" queries

## Example Queries

Once the skill is loaded, agents can answer questions like:

- "Find all AI startups in YC Summer 2024"
- "Show me top YC companies that are hiring"
- "What fintech startups did YC fund in Winter 2025?"
- "How many YC companies are in India?"
- "Show me all acquired YC companies"
- "What's the most recent YC batch and what industries are in it?"

## Data Source

Data comes from the same Algolia index powering [ycombinator.com/launches](https://www.ycombinator.com/launches). No API key needed — the query format is fully documented in the skill.

## Limitations

- **No founder data**: The public API doesn't expose founder names. For founder details, visit the YC launches page for the company.
- **Self-reported data**: Team size and hiring status are self-reported and may be outdated.
- **Public companies only**: The `ycdc_public` tag filter excludes companies that haven't opted into public listing.

## Structure

```
skills/
  ycombinator-skills/
    SKILL.md          # Full API spec (agents read this)
    REFERENCE.md      # Canonical batch/industry/region lists
    YC_FAQ.md         # YC program FAQ
```
