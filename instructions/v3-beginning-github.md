# Beginning GitHub

## Contents:  
[Add README.md file to git-demo project](#add-readmemd-file-to-git-demo-project)  
[Set up remote](#set-up-remote)  
[Push branch commit to remote](#push-branch-commit-to-remote)  
[Clone a repository](#clone-a-repository)  

---
Back to [V2 Intermediate Git](v2-intermediate-git.md)  
Go to [V4 Intermediate GitHub](v4-intermediate-github.md)  
Back to [README](../README.md)  

---

## Intro

These are the steps to continue building the git-demo app covered in the Beginning GitHub video. After watching the video, you can follow these steps one or more times until you feel comfortable with the commands. These steps are covered generically in the Beginning GitHub CheatSheet.

To start over from the beginning of this video, run the command:  
`git reset --hard v2-intermediate-git` to reset the local environment.  
Then do a force push to GitHub:  
`git push --force` or `git push -f`.  

---

## Add README.md file to git-demo project

Explanations:
- Create file named README.md
- Add text and optional Markup syntax for styling.
- Stage and commit it.

Commands:
```
cat << 'EOF' > README.md
Put info about the app here.
This page is displayed at the bottom of the GitHub repository's main page.
Use Markdown for styling.
EOF

git add README.md
git commit -m 'Add readme'
```

---

## Set up remote

### Create the remote on GitHub:
- Create a new empty Repository on GitHub named git-demo.
- Copy the URL.

### Set the remote locally and make the initial push:  

Explanations:
- Set remote alias "origin" to the GitHub remote URL.
- View all remote names. The -v verbose option shows the URL.
- Make initial push to the remote, setting "origin" as the upstream remote.
- Push all tags to the remote.

Commands:
```
git remote add origin [paste URL]
git remote -v
git push -u origin main
git push --tags
```

---

## Push branch commit to remote

Explanations:
- Create branch feature4.
- Add/modify code.
- Stage and commit it.
- Checkout main branch.
- Merge feature4 into main.
- Push main to remote.
- Delete feature4 branch.

Commands:
```
git checkout -b feature4

cat << 'EOF' > feature4.txt
Some text.
EOF

cat << 'EOF' >> app.txt
Feature 4.
EOF

git add .
git commit -m 'Add feature 4'
git checkout main
git merge feature4
git push
git branch -d feature4
```

VS Code: Optionally, use source control > 3 dots > Push

---

## Clone a repository

To clone a repository, go to the repo main page, click the Code button, then copy the URL.

Explanations:
- Open your terminal app on your computer and get the present working directory `pwd`.
- Change directories to the folder you want to project to be cloned to, such as to the desktop.
- Clone the repository. Paste in the repo's URL followed by the name of the repo (leave it blank to keep the same name as the cloned repo)
- Log the git history.
- Optionally delete the git repo.

Commands:
```
pwd
cd ~/Desktop
git clone [paste in URL] local-repo-name
cd local-repo-name
git log --oneline
rm -rf .git
```
