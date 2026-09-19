Git Cheatsheet – Daily Development Reference

Purpose: Office repo / Personal repo work pannumbothu frequently use panna Git commands.

Rule: Command run pannurathukku munnaadi branch name, file name, remote name correct-ah check pannunga.

Quick Navigation

Git Identity

Repository Status

Branches

Remote Repository

Pull / Fetch

Diff

Restore / Discard

Stage

Commit

Push

Feature Workflow

Merge

Conflict

History

Revert / Reset

Reflog

Stash

Branch Delete / Rename

Cleanup

Daily Checklist

Important Differences

Golden Rules

1.  Git Identity

Global Identity

Machine-level default identity:

git config --global user.name "Your Name"

git config --global user.email "your@email.com"

Check Global Identity

git config --global user.name

git config --global user.email

Repository-specific Identity

Personal project-ku personal Git account use panna:

git config --local user.name "Your Personal Name"

git config --local user.email "your-personal@email.com"

Check Local Identity

git config --local user.name

git config --local user.email

Check Which Config Is Actually Being Used

git config --show-origin --get user.name

git config --show-origin --get user.email

Full Local Config

git config --local --list

Full Global Config

git config --global --list

(END) vandha terminal-la q press pannunga.

2.  Check Current Repository Status

git status

Idhu current working tree-la:

modified files

deleted files

untracked files

staged files

current branch

ellam kaamikum.

3.  Check Current Branch

git branch

Current Branch Mattum

git branch --show-current

All Local + Remote Branches

git branch -a

4.  Create New Branch

New Branch Create + Immediately Switch

git checkout -b feature/my-feature

Modern Command

git switch -c feature/my-feature

Example

git checkout -b expense-api-binding

5.  Switch Branch

git checkout main

Modern Command

git switch main

Another Branch

git checkout expense-branch

git switch expense-branch

6.  Check Remote Repository

git remote -v

Detailed Remote Information

git remote show origin

7. ⬇️ Get Latest Changes from Remote

Download Remote Changes Only

git fetch origin

Current Branch-ku Latest Main

git pull origin main

Specific Branch

git pull origin expense-branch

pull = remote changes fetch + local branch-la integrate pannum.

8.  Check Changes

All Unstaged Changes

git diff

Specific File

git diff -- "src/app/dashboard/page.js"

Staged Changes

git diff --cached

Branch Comparison

git diff main...expense-branch

9.  Restore / Discard Local Changes

Discard Changes in One File

git restore -- "src/app/dashboard/page.js"

️ File commit pannala / stage pannala na local changes disappear aagum.

Discard Changes in Multiple Files

git restore -- "file1.js" "file2.js"

Discard ALL Unstaged Changes

git restore .

CAREFUL: Current uncommitted changes ellam permanently remove aagum.

10.  Unstage a File

Mistakenly git add pannita:

git restore --staged -- "src/app/dashboard/page.js"

All Staged Files Unstage

git restore --staged .

Idhu file changes-ah delete pannaadhu. Stage-la irundhu mattum remove pannum.

11.  Get One File from Another Branch

Example:
expense-branch la irukkura file-ah current branch-ku kondu vara:

git checkout expense-branch -- "src/app/[locale]/(layout1)/expense/component/expenseListTable.js"

Modern Equivalent

git restore --source expense-branch -- "src/app/[locale]/(layout1)/expense/component/expenseListTable.js"

️ IMPORTANT: git checkout --merge <file> is NOT the normal command for copying a file from another branch.

12.  Stage Changes

One File

git add "src/app/dashboard/page.js"

Multiple Files

git add "file1.js" "file2.js"

All Changes

git add .

13.  Commit Changes

Normal Commit

git commit -m "Add expense API binding"

Good Commit Message Examples

git commit -m "Fix dashboard notification pagination"

git commit -m "Add task status API integration"

git commit -m "Fix attachment preview loading"

14.  Push Branch

First Push for a New Branch

git push -u origin expense-branch

After Upstream Is Set

git push

Specific Branch

git push origin expense-branch

15. ️ Typical Feature Development Flow

Step 1 – Start from Main

git checkout main

Step 2 – Get Latest Main

git pull origin main

Step 3 – Create Feature Branch

git checkout -b expense-api-binding

Step 4 – Do Development

Code changes...

Step 5 – Check Changes

git status

git diff

