# Prompt 07 — Audit Log & Google Sheets Integration

## Sprint: 3
## Purpose: Add audit log, localStorage persistence, Google Sheets sync
## Tool: Claude AI (claude.ai)

---

## Prompt 7A — Audit Log

```
Add an audit trail feature:

1. Every successful form submission gets logged with:
   - Timestamp
   - All field values entered
   - Number of exceptions used
   - Which fields had exceptions + the rationale text
   - Whether the entry was flagged for manager review

2. Add a separate "Audit Log" tab that shows all 
   past submissions in a table format. Include:
   - Candidate name
   - Submission timestamp
   - Exception count
   - Flagged status (Yes/No)
   - A button to expand and see full details

3. Store the log in localStorage so it persists 
   across page refreshes.

4. Add a "Clear Log" button with a confirmation 
   dialog for testing.
```

### What the AI Generated
- Audit log tab in navigation
- renderAuditLog() function
- Table with Name, Timestamp, Exceptions, Flagged, Details
- showDetail() function for full entry view
- clearLog() function with confirm dialog
- localStorage save on every submission
- localStorage load on page open

### Test Results
| Action | Expected | Result |
|---|---|---|
| Submit entry | Appears in log | ✅ Pass |
| Refresh page | Data still there | ✅ Pass |
| Submit flagged entry | Shows Yes badge | ✅ Pass |
| Click View | Shows full details | ✅ Pass |
| Clear log | Confirmation shown | ✅ Pass |
| Confirm clear | Log empty | ✅ Pass |

---

## Prompt 7B — Google Sheets Integration

```
Add Google Sheets integration:

When form is submitted, send all data to this 
Google Apps Script URL:
[URL provided after deploying Apps Script]

Requirements:
- Use fetch() with async/await
- Method: POST
- Mode: no-cors (for cross-origin requests)
- Send data as JSON in request body
- Show loading state on submit button: "⏳ Saving..."
- If Google Sheets save succeeds → show 
  "Saved to Google Sheets: ✅ Yes" in success screen
- If Google Sheets save fails → show warning but 
  still complete the submission (localStorage fallback)
- Data must always be saved to localStorage first,
  regardless of Google Sheets result
```

### What the AI Generated
- SHEETS_URL constant with deployment URL
- submitForm() converted to async function
- fetch() call with POST, no-cors, JSON body
- Try/catch for error handling
- Loading state on submit button
- savedToSheets flag in entry object
- Updated success screen with Sheets status row

### The Integration Flow
```
User clicks Submit
        ↓
Button → "⏳ Saving..."
        ↓
Step 1: Save to localStorage (always)
        ↓
Step 2: fetch(SHEETS_URL, { method: POST, ... })
        ↓
    Success?          Failure?
        ↓                 ↓
savedToSheets=true  savedToSheets=false
        ↓                 ↓
"✅ Yes"            "⚠ Failed (saved locally)"
```

### Bug Found: CORS Error
- Problem: Local file (file://) cannot call https://
  Browser blocks this for security
- Error: "Failed to fetch"
- Fix: Host file on GitHub Pages (https://)
  Both are https:// → CORS resolved

### Key Learning
async/await is needed for network requests.
Without it, JavaScript doesn't wait for the
fetch to complete before moving to next line.
localStorage as fallback ensures data is never
lost even if internet connection fails.
