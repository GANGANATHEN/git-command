# Git Cheatsheet – Daily Development Reference

> Purpose: Office repo / Personal repo work pannumbothu frequently use panna Git commands.
> Commands copy-paste panna before branch/repo name and file name correct-ah check pannunga.

---

# 1. Git Identity

## Global Identity

Machine-level default identity:

```bash
git config --global user.name "Your Name"
```
```bash
git config --global user.email "your@email.com"
```

Check:

```bash
git config --global user.name
```
```bash
git config --global user.email
```

---

## Repository-specific Identity

Personal project-ku personal Git account use panna:

```bash
git config --local user.name "Your Personal Name"
```
```bash
git config --local user.email "your-personal@email.com"
```

Check:

```bash
git config --local user.name
```
```bash
git config --local user.email
```

---

## Check Which Config Is Being Used

```bash
git config --show-origin --get user.name
```
```bash
git config --show-origin --get user.email
```

Full local config:

```bash
git config --local --list
```
Full global config:

```bash
git config --global --list
```

> `(END)` vandha terminal-la `q` press pannunga.

---

# 2. Check Current Repository Status

git status

Idhu current working tree-la:

- modified files
- deleted files
- untracked files
- staged files
- current branch

ellam kaamikum.

---

# 3. Check Current Branch

```bash
git branch
```

Current branch mattum:

```bash
git branch --show-current
```

All local + remote branches:

```bash
git branch -a
```

---

# 4. Create New Branch

New branch create + immediately switch:

```bash
git checkout -b feature/my-feature
```

Modern command:

```bash
git switch -c feature/my-feature
```

Example:

```bash
git checkout -b expense-api-binding
```

---

# 5. Switch Branch

```bash
git checkout main
```

or:

```bash
git switch main
```

Another branch:

```bash
git checkout expense-branch
```

or:

```bash
git switch expense-branch
```

---

# 6. Check Remote Repository

```bash
git remote -v
```

Detailed remote information:

```bash
git remote show origin
```

---

# 7. Get Latest Changes from Remote

Download remote changes only:

```bash
git fetch origin
```

Current branch-ku latest changes:

```bash
git pull origin main
```

Specific branch:

```bash
git pull origin expense-branch
```

> `pull` = fetch + merge/rebase depending on configuration.

---

# 8. Check Changes

All unstaged changes:

```bash
git diff
```

Specific file:

```bash
git diff -- "src/app/dashboard/page.js"
```

Staged changes:

```bash
git diff --cached
```

Branch comparison:

```bash
git diff main...expense-branch
```

---

# 9. Restore / Discard Local Changes

## Discard changes in one file

```bash
git restore -- "src/app/dashboard/page.js"
```

> File commit pannala, stage pannala na local changes disappear aagum.

---

## Discard changes in multiple files

```bash
git restore -- "file1.js" "file2.js"
```

---

## Discard ALL unstaged changes

```bash
git restore .
```

> CAREFUL:
> Current uncommitted changes ellam permanently remove aagum.

---

# 10. Unstage a File

Mistakenly `git add` pannita:

```bash
git restore --staged -- "src/app/dashboard/page.js"
```

All staged files unstage:

```bash
git restore --staged .
```

> Idhu file changes-ah delete pannaadhu.
> Stage-la irundhu mattum remove pannum.

---

# 11. Get One File from Another Branch

Example:
`expense-branch` la irukkura file-ah current branch-ku kondu vara:

```bash
git checkout expense-branch -- "src/app/[locale]/(layout1)/expense/component/expenseListTable.js"
```

Modern equivalent:

```bash
git restore --source expense-branch -- "src/app/[locale]/(layout1)/expense/component/expenseListTable.js"
```

> IMPORTANT:
> `git checkout --merge <file>` is NOT the normal command for copying a file from another branch.

---

# 12. Stage Changes

One file:

```bash
git add "src/app/dashboard/page.js"
```

Multiple files:

```bash
git add "file1.js" "file2.js"
```

All changes:

```bash
git add .
```

---

# 13. Commit Changes

```bash
git commit -m "Add expense API binding"
```

Good commit message examples:

```bash
git commit -m "Fix dashboard notification pagination"
```
```bash
git commit -m "Add task status API integration"
```
```bash
git commit -m "Fix attachment preview loading"
```

---

# 14. Push Branch

First push for a new branch:

```bash
git push -u origin expense-branch
```

After upstream is set:

```bash
git push
```

Specific branch:

```bash
git push origin expense-branch
```

---

# 15. Typical Feature Development Flow

## Step 1 – Start from main

```bash
git checkout main
```

## Step 2 – Get latest main

```bash
git pull origin main
```

## Step 3 – Create feature branch

```bash
git checkout -b expense-api-binding
```

## Step 4 – Do development

Code changes...

