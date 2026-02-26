# 🛡️ AdmitGuard — Admission Data Validation System

## What is this?
AdmitGuard is a smart web form that replaces the 
unstructured Excel-based candidate tracking system 
used in the admission process.

It enforces eligibility rules at the point of data 
entry, handles exceptions with proper documentation, 
and maintains a full audit trail of all submissions.

## The Problem We're Solving
- Candidate data entered into Excel with zero validation
- Ineligible candidates only caught at the last stage
- No audit trail for exception decisions
- Rules are painful to update

## Our Solution
A browser-based form that:
- Validates all 11 candidate fields in real-time
- Blocks submission if strict rules are violated
- Allows soft-rule exceptions with documented rationale
- Logs all submissions with timestamps and exception details

## Tech Stack
- HTML, CSS, JavaScript (single file)
- Built using Claude AI (Vibe Coding approach)
- localStorage for data persistence (no backend needed)

## How to Run
1. Clone this repository
2. Open src/index.html in Chrome browser
3. That's it — no installation needed!

## Folder Structure
admitguard-yourname/
├── README.md
├── research-notes.md
├── sprint-log.md
├── prompts/
│   └── prompt-01-foundation.md
├── docs/
│   └── architecture.md
└── src/
    └── index.html


## Author
Your Name — PG Diploma in AI-ML & Agentic AI Engineering
IIT Gandhinagar — Cohort 2026