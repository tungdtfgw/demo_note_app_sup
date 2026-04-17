---
description: 'Add a git worktree for parallel work'
agent: 'agent'
tools: ['runInTerminal']
argument-hint: 'branch name for the worktree'
---
# Git Worktree

1. Take the branch name: `${input:branch:branch name (existing or new)}`
2. Run `git branch --list ${input:branch}` to check if branch exists.
3. Set worktree path to `../worktrees/${input:branch}`.
4. Show the plan and ask for confirmation:
   - Worktree path
   - Whether creating a new branch or using an existing one
5. After confirmation:
   - If branch exists: `git worktree add ../worktrees/${input:branch} ${input:branch}`
   - If new branch: `git worktree add -b ${input:branch} ../worktrees/${input:branch}`
6. Report success and remind me:
   - `cd ../worktrees/${input:branch}` to switch
   - `git worktree remove ../worktrees/${input:branch}` to clean up when done
