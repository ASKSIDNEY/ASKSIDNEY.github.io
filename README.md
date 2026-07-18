# ASKSIDNEY | Fix The Trader — hub site

Static marketing + funnel site for the AskSidney trading-psychology community.
Brand line: **"Fix the trader and the trading will fix itself."** Positioning: ranks **discipline, not profits** — no signals, ever.

> **Single source of truth:** the full project state, decisions, and strategy live in the Google Drive "brain" — doc **"00 — MASTER STATE & HANDOVER"**. Read that first. This README documents the *site* only.

## Pages

| Path | Purpose | Posts to CRM? |
|---|---|---|
| `/` (`index.html`) | Hub. 3 buttons in fixed order: **1) Trade with me** (Valetax IB link — the door) · **2) Join the free community** (→ `/join/`) · **3) Fastest way to scale up** (WeMaster, code **SID20**). | no |
| `/join/` (`join/index.html`) | Capture funnel. Sells the community, shows the 3 join steps, captures name + email + Valetax status. Has-account → routes to Skool; no-account → routes to the home Trade-with-me button and auto-fires Email 1. | **yes** (`form_type=join`) |
| `/tracker/` (`tracker/index.html`) | Free 30-day Habit Tracker lead magnet. | **yes** (`form_type=tracker`) |
| `/vote/` (`vote/index.html`) | "You pick what I build next" course vote + tracker delivery. | **yes** (`form_type=vote`) |

## Stack

- **Hosting:** GitHub Pages off `main`, served at https://asksidney.github.io (single-file HTML pages, inline CSS/JS, no build step).
- **Backend:** one Google Apps Script Web App (bound to the `AskSidney_CRM_v0` sheet) receives all form posts, logs to the sheet, and sends member emails via MailApp from Sidney's Gmail. Source lives in the Drive brain (`asksidney_crm` script, currently **v1.3**).
- **CRM script `/exec` URL** (all pages POST here — keep in sync):
  `https://script.google.com/macros/s/AKfycbyQHSgCLS6q6WfPxTyOhzs0co_KFm8R_gdINyGJFLX_ncfchNLFff2WS5OGJgMknLemyA/exec`

## Deploy / edit rules (read before touching anything)

1. **Editing pages:** commit directly to `main`; GitHub Pages redeploys automatically. Direct `git` from some environments is blocked — edits are made via the Zapier GitHub connector or the GitHub web UI.
2. **The Apps Script URL is shared by 4 pages** (`/join`, `/tracker`, `/vote`, and the script itself). If the script is redeployed as a **New deployment**, the `/exec` URL changes and every page breaks. **Always redeploy as "Manage deployments → Edit → New version"** on the existing deployment so the URL stays stable.
3. **Copy standards (brand law):**
   - Tagline everywhere: "Fix the trader and the trading will fix itself."
   - Broker requirement wording: **"open a live Valetax account and fund"** — never "$50" or "funded with any amount".
   - Disclosure: Sidney is an **"introducing partner with Valetax"** — never "broker".
   - The Valetax referral link appears only under **Trade with me**, the Skool About page, and Email 1 — **not** on `/join`.
   - Every page keeps the risk disclaimer footer.

## Related assets (not in this repo)

- Skool community: https://www.skool.com/asksidney-fix-the-trader-2642 (no API — human-operated)
- CRM sheet `AskSidney_CRM_v0` + Apps Script (Drive)
- Drive brain (decisions, strategy, SOPs) — start at "00 — MASTER STATE & HANDOVER"
