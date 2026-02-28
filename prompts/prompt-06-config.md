# Prompt 06 — Configurable Rules Engine

## Sprint: 3
## Purpose: Move all rules into a config object + create rules.json
## Tool: Claude AI (claude.ai)

---

## The Prompt

```
Refactor the validation rules so they are NOT 
hardcoded in the form logic. Instead, store all 
rules in a separate JSON configuration object.

The form should READ from this config object to 
determine what validations to apply. This way, 
the operations team can update rules by editing 
the config, not the form code.

Also add these missing validations that were 
identified during testing:

1. Percentage cannot be negative or above 100
2. CGPA cannot be negative or above 10
3. Test Score cannot be negative or above 100
4. Date of Birth cannot be in the future
5. Date of Birth year cannot be before 1900
6. Graduation Year max should be dynamic:
   current year + 4 (not hardcoded 2025)

For Full Name, add these quality checks:
- No special characters (@, #, !, etc.)
- No character repeating more than 3 times in a row
- Must contain at least one vowel
- No single character making up more than 50% of name

For Phone, add pattern detection:
- Block if all digits are the same (9999999999)
- Block if any digit repeats more than 6 times
- Block ascending sequence (9123456789)
- Block descending sequence (9876543210)

For Email, add domain validation:
- Whitelist of allowed personal domains
- Block list of fake domains
- Allow professional domains (.com, .in, .org)
- Fake domain detection (no vowels in domain name)
```

---

## What the AI Generated
- RULES config object with all 11 field rules
- Updated validateFullName() with quality checks
- Updated validatePhone() with pattern detection
- Updated validateEmail() with domain validation
- Updated validateScore() with range validation
- Updated validateTestScore() with range validation
- Updated validateDOB() with future date check
- Updated validateGradYear() with dynamic max year
- Separate rules.json file for config/ folder

## The RULES Config Structure
```javascript
const RULES = {
  full_name:    { type: 'strict', minLen: 2, noNumbers: true },
  email:        { type: 'strict', emailFormat: true },
  phone:        { type: 'strict', digits: 10, startsWith: [6,7,8,9] },
  dob:          { type: 'soft',   minAge: 18, maxAge: 35 },
  qualification:{ type: 'strict', required: true },
  grad_year:    { type: 'soft',   minYear: 2015, maxYear: 2025 },
  score:        { type: 'soft',   minPct: 60, minCgpa: 6.0 },
  test_score:   { type: 'soft',   minScore: 40 },
  interview:    { type: 'strict', blockIfRejected: true },
  aadhaar:      { type: 'strict', digits: 12 },
  offer_letter: { type: 'strict', linkedTo: 'interview' },
};
```

## Bugs Found and Fixed in This Sprint

| Bug | Root Cause | Fix |
|---|---|---|
| Name "@" not caught | Regex order wrong | Moved special char check first |
| "kdfdl.com" passing | Only checked length | Added vowel check on domain |
| DOB "0003" not blocked | Age calc edge case | Added year < 1900 strict check |
| Grad year hardcoded 2025 | Static value | Changed to currentYear + 4 |
| Negative score passing | No range check | Added min/max strict validation |

## Key Learning
Dynamic values are better than hardcoded values.
currentYear + 4 will always be correct.
2030 hardcoded will be wrong in 2027.
Rules in a config object = easy to update without
touching the validation logic.

## Status: Complete
