# Backlog

Priority scale: High, Medium, Low. IDs: B = bug, F = feature, D = planning/design (one shared running series).

## Open

### D-013 – Short privacy note in the app
- Priority: Low
- Status: Proposed (from the laws and regulations review 2026-11-13).
- The app has no privacy information beyond the footer line. A short note (e.g. in Settings) would say what is stored on the device, that nothing is sent to a server, and that share links and backups contain the list, including names and Swish numbers. Supports transparency under GDPR; not legal advice.

## Proposed runs

- **A** – standard model, low level – Privacy note
  - D-013 – Add a short privacy note in Settings, so users know what is stored and what share links contain

## Done

### B-012 – "Cancel" in the add-participant sheet is confusing
- Priority: Low
- Status: Done 2026-11-12. `personSheet(p, more)`: when reopened after adding, the close button reads Done and adds a typed name before closing.
- After adding a participant the sheet reopens for the next one, so the way out is "Cancel" even though people were added.
- Proposed fix: in add mode (only after at least one participant has been added in this round), label the button "Done". If the name field has text when Done is tapped, add that person first, then close. Editing an existing participant keeps "Cancel".

### B-005 – Page description always Swedish
- Priority: Low
- Status: Done 2026-11-12. `en/index.html` holds English description/Open Graph tags and forwards to the app (keeping `#import=`); share links use `en/` when Split is set to English. Root page got Swedish Open Graph tags.
- `<meta name="description">` is Swedish regardless of language (seen in link previews and search results).
- Decision (2026-11-12): shared links should preview in the language Split is set to.
- Proposed fix: link previews are made by services that read the page without running JS, so the language has to be in the URL. Add a small English entry page `en/index.html` with English title/description (plus Open Graph tags) that immediately forwards to the app, keeping the `#import=` data. When Split is set to English, share links point to `/en/`; in Swedish they point to the root as today. Add Open Graph tags to the root page too.

### F-011 – Warn before sharing a list that contains Swish numbers
- Priority: Medium
- Status: Done 2026-11-12. `share()` shows a warning sheet when the list has Swish numbers (Cancel / Share without numbers / Share anyway); `shareLink(strip)` builds the link.
- Share links contain the whole list, including Swish numbers, in the URL. Anyone who gets the link can see the numbers.
- Proposed fix: when the list has Swish numbers, show a sheet before sharing that names whose numbers are included and explains that everyone who gets the link can see them. Buttons: Cancel, Share without numbers, Share anyway. Lists without numbers share directly as today.

### B-010 – Generic font flashes before the real fonts load
- Priority: Medium
- Status: Done 2026-11-12. Fonts in `fonts/` (Inter latin + latin-ext as a variable font, Agbalumo latin) with OFL licence files; preloaded; `html.fl` hides the app until `document.fonts.load` resolves or 1 s passes. The gate script must stay after the `@font-face` rules.
- Cause: Inter and Agbalumo are loaded from Google Fonts with `display=swap`, so text is first drawn in a fallback font and swapped when the fonts arrive. A hard reload (Shift+reload) bypasses the cache, which makes it very visible; first-time visitors see it too.
- Proposed fix:
  - Self-host the fonts (latin subset, woff2; both are SIL Open Font License) and `preload` them, so they load from the same server without the extra Google connections. Also removes the dependency on Google Fonts.
  - Hide the app until the fonts are ready (`document.fonts.ready`), with a short time limit (about 1 s) so a slow connection never leaves the page blank.

### F-009 – Nudge the logo wordmark up slightly
- Status: Done 2026-11-12. `.brand .word` moved up 2px so "Split" sits better against the round icon.
- Priority: Low

