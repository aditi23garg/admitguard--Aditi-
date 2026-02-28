# Prompt 08 — UI Polish & Light/Dark Mode

## Sprint: 3
## Purpose: Polish UI, add light/dark mode, fix remaining bugs
## Tool: Claude AI (claude.ai)

---

## Prompt 8A — Light/Dark Mode Toggle

```
Add a light/dark mode toggle button in the header.

Requirements:
- Button in header right side
- Dark mode is default
- In dark mode → button says "☀️ Light Mode"
- In light mode → button says "🌙 Dark Mode"
- Clicking toggles between modes
- User preference saved to localStorage
- On page load → restore saved preference
- All text must be clearly visible in both modes
- All errors, warnings, success messages must 
  be visible in both modes
```

### What the AI Generated
- .theme-toggle button CSS
- body.light CSS overrides for all colours
- toggleTheme() JavaScript function
- Self-invoking function to load saved theme
- localStorage save/load for theme preference

### Bug Found: Header Text Invisible in Light Mode
- Problem: Header title "AdmitGuard" uses white text
  White text on light background = invisible
- Fix: Added body.light .header-text h1 { color: #1a202c }
  Dark text in light mode → clearly visible

---

## Prompt 8B — Input Quality Validation

```
Add quality validation to these fields:

Full Name:
- Block if same character repeats 3+ times in a row
  Example: "SSSSSS" → invalid
- Block if no vowels in name
  Example: "bcdfgh" → invalid  
- Block if one character is more than 50% of name
  Example: "SSSSAB" → invalid (S is 67%)
- Block special characters (@, #, !, etc.)
  Exception: allow dots and hyphens for names like 
  "A.P.J. Abdul Kalam" and "Mary-Jane"

Phone Number:
- Block if all 10 digits are the same
  Example: "9999999999" → invalid
- Block if any digit repeats more than 6 times
  Example: "9842222222" → invalid
- Block ascending sequence
  Example: "9123456789" → invalid
- Block descending sequence  
  Example: "9876543210" → invalid
```

### What the AI Generated
- Updated validateFullName() with 4 quality checks
- Updated validatePhone() with 4 pattern checks
- Descriptive error messages for each check

### Test Results After Fix

| Input | Check | Result |
|---|---|---|
| "SSSSSSSSS" | Repeated chars | ✅ Blocked |
| "bcdfgh" | No vowel | ✅ Blocked |
| "SSSSAB" | >50% same char | ✅ Blocked |
| "Raj@Patel" | Special char | ✅ Blocked |
| "A.P.J. Kalam" | Dot allowed | ✅ Passed |
| "9999999999" | All same | ✅ Blocked |
| "9842222222" | Too many 2s | ✅ Blocked |
| "9876543210" | Descending | ✅ Blocked |
| "9123456789" | Ascending | ✅ Blocked |
| "9845123456" | Valid | ✅ Passed |

---

## Prompt 8C — Confirmation & Success Screen

```
Add a confirmation modal before submission that 
shows a summary of all entered data.

After successful submission show a success screen:
- Green checkmark icon
- "Submission Successful!" heading
- Summary table with all key fields
- Exceptions used count
- Flagged for review status
- Saved to Google Sheets status
- "New Entry" button to reset form
```

### What the AI Generated
- Success screen HTML (hidden by default)
- showSuccess() function with dynamic summary
- resetForm() function to clear all state
- New Entry button

---

## Final Bugs Fixed in This Sprint

| Bug | Found How | Fix Applied |
|---|---|---|
| "sdjska@lsdkl" passing name | Screenshot review | Special char check moved first |
| "kdfdl.com" passing email | Screenshot review | Vowel check added to domain |
| "23-12-0003" DOB not blocked | Screenshot review | Year < 1900 explicit check |
| Header invisible in light mode | Visual testing | body.light colour overrides added |

---

## Overall Prompt Engineering Reflection

### What Made Prompts Work Well
- Giving specific examples: "Valid: 9845123456, Invalid: 9999999999"
- Defining exact error messages in the prompt
- Saying what NOT to do: "Do not hardcode 2025"
- One feature per prompt — never overloading

### What Caused Prompts to Need Iteration
- Edge cases not specified upfront
- Visual bugs only visible after testing in browser
- Cross-browser behavior differences

### R.I.C.E. Framework Usage
Every prompt followed this pattern:
- Role: "You are a senior frontend developer..."
- Intent: Clear description of what to build
- Constraints: Single file, no frameworks, specific rules
- Examples: Valid/invalid input pairs for each field

### Total Prompts Used: 8 major + multiple refinements
### Total Iterations: ~15 refinement cycles
### Key Takeaway: Iteration is the skill, not the first prompt
