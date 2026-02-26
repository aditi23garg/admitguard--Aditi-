AdmitGuard — Admission Data Validation & Compliance System
Problem Statement

The current admission process relies on manual data entry in Excel sheets. There is no system-enforced validation at the point of internal data entry. As a result, ineligible candidates may progress to advanced stages before being rejected. This leads to wasted operational effort, poor candidate experience, and compliance risks.

Where the Problem Occurs

The issue arises during internal operational data entry, where counsellors manually enter candidate details into tracking sheets. Since there is no structured rule engine, eligibility checks depend entirely on human judgment, increasing the probability of errors.

Proposed Solution

We propose building a rule-based admission validation system that:

Enforces strict eligibility rules at data entry

Allows structured exception handling with documented rationale

Maintains an audit trail of all submissions

Keeps validation rules configurable via a JSON configuration file

Tech Stack (Planned)

Google AI Studio (Build Mode)

HTML/CSS/JavaScript (AI-generated)

LocalStorage (for audit log persistence)

GitHub (version control)
