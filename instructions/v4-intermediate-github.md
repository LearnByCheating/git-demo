# Intermediate GitHub

## Contents:  

[Add collaborators](#add-collaborators)  
[Protect branches](#protect-branches)  
[Releases](#releases)  
[Add a software license](#add-a-software-license)  
[Fetch or Pull from the remote repository](#fetch-or-pull-from-the-remote-repository)  
[Collaborative Development models](#collaborative-development-models)  
[- Shared Repository Model - Simple example](#shared-repository-model---simple-example)  
[- Shared Repository Model - More involved example](#shared-repository-model---more-involved-example)  
[- Fork and Pull Model](#fork-and-pull-model)  
[Issues](#issues)  
[Add a final release](#add-a-final-release)  

---
Back to [V3 Beginning GitHub](v3-beginning-github.md)  
Back to [README](../README.md)  

---

## Intro

These are the steps to continue building the git-demo app covered in the Intermediate GitHub video. After watching the video, you can follow these steps one or more times until you feel comfortable with the commands. These steps are covered generically in the Intermediate GitHub CheatSheet.

To start over from the beginning of this video, run the command:  
`git reset --hard v3-beginning-github` to reset the local environment.  
Then do a force push to GitHub:  
`git push --force` or `git push -f`.  

---

## Add collaborators

To add collaborators to a GitHub repository:
1. Open Settings.
1. Click Collaborators and teams.
1. Click the Add people button. 
1. Enter the person's GitHub username.
1. Assign the appropriate role. 

---

## Protect Branches

To protect the main branch from force pushes or deletions:
1. Open Settings.
1. Click Branches.
1. Add Branch Protection rule.
1. To protect the "main" branch set Pattern to "main".
1. Check the protection options that you want. For example:
    - Require a pull request before merging. 
      - Require approvals. Note: you can't approve your own pull requests.
    - Allow Force Pushes. This allows collaborators with push (write) access to make force pushes.
    - Allow Deletions. This allows collaborators with push (write) access to delete the branch.  

---

## Releases

Explanations:
- You can convert tags into releases on GitHub.
- Log your commits. Tags will show up.
- Add tag name *v3-beginning-github* to the last commit. Default commit is the last commit.
- Log the commits again to see the new tag.
- Push the tag to the remote. Or to push all tags: `git push --tags`

Commands:
```
git log --oneline
git tag <commitId> v3-beginning-github
git log --oneline
git push origin v3-beginning-github
```

GitHub, make a release from a tag:  
1. Refresh the GitHub repository main page.
1. Click Releases.  
1. Click Tags 
1. Select a tag
1. Click Create release from tag
1. For the title, use semantic versioning (Major.Minor.Patch). First version is 1.0.0.
1. Release notes: List the changes from the last release.
1. Click Publish release.

---

## Add a software license

1. On Github click Add File.
1. File name: LICENSE or LICENSE.md.
1. Click Choose license template button.
1. Select a license (e.g., MIT License). 
1. Enter year and your name or leave the defaults.
1. Click Review and submit button.
1. Commit the new file directly on GitHub.  
   Alternatively, create a LICENSE file locally on your computer, copy and paste the License text from GitHub and make a commit.

---

## Fetch or Pull from the remote repository

If your local repository main branch is one or more commits behind the GitHub remote repository, do a fetch or pull.

### Fetch:

Explanations:
- Fetch downloads commits that are ahead of your local repository.
- Check the status. It will print how many commits you are behind.
- Print the difference between your local main branch and the remote origin/main branch.
- Merge the changes from the remote.
- log all commits since tag v3-beginning-github.
- Undo the last commit with the `reset` command.
- Log the commits again to confirm the last commit is gone.

Commands:
```
git fetch
git status
git diff main origin/main
git merge origin/main
  or with a custom message:
git merge -m "Add MIT License" origin/main
git log --oneline v3-beginning-github..
git reset --hard head^
git log --oneline v3-beginning-github..
```

VS Code: Optionally, use source control > 3 dots > Fetch 

### Pull:

Explanations:
- `Git pull` will download the commits and merge them.
- log all commits since tag v3-beginning-github.

Commands:
```
git pull
git glog v3-beginning-github..
```

VS Code: Optionally, use source control > 3 dots > Pull

---

## Collaborative Development models

---

## Shared Repository Model - Simple Example

**Part A:** Initial remote setup. Already done.

**Part B (Local repo):** In local repo create a topic branch, code it, sync main branch, push topic branch.  

Explanations:
- You can add/modify files manually, or with the Unix commands below.
- Make sure you understand each command, what it does, and why you are doing it.

Commands:
```
git pull
git checkout -b feature5

cat << 'EOF' > feature5.txt
Some text.
EOF

git add .
git commit -m 'Add feature5.txt'

cat << 'EOF' >> app.txt
Feature 5.
EOF

git commit -am 'Add feature 5 to app.txt'

git checkout main
git pull

git checkout feature5

git push origin feature5
```

**Part C (Remote repo):** Go to remote repo to create a pull request from the pushed topic branch.

Remote repo should have a notice saying "Feature5 had recent pushes".

If so: 
1. Click *Compare & Pull request* button 
1. Modify the commit message: Add feature 5
1. Open a pull request page: *Create pull request* dropdown
1. Click *Create Pull Request*.

If not:  
1. Click *Pull requests*.
1. Click *New pull request*.
1. Compare: feature5.
1. Click *Create Pull Request*.

**Part D:** Review pull request. Skip this step.

**Part E:** Incorporate review feedback. Skip this step.

**Part F (Remote repo):** Merge or Reject the Pull Request. Requires write access.

From the Pull Requests page, in the Conversations tab:
1. In the *Merge* button dropdown, make sure *Merge pull request* is selected.
1. Optionally, modify the message (e.g., "Merge pull request #1 feature5")
1. Click Confirm merge.
1. If you don't need the branch anymore, click *Delete branch*
1. Optionally, to view the new commits, go back to the main repo page and click the commits number.

**Part G (Local):** Sync the local repository with the remote.

```
git checkout main
git pull
git branch -D feature5

# To view the commit log:
git glog v3-beginning-github..
```

---

## Shared Repository Model - More involved Example

**Part A:** Initial remote setup. Already done.

**Part B (Local repo):** In local repo create a topic branch, code it, sync main branch, push topic branch.  

- You can add/modify files manually, or with the Unix commands below.
- Make sure you understand each command, what it does, and why you are doing it.

```
git pull
git checkout -b feature6

cat << 'EOF' > feature6.txt
Some text.
There is a problem on this line.
EOF

git add .
git commit -m 'Add feature6.txt'

cat << 'EOF' >> app.txt
Feature 6.
EOF

git commit -am 'Add feature 6 to app.txt'
```

**Add a commit directly to the Remote repo to put it out of sync with local repo:** 
- On GitHub, add a file called about.txt with some text directly on GitHub and commit it.

- Back to local repo: check out main, sync it with the remote, checkout feature6, merge in main, push branch.

```
git checkout main
git pull

git checkout feature6
git merge main

git push origin feature6
```

**Part C (Remote repo):** Go to remote repo to create a pull request from the pushed topic branch.

Remote repo should have a notice saying "Feature6 had recent pushes".

If so: 
1. Click *Compare & Pull request* button 
1. Modify the commit message: Add feature 6
1. Open a pull request page: *Create pull request* dropdown
1. Click *Create Pull Request*.

If not:  
1. Click *Pull requests*.
1. Click *New pull request*.
1. Compare: feature6.
1. Click *Create Pull Request*.


**Part D (Remote repo):** Optional Pull Request review by the repo owner, or other collaborator with write access. You cannot Approve or Request Changes on your own pull request, but you can add a comment to it.
- Branch protection can require that pull requests get approved by one or more reviewers before they can be merged.
- Reviewers can review it by opening the Pull request. To get there from the main page, click *Pull Requests*, then select *feature5*.
- With the pull request open the changes can be reviewed by clicking the *Files changed* tab.
- To submit your review, click the *Review changes* button. Select Approve, Request changes, or Comment. Click *Submit*.
- Make a comment that "There is a problem in feature6."

**Part E (Local repo):** Incorporate review feedback.
- Make a change to feature6.txt.
- Commit the change, then push it to the remote.
```
git commit -am 'Correct problem in feature6.txt'
git push origin feature6
```

**Part F (Remote repo):** Merge or Reject the Pull Request. Requires write access.  

Go to the Pull Requests page, Conversations tab:  
1. In the *Merge* button dropdown, change it to *Squash & merge*.
1. Optionally, modify the message (e.g., "Merge pull request #2 feature6")
1. Click *Confirm merge*.
1. If you don't need the branch anymore, click *Delete branch*
1. Optionally, to view the new commits, go back to the main repo page and click the commits number.

**Part G (Local repo):** Sync the local repository with the remote.

```
git checkout main
git pull
git branch -D feature6

# To view the commit log:
git glog v3-beginning-github..
```

---

## Fork and Pull Model

- You can't fork your own repository. You need to fork another account. GitHub has a Repo just to demonstrate forking. 
  - GitHub forking tutorial: https://docs.github.com/en/get-started/quickstart/fork-a-repo
  - GitHub repository that you can fork as practice: https://github.com/octocat/Spoon-Knife

Regardless, following are the steps from the video. Unless you have two accounts, you won't be able to follow them. 

**Part A:** Fork and clone the git-demo repo, then configure the remote:

**A1 (Remote repo):** Fork the Repo:
1. On the original GitHub repository Click *fork* button. 
1. Optionally, modify the repository name to git-demo-fork
1. Click *Create fork*
1. Get the URL by clicking the *Code* button, then the *URL copy icon*.

**A2-A3 (Local fork repo):** Clone the forked repo and set the remote:

Explanations:
- Open the Terminal and change directories to the folder you want to clone the fork into. 
- Add the original repository's URL to alias "upstream".
- Origin is automatically set when a repo is cloned.

Commands:
```
git clone https://github.com/your-username/git-demo-fork.git
git remote add upstream https://github.com/original-username/git-demo.git
git remote -v

git checkout -b feature7
```

**Part B (Local fork repo):** Create local topic branch and push it to the forked repo:

Commands:
```
git checkout -b feature7

cat << 'EOF' > feature7.txt
Some text.
This is a bug.
EOF

git add .
git commit -m 'Add feature7.txt'

cat << 'EOF' >> app.txt
Feature 7.
EOF

git commit -am 'Add feature 7 to app.txt'

git checkout main
git pull upstream main
git checkout feature7
git push origin feature7
```

**Part C (Forked remote repo):** Go to remote forked repo (git-demo-fork) to create a pull request from the topic branch.  

1. The main page should say: "feature7 had recent pushes". Click *Compare & pull request*
1. Opens to the original repository. Optionally, change the pull request title "Add feature 7" and/or add a comment.
1. Click *Create Pull Request* button.

**Part D (Original remote repo):** Pull request review. Skip this step.

**Part E (Local fork repo):** Incorporate review feedback. Skip this step.

**Part F (Original remote repo):** Merge or Reject Pull Request. Write access to the original repo is required.

1. You may need to refresh the original git-demo repo. Open the Pull request.
1. Change *Merge Pull Request* to *Rebase & Merge*.
1. Click *Confirm Merge* button.
1. Click *Delete branch* button.
1. Optionally, to view the new commits, go back to the main repo page and click the commits number.

**Part G (Local fork repo):** Sync local repo to the original git-demo remote, then push main to git-demo-fork remote:

```
git checkout main
git pull upstream main
git push origin main
git branch -D feature7
```

---

## Issues

### Create an issue
1. On the GitHub repository, click the Issues tab, then the *New Issues* button. 
1. Add a title: "Feature 7 contains a bug"
1. Add a message with more info.
1. Optionally add a label.
1. Optionally assign someone to the issue.
1. Click *Submit New Issue*. Issues are automatically assigned a number when created.

### Fix the issue 
Note: In the video, the issue is fixed in the forked local repo, but you can do it on the original (git-demo) local repo.

**Part B (Local fork repo):** Create a local topic branch and push it to forked repo.
In the commit extended message put the issue number like `fixes #1`. Change the number 1 to the actual issue number. 
```
git pull upstream main
git checkout -b patch-feature7

[In the feature7.txt file, change line 2 to "This bug has been patched."]

git commit -am 'Fix bug in feature7

fixes #1'
git checkout main
git pull upstream main
git checkout patch-feature7
git push origin patch-feature7
```

**Part C (Forked remote repo):** Go to remote forked repo `git-demo-fork` to create a pull request from the topic branch.

The main page should say: "patch-feature7 had recent pushes":
1. Click *Compare & pull request*
1. The original repository should open. Optionally, change the Pull request title to something like "Patch feature 7". Make sure the Pull Request comment includes the issue number `fixes #1`. 
1. Optionally, check box: "Allow edits by maintainers".
1. Click *Create Pull Request* button.

Note: putting the issue number in the Pull Request description will automatically close the issue when the Pull Request is merged. Preface the issue number with one of the following keywords: *close, closes, closed, fix, fixes, fixed, resolve, resolves, resolved*.
So if the issue number is 1, the Pull Request description would include something like `fixes #1`. 

**Part D (Original remote repo):** Pull request review. 
- Look over the change in the Pull Request's *Files changed* tab.

**Part E (Local fork repo):** Incorporate review feedback. 
- Skip this step.

**Part F (Original remote repo):** Merge or Reject Pull Request. Write access to original repo is required.

1. Open the Pull Request page on the Conversations tab.
1. Change *Merge Pull Request* to *Squash & Merge*.
1. Click *Confirm Merge* button.
1. Click *delete branch* button.

- The issue should now automatically have closed. You can still access it by clicking the *Issues* tab and selecting *Closed* issues.

**Part G (Local repo):** Sync the local repository with the remote.

```
git checkout main
git pull upstream main
git push origin main
git branch -D patch-feature7

# To view the commit log:
git glog v3-beginning-github..
```

---

## Add a final release

Add a tag to the last commit and push it to the remote:  
```
git tag v4-intermediate-github
git push origin v4-intermediate-github
```

Create a release from the v4 tag:  
1. On the GitHub repository click *Releases*
1. Click *Draft a new release* 
1. Choose a tag: v4-intermediate-github
1. Release title: 4.0.0
1. Describe: List the changes since the last commit.
1. Click *Publish release*
