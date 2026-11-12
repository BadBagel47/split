# Backlog

Priority scale: High, Medium, Low. IDs: B = bug, F = feature, D = planning/design (one shared running series).

## Open

### F-001 – Swish payments when settling up
- Priority: Medium
- Status: Proposed, awaiting go-ahead and answers to open questions.
- Goal: In the settle-up view, let the payer open Swish with recipient, amount and message prefilled.
- Proposal:
  - Optional Swish number per person (person sheet). Validate Swedish mobile numbers (07x…, +467x…) and Swish business numbers (123…).
  - "Swish" button on each settle-up card when the list currency is SEK and the recipient has a number.
  - Mobile: open the Swish app via the `swish://payment?data=…` deep link (payee, amount, message = list name, editable).
  - Desktop: show a QR code the payer scans with the Swish app (generated locally, no external service).
  - Payment is still confirmed manually with "Paid" (Swish gives no callback to private web apps).
- Open questions:
  - Should phone numbers be included in share links and backups? (Share links put the data in the URL.)
  - QR code on desktop: include it (adds a small built-in QR generator, ~3–4 kB) or mobile-only?

## Proposed runs

- **A** – Opus, medium – Swish in settle-up
  - F-001 – Swish number per person, Swish button/QR on settle-up cards

## Done

(none yet)