Step 6 – Stage

git add .

Step 7 – Commit

git commit -m "Add expense API binding"

Step 8 – Push

git push -u origin expense-api-binding

16.  Bring Latest Main into Your Feature Branch

First – Switch to Main

git checkout main

Get Latest Main

git pull origin main

Switch Back to Feature Branch

git checkout expense-branch

Merge Main

git merge main

If No Conflict

git push origin expense-branch

Feature branch-la work continue pannumbothu main changes latest-ah keep panna useful.

17.  Merge Feature Branch into Main

Switch to Main

git checkout main

Get Latest Main

git pull origin main

Merge Feature Branch

git merge expense-branch

If Everything Is Fine

git push origin main

18. ️ Merge Conflict

Merge pannumbothu conflict vandha:

git status

Git conflict files list pannum.

Conflict file open pannumbothu:

<<<<<<< HEAD

current branch code

=======

incoming branch code

>>>>>>> expense-branch

Correct code manually select pannunga.

Then Stage Resolved File

git add "conflicted-file.js"

Check Again

git status

Finish Merge

git commit

Push

git push

19.  Abort a Merge

Conflict vandhuduchu, merge continue panna vendam na:

git merge --abort

Merge start pannadhukku munnaadi irundha state-ku return aagum.

20.  Abort Rebase

Rebase conflict situation-la:

git rebase --abort

21.  View Commit History

Simple

git log

One-line Format

git log --oneline

Recent Commits

git log --oneline -10

Graph

git log --oneline --graph --decorate --all

22.  Check a Specific Commit

git show COMMIT_ID

Example

git show a1b2c3d

23. ️ Amend Last Commit

Last Commit Message Wrong

git commit --amend -m "Correct commit message"

Last Commit-la File Miss Aagiduchu

git add "missing-file.js"

git commit --amend --no-edit

️ Already pushed commit-ah amend pannina force push required aagalam. Shared branch-la avoid pannunga.

24. ↩️ Revert a Commit

Already pushed/shared branch commit-ah safely undo panna:

git revert COMMIT_ID

Then Push

git push

revert new commit create pannum. Shared branch-ku safer.

25. ⏪ Reset

Unstage Last Commit but Keep Changes

git reset --soft HEAD~1

Remove Commit and Keep Changes Unstaged

git reset HEAD~1

Remove Commit AND Changes

git reset --hard HEAD~1

--hard use pannumbothu careful. Uncommitted changes lose aagalam.

26.  Recover Lost Changes / Commits

Git Reflog

git reflog

Previous HEAD identify pannitu:

git checkout COMMIT_ID

Or Recovery Branch Create

git checkout -b recovery-branch COMMIT_ID

Accidentally reset/rebase pannumbothu reflog useful.

27.  Stash

Temporary-ah Current Changes Save

git stash

List

git stash list

Latest Stash Restore + Remove from Stash

git stash pop

Specific Stash

git stash apply stash@{0}

Stash with Message

git stash push -m "WIP expense page"

Delete One Stash

git stash drop stash@{0}

Delete All Stashes

git stash clear

Branch switch panna current work disturb aagumbothu stash useful.

28. ️ Delete Branch

Local Branch

git branch -d expense-branch

Force Delete

git branch -D expense-branch

Remote Branch

git push origin --delete expense-branch

️ -D use panna branch merge aagala irundhalum delete pannum.

29. ️ Rename Current Branch

git branch -m new-branch-name

If Already Pushed

git push -u origin new-branch-name

Old Remote Branch Delete

git push origin --delete old-branch-name

30.  Compare Branches

Commits Difference

git log main..expense-branch --oneline

Changes Difference

git diff main...expense-branch

31.  See Which Files Changed

Current Status

git status

Only Changed File Names

git diff --name-only

Committed Changes

git diff --name-only HEAD~1 HEAD

32.  Remove Untracked Files

Check First – Nothing Gets Deleted

git clean -n

Delete Untracked Files

git clean -f

Delete Untracked Files + Directories

git clean -fd

VERY CAREFUL: git clean Git track pannaadha files-ah delete pannum.

33.  Pull Before Starting Work

Daily recommended flow:

git checkout main

git pull origin main

git checkout -b feature/my-feature

34.  Before Commit Checklist

Check Status

git status

Check Code Changes

git diff

Check Staged Changes

git diff --cached

