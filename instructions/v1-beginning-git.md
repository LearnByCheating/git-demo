# Beginning Git

## Contents:  
[Install or update Git](#install-or-update-git)  
[Documentation and Help](#documentation-and-help)  
[Configure Git](#configure-git)  
[Set up a Local Git Repository](#set-up-a-local-git-repository)  
[.gitignore](#gitignore)  
[Commits](#commits)  
[Status, Diff, Log, and Show commands](#status-diff-log-and-show-commands)  
[Branches](#branches)  
[Branches Using VSCode Source Control sidebar](#branches-using-vscode-source-control-sidebar)  

---
Go to [V2 Intermediate Git](v2-intermediate-git.md)  
Back to [README](../README.md)  

---

## Intro

These are the steps to build the git-demo app covered in the Beginning Git video. After watching the video, you can follow these steps one or more times until you feel comfortable with the commands. These steps are covered generically in the Beginning Git CheatSheet.

To start over from the beginning of this video just delete the project.

---

## Install or update Git

- Check to see if Git is intalled by checking Git's version and location.
  ```
  git --version
  which git
  ```

- Download and install Git if it is not already installed: https://git-scm.com/downloads

---

## Documentation and Help

- Official Documentation: https://git-scm.com/docs 
  - Enter a command or search term for help on a specific topic
  - Or enter the command directly in the URL: https://git-scm.com/docs/git-commmand replacing "command" with the actual command.
- Help from the command line. 
  -  `git help command` replacing "command" with the actual command.
  - Help topics are displayed with the Unix Less program. To navigate the help screen use:
    - Press the ↑ key or ↓ key to go up or down one line.
    - Press `f` or a space to go forward one screen
    - Press `b` to go back one screen.
    - Press `g` to go to the beginning.
    - Press `G` to go to the end.
    - Press `/` followed by a search term to search for a term.
      - Then press `n` to go to the next occurence of the search term.
      - Press `N` to go to the previous occurence of the search term.
    - Press `q` to quit Less.

---

## Configure Git

Explanations:

- Add global variables to your git program including your username and email. These will be included in the meta information of all your commits.
- Set the default branch name to *main*.
- Add aliases for the `git log --oneline` and `git log --graph --oneline` commands.
- Then list all your global variables.

Commands:
```
git config --global user.name 'your name here'
git config --global user.email your-email-here
git config --global init.defaultBranch main
git config --global alias.olog 'log --oneline'
git config --global alias.glog 'log --graph --oneline'
git config --global --list
```

---

## Set up a Local Git Repository

Explanations:
- `pwd` Returns our present working directory.
- `cd path` changes directory to the path you provide.
- `mkdir directory-name` Creates a new directory.
- `git init` Initiates a new git repository for the project.
- `clear` Clears the screen.

Commands:
```
pwd
mkdir git-demo
cd git-demo
git init
```

- Git init creates a hidden directory called `.git`. To see it on Mac Finder, make sure hidden files are visible by entering `Shift+Command+.`

### Add files to the project:

Explanations:
- Create text files named app.txt and ignoreme.txt with some text.
- Below are the Unix commands to create a file and add text from the command line. You can also add them manually from your text editor.

Commands:
```
cat << 'EOF' > app.txt
Some text.
EOF

cat << 'EOF' > ignoreme.txt
Git ignores this whole file.
EOF
```

---

## .gitignore


- Add a git ignore file. Files and directories in this file will not be tracked by Git and will not get pushed to remotes like GitHub.

```
cat << 'EOF' > .gitignore
.DS_Store
ignoreme.txt
EOF
```

---

## Commits

- Note that VS Code color codes your files based on their Git status. 
  - Grey: Ignored by Git.
  - White: Unmodified since last commit.
  - Green: New file, not in a previous Git commit.
    - Followed by U: Not staged for commit.
    - Followed by A: Added to staging area.
  - Yellow: Modified since last commit.

Explanations:
- Take the below actions either from the command line, or using VS Code's Explorer and Source Control sidebars.
  - Make your first commit: 
    - Add the app.txt file to the staging area then make your first commit.
  - Make some changes, then make your second commit:
    - Append a line to the app.txt file.
    - Create a new file named file2.txt and add some text.
    - Stage the changes, then commit them.
  - Make more changes, then make your third commit.

Commands:
```
git add .
git commit -m 'First commit'

cat << 'EOF' >> app.txt
Second line.
EOF

cat << 'EOF' > file2.txt
Some text.
EOF

git add .
git commit -m 'Add file2'

cat << 'EOF' > file3.txt
Some text.
EOF

git add .
git commit -m 'Add file3'
```

---

## Status, Diff, Log, and Show commands

Explanations:
- Clear the screen then check `git status`. There should be nothing to change.
- Modify *app.txt* by adding lines to it, and create a new file.
- Check `git status`.
- View the changes to *app.txt* since the last commit.
- Add *app.txt* to the staging area, then commit it.
- Log command: Log all commits, last 2 commits, log commits on one line, log the olog alias.
- Show command: To show a specific commit, put all or the first part of the commitId after `git show`. *Head* is the last commit.

Commands:
```
clear
git status

cat << 'EOF' >> app.txt
Second line modified.
Third line.
EOF

cat << 'EOF' > file4.txt
Some text.
EOF

git status
git log
git log -2
git log --oneline
git log olog
git show <commitId>
git show head
git show head^
git show head~2
```

---

## Branches

Explanations:
- View list of all branches with the `git branch` command.
- Create and checkout a branch named *feature1*.
- Add *feature1.txt* and modify *app.txt*.
- Stage and commit the changes.
- Check status. Check the differences between the *main* and *feature1* branches.
- Checkout the *main* branch, merge *feature1*, then delete the *feature1* branch.
- Log the last 3 commits.

Commands:
```
git branch
git checkout -b feature1
git branch

cat << 'EOF' > feature1.txt
Some text.
EOF

cat << 'EOF' >> app.txt
Feature 1.
EOF

git status
git add .
git commit -m 'Add feature 1'

git status
git diff main feature1

git checkout main
git merge feature1
git branch -d feature1
git branch

git log -3
```

---

## Branches Using VSCode Source Control sidebar

Explanations:
- Below are the commands to:
  - Add a branch called *feature2*.
  - Add a file named *feature2* and modify the *app.txt* file.
  - Add the changes to the staging area and commit them.
  - View the differences between the *main* and *feature2* branches.
  - Checkout *main*, then merge *feature2*, and delete the *feature2* branch.
- Either use the below commands, or use the VS Code source control sidebar.

Commands:
```
git checkout -b feature2

cat << 'EOF' > feature2.txt
Some text.
EOF

cat << 'EOF' >> app.txt
Feature 2.
EOF

git add .
git commit -m 'Add feature 2'
git diff main feature2

git checkout main
git merge feature2
git branch -d feature2
git log -3
```
