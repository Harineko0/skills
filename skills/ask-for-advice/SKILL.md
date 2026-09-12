---
name: ask-for-advice
description: Seek read-only advice from Opus-5 Medium for high-level design and specification decisions, or GPT-6-Astra Medium for other questions such as implementation and debugging. Use for consultation; use ask-for-review for staged-file reviews.
---

# Ask for Advice

Let a caller such as GPT-5.6-Luna Max or Claude Sonnet-5 consult a stronger model while retaining responsibility for the task and implementation.

## Prepare the consultation

Write a self-contained request to a temporary UTF-8 file outside the repository. The advisor does not inherit the caller's conversation. Include:

- The user's goal, acceptance criteria, constraints, and relevant repository instructions.
- The precise question or decision, current approach, alternatives considered, and what remains uncertain. Distinguish observed facts from hypotheses.
- The absolute repository root, relevant file paths and symbols, and the exact scope or revision being discussed. Include relevant code, contracts, and diffs; attach their contents when the advisor cannot access the original files.
- Attempts already made, commands and relevant outputs, reproduction steps, and validation results or gaps. Preserve exact error messages and details that affect the decision.
- The requested answer: a recommendation with evidence, tradeoffs, assumptions, and concrete next steps. Ask the advisor to identify missing information rather than invent it.

Include enough primary evidence to assess alternatives independently, rather than only a summary supporting the caller's preferred answer. Omit unrelated material and secrets. Do not use a bare question or a file path as the entire request.

Explicitly instruct the advisor: **Provide advice only. Do not edit files, execute mutating commands, change external state, or delegate further. Read relevant sources as needed and cite file locations supporting your conclusions.**

## Start one read-only advisor

Honor an explicitly user-selected advisor. Otherwise route by the question, regardless of the caller's model or CLI:

- **Opus-5 Medium:** High-level design and specification decisions, including system architecture, responsibility boundaries, requirements interpretation, externally observable behavior, and contract tradeoffs.
- **GPT-6-Astra Medium:** All other advice, including implementation details within an agreed design, debugging, test implementation, refactoring, and performance investigation.

For a mixed question, resolve any blocking high-level design or specification decision with Opus first. Carry that decision into a separate Astra consultation only if implementation advice is still needed. Do not ask both models the same question by default.

Caller model names above are examples, not eligibility restrictions. Use the selected model and medium effort; do not silently substitute another model or effort if unavailable.

Run the selected command from the target repository root. Replace `/absolute/path/advice-request.txt` with the prepared request file. Pass the request through stdin so its contents are not interpreted as shell code.

GPT-6-Astra Medium:

```sh
codex exec --ignore-user-config --ephemeral \
  --model gpt-6-astra --sandbox read-only \
  -c 'approval_policy="never"' \
  -c 'model_reasoning_effort="medium"' \
  - < /absolute/path/advice-request.txt
```

Opus-5 Medium:

```sh
claude --print --model claude-opus-5 --effort medium \
  --restricted --permission-mode plan \
  --tools 'Read,Glob,Grep' --allowedTools 'Read,Glob,Grep' \
  --strict-mcp-config --mcp-config '{"mcpServers":{}}' \
  --disable-slash-commands --no-session-persistence \
  < /absolute/path/advice-request.txt
```

Check the installed CLI's help if these options are unsupported. Preserve enforced read-only access: Codex uses a read-only shell sandbox with no approval escalation; Claude exposes only read tools and no MCP servers. Do not replace these controls with prompt-only restrictions, permission bypasses, or unrestricted shell access. Do not enable external tools or integrations that can mutate state. If the required model or read-only controls cannot be provided, report the limitation and stop the consultation.

## Apply the advice

Read the complete response and check its claims against the primary evidence and the user's constraints. Resolve material gaps with a focused follow-up carrying the prior question, answer, and new evidence under the same model and read-only restrictions. Do not retry an unchanged request repeatedly or start both advisors by default.

The caller decides what to adopt, performs any authorized implementation, and validates the result. Report the useful conclusion and any remaining uncertainty; do not present advice as verified merely because it came from the stronger model.
