1. Setup and Config
git --version
Displays the installed git version

git config --global user.name
Configures the username used for git commits

git config --global user.eemail
Configures the email used for git commits

git init
Initializes a new Git repo

git status
Shows the current state of files in working directory and staging areas

git add
Adds new or modified giles to staging area

git add .
Stages all changes in the current directory

got commit
Saves staged changes as a commit in thr repo

git log
Displays the repo's commit history

git log --oneline
Displays commit history in a one liner format

git branch
Lists local branches and identifies the current branch

git diff
Shows staged changes compared with the last commit


## Git Branching Commands

### List branches
git branch

### Create a branch
git branch feature-1

### Switch to an existing branch
git switch feature-1

### Create and switch to a new branch
git switch -c feature-2

### Switch using older checkout command
git checkout feature-1

### Create and switch using checkout
git checkout -b feature-2

### View commit history
git log --oneline

### Delete a merged branch
git branch -d feature-2

### Force delete an unmerged branch
git branch -D feature-2

### Check current branch and working tree status
git status
