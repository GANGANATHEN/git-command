# Git Cheatsheet – Daily Development Reference

> Purpose: Office repo / Personal repo work pannumbothu frequently use panna Git commands.
> Commands copy-paste panna before branch/repo name and file name correct-ah check pannunga.

---

# 1. Git Identity

## Global Identity

Machine-level default identity:

git config --global user.name "Your Name"

git config --global user.email "your@email.com"

Check:

git config --global user.name

git config --global user.email

---

## Repository-specific Identity

Personal project-ku personal Git account use panna:

git config --local user.name "Your Personal Name"

git config --local user.email "your-personal@email.com"

Check:

git config --local user.name

git config --local user.email

---

## Check Which Config Is Being Used

git config --show-origin --get user.name

git config --show-origin --get user.email

Full local config:

git config --local --list

Full global config:

git config --global --list

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

git branch

Current branch mattum:

git branch --show-current

All local + remote branches:

git branch -a

---

# 4. Create New Branch

New branch create + immediately switch:

git checkout -b feature/my-feature

Modern command:

git switch -c feature/my-feature

Example:

git checkout -b expense-api-binding

---

# 5. Switch Branch

git checkout main

or:

git switch main

Another branch:

git checkout expense-branch

or:

git switch expense-branch

---

# 6. Check Remote Repository

git remote -v

Detailed remote information:

git remote show origin

---

# 7. Get Latest Changes from Remote

Download remote changes only:

git fetch origin

Current branch-ku latest changes:

git pull origin main

Specific branch:

git pull origin expense-branch

> `pull` = fetch + merge/rebase depending on configuration.

---

# 8. Check Changes

All unstaged changes:

git diff

Specific file:

git diff -- "src/app/dashboard/page.js"

Staged changes:

git diff --cached

Branch comparison:

git diff main...expense-branch

---

# 9. Restore / Discard Local Changes

## Discard changes in one file

git restore -- "src/app/dashboard/page.js"

> File commit pannala, stage pannala na local changes disappear aagum.

---

## Discard changes in multiple files

git restore -- "file1.js" "file2.js"

---

## Discard ALL unstaged changes

git restore .

> CAREFUL:
> Current uncommitted changes ellam permanently remove aagum.

---

# 10. Unstage a File

Mistakenly `git add` pannita:

git restore --staged -- "src/app/dashboard/page.js"

All staged files unstage:

git restore --staged .

> Idhu file changes-ah delete pannaadhu.
> Stage-la irundhu mattum remove pannum.

---

# 11. Get One File from Another Branch

Example:
`expense-branch` la irukkura file-ah current branch-ku kondu vara:

git checkout expense-branch -- "src/app/[locale]/(layout1)/expense/component/expenseListTable.js"

Modern equivalent:

git restore --source expense-branch -- "src/app/[locale]/(layout1)/expense/component/expenseListTable.js"

> IMPORTANT:
> `git checkout --merge <file>` is NOT the normal command for copying a file from another branch.

---

# 12. Stage Changes

One file:

git add "src/app/dashboard/page.js"

Multiple files:

git add "file1.js" "file2.js"

All changes:

git add .

---

# 13. Commit Changes

git commit -m "Add expense API binding"

Good commit message examples:

git commit -m "Fix dashboard notification pagination"

git commit -m "Add task status API integration"

git commit -m "Fix attachment preview loading"

---

# 14. Push Branch

First push for a new branch:

git push -u origin expense-branch

After upstream is set:

git push

Specific branch:

git push origin expense-branch

---

# 15. Typical Feature Development Flow

## Step 1 – Start from main

git checkout main

## Step 2 – Get latest main

git pull origin main

## Step 3 – Create feature branch

git checkout -b expense-api-binding

## Step 4 – Do development

Code changes...

## Step 5 – Check changes

git status

git diff

## Step 6 – Stage

git add .

## Step 7 – Commit

git commit -m "Add expense API binding"

## Step 8 – Push

git push -u origin expense-api-binding

---

# 16. Bring Latest Main into Your Feature Branch

First:

git checkout main

git pull origin main

Then:

git checkout expense-branch

Merge main:

git merge main

If no conflict:

git push origin expense-branch

> Feature branch-la work continue pannumbothu main changes latest-ah keep panna useful.

---

# 17. Merge Feature Branch into Main

First switch to main:

git checkout main

Get latest main:

git pull origin main

Merge feature branch:

git merge expense-branch

If everything is fine:

git push origin main

---

# 18. Merge Conflict

Merge pannumbothu conflict vandha:

git status

Git conflict files list pannum.

File open pannumbothu:

<<<<<<< HEAD

current branch code

=======

incoming branch code

>>>>>>> expense-branch

Correct code manually select pannunga.

Then:

git add "conflicted-file.js"

After all conflicts resolved:

git status

Then:

git commit

Finally:

git push

---

# 19. Abort a Merge

Conflict vandhuduchu, merge continue panna vendam na:

git merge --abort

> Merge start pannadhukku munnaadi irundha state-ku return aagum.

---

# 20. Abort Rebase

Rebase conflict situation-la:

git rebase --abort

---

# 21. View Commit History

Simple:

git log

One-line format:

git log --oneline

Recent commits:

git log --oneline -10

Graph:

git log --oneline --graph --decorate --all

---

# 22. Check a Specific Commit

git show COMMIT_ID

Example:

git show a1b2c3d

---

# 23. Amend Last Commit

Last commit message wrong:

