# Quorel

**The source of truth for the live web.**

Quorel turns any public website into a clean, versioned, API-ready dataset — without you writing a single scraper. Define what data you want once, and Quorel fetches it, structures it against your schema, and keeps it current every night. No pipelines. No maintenance. No dirty surprises.

---

## What it is

Most scraping gets you a snapshot. Quorel gives you a **source of truth** — structured, versioned, and live. Every refresh is a permanent snapshot. Nothing is ever overwritten. Roll back to any prior version instantly, diff any two versions side by side, and consume your data from a clean API in any format you need.

---

## Get started in 5 minutes

1. Go to [quorel.vercel.app](https://quorel.vercel.app) and create a free account
2. Paste your URLs or describe your intent in plain English
3. Define your schema — tell Quorel which fields you want and what they mean
4. Hit **Create** — your dataset is live and refreshing nightly from that moment

No config files. No infrastructure. No maintenance.

---

## Core concepts

### Datasets

A dataset is a named collection of structured entities extracted from one or more public URLs. Every dataset has a schema, a version history, and a public or private API endpoint.

### Schema

You define your schema in plain English — field names and what they mean. Quorel's AI extraction engine maps web content to your structure precisely on every refresh. No CSS selectors. No XPath. No brittle rules that break when the page changes.

### Versions

Every refresh that produces a meaningful change creates a new immutable version. Nothing is ever overwritten. Your full history is always queryable, diffable, and downloadable.

### Nightly refresh

Your sources are re-processed automatically every night. Your dataset is always current by morning. You can also trigger additional refreshes on demand via your ping URL.

---

## API

Public datasets are accessible to anyone — no account needed.

```
GET https://quorel.vercel.app/api/{dataset_id}
```

**Query params**

| Param    | Description                                              |
| -------- | ---------------------------------------------------------|
| `format` | `json`, `csv`, `jsonl`, `xml`, `xlsx`, `tsv`, `parquet`  |
| `limit`  | Number of entities to return (max 500)                   |
| `page`   | Page number for pagination                                |
| `sort`   | Field and direction e.g. `score:desc`                     |

**Private datasets** — pass your private key in the Authorization header:

```
Authorization: Bearer YOUR_PRIVATE_KEY
```

---

## On-demand refresh — Ping URL

Every dataset gets a dedicated ping URL. Hit it from any external scheduler, CI pipeline, or automation tool to trigger an additional refresh outside the nightly cycle.

```
GET https://quorel.vercel.app/ping/{your-ping-key}
```

Available on Pro and above.

---

## Webhooks

Register a webhook endpoint and Quorel will POST to it the moment your dataset finishes refreshing. Build reactive pipelines without polling.

```json
{
  "dataset_id": 142,
  "name": "remote-jobs",
  "version": 67,
  "entity_count": 1204,
  "fired_at": "2026-06-20T03:00:00Z"
}
```

Available on Pro and above.

---

## Version history & diff

Every version is permanent. From your dataset dashboard you can:

- **Diff** any two versions side by side — added rows, removed entries, modified field values
- **Rollback** to any prior version in one click
- **Freeze** a version to lock it permanently as your stable source

---

## The Marketplace

Browse hundreds of public datasets across tech, finance, jobs, AI, and research — already built, maintained, and refreshed nightly.

→ [quorel.vercel.app/datasets](https://quorel.vercel.app/datasets)

**Clone any public dataset** and make it yours — add your own URLs, adjust the schema, and publish it back. You own it fully from day one.

---

## MCP — AI Agent access

Every Quorel dataset ships with a native MCP server, included on every plan. Connect Claude or any MCP-compatible agent and let it browse, query, and edit your data conversationally — no scripts required.

**Available MCP tools**

| Tool                  | What it does                                                              |
| ---------------------- | -------------------------------------------------------------------------|
| `list_datasets`        | List all datasets owned by the authenticated user                        |
| `get_dataset_schema`   | Inspect a dataset's fields, versions, and metadata                       |
| `query_dataset`        | Filter, sort, dedupe, and paginate entities; export in any format        |
| `get_entity`           | Fetch a single entity by its index                                       |
| `pull_for_edit`        | Pull the full entity list for agent-driven cleanup                       |
| `update_entity`        | Patch a single entity's fields in the alt version                        |
| `delete_entity`        | Remove one or more entities from the alt version                        |
| `push_alt_version`     | Publish a cleaned/processed batch as the alt version                     |
| `append_alt_version`   | Append a processed batch to an existing alt version                      |

**Example**

```
query_dataset(dataset_id: 142, keywords: "senior remote", sort: "salary:desc", limit: 5)
→ 47 entities matched, returned as JSON sorted by salary

pull_for_edit(dataset_id: 142, use_alt: false)
→ Claude reviews 1,204 entities, dedupes and fixes null fields

push_alt_version(dataset_id: 142, version: 3, entities: [...])
→ live at /remote-jobs/v3/alt
```

MCP access is included on every plan, including Free.

---

## Plans

|                  | Free | Pro    | Scale       |
| ---------------- | ---- | ------ | ----------- |
| Datasets         | 1    | 5      | Unlimited   |
| URLs per dataset | 20   | 100    | 500         |
| Nightly refresh  | ✓    | ✓      | ✓           |
| Ping URL         | —    | ✓      | ✓           |
| Webhooks         | —    | ✓      | ✓           |
| MCP access       | ✓    | ✓      | ✓           |
| Price            | $0   | $19/mo | Coming soon |

Full plan details at [quorel.vercel.app](https://quorel.vercel.app#pricing)

---

## Links

- **Product** — [quorel.vercel.app](https://quorel.vercel.app)
- **Marketplace** — [quorel.vercel.app/datasets](https://quorel.vercel.app/datasets)
- **Docs** — [quorel.vercel.app/docs](https://quorel.vercel.app/docs)
- **X / Twitter** — [@PhantomDev001](https://x.com/PhantomDev001)
- **GitHub** — [var-raphael](https://github.com/var-raphael)

---

*Public beta · No credit card required · Upgrade anytime*

