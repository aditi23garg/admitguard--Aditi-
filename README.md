# 🛡️ AdmitGuard — Admission Data Validation & Compliance System

> A smart browser-based form that replaces unstructured Excel-based 
> candidate tracking with real-time validation, exception handling, 
> and a full audit trail.

---

## 🔗 Live App
**👉 https://aditi23garg.github.io/admitguard--Aditi-/**

No installation needed. Open in any browser and use immediately.

---

## 📋 The Problem We're Solving

Education companies managing admission pipelines face a critical 
data integrity problem:

- Candidate data entered into Excel with **zero validation rules**
- Ineligible candidates only discovered at **final document verification**
- **No structured way** to handle exceptions or document approvals
- Rules change between cohorts — **painful to update** in spreadsheets

This causes wasted counselor hours, damaged candidate experience, 
and compliance risk with institutional partners.

---

## ✅ Our Solution

AdmitGuard enforces eligibility rules **at the point of data entry** — 
not at the end of the pipeline.

### Key Features

| Feature | Status |
|---|---|
| 11-field candidate admission form | ✅ Built |
| Real-time field-level validation | ✅ Built |
| Strict rules — block submission | ✅ Built |
| Soft rules — yellow warnings | ✅ Built |
| Exception toggle + rationale system | ✅ Built |
| Rationale validation (30 chars + keywords) | ✅ Built |
| Exception counter (flags if > 2) | ✅ Built |
| Success screen with submission summary | ✅ Built |
| Audit log with all submissions | ✅ Built |
| Data persistence via localStorage | ✅ Built |
| Google Sheets real-time sync | ✅ Built |
| Light / Dark mode toggle | ✅ Built |
| Hosted on GitHub Pages | ✅ Live |

---

## 🔍 Validation Rules

### 🔴 Strict Rules (No exceptions — blocks submission)

| Field | Rule |
|---|---|
| Full Name | Required, min 2 chars, no numbers, no special characters, no repeated patterns |
| Email | Valid format, whitelisted domains, fake domain detection |
| Phone | 10 digits, starts with 6/7/8/9, no repeated/sequential patterns |
| Qualification | Must select from dropdown |
| Interview Status | If Rejected → submission completely blocked |
| Aadhaar | Exactly 12 digits, no letters |
| Offer Letter | Cannot be Yes if status is Rejected |

### 🟡 Soft Rules (Exception allowed with valid rationale)

| Field | Rule |
|---|---|
| Date of Birth | Age must be 18–35 years |
| Graduation Year | Must be between 2015 and current year + 4 |
| Percentage / CGPA | Percentage ≥ 60% or CGPA ≥ 6.0 |
| Screening Test Score | Must be ≥ 40 out of 100 |

### Exception Rationale Rules
- Minimum **30 characters**
- Must contain one of: `approved by`, `special case`, 
  `documentation pending`, `waiver granted`
- If **more than 2 exceptions** on one entry → flagged for manager review

---

## 🏗️ Technical Architecture

```
User fills form
      ↓
Validation Engine reads RULES config object
      ↓
Strict rules → block submission with red errors
Soft rules   → show yellow warning + exception toggle
      ↓
On Submit:
  1. Save to localStorage (works offline)
  2. Send to Google Sheets via Apps Script
      ↓
Audit Log updated with full entry details
```

### Tech Stack

| Layer | Technology |
|---|---|
| Structure | HTML5 |
| Design | CSS3 with CSS Variables |
| Logic | Vanilla JavaScript |
| Storage | localStorage (browser) |
| Data Sync | Google Apps Script |
| Hosting | GitHub Pages (free) |
| Build Tool | None — single file app |

**No frameworks. No dependencies. No installation.**  
Just one HTML file that runs in any browser.

---

## 📁 Folder Structure

```
admitguard--Aditi-/
├── index.html              ← Live app (root for GitHub Pages)
├── README.md               ← This file
├── research-notes.md       ← Vibe Coding research documentation
├── sprint-log.md           ← Sprint-by-sprint build log
├── prompts/
│   ├── prompt-01-foundation.md
│   ├── prompt-02-strict.md
│   └── ...
├── docs/
│   ├── wireframe.png       ← Initial wireframe sketch
│   └── architecture.md     ← Technical architecture notes
└── src/
    └── index.html          ← Copy of app in src folder
```

---

## 🚀 How to Run Locally

```
1. Clone the repository:
   git clone https://github.com/aditi23garg/admitguard--Aditi-.git

2. Open index.html in Chrome browser

3. That's it — no installation, no server needed!
```

> **Note:** Google Sheets sync only works on the live hosted version.
> When running locally, data is saved to localStorage only.

---

## 🧪 How to Test

### Strict Rule Tests
```
Full Name:    Type "Raj123"      → error (has numbers)
Full Name:    Type "SSSSSSS"     → error (repeated chars)
Email:        Type "abc@xyz.com" → error (fake domain)
Phone:        Type "9999999999"  → error (all same digit)
Phone:        Type "9876543210"  → error (sequential)
Aadhaar:      Type "12345678901" → error (11 digits only)
Interview:    Select "Rejected"  → submission blocked
```

### Soft Rule Tests
```
DOB:          Enter age 37      → yellow warning + exception toggle
Grad Year:    Enter 2010        → yellow warning + exception toggle
Score:        Enter 55%         → yellow warning + exception toggle
Test Score:   Enter 35          → yellow warning + exception toggle
```

### Exception Tests
```
Toggle exception → enter rationale < 30 chars    → error
Toggle exception → enter rationale without keyword → error
Toggle exception → enter valid rationale           → accepted
Add 3 exceptions → flag banner appears             → ✅
```

---

## 🔌 Google Sheets Integration

Data is automatically synced to Google Sheets on every submission.

**Sheet columns:**
```
Timestamp | Full Name | Email | Phone | DOB | Qualification |
Grad Year | Score | Score Mode | Test Score | Interview Status |
Aadhaar | Offer Letter | Exception Count | Flagged | Exception Details
```

**Fallback:** If Google Sheets sync fails (e.g. no internet), 
data is still saved to localStorage. Nothing is lost.

---

## 🏃 Sprint Summary

| Sprint | Goal | Status |
|---|---|---|
| Sprint 0 | Planning, setup, wireframe | ✅ Complete |
| Sprint 1 | Form structure + strict validation | ✅ Complete |
| Sprint 2 | Soft rules + exception system | ✅ Complete |
| Sprint 3 | Config + audit log + Sheets + hosting | ✅ Complete |
| Sprint 4 | Presentation prep | ✅ Complete |

---

## 🤖 Built Using

This project was built using **Vibe Coding** — describing requirements 
in plain English and iterating with **Claude AI** to generate, 
debug, and refine the code.

Prompting approach: **R.I.C.E. Framework**
- **R**ole → "You are a senior frontend developer..."
- **I**ntent → What to build
- **C**onstraints → What rules to follow  
- **E**xamples → Valid/invalid input samples

---

## 👩‍💻 Author

**Aditi Garg**  
PG Diploma in AI-ML & Agentic AI Engineering  
IIT Gandhinagar — Cohort 2026

---

## 📄 License

This project is part of the Week 1 assessment for the  
PG Diploma in AI-ML & Agentic AI Engineering at IIT Gandhinagar.
