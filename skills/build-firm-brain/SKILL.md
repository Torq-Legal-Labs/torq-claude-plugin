---
name: build-firm-brain
description: "Use when a firm owner, or a member granted Brain authoring, wants to build, resume or deepen the firm's Firm Brain in Torq through its guided interview, section by section."
---

# Build The Firm Brain

Use this skill when an owner (or a granted contributor) wants to build or deepen their Firm Brain by chatting. This is a GUIDED, SERVER-DRIVEN interview: the server owns the cursor, the required-section set, and the completion decision. Your job is to converse each section to a good answer and confirm it — never to decide when the Brain is "done".

Pick the scope (the `kind` argument) up front and keep it fixed for the whole run:
- onboarding: the owner's first pass over every section.
- cascade: a contributor answering only the sections assigned to them.
- gap_fill: a re-launchable deepening pass over the sections the Brain is currently missing (thin or skipped).

Loop:
1. Call resume_brain_interview with the kind. Read currentSectionKey (where to resume), the per-section status + any proposed draft, and isComplete. If isComplete is already true, tell the user the required set is satisfied and stop — do not re-open resolved sections.
2. Work the section at currentSectionKey. Call answer_brain_section (kind + the user's message). Pass message:null on the very first turn of an unopened interview so the coach speaks the section's opening prompt. Relay the coach's message events to the user and gather their answer.
3. Keep looping answer_brain_section for the same section until an event with type "proposed" returns a section body. Do not fabricate the body yourself — use exactly what "proposed" carries (the user may refine it in another turn first).
4. Read the proposed body back to the user in plain language and get explicit confirmation. Then call confirm_brain_section with confirm:true and that body to write it. If the user wants to skip a non-required section, call confirm_brain_section with confirm:false.
5. confirm_brain_section returns the next currentSectionKey and the server-computed isComplete. Trust those: move to the returned currentSectionKey and repeat from step 2. When isComplete is true, stop — the required set is satisfied.

Determinism and safety:
6. Completion is the server's required-section check, never your judgment. A section that scores thin is re-entered by the server through the gap set on a later gap_fill run — do not force it or mark the Brain complete to move on.
7. There is one interview per (firm, user): a second start resumes the in-flight run rather than restarting it, so always resume before answering.
8. A confirm outside the acting user's allowed sections (cascade/gap_fill scope) is rejected by the server — respect the scope you chose and confirm only sections the state offers.

While a section is open:
9. Your job is to elicit the owner's answer and record it with answer_brain_section, not to fetch data. Do not call Salesforce, QuickBooks, ads, phone or any other connected-source tool to fill in, check or enrich their answer: what they tell you is the answer. If they ask an unrelated question, answer it, then bring the conversation back to the open section.

Torq tools this guide uses: `resume_brain_interview`, `answer_brain_section`, `confirm_brain_section`. They come from the Torq connector. If they are not available, Torq is not connected or the member's Torq permissions do not include them; setup is at https://torqlegallabs.com/claude.
