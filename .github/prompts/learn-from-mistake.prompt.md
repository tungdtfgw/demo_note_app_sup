---
description: 'Record a mistake and its fix into mistakes.md'
agent: 'agent'
tools: ['search/codebase', 'read', 'edit']
argument-hint: 'describe what went wrong'
---
# Learn From Mistake

When I describe a bug, bad pattern, or something the AI got wrong, your job is to analyze it and add an entry to `mistakes.md`.

## Steps

1. Listen to my description of the mistake.
2. If needed, search the codebase to understand the context and find the root cause.
3. Summarize into a single table row with these columns:
   - **Date:** today's date (YYYY-MM-DD)
   - **Mistake:** what happened (1 sentence)
   - **Root Cause:** why it happened (1 sentence)
   - **Fix / Rule:** what to do differently going forward (1 sentence, actionable)
4. Show me the proposed entry and wait for confirmation.
5. After confirmation, append the row to the table in `mistakes.md`.

## Rules

- Keep each cell to **one sentence**. No paragraphs.
- Write in English.
- If a similar mistake already exists in the table, update that row instead of adding a duplicate.
- Do NOT modify `.github/copilot-instructions.md` or any instructions files — only `mistakes.md`.