### F-008 – Dates as YYYY-MM-DD in all languages
- Priority: Medium
- Status: Done 2026-11-12. Visible text field `#e-date` (typed dates validated by `parseISODate`, also accepts YYYYMMDD); an invisible native `#e-date-pick` over the chevron opens the device's picker. `dayLabel` returns ISO dates except Today/Yesterday.
- Goal: show dates as YYYY-MM-DD regardless of app and device language.
- Proposal:
  - Date field on the expense screen: replace the visible native date input (whose format follows the device language and can't be forced) with a text field showing YYYY-MM-DD, plus the chevron/button that opens the native date picker. Typed dates are validated.
  - Date headings in the expense list and "Already paid": use YYYY-MM-DD instead of "10 november".
- Decision (2026-11-12): keep "Today"/"Yesterday" for the two most recent days; YYYY-MM-DD for all other dates.
- Supersedes the remaining part of B-004.

### B-002 – Default list names keep their original language
- Status: Done 2026-11-12. `renameDefaults` renames lists whose name is exactly the old language's default ("Våra utgifter"/"Our expenses", "Lista N"/"List N").
- Priority: Medium
- Lists created automatically get a name in the current language ("Våra utgifter", "Lista 2" / "Our expenses", "List 2"). After switching language the name stays in the old language, so the UI mixes Swedish and English.
- Proposed fix: when the language changes, rename lists whose name is still exactly a default name in the old language.

### B-003 – English: amount field shows "kr" while amounts show "SEK"
- Status: Done 2026-11-12. `curSym` now takes the currency label from `Intl` in the current language ("kr" in Swedish, "SEK" in English).
- Priority: Low
- In English, amounts are formatted as "SEK 1,000" but the suffix in the amount field on the expense screen says "kr".
- Proposed fix: use the same currency label as the formatted amounts in the current language.

### B-004 – Date field follows the browser language, not the app language
- Status: Done 2026-11-12 (partial). The date input gets `lang` set to the app locale. Chrome and Safari still use the device/browser language for the picker; a full fix would need a custom date picker.
- Priority: Low
- The native date picker on the expense screen uses the browser/phone language and format (e.g. mm/dd/yyyy on an English phone with the app in Swedish).
- Proposed fix: set `lang` on the date input to the app language (respected by some browsers). A full fix would need a custom date picker; not proposed.

### B-006 – English percent spacing
- Status: Done 2026-11-12. English percent strings without space ("100% assigned").
- Priority: Low
- English shows "100 % assigned" / "10 % left to assign" with a space before %, which is Swedish style. English style is "100%".
- Proposed fix: use language-specific percent formatting.

### B-007 – Date field has a native arrow/icon that doesn't match the category field
- Status: Done 2026-11-12. Date input uses the same chevron as the select; the native picker indicator is invisible and stretched over the field so tapping anywhere opens the picker; value left-aligned on iOS.
- Priority: Medium
- The category select uses a custom chevron (`appearance: none` + SVG), but the date input keeps the browser's own picker indicator (a calendar icon on desktop Chrome, a native arrow on mobile browsers), so the two fields directly above each other look different.
- Proposed fix: hide the native indicator, give the date field the same custom icon as the select (stretching the invisible native indicator over the field so tapping anywhere still opens the picker), and left-align the value on iOS.

### F-001 – Swish payments when settling up
- Priority: Medium
- Status: Done 2026-11-12. QR payload verified by decoding; not yet scanned with a real Swish app (format taken from open-source implementations, Swish's developer docs were not reachable).
- Goal: In the settle-up view, let the payer open Swish with recipient, amount and message prefilled.
- Proposal:
  - Optional Swish number per person (person sheet). Validate Swedish mobile numbers (07x…, +467x…) and Swish business numbers (123…).
  - "Swish" button on each settle-up card when the list currency is SEK and the recipient has a number.
  - Mobile: open the Swish app via the `swish://payment?data=…` deep link (payee, amount, message = list name, editable).
  - Desktop: show a QR code the payer scans with the Swish app (generated locally, no external service).
  - Payment is still confirmed manually with "Paid" (Swish gives no callback to private web apps).
- Decisions (2026-11-12):
  - Swish numbers are included in share links and backups (user approved; share links put them in the URL).
  - Desktop shows a QR code to scan with the phone (built-in QR generator, no external service).
- Implementation notes:
  - Numbers stored per person as `swish`: Swedish mobile as `46XXXXXXXXX`, business numbers as `123XXXXXXX` (`swishNorm`).
  - QR payload: `C<payee>;<amount>;<message>;4` (only message editable). Deep link: `swish://payment?data=<JSON>` (shown as "Open Swish" on touch devices).
  - QR codes are generated by the built-in `qrSvg` (byte mode, ECC M, versions 1–10).
