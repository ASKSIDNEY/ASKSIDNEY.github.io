# AskSidney — Landing Pages (GitHub Pages)

Free capture stack for **AskSidney | Fix The Trader**: GitHub Pages (hosting) + Google Apps Script (capture + delivery) + Google Sheet (CRM v0). $0/month.

**Live URLs (once Pages is enabled):**
- `https://asksidney.github.io/` → redirects to `/tracker/`
- `https://asksidney.github.io/tracker/` — free Habit Tracker lead magnet (always-on, link-in-bio)
- `https://asksidney.github.io/vote/` — campaign vote page *(Step 2 — coming)*

## Structure

```
index.html            → root redirect to /tracker/
tracker/index.html    → lead magnet page (posts form_type=tracker)
vote/index.html       → campaign page (posts form_type=vote) [Step 2]
apps-script/Code.gs   → the CRM engine (lives in Google Sheets, versioned here)
```

## Setup — three phases

### Phase A — Hosting (GitHub, one time)
1. This repo must be **public** and named `ASKSIDNEY.github.io`.
2. Settings → Pages → Source: **Deploy from a branch** → Branch: `main` / `/ (root)` → Save.
3. Site appears at `https://asksidney.github.io/` within ~2 minutes.

### Phase B — CRM engine (Google, one time)
1. Create a Google Sheet named `AskSidney_CRM_v0` (on Sidney's Google account).
2. Extensions → Apps Script → paste all of `apps-script/Code.gs` over the default file → Save.
3. Deploy → New deployment → **Web app** · Execute as: **Me** · Who has access: **Anyone** → Deploy → authorize → copy the **`/exec` URL**.
4. Send that URL to Claude — it gets inserted into the pages (the `SCRIPT_URL` constant) and pushed. Done.

### Phase C — Test end-to-end
1. Open `/tracker/`, submit with a real email.
2. Within ~10s: a row appears in the sheet + the tracker email arrives from Gmail.
3. Submit again with the same email → row marked `DUPLICATE`, no second email.

## How updates work
Claude edits and pushes; Pages redeploys automatically in ~1–2 minutes. No build step, no dependencies — plain HTML.

## Source tagging
Share links with `?src=tiktok`, `?src=ig`, `?src=bio` — the page passes the tag into the CRM's Source column.

## Custom domain (later — Decision D-020)
When the domain is bought (before the 5K reactivation blast): add it in Settings → Pages → Custom domain (creates a `CNAME` file), point DNS `A/ALIAS` records at GitHub Pages, keep HTTPS enforced. URLs upgrade; nothing gets rebuilt.

## Known limits (by design — CRM v0)
- Gmail ~100 sends/day → move delivery to Brevo free if signups approach 80/day.
- No drip sequences, no broadcasts — the 5K reactivation waits for Brevo + custom domain.
- Everything exports via CSV; nothing is lost by starting here.
