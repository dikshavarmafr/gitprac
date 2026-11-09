## Git Merge — Hands-on Learnings

### 1. What is a fast-forward merge?

A fast-forward merge happens when the target branch has no new commits since the feature branch was created. Git simply moves the target branch pointer forward to the latest commit on the feature branch.

**Example:** Merging `feature-login` into `main`.

### 2. When does Git create a merge commit?

When both branches have independent commits and their histories have diverged, Git creates a new merge commit with two parent commits to combine the histories.

**Example:** Merging `feature-signup` into `main`.

### 3. What is a merge conflict?

A merge conflict occurs when Git cannot automatically combine changes from different branches, such as when both branches modify the same line differently.

Git pauses the merge and asks us to resolve the conflict manually.

### 4. How do you resolve a merge conflict?

1. Run `git status` to identify conflicted files.
2. Open the conflicted file.
3. Decide which changes to keep (or combine both).
4. Remove Git's conflict markers.
5. Run `git add <filename>`.
6. Run `git commit` to complete the merge.

### 5. What are Git conflict markers?

- `<<<<<<< HEAD` — current branch changes.
- `=======` — separator between the changes.
- `>>>>>>> branch-name` — incoming branch's changes.

### 6. What did I learn?

- Fast-forward merges move a branch pointer without creating a merge commit.
- Diverged branches require a merge commit.
- Merge conflicts require manual resolution.
- `git add` marks a conflict as resolved.
- `git commit` completes the merge.

