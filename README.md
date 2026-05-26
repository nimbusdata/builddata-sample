---
license: cc-by-4.0
language:
  - en
  - fr
size_categories:
  - 1K<n<10K
tags:
  - canada
  - construction
  - real-estate
  - permits
  - building-permits
  - municipal
  - rag
  - llm-training
pretty_name: BuildData — Canadian Construction Records (Sample)
configs:
  - config_name: default
    data_files:
      - split: train
        path: builddata_sample.jsonl
---

# BuildData — Canadian Construction Records (Sample)

**Sample of 5,000 Canadian municipal construction records across 54 cities.**
Mix of building permits, business licences, development permits, planning
applications, and inspections. Last 3 months of data from the full
[BuildData API](https://builddata.ca).

> **Want the full dataset?** 8.6M+ records across 60 cities, normalized + geocoded,
> daily refresh, query by city / address / value / type / date.
> **[Get an API key →](https://builddata.ca/pricing)**

## What's in here

| Field | Type | Description |
|---|---|---|
| `source_id` | string | Originating system (city's open-data portal) |
| `entity_type` | string | `permit`, `licence`, `development_permit`, `planning_application`, `inspection` |
| `record_id` | string | Stable per-record identifier from the source |
| `municipality` | string | City name |
| `event_date` | string (ISO date) | Issue date for permits/licences, application date for planning |
| `category` | string | Permit type / licence type / planning stage |
| `data` | object | Full raw record from the source (JSON) — addresses, values, descriptions, GIS data |

## Composition (sample)

| entity_type | rows |
|---|---|
| permit | 2,500 |
| licence | 700 |
| development_permit | 700 |
| planning_application | 700 |
| inspection | 400 |

54 unique municipalities represented. The full dataset spans 60 cities including
Toronto, Montréal, Vancouver, Calgary, Edmonton, Ottawa, Winnipeg, Québec City,
Halifax, Saint John, plus 50 more.

## Use cases

- **RAG / agents** — ground LLM responses in real Canadian construction activity
- **Domain fine-tuning** — train models on construction vocabulary, NOC codes, GIS schemas
- **Real-estate intelligence** — track building permits as a leading indicator of property changes
- **Construction lead generation** — discover contractors, developers, suppliers active in a market
- **Insurance underwriting** — property age, renovation history, code compliance signals
- **Schema exploration** before committing to API integration

## Limitations of this sample

- **Snapshot only** — frozen 2026-02-25 to 2026-05-25. New permits issued daily; this sample will not reflect them.
- **5K rows** — full dataset is 8.6M+. Sample is enough to test schema, prompts, prototypes; not enough for production analytics.
- **No querying** — can't filter by city, value range, address, or date. Use the API for that.
- **No geocoded coordinates surfaced** — the full API returns `latitude`/`longitude`; sample omits them to keep payload small (still inside `data` for some sources).

## Production access

- **Docs:** https://builddata.ca/docs
- **Pricing:** https://builddata.ca/pricing — free tier 25 req/day, Pro $49/mo 1K req/day
- **Quickstart:**
  ```bash
  curl "https://api.builddata.ca/permit?municipality=Toronto&limit=10" \
    -H "x-api-key: YOUR_KEY"
  ```
- **Export:** `https://api.builddata.ca/permit/export?format=csv&limit=1000` (no key, JSON/CSV/XLSX)

## License & attribution

Data sourced from Canadian municipal open-data portals (Toronto CKAN, Vancouver
Opendatasoft, Calgary Socrata, Edmonton Socrata, etc.). All source data is
under open government / municipal licences. Sample redistribution is permitted
under CC-BY-4.0.

## Contact

- API and enterprise inquiries: nicolas@builddata.ca
- Bug reports: https://github.com/NicolasPrimeau/Nimbus (or via the contact link on builddata.ca)

## Mirror locations

The same sample is published in three places — pick whichever you prefer:

- **Hugging Face:** https://huggingface.co/datasets/nimbusdata/builddata-canadian-construction-sample
- **Kaggle:** https://www.kaggle.com/datasets/niexon/builddata-canadian-construction-sample
- **GitHub:** https://github.com/nimbusdata/builddata-sample
