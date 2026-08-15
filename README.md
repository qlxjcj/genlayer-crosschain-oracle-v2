# Crosschain Oracle v2 — Multi-Source Data Aggregation with Feed History & Staleness Detection

A decentralized oracle on GenLayer that aggregates and verifies data from multiple web sources. Each feed supports custom schemas and multiple source URLs; AI validator consensus (`gl.eq_principle.prompt_comparative`) extracts, normalizes, and cross-checks values across sources.

## Features

- Feed creation with custom data schemas and multiple source URLs
- Multi-source AI consensus aggregation and normalization
- Feed history tracking (last 20 snapshots with timestamps)
- Auto-staleness detection with configurable max age
- Deviation threshold monitoring across sources (local computation)
- Confidence scoring with data quality warnings
- Per-feed SLA controls and freshness checks
- Subscriber system for consumers

## Frontend

A full dApp frontend (`index.html`) supports the complete workflow: connect wallet, create a feed, update it through AI consensus, check staleness, read the latest value, browse feed history, and subscribe.

- Live: https://qlxjcj.github.io/genlayer-crosschain-oracle-v2/
- Contract: `0xf2e32c8550C0C48F2C0D5020fcB19F916B9ad3FE` (Bradbury)

## Contract methods

### Writes
- `create_feed(description, sources_json, schema_json, max_staleness, deviation_threshold)`
- `update_feed(feed_id)` — AI consensus aggregation from all sources
- `subscribe(feed_id)` / `unsubscribe(feed_id)`

### Views
- `get_latest_value(feed_id)` — current value, freshness, update count
- `check_staleness(feed_id)` — is_stale, seconds since update, max staleness
- `get_feed_history(feed_id, limit)` — last N snapshots
- `get_feed(feed_id)` — full feed record
- `get_feed_count()` / `list_feeds()` / `get_subscribers(feed_id, user)`

## Consensus discipline

All consequential outputs (values dict, confidence, sources_used, warnings) are bound inside `gl.eq_principle.prompt_comparative` — the label alone is never enough.
