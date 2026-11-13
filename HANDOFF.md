# HANDOFF

Rules version: 1.6
Inventory: 2026-11-12 (supplemented 2026-11-13: all remote branches, git history for sensitive data, laws and regulations)

## Project
- Split: split expenses, calculate tips and settle up. Mobile-first web app.
- Project language: Swedish (README and default UI). The app UI is also available in English (string tables `T.sv` / `T.en` near the top of the script).
- The whole app is a single file: `index.html` (HTML, CSS and JS). No build step, no dependencies. Fonts are self-hosted in `fonts/` (no external requests).
- All data is stored locally in the browser (`localStorage`). No accounts, no backend.
- Lists can be shared via a link (`#import=` + base64url-encoded list JSON) and backed up as JSON. English share links go via `en/index.html` (English link preview, forwards to the app). Sharing a list with Swish numbers shows a warning first.
- Swish (F-001): optional Swish number per person; settle-up cards in SEK get a "Swish" button that opens a sheet with a QR code (and a deep link on touch devices). Swish has no callback, so payments are still confirmed with "Paid".

## Goals and way of working
- Goal: a simple, private expense splitter that works without accounts or servers.
- Work follows the global agent rules (see AGENTS.md): items are collected in the backlog, proposed as run groups and run after a go-ahead.

## Publishing
- GitHub Pages from `main`, custom domain `split.trythis.one` (`CNAME`).
- Agents push to `claude/*` branches; `.github/workflows/auto-merge.yml` (agent-rules template, added by the user 2026-11-12) merges them into `main` and triggers a Pages build. Verified working 2026-11-12.

## Current state
- Latest work: D-013 privacy note in Settings (2026-11-13); B-012 Done button when adding participants; B-005 link preview follows the app language and F-011 warning before sharing Swish numbers; B-010 self-hosted fonts; F-008 dates as YYYY-MM-DD; F-001 Swish in settle-up.
- Needs a real-device check: Swish QR code and "Open Swish" on iPhone and Android (F-001); date picker arrow (B-007/F-008).
- Next: see docs/BACKLOG.md.

## Decisions
- 2026-11-12: Swish numbers are included in share links and backups (F-001).
- 2026-11-12: Desktop shows a Swish QR code to scan with the phone (F-001).
- 2026-11-12: Dates are shown as YYYY-MM-DD in all languages, except "Today"/"Yesterday" (F-008).
- 2026-11-12: Shared links preview in the language Split is set to, via `en/` for English (B-005).
- 2026-11-12: Lists with an automatic name are renamed when the language changes (B-002).

## Environment and one-time actions
- 2026-11-13: Agents cannot push to `main` directly or create workflow files; they push to `claude/*` and rely on auto-merge.
- 2026-11-13: Swish developer documentation (developer.swish.nu, developer.getswish.se) is not reachable from the agent environment.
- One-time action done: auto-merge workflow (2026-11-12).

## Laws and regulations (brief review 2026-11-13)
- Local storage (`localStorage`) is only used for the service the user asks for; this is normally exempt from consent under the Swedish Electronic Communications Act (LEK 9:28). Not legal advice.
- No third-party requests since fonts are self-hosted (B-010); Google Fonts previously sent visitors' IP addresses to Google.
- Personal data (names, Swish numbers) stays on the device unless the user shares a link or backup; sharing warns about Swish numbers (F-011). A short privacy note is in Settings (D-013).
- Fonts are under the SIL Open Font License; licence files are in `fonts/`.

## Sensitive information
- No secrets or sensitive data found in branches or git history (2026-11-13).

## Documentation map
- `README.md` – user-facing description (Swedish).
- `docs/BACKLOG.md` – features, bugs, proposed runs and done items.
- `shots/` – design screenshots of v2.
- `fonts/OFL-*.txt` – font licences.
- Branch `v1-gammal` – first version, kept for reference (already in main's history).
