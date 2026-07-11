# marketplace-monitoring

Automated MacBook price monitoring across Indonesian/SEA marketplaces (Tokopedia, Shopee Indonesia, Carousell), powered by a scheduled Claude Code cloud routine.

## How it works

Every 6 hours, a cloud agent (routine) spins up with this repository checked out and:

1. Searches Tokopedia, Shopee ID, and Carousell for:
   - **MacBook Pro M4 Pro** priced under **Rp30.000.000**
   - **MacBook Air M4** priced under **Rp16.000.000**
2. Writes a timestamped markdown report to [`reports/`](reports/) with matching listings, the cheapest match per product, and a coverage section noting which platforms could be queried.
3. Commits the report and pushes it to this repository's `main` branch.

## Repository layout

- [`routine/prompt.md`](routine/prompt.md) — the exact prompt the cloud agent runs with
- [`routine/routine.json`](routine/routine.json) — routine configuration (schedule, model, tools)
- `reports/` — generated price reports, one file per run (`YYYY-MM-DD-HHMM.md`, WIB time)

## Managing the routine

The routine is managed at <https://claude.ai/code/routines/trig_01GzAja9j5HsNqX9k7iPut95>. It runs on the cron schedule `0 */6 * * *` (UTC), i.e. 07:00, 13:00, 19:00, and 01:00 WIB.

> **Note:** for the cloud agent to push reports here, the Claude GitHub App must be installed on this repository (<https://github.com/apps/claude>).
