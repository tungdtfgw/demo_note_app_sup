---
description: 'Initialize a new project from this template'
agent: 'agent'
tools: ['runInTerminal']
argument-hint: 'remote repo URL (e.g. git@github.com:user/repo.git)'
---
# New Project from Template

> **Use only when cloning this template to start a new project.** This is a destructive, one-time command.

## Safety Check

1. Run `ls -A` at the project root.
2. Check if there are files or folders **beyond** the expected template files:
   - `.github/` (instructions + prompts)
   - `.gitignore`
   - `PRD.md`
   - `README.md`
   - `AGENTS.md`
   - `mistakes.md`
3. If extra files exist (e.g. `src/`, `app/`, `node_modules/`, `package.json`), **stop immediately** and warn:
   > "This project already has content beyond the template. Running `/new-project` would reset git history. Aborting."

## Process

If the safety check passes:

1. **Remove old git info:**
   ```
   rm -rf .git
   ```

2. **Initialize fresh repo:**
   ```
   git init
   ```

3. **Stage all template files:**
   ```
   git add -A
   ```

4. **Create initial commit:**
   ```
   git commit -m "chore: initialize project from template"
   ```

5. **Set up remote and push:**
   - Ask for the remote URL: `${input:remote:remote repo URL (e.g. git@github.com:user/repo.git)}`
   - Default branch name is `main` unless the user specifies otherwise.
   ```
   git branch -M main
   git remote add origin <remote-url>
   git push -u origin main
   ```

6. Report success:
   - New repo initialized
   - Remote set to `<url>`
   - Initial commit pushed to `main`
