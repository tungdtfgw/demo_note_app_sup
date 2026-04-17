---
description: 'Summarize session changes and update AGENTS.md'
agent: 'agent'
tools: ['runInTerminal', 'search/codebase', 'read', 'edit']
---
# Wrap Up Session

Your job is to update `AGENTS.md` with a concise summary of what happened in this session.

## Steps

1. **Gather changes** (try in order, use first that works):
   - Run `git diff --stat` and `git log --oneline -10` in terminal.
   - If terminal is unavailable, scan conversation history for all file edits and decisions made.
2. Read `AGENTS.md` to see its current content.
3. Update the following sections in `AGENTS.md` at the project root:

### Current State
- Update the phase and status to reflect where the project is now.

### Architecture Decisions
- Append any new decisions made in this session (one line each).
- Format: `- **Decision:** reason (YYYY-MM-DD)`

### Recent Changes
- Replace the content with a brief summary of this session's work.
- Format: bullet list, max 5 items, each under 80 chars.
- Include the date: `### Session YYYY-MM-DD`

### TODOs
- Check off completed items.
- Add new TODOs discovered during the session.

4. Show me the proposed changes and **wait for approval** before writing.

## Rules
- Keep `AGENTS.md` **under 80 lines** total. Remove outdated entries if needed.
- Be concise — one line per item, no paragraphs.
- Do NOT touch `.github/copilot-instructions.md` — that file is fixed.
