# Research Notes — Vibe Coding & AdmitGuard Build

## What is Vibe Coding?

Vibe Coding means describing what you want to build in plain English
and letting an AI generate the code. You don't write the code from 
scratch — you describe, iterate, test, and refine.

The skill is NOT in typing code.
The skill IS in:
- Writing clear, specific prompts
- Testing the output thoroughly
- Identifying what's wrong
- Iterating until it's right

---

## Tool I Used

Instead of Google AI Studio, I used **Claude AI by Anthropic**
directly in the browser (claude.ai).

### Why Claude instead of Google AI Studio?
- No new tool setup needed
- Can explain every line of generated code
- Easy to iterate — ask to fix, modify, explain
- Can build, debug, and improve in one conversation
- Generated complete HTML + CSS + JS in one file

### How it worked:
```
I described what to build
        ↓
Claude generated the code
        ↓
I copied into index.html
        ↓
Opened in Chrome → tested
        ↓
Found issues → described to Claude
        ↓
Claude fixed → I tested again
        ↓
Repeat until perfect
```

---

## Resources I Used

### 1. Project Brief (Primary Resource)
- Read and annotated the full AdmitGuard project brief
- Identified all 12 eligibility rules
- Understood difference between strict and soft rules
- Understood the exception rationale system

### 2. Anthropic Prompt Engineering Guide
- URL: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering
- Key learning: Be specific, set role, add constraints, give examples

### 3. Claude AI (claude.ai)
- Used for Vibe Coding throughout the project
- Generated all HTML, CSS, JavaScript code
- Debugged issues as they were found
- Explained every part of the code

### 4. GitHub Docs
- URL: https://docs.github.com
- Used for: repo setup, commits, GitHub Pages hosting

### 5. Google Apps Script Documentation
- Used for: connecting webpage to Google Sheets
- Key learning: doPost() function receives POST requests
- Deployment: Web app with "Anyone" access

---

## Key Things I Learned

### About Vibe Coding
- First output is NEVER perfect — iteration is the skill
- One feature per prompt gives better results than one big prompt
- Always test with edge cases — AI misses them often
- Read and understand the generated code — don't just copy paste
- The quality of your prompt directly determines quality of output

### About Prompt Engineering (R.I.C.E. Framework)
```
R → Role
    "You are a senior frontend developer..."
    Giving AI a role improves output quality significantly

I → Intent
    "Build a candidate admission form with 11 fields..."
    Be specific about WHAT you want

C → Constraints
    "Single HTML file, no frameworks, clean professional design..."
    Tell AI what NOT to do — equally important

E → Examples
    "Valid phone: 9876543210. Invalid: 1234567890 (starts with 1)"
    Show good and bad examples for validation rules
```

### About JavaScript Validation
- Regex patterns are powerful for validation
  Example: `/^\d{10}$/` checks exactly 10 digits
- Real-time validation (as user types) is better UX than on-submit
- Edge cases matter — always test boundary values
  Example: age exactly 18, age exactly 35
- `async/await` needed for sending data to external APIs

### About HTML/CSS
- CSS variables make theming (light/dark mode) easy
  Change one variable → updates everywhere
- Single file apps (HTML+CSS+JS) are powerful for prototypes
- `localStorage` stores data in browser without a server

### About Git & GitHub
- `git add .` → stages all changes
- `git commit -m "message"` → saves snapshot
- `git push origin main` → uploads to GitHub
- `git pull origin main --rebase` → get remote changes first
- Commit messages should be descriptive and follow format:
  `sprint-N: what you did`

### About Deployment
- GitHub Pages turns a repo into a free live website
- index.html must be in ROOT folder for GitHub Pages
- CORS error: local files can't call internet APIs
  Fix: host the file online (GitHub Pages)
- `no-cors` mode in fetch() allows cross-origin requests

