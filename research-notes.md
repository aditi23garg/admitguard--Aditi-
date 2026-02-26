# Research Notes — Vibe Coding & Google AI Studio

## What is Vibe Coding?
Vibe Coding means describing what you want to build 
in plain English, and letting an AI generate the code. 
You guide it, iterate on it, and refine it — but you 
don't write the code from scratch yourself.

## What Tool Am I Using?
Instead of Google AI Studio, I am using Claude by 
Anthropic directly in the browser. Claude generates 
the complete HTML + CSS + JS code which I copy into 
a local file and run in Chrome.

## Why This Approach?
- No new tool setup needed
- Can explain every line of generated code
- Easy to iterate — just ask Claude to modify
- Understand the code, not just copy-paste it

## Resources I Read
1. Project Brief 
2. Anthropic Prompt Engineering Guide:
   https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering

## Key Things I Learned
- Good prompts have: Role, Intent, Constraints, Examples
- Build one feature at a time — don't overload one prompt
- Always test with edge cases after building each feature
- The first AI output is rarely perfect — iteration is the skill

## Prompting Approach I Will Use (R.I.C.E.)
R — Role: Tell the AI who it is
I — Intent: What to build
C — Constraints: What rules to follow
E — Examples: Show good/bad examples

## Questions I Had (Now Answered)
Q: Do I need Google AI Studio?
A: No. Claude can generate the same code directly.

Q: Do I need a backend/server?
A: No. Single HTML file runs in any browser.

Q: Where is data stored?
A: localStorage — data stays in the browser itself.