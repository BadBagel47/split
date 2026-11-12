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

## Current state
- v2 design is live.
- Next: F-001 Swish payments in the settle-up view (see BACKLOG.md), awaiting go-ahead.

## Notes
- Personal data: any per-person data added to a list (e.g. phone numbers for Swish) ends up in share links and backups. Keep that in mind when adding fields. The user approved including Swish numbers in share links and backups (2026-11-12).