Check These Before Commit

Correct files modified?

Debug console.log remove pannacha?

Unwanted files stage aagala?

Environment files accidentally stage aagala?

API URLs correct-ah?

Secrets / tokens commit aagala?

Build errors irukka?

Commit message meaningful-ah?

Stage

git add .

Commit

git commit -m "Your message"

35.  Before Push Checklist

Check Status

git status

Check Current Branch

git branch --show-current

Check Recent Commits

git log --oneline -5

Compare with Main

git diff main...HEAD

Push

git push

36.  If You Accidentally Added a Secret

Immediately remove from current staging:

git restore --staged .env

️ Already committed secret-na file remove pannradhu mattum sufficient illa.

Secret value itself rotate/revoke pannunga.

Git history cleanup may also be required.

37.  Check Ignored Files

All Ignored Files

git status --ignored

Check Whether a File Is Ignored

git check-ignore -v "filename"

Example

git check-ignore -v ".env"

38.  Common Git Commands – Quick Reference

Check Status

git status

Current Branch

git branch --show-current

Create Branch

git checkout -b branch-name

Switch Branch

git checkout branch-name

Get Latest

git pull origin main

Check Changes

git diff

Stage

git add .

Commit

git commit -m "message"

Push

git push

New Branch Push

git push -u origin branch-name

Discard File Changes

git restore -- "file"

Unstage

git restore --staged -- "file"

Copy File from Another Branch

git checkout branch-name -- "file"

Merge

git merge branch-name

Abort Merge

git merge --abort

History

git log --oneline

Temporary Save

git stash

Restore Stash

git stash pop

Recover History

git reflog

39.  Nano Editor

Some Git operations editor open pannumbothu Nano varalam.

Save

Ctrl + O

Confirm

Enter

Exit

Ctrl + X

40.  Vim Editor

Git editor Vim open pannina:

Save + Exit

Esc

:wq

Enter

Exit Without Saving

Esc

:q!

Enter

41.  Recommended Daily Workflow

Start Work

git checkout main

git pull origin main

git checkout -b feature/my-feature

During Development

git status

git diff

Before Commit

git add .

git diff --cached

git commit -m "Describe the change"

Push

git push -u origin feature/my-feature

Later Pushes

git push

Finish / Merge

git checkout main

git pull origin main

git merge feature/my-feature

git push origin main

42.  Important Difference

git restore "file"

→ Local file changes discard.

git restore -- "file"

git restore --staged "file"

→ Staging-la irundhu remove; code changes remain.

git restore --staged -- "file"

git checkout branch -- "file"

→ Another branch-la irukkura specific file-ah current branch-ku copy pannum.

git checkout branch-name -- "file"

git merge branch

→ Another branch changes current branch-kku merge pannum.

git merge branch-name

git revert COMMIT_ID

→ Existing commit-ah undo panna new commit create pannum.

git revert COMMIT_ID

git reset

→ Current branch history / HEAD move pannum.

git reset HEAD~1

git stash

→ Temporary local changes save pannum.

git stash

git fetch

→ Remote changes download mattum pannum; current branch automatically change aagadhu.

git fetch origin

git pull

→ Remote changes fetch + integrate pannum.

git pull origin main

43. ️ Golden Rule

Before destructive commands:

git status

git diff

If doubt irundha:

git stash

Then experiment pannunga.

Especially Careful With

git reset --hard

git clean -fd

git push --force

git push --force-with-lease

git branch -D

git stash clear

️ Shared / main branch-la force push avoid pannunga.

--force-with-lease is safer than plain --force, but still use only when you understand the history change.

Git Command Safety Guide

Symbol

Meaning



Normal / commonly used



Information / checking



Use carefully



Destructive / high risk



Branch / workflow

Safe Daily Commands

git status

git diff

git branch

git log --oneline

Use Carefully

git restore -- "file"

git stash pop

git branch -d branch-name

git revert COMMIT_ID

High Risk

git reset --hard HEAD~1

git clean -fd

git push --force

git stash clear

Final Reminder

Before changing anything:

git status

Before committing:

git diff

Before pushing:

git status

git branch --show-current

If something goes wrong:

git reflog

If you are unsure about local changes:

git stash

Check → Change → Diff → Stage → Commit → Push

This order follow pannina daily Git workflow clean-ah maintain panna mudiyum.
