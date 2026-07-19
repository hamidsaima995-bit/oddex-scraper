# ODDEX Scraper

News scraper that collects headlines from multiple sources and stores them in a Postgres database (Supabase). Built to feed the live news ticker on [oddexvibe.com](https://oddexvibe.com).

## What it does

- Scrapes HTML from multiple sites in parallel using Cheerio
- Maps each headline to a trading asset symbol via keyword matching
- Deduplicates at the database level so repeat runs don't create duplicates
- Handles failures gracefully — retries with exponential backoff, per-site error isolation

## Stack

Node.js · Cheerio · Supabase (PostgreSQL)

## Design notes

**Retry logic** — Each fetch retries up to 2 times with increasing delays (2s, 4s) and a 10-second timeout. Scraping targets go down or rate-limit; the pipeline shouldn't.

**Per-site isolation** — Each source has its own parser function. When one site changes its HTML structure, the others keep working.

**Deduplication** — A unique constraint on the headline column with upsert and ignoreDuplicates. Handled by the database rather than in application memory, so it survives restarts.

**Parallel execution** — All sources are scraped concurrently with Promise.all rather than sequentially.

## Setup

Install dependencies with npm install, then set these environment variables:

SUPABASE_URL — your Supabase project URL
SUPABASE_SERVICE_KEY — your Supabase service key

Run with: node scraper.js

## Schema

The scraper writes to a news_items table with columns for headline (unique), source, symbol, impact, ai_comment, and created_at.
