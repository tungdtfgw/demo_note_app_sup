---
description: 'Create a new branch with naming convention'
agent: 'agent'
tools: ['runInTerminal']
argument-hint: 'short description of the branch purpose'
---
# Git Branch

1. Take the user's input: `${input:purpose:what is this branch for?}`
2. Determine the branch type from the purpose:
   - New feature → `feat/`
   - Bug fix → `fix/`
   - Refactor / cleanup → `chore/`
   - Documentation → `docs/`
3. Generate the branch name: `type/short-kebab-case-description`
   - Max 50 chars total, lowercase, no special characters.
4. Show the proposed branch name and ask for confirmation.
5. After confirmation, run:
   ```
   git checkout -b <branch-name>
   ```
6. Report success and current branch.
