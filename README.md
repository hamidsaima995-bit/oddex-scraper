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

**Retry logic** — Each fetch retries up to 2 times with
