---
description: 'Pull latest changes with rebase'
agent: 'agent'
tools: ['runInTerminal']
---
# Git Pull

1. Run `git status --short` to check for uncommitted changes.
   - If dirty: warn me and ask whether to stash first.
2. Run `git pull --rebase`.
3. If conflicts occur:
   - List conflicting files.
   - Ask me how to resolve each one.
4. Report the result: how many commits pulled, any notable changes.