## Step 5 – Check changes

```bash
git status
```
```bash
git diff
```

## Step 6 – Stage

```bash
git add .
```

## Step 7 – Commit

```bash
git commit -m "Add expense API binding"
```

## Step 8 – Push

```bash
git push -u origin expense-api-binding
```

---

# 16. Bring Latest Main into Your Feature Branch

First:

```bash
git checkout main
```
```bash
git pull origin main
```

Then:

```bash
git checkout expense-branch
```

Merge main:

```bash
git merge main
```

If no conflict:

```bash
git push origin expense-branch
```

> Feature branch-la work continue pannumbothu main changes latest-ah keep panna useful.

---

# 17. Merge Feature Branch into Main

First switch to main:

```bash
git checkout main
```

Get latest main:

```bash
git pull origin main
```

Merge feature branch:

```bash
git merge expense-branch
```

If everything is fine:

```bash
git push origin main
```

---

# 18. Merge Conflict

Merge pannumbothu conflict vandha:

```bash
git status
```

Git conflict files list pannum.

File open pannumbothu:

```bash
<<<<<<< HEAD

current branch code

=======

incoming branch code

>>>>>>> expense-branch
```

Correct code manually select pannunga.

Then:

```bash
git add "conflicted-file.js"
```

After all conflicts resolved:

```bash
git status
```

Then:

```bash
git commit
```

Finally:

```bash
git push
```

---

# 19. Abort a Merge

Conflict vandhuduchu, merge continue panna vendam na:

```bash
git merge --abort
```

> Merge start pannadhukku munnaadi irundha state-ku return aagum.

---

# 20. Abort Rebase

Rebase conflict situation-la:

```bash
git rebase --abort
```

---

# 21. View Commit History

Simple:

```bash
git log
```

One-line format:

```bash
git log --oneline
```

Recent commits:

```bash
git log --oneline -10
```

Graph:

```bash
git log --oneline --graph --decorate --all
```

---

# 22. Check a Specific Commit

```bash
git show COMMIT_ID
```

Example:

git show a1b2c3d

---

# 23. Amend Last Commit

Last commit message wrong:

```bash
git commit --amend -m "Correct commit message"
```

Last commit-la file miss aagiduchu:

```bash
git add "missing-file.js"
```
```bash
git commit --amend --no-edit
```

> Already pushed commit-ah amend pannina force push required aagalam.
> Shared branch-la avoid pannunga.

---

# 24. Revert a Commit

Already pushed/shared branch commit-ah safely undo panna:

```bash
git revert COMMIT_ID
```

Then:

```bash
git push
```

> `revert` new commit create pannum.
> Shared branch-ku safer.

---

# 25. Reset

## Unstage last commit but keep changes

```bash
git reset --soft HEAD~1
```

## Remove commit and keep changes unstaged

```bash
git reset HEAD~1
```

## Remove commit AND changes

```bash
git reset --hard HEAD~1
```

> `--hard` use pannumbothu careful.
> Uncommitted changes lose aagalam.

---

# 26. Recover Lost Changes / Commits

Git reflog:

```bash
git reflog
```

Previous HEAD identify pannitu:

```bash
git checkout COMMIT_ID
```

or branch create panna:

```bash
git checkout -b recovery-branch COMMIT_ID
```

> Accidentally reset/rebase pannumbothu reflog useful.

---

# 27. Stash

Temporary-ah current changes save panna:

```bash
git stash
```

List:

```bash
git stash list
```

Latest stash restore:

```bash
git stash pop
```

Specific stash:

```bash
git stash apply stash@{0}
```

Stash with message:

```bash
git stash push -m "WIP expense page"
```

Delete one stash:

```bash
git stash drop stash@{0}
```

Delete all stashes:

```bash
git stash clear
```

> Branch switch panna current work disturb aagumbothu stash useful.

---

# 28. Delete Branch

Local branch:

```bash
git branch -d expense-branch
```

Force delete:

```bash
git branch -D expense-branch
```

Remote branch:

```bash
git push origin --delete expense-branch
```

> `-D` use panna branch merge aagala irundhalum delete pannum.

---

# 29. Rename Current Branch

```bash
git branch -m new-branch-name
```

If already pushed:

```bash
git push -u origin new-branch-name
```

Old remote branch delete:

```bash
git push origin --delete old-branch-name
```

---

# 30. Compare Branches

Commits difference:

```bash
git log main..expense-branch --oneline
```

Changes difference:

```bash
git diff main...expense-branch
```

---

# 31. See Which Files Changed

```bash
git status
```

Only changed file names:

```bash
git diff --name-only
```

Committed changes:

```bash
git diff --name-only HEAD~1 HEAD
```

---

# 32. Remove Untracked Files

Check first:

```bash
git clean -n
```

Delete untracked files:

```bash
git clean -f
```

