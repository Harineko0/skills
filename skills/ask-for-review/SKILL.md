---
name: ask-for-review
description: Ask Codex CLI to review staged files for a specified concern. Use when invoking /ask-for-review or requesting a staged-file review through codex exec.
---

# Ask for Review

Replace `XXX` with the requested review concern or just a plan file, then run exactly once from the repository root:

```
codex exec -m gpt-6-astra -c 'model_reasoning_effort="medium"' "/review Review the changes in the staged files regarding XXX."
```

Return the review result without modifying the reviewed files.
