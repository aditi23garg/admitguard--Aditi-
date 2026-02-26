# Architecture — AdmitGuard

## How the App Works

### Data Flow
User fills form 
    → Real-time validation runs on each field
    → Strict rules: block if violated
    → Soft rules: show warning + exception option
    → Exception rationale validated
    → Exception counter updated
    → Submit button enabled/disabled accordingly
    → On submit: data saved to localStorage
    → Audit log updated

### Components
1. FORM (index.html)
   - 11 input fields
   - Inline validation messages
   - Exception toggles + rationale fields
   - Exception counter display
   - Submit button

2. VALIDATION ENGINE (JavaScript)
   - Reads rules from config object
   - Runs strict and soft validations
   - Manages exception state

3. RULES CONFIG (JSON object in JS)
   - All rules defined in one place
   - Easy to update without touching form logic

4. AUDIT LOG (localStorage)
   - Stores all submissions
   - Persists across page refreshes
   - Displayed in audit log tab

### Tech Stack
- HTML → Page structure
- CSS  → Visual design
- JS   → Validation logic + data storage
- localStorage → Data persistence (no server needed)

### File Structure
src/
└── index.html   (entire app in one file)