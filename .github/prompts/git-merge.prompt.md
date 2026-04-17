---
description: 'Merge a branch into the current branch'
agent: 'agent'
tools: ['runInTerminal']
argument-hint: 'source branch to merge from'
---
# Git Merge

1. Take the source branch: `${input:source:branch to merge from}`
2. Run `git branch --show-current` to show current (target) branch.
3. Run `git log HEAD..${input:source} --oneline` to preview incoming commits.
4. Show the plan: "Merge `${input:source}` → `<current branch>` (X commits)" and wait for confirmation.
5. After confirmation, run `git merge ${input:source}`.
6. If conflicts:
   - List conflicting files with `git diff --name-only --diff-filter=U`.
   - Ask me how to resolve or whether to abort with `git merge --abort`.
7. If success, report the merge result and suggest deleting the source branch if it was a feature branch.
