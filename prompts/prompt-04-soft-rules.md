# Prompt 04 — Soft Rule Validation

## Sprint: 2
## Purpose: Add soft rule validation with yellow warnings
## Tool: Claude AI (claude.ai)

---

## The Prompt

```
Now add SOFT rule validations. These are different 
from strict rules — they block submission by default 
BUT the user can override them.

Soft rules:
1. Date of Birth: Candidate must be between 18 and 
   35 years old (calculated from today's date to DOB). 
2. Graduation Year: Must be between 2015 and 2025.
3. Percentage/CGPA: If in percentage mode, must be 
   >= 60%. If in CGPA mode (10-point scale), must 
   be >= 6.0.
4. Screening Test Score: Must be >= 40 out of 100.

When a soft rule is violated:
- Show a yellow/amber warning (not red error) 
  below the field
- Show a toggle/checkbox labeled "Request Exception"
- When the toggle is ON, show a text area labeled 
  "Exception Rationale"
- The rationale must be at least 30 characters long
- The rationale must contain at least ONE of these 
  phrases: "approved by", "special case", 
  "documentation pending", "waiver granted"
- If the rationale doesn't meet these conditions, 
  show a helpful error message
- If the rationale IS valid, the soft rule violation 
  is overridden and submission is allowed

Keep the form visually clear:
- Strict errors in red
- Soft warnings in amber/yellow
- Valid fields in green
```

---

## What the AI Generated
- validateDOB() with age calculation
- validateGradYear() with range check
- validateScore() with mode-aware threshold
- validateTestScore() with threshold check
- Exception block HTML for each soft rule field
- toggleRationale() function
- validateRationale() function with keyword check
- Updated canSubmit() to handle soft rule exceptions

## What Worked
- Yellow warnings appeared correctly
- Exception toggle showed/hid rationale area
- Rationale validation worked for length and keywords
- Visual distinction between red errors and yellow warnings

## What Needed Fixing
- Age calculation had edge case with leap years
  → Fixed by checking month and day difference
- Score validation needed to be mode-aware
  → Fixed by reading scoreMode variable

## Key Learning
Soft rules need TWO checks:
1. Is the rule violated? → show warning
2. If violated, is the exception valid? → allow/block submit
The canSubmit() function must check BOTH conditions.
