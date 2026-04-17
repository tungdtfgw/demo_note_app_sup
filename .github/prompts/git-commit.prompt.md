---
description: 'Stage and commit with a conventional commit message'
agent: 'agent'
tools: ['runInTerminal']
---
# Git Commit

1. Run `git diff --cached --stat` to see staged files. If nothing is staged, run `git status` and ask me what to stage.
2. Run `git diff --cached` to read the actual changes.
3. Generate a **conventional commit** message:
   - Format: `type(scope): short description`
   - Types: `feat`, `fix`, `refactor`, `docs`, `chore`, `style`, `test`
   - Scope: the area affected (e.g., `storage`, `notes`, `navigation`)
   - Description: imperative mood, lowercase, no period, max 72 chars
   - If the change is non-trivial, add a body explaining **why** (not what).
4. Show me the proposed message and wait for my confirmation.
5. Only after I confirm, run `git commit -m "..."`.
