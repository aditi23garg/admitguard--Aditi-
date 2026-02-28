# Prompt 02 — Strict Validation Rules

## Sprint: 1
## Purpose: Add strict validation rules to the form
## Tool: Claude AI (claude.ai)

---

## The Prompt

```
Now add validation for STRICT rules only.
These rules block form submission if violated.
No exceptions allowed for these.

Rules:
1. Full Name: required, min 2 chars, no numbers
2. Email: valid format (must have @ and domain)
3. Phone: exactly 10 digits, starts with 6/7/8/9
4. Qualification: must select an option (not blank)
5. Interview Status: if "Rejected" → block submission
   completely, show red banner at top of form saying
   "Rejected candidates cannot be enrolled."
6. Aadhaar: exactly 12 digits, no letters
7. Offer Letter "Yes" only allowed if Interview 
   Status is "Cleared" or "Waitlisted"

Show errors in RED text below each field as user 
types. Submit button disabled until all strict 
rules pass.
```

---

## What the AI Generated
- validateFullName() function
- validateEmail() function
- validatePhone() function
- validateAadhaar() function
- validateQualification() function
- validateInterviewStatus() function with red banner
- validateOfferLetter() function with conditional check
- canSubmit() function checking all rules
- Event listeners on all input fields

## What Worked
- Red error messages appeared inline correctly
- Submit button correctly disabled
- Rejected banner appeared when status = Rejected
- Offer letter conditional rule worked

## What Needed Fixing
- Phone validation initially accepted letters
  → Fixed by using /^\d{10}$/ regex
- Email validation was too basic initially
  → Improved in later prompt

## Key Learning
Regex patterns are powerful for validation.
/^\d{10}$/ means: start(^), exactly 10 digits(\d{10}), end($)
Being specific about what "valid" means gives better results.
