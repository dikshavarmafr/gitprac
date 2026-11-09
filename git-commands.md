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

## GitHub Remote Commands

### Add a remote repository
git remote add origin <repository-url>

### List remote repositories
git remote -v

### Push main branch
git push -u origin main

### Push a feature branch
git push -u origin feature-1

### List remote branches
git branch -r

### Fetch changes from remote
git fetch origin

### Pull changes from remote
git pull

### Difference between origin and upstream
origin: Usually points to your own remote repository.
upstream: Usually points to the original repository when working with a fork.

## Git Merge — Hands-on Learnings

### 1. What is a fast-forward merge?
A fast-forward merge happens when the target branch has no independent commits. Git simply moves its pointer forward.

Example: Merging feature-login into main.

### 2. When does Git create a merge commit?
When both branches have independent commits and their histories have diverged, Git creates a new commit with two parents.

Example: Merging feature-signup into main.

### 3. What is a merge conflict?
A merge conflict occurs when Git cannot automatically combine competing changes, such as when two branches modify the same line differently.

### 4. How do you resolve a merge conflict?
1. Run git status.
2. Open the conflicted file.
3. Decide which changes to keep.
4. Remove conflict markers.
5. Run git add <filename>.
6. Run git commit to complete the merge.

### 5. What are Git conflict markers?
- <<<<<<< HEAD: Current branch changes.
- =======: Separates competing changes.
- >>>>>>> branch-name: Incoming branch changes.

### 6. What did I learn?
- Fast-forward merges move branch pointers.
- Diverged branches require a merge commit.
- Merge conflicts require manual resolution.
- git add marks conflicts as resolved.
- git commit completes the merge.
