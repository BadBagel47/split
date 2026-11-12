# HANDOFF

Rules version: 1.0

## Inventory
- Done 2026-11-12.
- Branches: `main` (default), `v1-gammal` (first version, kept for reference; already contained in main's history), `claude/*` agent branches.
- Open PRs / Issues: none.
- Existing documentation: `README.md` only (Swedish, user-facing). No previous bug/TODO lists.
- Publishing: GitHub Pages from `main` with custom domain `split.trythis.one` (`CNAME`). No GitHub Actions in the repo.
- Auto-merge workflow (`.github/workflows/auto-merge.yml`): missing. Needed since agents can only push to their own `claude/` branch.

## Project
- Split: split expenses, calculate tips and settle up. Mobile-first web app.
- The whole app is a single file: `index.html` (HTML, CSS and JS). No build step, no dependencies.
- All data is stored locally in the browser (`localStorage`). No accounts, no backend.
- UI languages: Swedish and English (string tables near the top of the script).
- Lists can be shared via a link (`#import=` + base64url-encoded list JSON) and backed up as JSON.
- `shots/` holds design screenshots of v2.
- Swish (F-001): optional Swish number per person; settle-up cards in SEK get a "Swish" button that opens a sheet with a QR code (and a deep link on touch devices). Swish has no callback, so payments are still confirmed with "Paid".

## Current state
- v2 design is live.
- F-001 Swish payments in settle-up is done (2026-11-12). Needs a real-device check: scan a QR code and tap "Open Swish" on iPhone and Android.
- Next: language consistency bugs B-002–B-007 (see BACKLOG.md), awaiting go-ahead.

## Notes
- Personal data: any per-person data added to a list (e.g. phone numbers for Swish) ends up in share links and backups. Keep that in mind when adding fields. The user approved including Swish numbers in share links and backups (2026-11-12).
