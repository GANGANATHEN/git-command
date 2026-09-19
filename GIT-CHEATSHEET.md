# 🚀 Git Cheatsheet – Daily Development Reference

> **Purpose:** Office repo / Personal repo work pannumbothu frequently use panna Git commands.
>
> **Rule:** Command run pannurathukku munnaadi branch name, file name, remote name correct-ah check pannunga.

---

## 🎯 Quick Navigation

- [Git Identity](#1-git-identity)
- [Repository Status](#2-check-current-repository-status)
- [Branches](#3-check-current-branch)
- [Remote Repository](#6-check-remote-repository)
- [Pull / Fetch](#7-get-latest-changes-from-remote)
- [Diff](#8-check-changes)
- [Restore / Discard](#9-restore--discard-local-changes)
- [Stage](#12-stage-changes)
- [Commit](#13-commit-changes)
- [Push](#14-push-branch)
- [Feature Workflow](#15-typical-feature-development-flow)
- [Merge](#16-bring-latest-main-into-your-feature-branch)
- [Conflict](#18-merge-conflict)
- [History](#21-view-commit-history)
- [Revert / Reset](#24-revert-a-commit)
- [Reflog](#26-recover-lost-changes--commits)
- [Stash](#27-stash)
- [Branch Delete / Rename](#28-delete-branch)
- [Cleanup](#32-remove-untracked-files)
- [Daily Checklist](#41-recommended-daily-workflow)
- [Important Differences](#42-important-difference)
- [Golden Rules](#43-golden-rule)

---

# 1. 🔐 Git Identity

## 🌍 Global Identity

Machine-level default identity:

```bash
git config --global user.name "Your Name"
```

```bash
git config --global user.email "your@email.com"
```

### Check Global Identity

```bash
git config --global user.name
```

```bash
git config --global user.email
```

---

## 🏠 Repository-specific Identity

Personal project-ku personal Git account use panna:

```bash
git config --local user.name "Your Personal Name"
```

```bash
git config --local user.email "your-personal@email.com"
```

### Check Local Identity

```bash
git config --local user.name
```

```bash
git config --local user.email
```

---

## 🔎 Check Which Config Is Actually Being Used

```bash
git config --show-origin --get user.name
```

```bash
git config --show-origin --get user.email
```

### Full Local Config

```bash
git config --local --list
```

### Full Global Config

```bash
git config --global --list
```

> 💡 `(END)` vandha terminal-la `q` press pannunga.

---

# 2. 📊 Check Current Repository Status

```bash
git status
```

Idhu current working tree-la:

- modified files
- deleted files
- untracked files
- staged files
- current branch

ellam kaamikum.

---

# 3. 🌿 Check Current Branch

```bash
git branch
```

### Current Branch Mattum

```bash
git branch --show-current
```

### All Local + Remote Branches

```bash
git branch -a
```

---

# 4. ➕ Create New Branch

### New Branch Create + Immediately Switch

```bash
git checkout -b feature/my-feature
```

### Modern Command

```bash
git switch -c feature/my-feature
```

### Example

```bash
git checkout -b expense-api-binding
```

---

# 5. 🔄 Switch Branch

```bash
git checkout main
```

### Modern Command

```bash
git switch main
```

### Another Branch

```bash
git checkout expense-branch
```

```bash
git switch expense-branch
```

---

# 6. 🌐 Check Remote Repository

```bash
git remote -v
```

### Detailed Remote Information

```bash
git remote show origin
```

---

# 7. ⬇️ Get Latest Changes from Remote

### Download Remote Changes Only

```bash
git fetch origin
```

### Current Branch-ku Latest Main

```bash
git pull origin main
```

### Specific Branch

```bash
git pull origin expense-branch
```

> 💡 `pull` = remote changes fetch + local branch-la integrate pannum.

---

# 8. 🔍 Check Changes

### All Unstaged Changes

```bash
git diff
```

### Specific File

```bash
git diff -- "src/app/dashboard/page.js"
```

### Staged Changes

```bash
git diff --cached
```

### Branch Comparison

```bash
git diff main...expense-branch
```

---

# 9. 🧹 Restore / Discard Local Changes

## Discard Changes in One File

```bash
git restore -- "src/app/dashboard/page.js"
```

> ⚠️ File commit pannala / stage pannala na local changes disappear aagum.

---

## Discard Changes in Multiple Files

```bash
git restore -- "file1.js" "file2.js"
```

---

## Discard ALL Unstaged Changes

```bash
git restore .
```

> 🚨 **CAREFUL:** Current uncommitted changes ellam permanently remove aagum.

---

# 10. 📤 Unstage a File

Mistakenly `git add` pannita:

```bash
git restore --staged -- "src/app/dashboard/page.js"
```

### All Staged Files Unstage

```bash
git restore --staged .
```

> 💡 Idhu file changes-ah delete pannaadhu. Stage-la irundhu mattum remove pannum.

---

# 11. 📄 Get One File from Another Branch

Example:
`expense-branch` la irukkura file-ah current branch-ku kondu vara:

```bash
git checkout expense-branch -- "src/app/[locale]/(layout1)/expense/component/expenseListTable.js"
```

### Modern Equivalent

```bash
git restore --source expense-branch -- "src/app/[locale]/(layout1)/expense/component/expenseListTable.js"
```

> ⚠️ **IMPORTANT:** `git checkout --merge <file>` is NOT the normal command for copying a file from another branch.

---

# 12. 📦 Stage Changes

### One File

```bash
git add "src/app/dashboard/page.js"
```

### Multiple Files

```bash
git add "file1.js" "file2.js"
```

### All Changes

```bash
git add .
```

---

# 13. 💾 Commit Changes

### Normal Commit

```bash
git commit -m "Add expense API binding"
```

### Good Commit Message Examples

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

# 14. 🚀 Push Branch

### First Push for a New Branch

```bash
git push -u origin expense-branch
```

### After Upstream Is Set

```bash
git push
```

### Specific Branch

```bash
git push origin expense-branch
```

---

# 15. 🛠️ Typical Feature Development Flow

## Step 1 – Start from Main

```bash
git checkout main
```

## Step 2 – Get Latest Main

```bash
git pull origin main
```

## Step 3 – Create Feature Branch

```bash
git checkout -b expense-api-binding
```

## Step 4 – Do Development

```text
Code changes...
```

## Step 5 – Check Changes

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

# 16. 🔄 Bring Latest Main into Your Feature Branch

### First – Switch to Main

```bash
git checkout main
```

### Get Latest Main

```bash
git pull origin main
```

### Switch Back to Feature Branch

```bash
git checkout expense-branch
```

### Merge Main

```bash
git merge main
```

### If No Conflict

```bash
git push origin expense-branch
```

> 💡 Feature branch-la work continue pannumbothu main changes latest-ah keep panna useful.

---

# 17. 🔀 Merge Feature Branch into Main

### Switch to Main

```bash
git checkout main
```

### Get Latest Main

```bash
git pull origin main
```

### Merge Feature Branch

```bash
git merge expense-branch
```

### If Everything Is Fine

```bash
git push origin main
```

---

# 18. ⚔️ Merge Conflict

Merge pannumbothu conflict vandha:

```bash
git status
```

Git conflict files list pannum.

Conflict file open pannumbothu:

```text
<<<<<<< HEAD

current branch code

=======

incoming branch code

>>>>>>> expense-branch
```

Correct code manually select pannunga.

### Then Stage Resolved File

```bash
git add "conflicted-file.js"
```

### Check Again

```bash
git status
```

### Finish Merge

```bash
git commit
```

### Push

```bash
git push
```

---

# 19. 🛑 Abort a Merge

Conflict vandhuduchu, merge continue panna vendam na:

```bash
git merge --abort
```

> 💡 Merge start pannadhukku munnaadi irundha state-ku return aagum.

---

# 20. 🛑 Abort Rebase

Rebase conflict situation-la:

```bash
git rebase --abort
```

---

# 21. 📜 View Commit History

### Simple

```bash
git log
```

### One-line Format

```bash
git log --oneline
```

### Recent Commits

```bash
git log --oneline -10
```

### Graph

```bash
git log --oneline --graph --decorate --all
```

---

# 22. 🔎 Check a Specific Commit

```bash
git show COMMIT_ID
```

### Example

```bash
git show a1b2c3d
```

---

# 23. ✏️ Amend Last Commit

### Last Commit Message Wrong

```bash
git commit --amend -m "Correct commit message"
```

### Last Commit-la File Miss Aagiduchu

```bash
git add "missing-file.js"
```

```bash
git commit --amend --no-edit
```

> ⚠️ Already pushed commit-ah amend pannina force push required aagalam. Shared branch-la avoid pannunga.

---

# 24. ↩️ Revert a Commit

Already pushed/shared branch commit-ah safely undo panna:

```bash
git revert COMMIT_ID
```

### Then Push

```bash
git push
```

> 💡 `revert` new commit create pannum. Shared branch-ku safer.

---

# 25. ⏪ Reset

## Unstage Last Commit but Keep Changes

```bash
git reset --soft HEAD~1
```

## Remove Commit and Keep Changes Unstaged

```bash
git reset HEAD~1
```

## Remove Commit AND Changes

```bash
git reset --hard HEAD~1
```

> 🚨 `--hard` use pannumbothu careful. Uncommitted changes lose aagalam.

---

# 26. 🧯 Recover Lost Changes / Commits

### Git Reflog

```bash
git reflog
```

Previous HEAD identify pannitu:

```bash
git checkout COMMIT_ID
```

### Or Recovery Branch Create

```bash
git checkout -b recovery-branch COMMIT_ID
```

> 💡 Accidentally reset/rebase pannumbothu `reflog` useful.

---

# 27. 📦 Stash

### Temporary-ah Current Changes Save

```bash
git stash
```

### List

```bash
git stash list
```

### Latest Stash Restore + Remove from Stash

```bash
git stash pop
```

### Specific Stash

```bash
git stash apply stash@{0}
```

### Stash with Message

```bash
git stash push -m "WIP expense page"
```

### Delete One Stash

```bash
git stash drop stash@{0}
```

### Delete All Stashes

```bash
git stash clear
```

> 💡 Branch switch panna current work disturb aagumbothu stash useful.

---

# 28. 🗑️ Delete Branch

## Local Branch

```bash
git branch -d expense-branch
```

## Force Delete

```bash
git branch -D expense-branch
```

## Remote Branch

```bash
git push origin --delete expense-branch
```

> ⚠️ `-D` use panna branch merge aagala irundhalum delete pannum.

---

# 29. ✏️ Rename Current Branch

```bash
git branch -m new-branch-name
```

### If Already Pushed

```bash
git push -u origin new-branch-name
```

### Old Remote Branch Delete

```bash
git push origin --delete old-branch-name
```

---

# 30. 📊 Compare Branches

### Commits Difference

```bash
git log main..expense-branch --oneline
```

### Changes Difference

```bash
git diff main...expense-branch
```

---

# 31. 📋 See Which Files Changed

### Current Status

```bash
git status
```

### Only Changed File Names

```bash
git diff --name-only
```

### Committed Changes

```bash
git diff --name-only HEAD~1 HEAD
```

---

# 32. 🧹 Remove Untracked Files

### Check First – Nothing Gets Deleted

```bash
git clean -n
```

### Delete Untracked Files

```bash
git clean -f
```

### Delete Untracked Files + Directories

```bash
git clean -fd
```

> 🚨 **VERY CAREFUL:** `git clean` Git track pannaadha files-ah delete pannum.

---

# 33. 🔄 Pull Before Starting Work

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

# 34. ✅ Before Commit Checklist

### Check Status

```bash
git status
```

### Check Code Changes

```bash
git diff
```

### Check Staged Changes

```bash
git diff --cached
```

### Check These Before Commit

- Correct files modified?
- Debug `console.log` remove pannacha?
- Unwanted files stage aagala?
- Environment files accidentally stage aagala?
- API URLs correct-ah?
- Secrets / tokens commit aagala?
- Build errors irukka?
- Commit message meaningful-ah?

### Stage

```bash
git add .
```

### Commit

```bash
git commit -m "Your message"
```

---

# 35. 🚀 Before Push Checklist

### Check Status

```bash
git status
```

### Check Current Branch

```bash
git branch --show-current
```

### Check Recent Commits

```bash
git log --oneline -5
```

### Compare with Main

```bash
git diff main...HEAD
```

### Push

```bash
git push
```

---

# 36. 🔒 If You Accidentally Added a Secret

Immediately remove from current staging:

```bash
git restore --staged .env
```

> ⚠️ Already committed secret-na file remove pannradhu mattum sufficient illa.
>
> Secret value itself rotate/revoke pannunga.
>
> Git history cleanup may also be required.

---

# 37. 🚫 Check Ignored Files

### All Ignored Files

```bash
git status --ignored
```

### Check Whether a File Is Ignored

```bash
git check-ignore -v "filename"
```

### Example

```bash
git check-ignore -v ".env"
```

---

# 38. ⚡ Common Git Commands – Quick Reference

### Check Status

```bash
git status
```

### Current Branch

```bash
git branch --show-current
```

### Create Branch

```bash
git checkout -b branch-name
```

### Switch Branch

```bash
git checkout branch-name
```

### Get Latest

```bash
git pull origin main
```

### Check Changes

```bash
git diff
```

### Stage

```bash
git add .
```

### Commit

```bash
git commit -m "message"
```

### Push

```bash
git push
```

### New Branch Push

```bash
git push -u origin branch-name
```

### Discard File Changes

```bash
git restore -- "file"
```

### Unstage

```bash
git restore --staged -- "file"
```

### Copy File from Another Branch

```bash
git checkout branch-name -- "file"
```

### Merge

```bash
git merge branch-name
```

### Abort Merge

```bash
git merge --abort
```

### History

```bash
git log --oneline
```

### Temporary Save

```bash
git stash
```

### Restore Stash

```bash
git stash pop
```

### Recover History

```bash
git reflog
```

---

# 39. 📝 Nano Editor

Some Git operations editor open pannumbothu Nano varalam.

### Save

```text
Ctrl + O
```

### Confirm

```text
Enter
```

### Exit

```text
Ctrl + X
```

---

# 40. 📝 Vim Editor

Git editor Vim open pannina:

### Save + Exit

```text
Esc
```

```text
:wq
```

```text
Enter
```

### Exit Without Saving

```text
Esc
```

```text
:q!
```

```text
Enter
```

---

# 41. 🏆 Recommended Daily Workflow

## 🌅 Start Work

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

## 💻 During Development

```bash
git status
```

```bash
git diff
```

---

## 📦 Before Commit

```bash
git add .
```

```bash
git diff --cached
```

```bash
git commit -m "Describe the change"
```

---

## 🚀 Push

```bash
git push -u origin feature/my-feature
```

---

## 🔁 Later Pushes

```bash
git push
```

---

## 🏁 Finish / Merge

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

---

# 42. 🧠 Important Difference

## `git restore "file"`

→ Local file changes discard.

```bash
git restore -- "file"
```

---

## `git restore --staged "file"`

→ Staging-la irundhu remove; code changes remain.

```bash
git restore --staged -- "file"
```

---

## `git checkout branch -- "file"`

→ Another branch-la irukkura specific file-ah current branch-ku copy pannum.

```bash
git checkout branch-name -- "file"
```

---

## `git merge branch`

→ Another branch changes current branch-kku merge pannum.

```bash
git merge branch-name
```

---

## `git revert COMMIT_ID`

→ Existing commit-ah undo panna new commit create pannum.

```bash
git revert COMMIT_ID
```

---

## `git reset`

→ Current branch history / HEAD move pannum.

```bash
git reset HEAD~1
```

---

## `git stash`

→ Temporary local changes save pannum.

```bash
git stash
```

---

## `git fetch`

→ Remote changes download mattum pannum; current branch automatically change aagadhu.

```bash
git fetch origin
```

---

## `git pull`

→ Remote changes fetch + integrate pannum.

```bash
git pull origin main
```

---

# 43. 🛡️ Golden Rule

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

## 🚨 Especially Careful With

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

> ⚠️ Shared / main branch-la force push avoid pannunga.
>
> `--force-with-lease` is safer than plain `--force`, but still use only when you understand the history change.

---

# 🎨 Git Command Safety Guide

| Symbol | Meaning |
|---|---|
| 🟢 | Normal / commonly used |
| 🔵 | Information / checking |
| 🟡 | Use carefully |
| 🔴 | Destructive / high risk |
| 🟣 | Branch / workflow |

### 🟢 Safe Daily Commands

```bash
git status
```

```bash
git diff
```

```bash
git branch
```

```bash
git log --oneline
```

### 🟡 Use Carefully

```bash
git restore -- "file"
```

```bash
git stash pop
```

```bash
git branch -d branch-name
```

```bash
git revert COMMIT_ID
```

### 🔴 High Risk

```bash
git reset --hard HEAD~1
```

```bash
git clean -fd
```

```bash
git push --force
```

```bash
git stash clear
```

---

# 💡 Final Reminder

**Before changing anything:**

```bash
git status
```

**Before committing:**

```bash
git diff
```

**Before pushing:**

```bash
git status
```

```bash
git branch --show-current
```

**If something goes wrong:**

```bash
git reflog
```

**If you are unsure about local changes:**

```bash
git stash
```

> 🚀 **Check → Change → Diff → Stage → Commit → Push**
>
> This order follow pannina daily Git workflow clean-ah maintain panna mudiyum.
