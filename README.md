# Oddex Scraper

A small news scraper for OddexVibe. It fetches news pages, pulls out the parts it needs with Cheerio, and saves them to Supabase so the game can turn real headlines into in-game market events.

## Tech

- Node.js
- Cheerio for parsing HTML
- Supabase for storage

## What is inside

- `scraper.js`, the scraper
- `package.json`, dependencies and the start script

## Configuration

The scraper needs the Supabase URL and key set as environment variables. Set them in your host dashboard, or in a local `.env` file for development. Do not commit real values.

## Running it locally

You need Node.js installed.

```
npm install
npm start
```

## Related

This feeds data to OddexVibe (https://oddexvibe.com) and works alongside the ODDEX-BACKEND service.

## Author

Saima Hamid, Ninja Tech, Lahore. https://ninjatechdev.com
