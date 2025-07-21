# Basics of Git and GitHub

These notes cover essential Git and GitHub commands for documenting, managing, and collaborating on projects.

## Terminology
- **Git:** Version control/source control system to manage changes made to files or code locally.
- **Commits:** Checkpoints or changes made to the code or one or more files.
- **Staging:** Holding changes before committing.
- **Branch:** Alternate version of code that can be worked on without affecting the original version.
- **Merging:** Combining different branches into one.
- **Rebasing:** A way to integrate changes from one branch onto another while maintaining a linear history.

## Git Basics
### Configuration
Set your username and email for Git:
```sh
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Initialize a Repository
Start tracking a folder with Git:
```sh
git init
```

### Branching
Branches allow development without affecting other versions of the code. For instance, you can implement a feature in a separate branch and merge it once verified.

- **Create a new branch**:
  ```sh
  git branch <branch_name>
  ```
- **Switch to a branch**:
  ```sh
  git checkout <branch_name>
  ```
- **Create and switch to a new branch**:
  ```sh
  git checkout -b <branch_name>
  ```
- **Merge branches** (navigate to the destination branch):
  ```sh
  git merge <source_branch_name>
  ```
- **Push all branches to remote**:
  ```sh
  git push --all origin
  ```

### Rebasing

Rebasing is used to integrate changes from one branch (e.g., `main`) onto another branch (e.g., `feature-branch`) and place all your changes on top of the latest branch history. This keeps a linear project history, avoiding unnecessary merge commits.

1. **Switch to your feature branch**:

   ```bash
   git checkout <your-feature-branch>
   ```

2. **Fetch the latest changes from the remote repository**:

   ```bash
   git fetch origin
   ```

3. **Rebase your feature branch onto the latest `master` branch**:

   ```bash
   git rebase origin/master
   ```

   This command will:

   * Apply any new commits from `origin/master` that your feature branch doesn’t yet have.
   * Place your commits on top of these new `master` commits in the commit history.

4. **Resolve any conflicts if they arise**:

   * If conflicts occur during the rebase, Git will pause and give you the opportunity to resolve them.
   * Use `git status` to identify conflicted files and manually fix each one.
   * After resolving, use `git add <file>` to mark them as resolved, and then continue the rebase with:

     ```bash
     git rebase --continue
     ```

5. **Force-push the rebased branch back to the remote**:
   Since you've updated your local commit layout, you’ll need to force-push:

   ```bash
   git push origin <your-feature-branch> --force
   ```

   ⚠️ **Note**: Only force-push if you’re sure it won’t disrupt other collaborators.

This ensures that your feature branch is based on the latest `master`, and your changes appear cleanly on top.

### Squashing commits into one

Sometimes, especially after you've already pushed changes to the remote and are preparing to merge a pull request, it's useful to combine all your feature branch commits into a single commit. This keeps the commit history focused and easy to follow.

1. **Start an interactive rebase**:

   ```bash
   git rebase -i origin/master
   ```

2. **In the editor that appears**, change all but the first `pick` to `squash` (or just `s`). Example:

   ```
   pick 123abc First commit
   squash 456def Fix A
   squash 789ghi Refactor
   ```

3. **Edit the final commit message** if prompted, then save and close.

4. **Push your updated branch to the remote**:

   ```bash
   git push origin <your-feature-branch> --force
   ```

This can be used to clean up your branch before review or merging, ensuring your contribution is easy to read and review.

### Custom squash example with grouped commits

Sometimes, instead of squashing all your commits into one, you may want to **group related commits together** and give each group a meaningful message. This is useful for keeping the history clean while still showing logical steps in your work.

1. Start an interactive rebase, looking back far enough to include all the commits you want to reorganize:

   ```bash
   git rebase -i HEAD~10
   ```

2. In the editor that opens, you'll see a list like this:

   ```
   pick a1 First commit
   pick b2 Add feature A
   pick c3 Refactor feature A
   pick d4 Fix bug in feature A
   pick e5 Add feature B
   pick f6 Minor tweaks to feature B
   pick g7 Prepare for production
   pick h8 Fix logging
   pick i9 Adjust Dockerfile
   pick j0 Final cleanup
   ```

3. Modify the list to group and squash related commits:

   ```
   pick a1 First commit

   pick b2 Add feature A
   squash c3 Refactor feature A
   squash d4 Fix bug in feature A
   # -> Final message: Implement and refine feature A

   pick e5 Add feature B
   squash f6 Minor tweaks to feature B
   # -> Final message: Add feature B

   pick g7 Prepare for production
   squash h8 Fix logging
   squash i9 Adjust Dockerfile
   squash j0 Final cleanup
   # -> Final message: Production readiness and cleanup
   ```

4. When prompted, replace each group’s combined commit message with a clear summary (as shown in the comments above).

5. After resolving any conflicts, complete the rebase and update the remote branch:

   ```bash
   git push origin <your-feature-branch> --force
   ```

This technique is helpful when you want to preserve meaningful history but reduce noise in your commits.

## Pushing Local Code to GitHub
1. **Create or use an existing GitHub repository.**
2. **Set the remote repository:**
   ```sh
   git remote add origin <repository URL>
   ```
3. **Switch to the main branch:**
   ```sh
   git branch -M main
   ```
4. **Push the code:**
   ```sh
   git push -u origin main
   ```

### Staging and Committing
- **Stage changes**:
  ```sh
  git add <filename>
  ```
- **Stage all files**:
  ```sh
  git add .
  ```
- **Commit changes**:
  ```sh
  git commit -m "commit message"
  ```
- **Review commit before committing**:
  ```sh
  git commit --dry-run
  ```

### Rolling Back Changes
- **Revert unstaged changes**:
  ```sh
  git checkout <filename>
  ```
- **Revert staged changes**:
  ```sh
  git restore --staged <filename>
  ```
- **Revert committed changes**:
  ```sh
  git revert HEAD
  ```
- **Hard reset to a previous commit**:
  ```sh
  git reset --hard <target commit ID>
  ```

### Viewing Differences
- **Difference between staged and previous commit**:
  ```sh
  git diff --cached
  ```
- **Difference between two commits**:
  ```sh
  git diff <commit1 name> <commit2 name>
  ```

### Using `.gitignore`
Create a `.gitignore` file to exclude files from Git:
```
# Example .gitignore entries
node_modules/
*.log
```

### Git SSH Login to Remote Repository
SSH-based authentication is an alternative to username-password login and is considered more secure. Use SSH keys by generating them with:
```sh
ssh-keygen
```
To access the public key:
```sh
cat ~/.ssh/id_rsa.pub
```
Copy the output and add it to GitHub under "SSH and GPG keys" in account settings.

### Miscellaneous Commands
- **View commit history**:
  ```sh
  git log
  ```
- **Check status of changes**:
  ```sh
  git status
  ```
- **Checkout a specific commit**:
  ```sh
  git checkout <commit_hash>
  ```
- **Stash changes temporarily**:
  ```sh
  git stash
  ```
- **Show changes in a commit**:
  ```sh
  git show <commit_id>
  ```
- **Remove a file from index and delete it**:
  ```sh
  git rm <filename>
  ```

### Cherry-Picking
Cherry-picking is used to apply a specific commit from one branch to another. This is often used to bring specific changes to other branches without merging an entire branch.

1. **Basic Cherry-Pick** (when target branch is *not* protected):
   - Checkout the target branch:
     ```sh
     git checkout <target_branch>
     ```
   - Cherry-pick the desired commit by using its hash:
     ```sh
     git cherry-pick <commit-hash>
     ```
   - Push the changes:
     ```sh
     git push origin <target_branch>
     ```

2. **Cherry-Picking to a Protected Branch**:
   If a branch is protected, direct pushes are not allowed, and changes must go through a pull request.
   - **Step 1**: Create a new branch from the target branch (e.g., `target-update`):
     ```sh
     git checkout -b target-update <target_branch>
     ```
   - **Step 2**: Cherry-pick the commit:
     ```sh
     git cherry-pick <commit-hash>
     ```
   - **Step 3**: Push the new branch:
     ```sh
     git push origin target-update
     ```
   - **Step 4**: Create a pull request from `target-update` to `<target_branch>` on GitHub, ensuring any required checks pass.
   - **Step 5**: Merge the pull request to complete the process.
