# Intermediate Git

## Contents:

[Tags](#tags)  
[Merge Conflict](#merge-conflict)  
[Rename and Delete files](#rename-and-delete-files)  
[Git Undo/Redo/Modify Commits](#git-undoredomodify-commits)  
[- Unstage Changes](#unstage-changes)  
[- Discard Changes](#discard-changes)  
[- Amend Last Commit](#amend-last-commit)  
[- Revert](#revert)  
[- Reset](#reset)  
[- Rebase](#rebase)  
[Stash](#stash)  

---
Back to [V1 Beginning Git](v1-beginning-git.md)  
Go to [V3 Beginning GitHub](v3-beginning-github.md)  
Back to [README](../README.md)  

---

## Intro

These are the steps to continue building the git-demo app covered in the Intermediate Git video. After watching the video, you can follow these steps one or more times until you feel comfortable with the commands. These steps are covered generically in the Intermediate Git CheatSheet.

To start over from the beginning of this video, run the command:  
`git reset --hard v1-beginning-git`

---

## Tags

Explanations:
- Log all the commits from the previous video.
- Add a tag named "v1-beginning-git" to the last commit. Get its commit Id from the log.
- List all tags with `git tag -l`.
- Delete the tag.
- Add the tag back again.  

Commands:
```
git log --oneline
git tag v1-beginning-git <commitId>
git tag -l
git tag -d v1-beginning-git <commitId>
git tag v1-beginning-git <commitId>
```

VS Code: Optionally, use source control > 3 dots > Tags  

---

## Merge Conflict

We will create a merge conflict between the main and a new branch, then resolve it.

### 1) Add and checkout a branch called feature3.
- Add a file called feature3.txt and modify app.txt.

```
git checkout -b feature3
```

### 2) Add a file and modify app.txt
```
cat << 'EOF' > feature3.txt
Some text.
EOF
```
Open file: app.txt
Change line 3 to: "Third line modified in feature3 branch."
Add "Feature 3." to the end of the file.
```
git add .
git commit -m 'Add feature 3'
```

### 3) Checkout main, modify app.txt and commit the change.
```
git checkout main
```
Open file: app.txt
Modify line 3 to: "Third line modified in main branch."
```
git commit -am 'Modify app.txt'
```
Now the main branch and feature3 branch are out of sync.


### 4) Checkout feature3 branch and merge main.
```
git checkout feature3
git merge main
```

### 5) Resolve merge conflict.

- Resolve the conflict:
  - Button: Resolve in Merge Editor
  - Put "and" between them > Button: Complete Merge

- Commit the conflict merge.
```
git commit -m 'Fix app.txt merge conflict'
```
Or Change message to above and click Commit Check

Then merge feature3 into main, and delete the feature3 branch.

```
git checkout main
git merge feature3
git branch -d feature3
```

---

## Rename and Delete files

Explanations:
- Create a branch called practice to try out the various git modification commands.
- Rename file3.txt to file3b.txt.
- Delete file4.txt
- These commands will stage these changes for commit.

Commands:
```
git checkout -b practice
git mv file3.txt file3b.txt
git rm file4.txt
git status
```

---

## Git Undo/Redo/Modify Commits

### a) Unstage Changes

Explanations:
- Unstage the renamed and deleted file3 and file4 file changes using the `git restore --staged .` or `git restore -S .` commmand.
- Restage them.
- Unstage them again using the `git reset` command.

Commands:
```
git restore --staged .
git add .
git reset
```

VS Code: Optionally, use source control sidebar to unstage changes.  



---

### b) Discard Changes

Explanations:
- View git status of files.
- Discard all changes to tracked files since last commit.
- View git status again.
- Check to see what untracked files would be deleted with the clean command.
- Delete all untracked files.

Commands:
```
git status
git restore .
git status
git clean -n
git clean -f
```

VS Code: Optionally, use source control > 3 dots > Changes > Discard All Changes 

---
### c) Amend Last Commit

Amend the last commit by adding new changes.

- Create a file called practice.txt, add it to the staging area and commit it.
- Modify the practice.txt file and stage the commit
- Log the most recent commits.
- Amend the last commit to add this change without changing the original commit message.
- Log the most recent commits again.

```
cat << 'EOF' > feature.txt
Some text.
EOF

git add .
git commit -m 'Add practice.txt'

cat << 'EOF' >> feature.txt
Second line.
EOF

git add .
git log --oneline -3
git commit --amend -m 'Add practice feature' > --no-edit
git log --oneline -3
```

Optionally, use the VS Code source control sidebar to amend the last commit:
- Source Control: 3 Dots > Commit > Commit Staged (Amend)


---

### d) Revert

Undo the changes from a previous commit with a new commit that reverses it.

- Revert the last commit. "Head" represents that last commit.
- View the last 3 commits.

```
git revert head
git olog -3
```

---

### e) Reset

Undo the prior commit. Either discard the changes from that commit, or put them in the working directory, or put them in the staging area.

Explanations:
- Undo and discard the last commit (--hard option)
- Undo last commit, putting changes in the working directory (default).
- Stage and commit those changes again.
- Undo last commit, putting changes in the staging area (--soft option)
- Commit those changes again.

Commands:
```
git log --oneline -3
git reset --hard head^
git log --oneline -2
git reset head^
git log --oneline -1
git add .
git commit -m 'Add practice.txt'
git log --oneline -2
git reset --soft head^
git log --oneline -1
git commit -m 'Add practice.txt'
git log --oneline -2
```

VS Code: Optionally, use source control > 3 dots > Commit > Undo Last Commit

---

### f) Rebase

Reorder, combine, edit, or delete previous commits.

---
#### f1) Create two files and two commits.

- Add a practice2 file, stage it and commit it.
- Add a practice3 file, stage it and commit it.

```
git log --oneline

cat << 'EOF' > practice2.txt
Some text.
EOF

git add .
git commit -m 'Add practice2'

cat << 'EOF' > practice3.txt
Some text.
EOF

git add .
git commit -m 'Add practice3'

git log --oneline -4
```

---
#### f2) Reorder the commits.

- Rebase the last 3 commits. Either use the commitId for the commit before the last 3 commits, or use head~3.

```
git rebase -i head~3
```
Reorder line 3 and line 2, then save and close the window.
```
git log --oneline -4
```

---
#### f3) Change a previous commit message.

```
git rebase -i main
```
- Change "pick" to "reword" or "r" in front of the "Add practice 2" commit. Then save and close the file. 
- The commit edit message window will open. Change it to "Add practice2 reworded" then close the window.
```
git log --oneline -4
```

---
#### f4) Squash commits (Combine two commits).
- Combine the practice2 and practice3 commits.

```
git rebase -i main
```
- Change "pick" to "squash" or "s" in front of the practice3 commit. Save and close the file.
- The commit edit message window will open. Change it to "Add practice2 and practice3" then close the window.
```
git log --oneline -4
```

---
#### Add a new file and commit.

- Add a practice4 file, stage it and commit it.

```
cat << 'EOF' > practice4.txt
Some text.
EOF

git add .
git commit -m 'Add practice4'
git log --oneline -4
```

---
#### f5) Edit a prior commit

```
git rebase -i main
```
- Change "pick" to "edit" or "e" in front of the first commit of the branch "Add practice.txt". Save and close the window.
- In the practice.txt file add the text "Third line" on line 3 and save it.
```
git add practice.txt
git commit --amend
```
- The commit edit message window will open. Optionally, change it to "Add practice.txt amended" then save and close the window.
```
git rebase --continue
```

---
#### f6) Delete a previous commit

```
git rebase -i main
```
- Change "pick" to "drop" or "d", or just delete the whole line. Then save and close the window.
```
git log --oneline -3
```

---
#### f7)Abort a rebase
- If you run into problems in the middle of a rebase, you can abort the process by running:
```
git rebase --abort
```
Or in VS Code source control sidebar: 3 dots > Commit > Abort Rebase

---

## Stash

Use `git stash` to play around with some ideas without formally creating a branch.  
Or if you aren't ready to make a commit but need to temporarily put your changes aside while you go to another branch.

- Go back to the main branch.
```
git checkout main
```
- Modify the app.txt file in some way and save it.

- Stash the change.
- List the stash.
- Remove the last stash and put it in your working directory.
- Confirm the stash is gone.
- Discard the changes to app.txt
```
git stash
git stash list
git stash pop
git stash list
git restore app.txt
```
- Make another change to app.txt and save it.
- Stash the change with a message.
- Create a file called feature4.txt and stash it with a message.
- List your stashes.
- Show stash index 1
- Show stash index 1 with the changes.
- Use git stash apply 0 to put the stash in the working directory, without deleting the stash.
- List the stashes again to confirm it's still there.
- Delete stash index 1
- Delete all remaining stashes
```
git stash -m 'Modify app.txt'

cat << 'EOF' > feature4.txt
Some text.
EOF

git stash -um 'Feature 4'
git stash list
git stash show 1
git stash show 1 -p
git stash apply 0
git stash list
git stash drop 1
git stash clear
```

VS Code: Optionally, use source control > 3 dots > Stash

---

## Wrap up

Explanations:
- Check git status.
- Discard any uncommitted changes. Delete untracked files in necessary.
- Add a tag named v2-intermediate-git to the last commit.
- list all your tags.
- List all your branches.
- List all your commits

Commands:
```
git status
git restore .

git tag -am 'V2 Intermediate Git' v2-intermediate-git
git tag -l
git branch
git glog
```