### About Google Sheets Integration
- Google Apps Script acts as middleware between webpage and Sheets
- `doPost(e)` function receives data sent from webpage
- `sheet.appendRow(row)` adds a new row to the sheet
- Deploy as Web App with "Anyone" access for public forms
- Always have localStorage as fallback in case Sheets fails

---

## Bugs Found During Testing & How Fixed

### Bug 1 — Name field accepting "@" symbol
- Problem: Special character check had wrong regex
- Fix: `/[^a-zA-Z\s.\-']/` blocks everything except letters,
  spaces, dots, hyphens, apostrophes

### Bug 2 — Fake email domains passing (e.g. kdfdl.com)
- Problem: Only checked domain length > 3 chars
- Fix: Added vowel check — real company domains almost always
  have vowels. "kdfdl" has no vowels → blocked
- Exception: Short 3-letter domains like tcs, ibm, hcl are exempt

### Bug 3 — DOB year "0003" not blocked
- Problem: Age calculation behaved unexpectedly with year 0003
- Fix: Explicit check `dob.getFullYear() < 1900` → blocked

### Bug 4 — Graduation year max was hardcoded
- Problem: Hardcoded 2025 would become wrong next year
- Fix: Dynamic calculation `currentYear + 4` → always correct

### Bug 5 — Percentage/CGPA accepting negative values
- Problem: No range check existed
- Fix: Added strict blocks for negative values and above-max values

### Bug 6 — Google Sheets "Failed to fetch" error
- Problem: Local file (file://) cannot call internet APIs (CORS)
- Fix: Hosted on GitHub Pages (https://) → CORS resolved

---

## What Worked Well

```
✅ Building one feature at a time (not everything at once)
✅ Testing each feature before moving to next
✅ Describing bugs exactly to Claude → got precise fixes
✅ Using localStorage as fallback for Google Sheets
✅ GitHub Pages for free, instant hosting
✅ CSS variables for easy light/dark mode
✅ Rules config object → all rules in one place
```

## What Was Challenging

```
⚠️ CORS error took time to understand and fix
⚠️ DOB year validation had unexpected edge cases
⚠️ Email domain validation needed multiple iterations
⚠️ Git push rejected → needed git pull first
⚠️ index.html needed to be in root for GitHub Pages
```

---

## Questions I Had (Now Answered)

**Q: Do I need Google AI Studio specifically?**
A: No. Claude AI works better for this use case — 
   generates complete code and explains it in the same conversation.

**Q: Do I need a backend server?**
A: No. Single HTML file runs in any browser.
   Google Sheets via Apps Script handles data storage.

**Q: Where is data stored?**
A: Two places — localStorage (browser) and Google Sheets.
   localStorage works offline, Sheets needs internet.

**Q: What is CORS and why did it block Google Sheets?**
A: CORS = Cross Origin Resource Sharing.
   Browser blocks local files from calling internet APIs for security.
   Fix: Host the file online so both are https://.

**Q: How does Google Apps Script work?**
A: It's a server-side script that runs on Google's servers.
   Our webpage sends data → Apps Script receives it → 
   adds row to Google Sheet.

**Q: What is async/await in JavaScript?**
A: JavaScript normally doesn't wait for things.
   async/await tells it to wait for a network request
   to complete before moving to the next line.

---

## Final Reflection

The most important lesson from this project:

> "The first AI output is a starting point, not a final answer.
>  The real skill is in testing, finding gaps, and iterating.
>  AI is a multiplier — it amplifies your thinking,
>  not a replacement for it."

Building AdmitGuard taught me that Vibe Coding is not about
getting perfect code in one prompt. It's about having a clear
understanding of the problem, breaking it into small pieces,
and systematically building and refining each piece.

The bugs we found — fake names, fake emails, impossible dates —
were found because we THOUGHT about edge cases, not because
the AI automatically handled them.

That's the skill. That's what separates a good Vibe Coder
from someone who just copies AI output.
