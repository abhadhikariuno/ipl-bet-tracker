# IPL 2026 Bet Tracker

A single-page web app for tracking friendly IPL 2026 match bets among 3 players. Picks and results are stored in a shared Google Sheet via Google Apps Script — no server required.

## Features

- **Match picker** — auto-selects today's match (or the most recent past match)
- **Per-player picks** — each player picks a winner before the match
- **Payout calculator** — computes who owes what based on a configurable stake
- **Shared ledger** — running totals synced live from Google Sheets
- **IPL points table** — tracks team standings across the season
- **Picks history** — view all picks per player across all matches
- **Rain / No Result** support — all stakes returned on abandoned matches
- **Playoff support** — manual team entry for Qualifier 1, Eliminator, Qualifier 2, and Final

## Betting Rules

- Players 2 and 3 must always pick opposite teams.
- **If two players agree:** winner gains the full stake, loser splits the loss.
- **If all three split (P1 vs P2+P3 or similar):** the odd one out wins double or loses double.
- Stake is configurable per result (default: $10).

## Setup

### 1. Google Apps Script

You need a Google Apps Script deployed as a web app to act as the backend.

1. Open [Google Sheets](https://sheets.google.com) and create a new spreadsheet.
2. Go to **Extensions → Apps Script**.
3. Paste your Apps Script code (handles `getAll`, `savePick`, `saveResult`, `saveConfig` actions).
4. Click **Deploy → New deployment → Web app**.
   - Execute as: **Me**
   - Who has access: **Anyone**
5. Copy the deployment URL.

### 2. First Launch

1. Open `index.html` in any modern browser (or serve it locally — see below).
2. On first visit, paste your **Apps Script URL** and enter the **3 player names**.
3. Each player visits the same URL and selects their name on the "Who are you?" screen.
4. Player identity is saved in `localStorage` — no login required.

### Running Locally

```bash
python3 -m http.server 8080
```

Then open [http://localhost:8080](http://localhost:8080).

## Match Times

All match times are displayed in **CDT (Central Daylight Time, UTC−5)**, which is in effect for the entire IPL season (March–May).

| IST | CDT |
|-----|-----|
| 3:30 PM | 5:00 AM |
| 7:30 PM | 9:00 AM |

## Season Coverage

**74 matches** — March 28 to May 31, 2026

| Phase | Matches | Dates |
|-------|---------|-------|
| League Phase 1 | 1–20 | Mar 28 – Apr 12 |
| League Phase 2 | 21–40 | Apr 13 – Apr 28 |
| League Phase 3 | 41–70 | Apr 29 – May 24 |
| Playoffs | 71–74 | TBC (Final: May 31) |

## Tech Stack

- Vanilla HTML/CSS/JavaScript — zero dependencies, zero build step
- Google Apps Script — backend API (JSONP)
- Google Sheets — data store
- `localStorage` — saves your identity and Apps Script URL in the browser

## File Structure

```
index.html   — entire app (single file)
```
