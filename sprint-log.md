# Sprint Log — AdmitGuard
# Admission Data Validation & Compliance System
# Author: Aditi Garg | IIT Gandhinagar | Feb 2026

---

## Sprint 0 (Day 3 — Wednesday)
**Goal:** Understand problem, plan approach, set up repo, research tools

### What I Did
- Read and annotated the full AdmitGuard project brief
- Created GitHub repository: admitguard--Aditi-
- Written README.md with problem statement and approach
- Created complete folder structure:
  docs/, prompts/, src/, config/
- Drew wireframe on Excalidraw — all 11 fields mapped
- Created research-notes.md and documented learnings
- Created sprint-log.md and architecture.md
- Drafted first 3 prompts on paper before running them

### Key Decisions
- Used Claude AI instead of Google AI Studio
  Reason: Same Vibe Coding approach, easier to iterate,
  can explain every line of generated code in same conversation
- Chose single-page form over multi-step wizard
  Reason: Simpler UX, all fields visible at once,
  easier to see exception counter and submit button

### Research Done
- Read full project brief thoroughly
- Read Anthropic Prompt Engineering Guide
- Studied R.I.C.E. prompting framework
- Researched localStorage for client-side storage
- Researched GitHub Pages for free hosting

### Blockers
- None

### Commits
- sprint-0: project setup, planning docs, and research notes
- sprint-0: wireframe added

---

## Sprint 1 (Day 4 — Thursday)
**Goal:** Working form with all 11 fields and strict validation

### What I Did
- Generated complete form structure with all 11 fields
  using Claude AI (Vibe Coding approach)
- Implemented strict validation rules:
  → Full Name: required, min 2 chars, no numbers
  → Email: valid format check
  → Phone: 10 digits, starts with 6/7/8/9
  → Qualification: must select from dropdown
  → Interview Status: blocks if Rejected
  → Aadhaar: exactly 12 digits, no letters
  → Offer Letter: cannot be Yes if status is Rejected
- Added real-time inline validation (errors as user types)
- Submit button disabled until all strict rules pass
- Tested all 6 edge cases from the brief:
  → Name too short, has numbers
  → Phone starts with 1, too short
  → Aadhaar 11 digits, has letters
  → Rejected + submit → blocked
  → Waitlisted + offer Yes → allowed
  → Rejected + offer Yes → blocked

### Key Decisions
- Real-time validation instead of on-submit validation
  Reason: Better user experience — errors shown immediately
- Single HTML file (HTML + CSS + JS together)
  Reason: No dependencies, opens in any browser, easy to share

### AI Evaluation
- Prompt 1 output was ~80% correct
  Had to refine dropdown behavior in second prompt
- Phone validation initially accepted letters
  Fixed by being more specific in edge case prompt
- Email validation was too basic initially
  Improved significantly in later iteration

### Blockers
- None

### Commits
- sprint-1: base form structure with 11 fields
- sprint-1: strict validation rules added
- sprint-1: edge case handling complete

---

## Sprint 2 (Day 5 — Friday AM)
**Goal:** Soft rules + exception system

### What I Did
- Added soft rule validations with yellow warnings:
  → Date of Birth: age 18-35
  → Graduation Year: 2015 to current year + 4
  → Percentage/CGPA: ≥ 60% or ≥ 6.0
  → Screening Test Score: ≥ 40
- Built exception toggle system:
  → Yellow warning appears when soft rule violated
  → "Request Exception" checkbox shows
  → When checked → rationale text area appears
- Implemented rationale validation:
  → Minimum 30 characters
  → Must contain keyword: "approved by", "special case",
    "documentation pending", or "waiver granted"
- Built exception counter:
  → Shows "Active Exceptions: X/4"
  → Flag banner appears when count > 2
- Tested all soft rule scenarios thoroughly

### Key Decisions
- Visual distinction between strict (red) and soft (yellow)
  Reason: Operators must instantly see which type of issue it is
- Exception rationale keywords enforced strictly
  Reason: Prevents gaming the system with meaningless overrides

### Blockers
- None

### Commits
- sprint-2: soft rules and exception system
- sprint-2: exception counter and flagging

---

## Sprint 3 (Day 5 — Friday PM + Evening)
**Goal:** Config engine + audit log + polish + deployment

### What I Did

#### Configurable Rules Engine
- Created RULES config object in JavaScript
  All rules stored in one place — not scattered in code
- Created rules.json in config/ folder
  Complete rule documentation for all 11 fields
  Includes validations, error messages, descriptions

#### Audit Log
- Built audit log tab with full submission table
- Columns: Name, Timestamp, Exceptions, Flagged, Details
- localStorage persistence — data survives page refresh
- Clear log button with confirmation dialog

#### UI Polish + Light/Dark Mode
- Added light/dark mode toggle button in header
- User preference saved to localStorage
- Fixed header text visibility in light mode
- Professional dark theme as default

