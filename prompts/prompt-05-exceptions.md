# Prompt 05 — Exception Counter & Flagging

## Sprint: 2
## Purpose: Add exception counter and manager review flag
## Tool: Claude AI (claude.ai)

---

## The Prompt

```
Add a system-level rule:

Count the number of active exceptions on the 
current form. Display this count prominently 
near the submit button as: 
"Active Exceptions: X/4"

If the count exceeds 2, show a warning banner:
"⚠️ This candidate has more than 2 exceptions. 
Entry will be flagged for manager review."

The submit button should still work, but the 
entry should be visually marked as "Flagged" 
in any data display.

Also update the audit log so flagged entries 
show clearly.
```

---

## What the AI Generated
- updateExceptionCounter() function
- Exception counter display element (0/4)
- Flag banner HTML (hidden by default)
- Updated submitForm() to include flagged status
- Updated audit log to show flagged badge

## How the Counter Works
```javascript
// Count active exceptions
const activeExcs = Object.keys(excActive)
  .filter(k => excActive[k] && softViolated[k]);
const count = activeExcs.length;

// Update display
document.getElementById('exc-counter')
  .textContent = count + ' / 4';

// Show flag banner if > 2
if (count > 2) {
  flagBanner.classList.add('visible');
}
```

## What Worked
- Counter updated in real-time as exceptions toggled
- Flag banner appeared correctly at 3+ exceptions
- Flag banner disappeared when exception removed
- Audit log showed flagged badge correctly

## What Needed Fixing
- Counter was not updating when exception unchecked
  → Fixed by calling updateExceptionCounter() 
    in toggleRationale() function

## Test Results

| Exceptions | Counter | Flag Banner |
|---|---|---|
| 0 | 0/4 | Hidden |
| 1 | 1/4 | Hidden |
| 2 | 2/4 | Hidden |
| 3 | 3/4 | ⚠️ Visible! |
| 4 | 4/4 | ⚠️ Visible! |
| Back to 2 | 2/4 | Hidden again |

## Key Learning
System rules are computed automatically — 
not controlled by the user.
The excActive and softViolated objects together 
determine if an exception is truly "active".
Both must be true for the counter to increment.
