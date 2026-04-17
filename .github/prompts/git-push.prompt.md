---
description: 'Push current branch to remote'
agent: 'agent'
tools: ['runInTerminal']
---
# Git Push

1. Run `git branch --show-current` to identify the current branch.
2. Run `git log @{upstream}..HEAD --oneline 2>/dev/null || echo "No upstream set"` to show unpushed commits.
3. Show me the branch name and list of commits to be pushed.
4. Wait for my confirmation.
5. After confirmation:
   - If upstream exists: `git push`
   - If no upstream: `git push -u origin <branch>`