#### Smart Validation Improvements
- Full Name:
  → Added special character blocking
  → Added repeated character detection
  → Added vowel requirement
- Email:
  → Added domain whitelist
  → Added fake domain detection (no vowels in domain)
  → Added blocked domains list
  → 3-letter domain exemption (tcs, ibm, hcl)
- Phone:
  → Added all-same-digit detection
  → Added too-many-repeats detection
  → Added sequential pattern detection
- Score: Added range validation (negative + above max)
- Test Score: Added range validation
- DOB: Added future date block, year < 1900 block
- Graduation Year: Made max dynamic (current year + 4)

#### Google Sheets Integration
- Created Google Apps Script (doPost function)
- Deployed as Web App with "Anyone" access
- Connected webpage to Apps Script via fetch()
- async/await for non-blocking submission
- localStorage fallback if Sheets fails
- Success screen shows "Saved to Google Sheets: ✅ Yes"

#### GitHub Pages Deployment
- Moved index.html to root folder
- Enabled GitHub Pages on main branch
- Live URL: https://aditi23garg.github.io/admitguard--Aditi-/
- CORS issue resolved by hosting on https://

### Key Decisions
- GitHub Pages for hosting
  Reason: Free, permanent, fixes CORS issue with Google Sheets
- localStorage as fallback for Google Sheets
  Reason: Data never lost even if internet fails
- Dynamic graduation year max (currentYear + 4)
  Reason: Hardcoded value would become wrong every year

### Blockers
- CORS error: local file couldn't call Google Sheets API
  Root cause: Browser blocks file:// → https:// requests
  Fix: Hosted on GitHub Pages (https://) → resolved
- Git push rejected (remote had changes)
  Fix: git pull origin main --rebase → then push

### Commits
- sprint-3: configurable rules engine refactored
- sprint-3: audit log and data persistence
- sprint-3: UI polish and light/dark mode
- sprint-3: smart validation improvements
- sprint-3: google sheets integration added
- sprint-3: index.html added to root for GitHub Pages
- sprint-3: rules.json config file added

---

## Sprint 4 (Day 5 Evening + Day 6 Morning)
**Goal:** Presentation prep + final documentation

### What I Did
- Updated README.md with complete project documentation
  → Live app link
  → Complete features table
  → All validation rules documented
  → Technical architecture diagram
  → How to run locally
  → How to test (with exact test cases)
  → Sprint summary table
- Updated research-notes.md with full learnings
  → R.I.C.E. framework explained
  → All bugs found and fixed documented
  → Honest reflection on what worked/challenged
- Created rules.json configuration file
- Created presentation slides (9 slides, Google Slides)
- Written speaker notes for each slide
- Rehearsed presentation — under 5 minutes
- Prepared answers for 3 tough Q&A questions

### Presentation Structure
```
Slide 1 → Title (15 sec)
Slide 2 → Problem Statement (45 sec)
Slide 3 → Impact Analysis (30 sec)
Slide 4 → Proposed Solution (45 sec)
Slide 5 → Live Demo (90 sec)
Slide 6 → Technical Architecture (30 sec)
Slide 7 → Prompt Engineering Approach (30 sec)
Slide 8 → Limitations & Next Steps (20 sec)
Slide 9 → Recommendation (15 sec)
Total  → 5 minutes exactly
```

### Q&A Preparation
- Q: What if we need to add a new rule next month?
  A: Edit rules.json config file — no code changes needed

- Q: How do you ensure rationale isn't gamed?
  A: 30 char minimum + required keywords + manager review flag

- Q: Why webpage over Google Sheets add-on?
  A: Full control over validation logic + better UX +
     still integrates with Google Sheets for data storage

### Blockers
- None

### Commits
- sprint-4: README updated with complete documentation
- sprint-4: research notes updated with complete learnings
- sprint-4: sprint log completed
- sprint-4: presentation deck added to docs/

---

## Project Summary

### Final App Stats
```
Total fields:          11
Strict rules:          7
Soft rules:            4
Validation checks:     25+
Lines of code:         ~1600
Commits:               15+
Build time:            2 days
```

### Features Delivered
```
Must Have (FR-1 to FR-8):    ✅ All 8 delivered
Should Have (FR-9):          ✅ Delivered
Good to Have (FR-12):        ✅ Light/Dark mode delivered
Bonus:                       ✅ Google Sheets integration
Bonus:                       ✅ GitHub Pages hosting
```

### Live App
```
URL: https://aditi23garg.github.io/admitguard--Aditi-/
```

### Key Takeaway
The most valuable lesson from this project was that Vibe Coding
is not about getting perfect code in one prompt. It is about
understanding the problem deeply, breaking it into small pieces,
testing thoroughly, and iterating systematically.

The bugs we found — fake names passing, fake email domains accepted,
impossible dates not blocked — were found because we THOUGHT about
edge cases. That thinking is the real skill. AI amplifies it.

## Final Status: COMPLETE ✅
Live URL: https://aditi23garg.github.io/admitguard--Aditi-/