Delete untracked files + directories:

```bash
git clean -fd
```

> VERY CAREFUL:
> `git clean` Git track pannaadha files-ah delete pannum.

---

# 33. Pull Before Starting Work

Daily recommended flow:

```bash
git checkout main
```

```bash
git pull origin main
```
```bash
git checkout -b feature/my-feature
```

---

# 34. Before Commit Checklist

```bash
git status
```
```bash
git diff
```
```bash
git diff --cached
```

Check:

- Correct files modified?
- Debug console.log remove pannacha?
- Unwanted files stage aagala?
- Environment files accidentally stage aagala?
- API URLs correct-ah?
- Secrets / tokens commit aagala?
- Build errors irukka?
- Commit message meaningful-ah?

Then:

```bash
git add .
```
```bash
git commit -m "Your message"
```

---

# 35. Before Push Checklist

```bash
git status
```
```bash
git branch --show-current
```
```bash
git log --oneline -5
```
```bash
git diff main...HEAD
```

Then:

```bash
git push
```

---

# 36. If You Accidentally Added a Secret

Immediately remove from current staging:

```bash
git restore --staged .env
```

> IMPORTANT:
> Already committed secret-na file remove pannradhu mattum sufficient illa.
> Secret value itself rotate/revoke pannunga.
> Git history cleanup may also be required.

---

# 37. Check Ignored Files

```bash
git status --ignored
```

Check whether a file is ignored:

```bash
git check-ignore -v "filename"
```

Example:

```bash
git check-ignore -v ".env"
```

---

# 38. Common Git Commands – Quick Reference

Check status:

```bash
git status
```

Current branch:

```bash
git branch --show-current
```

Create branch:

```bash
git checkout -b branch-name
```

Switch branch:

```bash
git checkout branch-name
```

Get latest:

```bash
git pull origin main
```

Check changes:

```bash
git diff
```

Stage:

```bash
git add .
```

Commit:

```bash
git commit -m "message"
```

Push:

```bash
git push
```

New branch push:

```bash
git push -u origin branch-name
```

Discard file changes:

```bash
git restore -- "file"
```

Unstage:

```bash
git restore --staged -- "file"
```

Copy file from another branch:

```bash
git checkout branch-name -- "file"
```

Merge:

```bash
git merge branch-name
```

Abort merge:

```bash
git merge --abort
```

History:

```bash
git log --oneline
```

Temporary save:

```bash
git stash
```

Restore stash:

```bash
git stash pop
```

Recover history:

```bash
git reflog
```

---

# 39. Nano Editor

Some Git operations editor open pannumbothu Nano varalam.

Save:

```bash
Ctrl + O
```

Confirm:
Enter

Exit:

```bash
Ctrl + X
```bash

---

# 40. Vim Editor

Git editor Vim open pannina:

Esc

:wq

Enter

Exit without saving:

Esc

:q!

Enter

---

# 41. Recommended Daily Workflow

# Start Work

```bash
git checkout main
```
```bash
git pull origin main
```
```bash
git checkout -b feature/my-feature
```


# During Development

```bash
git status
```
```bash
git diff
```


# Before Commit

```bash
git add .
```
```bash
git diff --cached
```
```bash
git commit -m "Describe the change"
```


# Push

```bash
git push -u origin feature/my-feature
```


# Later Pushes

```bash
git push
```


# Finish / Merge

```bash
git checkout main
```
```bash
git pull origin main
```
```bash
git merge feature/my-feature
```
```bash
git push origin main
```


# 42. Important Difference

```bash
git restore "file"
```

→ Local file changes discard.

```bash
git restore --staged "file"
```

→ Staging-la irundhu remove; code changes remain.

```bash
git checkout branch -- "file"
```

→ Another branch-la irukkura specific file-ah current branch-ku copy pannum.


```bash
git merge branch
```

→ Another branch changes current branch-kku merge pannum.

```bash
git revert COMMIT_ID
```

→ Existing commit-ah safely undo panna new commit create pannum.

```bash
git reset
```

→ Current branch history/HEAD move pannum.

```bash
git stash
```

→ Temporary local changes save pannum.

```bash
git fetch
```

→ Remote changes download mattum pannum.

```bash
git pull
```
→ Remote changes fetch + integrate pannum.

---

# 43. Golden Rule

Before destructive commands:

```bash
git status
```
```bash
git diff
```

If doubt irundha:

```bash
git stash
```

Then experiment pannunga.

Especially careful with:

```bash
git reset --hard
```
```bash
git clean -fd
```
```bash
git push --force
```
```bash
git push --force-with-lease
```
```bash
git branch -D
```
```bash
git stash clear
```

> Shared/main branch-la force push avoid pannunga.
> `--force-with-lease` is safer than plain `--force`, but still use only when you understand the history change.
