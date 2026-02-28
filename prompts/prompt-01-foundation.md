# Prompt 01 — Foundation Form Structure

## Sprint: 1
## Purpose: Build the basic form with all 11 fields
## Tool: Claude AI (claude.ai)

---

## The Prompt

```
Role: You are a senior frontend developer building 
an internal business tool for an education company.

Task: Create a candidate admission form with these 
11 fields:
- Full Name (text input)
- Email (text input)
- Phone (text input)
- Date of Birth (date picker)
- Highest Qualification (dropdown: B.Tech, B.E., 
  B.Sc, BCA, M.Tech, M.Sc, MCA, MBA)
- Graduation Year (number input)
- Percentage or CGPA (number input with toggle 
  to switch between percentage and CGPA mode)
- Screening Test Score (number input, 0-100)
- Interview Status (dropdown: Cleared, Waitlisted, 
  Rejected)
- Aadhaar Number (text input)
- Offer Letter Sent (Yes/No toggle)

Constraints:
- Single HTML file (HTML + CSS + JS all in one file)
- Clean, professional design — not a generic template
- Each field has: label, input box, and space for 
  error message below it
- Submit button at the bottom
- Do NOT add any validation logic yet. 
  Just build the form structure first.
```

---

## What the AI Generated
- Complete HTML file with all 11 fields
- Dark professional theme with CSS variables
- Card-based layout with section grouping
- Submit button at the bottom
- Space for error messages below each field

## What Worked
- Form structure was clean and professional
- Dark theme looked good immediately
- Two-column grid layout was correct
- Dropdown options were correctly set

## What Needed Fixing
- Percentage/CGPA toggle needed refinement
- Offer Letter Yes/No toggle needed custom styling
- Header subtitle had "Futurense Technologies" branding
  → Changed to generic "Admission Data Validation & Compliance System"

## Key Learning
Starting with structure only (no validation) was the right approach.
Trying to build everything in one prompt produces messy output.
One feature at a time = cleaner, more controllable result.

## Status: Complete