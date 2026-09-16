---
name: create-final-plan
description: Write the final version of an implementation/design plan document, in the required section structure, once the approach is settled. Use whenever finalizing a plan file, wrapping up a planning phase before coding starts, or the user asks to "write up the plan," even if they don't name the sections explicitly.
---

# Create Final Plan

Write a final plan only after the approach is settled — through exploration, design discussion, or user confirmation. This is not the place to weigh alternatives; that belongs earlier in the process. By the time you write this document, you've already decided what to do — the job here is to record it clearly enough that someone else (or a future you) could execute it without re-deriving the reasoning.

## Structure

Use these headings. Adapt exact wording to the project's voice, but keep the content each one carries:

- **Context** — Explain why this change is happening: the problem or need behind it, what prompted it, and the outcome it's meant to produce. A plan that jumps straight to "do X" forces the reader to reconstruct the motivation from the steps, which is slower and more error-prone than just stating it.
- **Approach** — Describe the recommended approach only. Alternatives you considered and rejected belong in your own working notes or in conversation with the user, not in the final document — they add length without helping whoever executes the plan.
- **Files to change** — Name the critical files the work touches. If a pattern repeats across many files (e.g., the same migration applied to twenty models), describe the pattern once and give two or three representative paths rather than enumerating every file — a full list adds no information the reader can't derive from the pattern itself, and it goes stale the moment the file set shifts.
- **Reuse** — Point to existing functions, utilities, or components that should be reused, with their file paths. Plans that skip this tend to get implemented with fresh code that duplicates something already in the codebase.
- **Verification** — Describe how to confirm the change works end-to-end: what to run, what to click through, what output or test result confirms success. A plan without this leaves "done" undefined.

## Calibrating detail

Match the plan's length to the task's complexity — a config tweak and a multi-service migration don't need the same document. The target is a document that's concise enough to scan in one pass but detailed enough that someone unfamiliar with the recent discussion could execute it correctly. If a section would just restate what's obvious from the codebase, keep it brief rather than padding it for symmetry.
