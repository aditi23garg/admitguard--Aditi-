# Prompt 03 — Edge Case Testing & Fixes

## Sprint: 1
## Purpose: Test strict rules against edge cases and fix issues
## Tool: Claude AI (claude.ai)

---

## The Prompt

```
Test the form against these edge cases and fix 
any issues you find:

1. Name field: Enter "A" (too short), "John123" 
   (has numbers), "" (empty)
2. Phone: Enter "1234567890" (doesn't start with 6-9), 
   "98765" (too short)
3. Aadhaar: Enter "12345678901" (11 digits), 
   "12345678901a" (has letter)
4. Set Interview Status to "Rejected" then try to submit
5. Set Interview Status to "Waitlisted" then set 
   Offer Letter to "Yes" — should work
6. Set Interview Status to "Rejected" then set 
   Offer Letter to "Yes" — should block

Make sure all edge cases are handled correctly.
```

---

## What the AI Generated
- Refined validation functions for all edge cases
- Better error messages for each specific scenario
- Fixed phone validation to reject non-digit input
- Fixed Aadhaar to reject mixed alphanumeric input

## Test Results After Fix

| Test Case | Expected | Result |
|---|---|---|
| Name "A" | Too short error | ✅ Pass |
| Name "John123" | No numbers error | ✅ Pass |
| Name "" | Required error | ✅ Pass |
| Phone "1234567890" | Must start 6-9 | ✅ Pass |
| Phone "98765" | Must be 10 digits | ✅ Pass |
| Aadhaar "12345678901" | Must be 12 digits | ✅ Pass |
| Aadhaar "12345678901a" | No letters | ✅ Pass |
| Status "Rejected" + submit | Blocked | ✅ Pass |
| Status "Waitlisted" + offer Yes | Allowed | ✅ Pass |
| Status "Rejected" + offer Yes | Blocked | ✅ Pass |

## What Worked
- All 6 edge cases passed after fixes
- Error messages were clear and user-friendly

## Key Learning
Always test with boundary values:
- Too short (below minimum)
- Too long (above maximum)  
- Wrong type (letters instead of numbers)
- Empty (blank)
- Exact boundary (exactly at limit)
Testing reveals bugs that prompts miss.