git commit --amend -m "Correct commit message"

Last commit-la file miss aagiduchu:

git add "missing-file.js"

git commit --amend --no-edit

> Already pushed commit-ah amend pannina force push required aagalam.
> Shared branch-la avoid pannunga.

---

# 24. Revert a Commit

Already pushed/shared branch commit-ah safely undo panna:

git revert COMMIT_ID

Then:

git push

> `revert` new commit create pannum.
> Shared branch-ku safer.

---

# 25. Reset

## Unstage last commit but keep changes

git reset --soft HEAD~1

## Remove commit and keep changes unstaged

git reset HEAD~1

## Remove commit AND changes

git reset --hard HEAD~1

> `--hard` use pannumbothu careful.
> Uncommitted changes lose aagalam.

---

# 26. Recover Lost Changes / Commits

Git reflog:

git reflog

Previous HEAD identify pannitu:

git checkout COMMIT_ID

or branch create panna:

git checkout -b recovery-branch COMMIT_ID

> Accidentally reset/rebase pannumbothu reflog useful.

---

# 27. Stash

Temporary-ah current changes save panna:

git stash

List:

git stash list

Latest stash restore:

git stash pop

Specific stash:

git stash apply stash@{0}

Stash with message:

git stash push -m "WIP expense page"

Delete one stash:

git stash drop stash@{0}

Delete all stashes:

git stash clear

> Branch switch panna current work disturb aagumbothu stash useful.

---

# 28. Delete Branch

Local branch:

git branch -d expense-branch

Force delete:

git branch -D expense-branch

Remote branch:

git push origin --delete expense-branch

> `-D` use panna branch merge aagala irundhalum delete pannum.

---

# 29. Rename Current Branch

git branch -m new-branch-name

If already pushed:

git push -u origin new-branch-name

Old remote branch delete:

git push origin --delete old-branch-name

---

# 30. Compare Branches

Commits difference:

git log main..expense-branch --oneline

Changes difference:

git diff main...expense-branch

---

# 31. See Which Files Changed

git status

Only changed file names:

git diff --name-only

Committed changes:

git diff --name-only HEAD~1 HEAD

---

# 32. Remove Untracked Files

Check first:

git clean -n

Delete untracked files:

git clean -f

Delete untracked files + directories:

git clean -fd

> VERY CAREFUL:
> `git clean` Git track pannaadha files-ah delete pannum.

---

# 33. Pull Before Starting Work

Daily recommended flow:

git checkout main

git pull origin main

git checkout -b feature/my-feature

---

# 34. Before Commit Checklist

git status

git diff

git diff --cached

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

git add .

git commit -m "Your message"

---

# 35. Before Push Checklist

git status

git branch --show-current

git log --oneline -5

git diff main...HEAD

Then:

git push

---

# 36. If You Accidentally Added a Secret

Immediately remove from current staging:

git restore --staged .env

> IMPORTANT:
> Already committed secret-na file remove pannradhu mattum sufficient illa.
> Secret value itself rotate/revoke pannunga.
> Git history cleanup may also be required.

---

# 37. Check Ignored Files

git status --ignored

Check whether a file is ignored:

git check-ignore -v "filename"

Example:

git check-ignore -v ".env"

---

# 38. Common Git Commands – Quick Reference

Check status:
git status

Current branch:
git branch --show-current

Create branch:
git checkout -b branch-name

Switch branch:
git checkout branch-name

Get latest:
git pull origin main

Check changes:
git diff

Stage:
git add .

Commit:
git commit -m "message"

Push:
git push

New branch push:
git push -u origin branch-name

Discard file changes:
git restore -- "file"

Unstage:
git restore --staged -- "file"

Copy file from another branch:
git checkout branch-name -- "file"

Merge:
git merge branch-name

Abort merge:
git merge --abort

History:
git log --oneline

Temporary save:
git stash

Restore stash:
git stash pop

Recover history:
git reflog

---

# 39. Nano Editor

Some Git operations editor open pannumbothu Nano varalam.

Save:
Ctrl + O

Confirm:
Enter

Exit:
Ctrl + X

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

git checkout main

git pull origin main

git checkout -b feature/my-feature


# During Development

git status

git diff


# Before Commit

git add .

git diff --cached

git commit -m "Describe the change"


# Push

git push -u origin feature/my-feature


# Later Pushes

git push


# Finish / Merge

git checkout main

git pull origin main

git merge feature/my-feature

git push origin main


# 42. Important Difference

git restore "file"
→ Local file changes discard.

git restore --staged "file"
→ Staging-la irundhu remove; code changes remain.

git checkout branch -- "file"
→ Another branch-la irukkura specific file-ah current branch-ku copy pannum.

git merge branch
→ Another branch changes current branch-kku merge pannum.

git revert COMMIT_ID
→ Existing commit-ah safely undo panna new commit create pannum.

git reset
→ Current branch history/HEAD move pannum.

git stash
→ Temporary local changes save pannum.

git fetch
→ Remote changes download mattum pannum.

git pull
→ Remote changes fetch + integrate pannum.

---

# 43. Golden Rule

Before destructive commands:

git status

git diff

If doubt irundha:

git stash

Then experiment pannunga.

Especially careful with:

git reset --hard

git clean -fd

git push --force

git push --force-with-lease

git branch -D

git stash clear

> Shared/main branch-la force push avoid pannunga.
> `--force-with-lease` is safer than plain `--force`, but still use only when you understand the history change.
