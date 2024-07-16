# Basics of Git and GitHub

These notes cover essential Git and GitHub commands for documenting, managing, and collaborating on projects.

## Terminology
- **Git:** Version control/source control system, i.e., lets us manage the changes we made to files or code. Works locally.
- **Commits:** Checkpoints or changes made to the code or one or more files.
- **Staging:** Holding changes before committing.
- **Branch:** Alternate version of a code. These can be worked on with or without changing the original version.
- **Merging:** Synchronizing different branches.

## Git Basics
### Configuration
To identify yourself for Git to track changes, configure your username and email:
```sh
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Initialize a Repository
To start managing a folder with Git:
```sh
git init
```

## Pushing Local Code to GitHub
1. **Create or use an existing GitHub repository.**
2. **Set the remote repository:**
   ```sh
   git remote add origin <repository URL>
   ```
3. **Navigate to the main branch:**
   ```sh
   git branch -M main
   ```
4. **Push the code:**
   ```sh
   git push -u origin main
   ```

### Branching
Branching is a very useful feature of Git. For example, if we want to implement any feature but do not want it to affect the rest of the code in any way, then we will write that feature in a different branch.
Create a new branch:
```sh
git branch <branch_name>
```
Switch to a branch:
```sh
git checkout <branch_name>
```
Create and switch to a new branch:
```sh
git checkout -b <branch_name>
```
No branch knows about or is affected by the content of other branches.
Once the code in a branch is verified as okay, it can be moved into the main or master branch. We navigate to the destination branch and hit the following command for merging two branches:
```sh
git merge <source_branch_name>
```
When multiple branches are present locally, the following command can be used to push all the branches to the remote repository:
```sh
git push --all origin
```

### Staging and Committing
Stage changes:
```sh
git add <filename>
```
Stage all files:
```sh
git add .
```
Commit changes:
```sh
git commit -m "commit message"
```
Review commit before committing:
```sh
git commit --dry-run
```

### Rolling Back Changes
#### Revert Unstaged Changes
When files haven't been staged:
```sh
git checkout <filename>
```
This will revert a file to its previous condition.

#### Revert Staged Changes
When files have been staged but not committed:
```sh
git restore --staged <filename>
```

#### Revert Committed Changes
When files have been committed:
```sh
git revert HEAD
```

#### Hard Reset to a Previous Commit
Revert and not store any history:
```sh
git reset --hard <target commit ID>
```
All the history after this commit will be removed.

### Viewing Differences
Check the difference between the current commit and the one that is about to happen (files are in staging):
```sh
git diff --cached
```
Check the difference between two commits:
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
Include `.gitignore` itself to hide it:
```
.gitignore
```

### Git SSH Login to Remote Repository
By default, Git login is based on username and password, but SSH-based authentication can also be used. This is done through SSH keys, which need to be generated beforehand with the command:
```sh
ssh-keygen
```
To get the public key:
1. Run:
   ```sh
   cat ~/.ssh/id_rsa.pub
   ```
2. Copy the output and add it to your GitHub account from account settings under "SSH and GPG keys."

Keys will be compared, and if the keys match, authentication will be successful. SSH login is considered to be safer.

### Miscellaneous Commands
View commit history:
```sh
git log
```
Check the status of changes:
```sh
git status
```
Checkout a specific commit:
```sh
git checkout <commit_hash>
```
Stash changes temporarily:
```sh
git stash
```
Show changes in a commit:
```sh
git show <commit_id>
```
Remove a file from the index and delete it:
```sh
git rm <filename>
```
