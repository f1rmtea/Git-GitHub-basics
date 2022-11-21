# Basics of Git and GitHub
These notes are based on a practical approach  and all the essentials that one may require for documenting, managing or collaborating on projects have been included. 

## Terminology
- Git: Version control/ source control system, i.e., lets us manage the changes we made to files or a code. Works locally.
- Commits: Checkpoints or changes made to the code or one or more files.
- Staging: Holding changes before committing.
- Branch: Alternate version of a code. These can we worked on with or without changing the original version.
- Merging: Synchronizing different branches.

## Prerequisites
- Git; can be downloaded from the [Git website](https://git-scm.com/).
- VS code or any other IDE with similar capabilities.
- node.js

## Git 
Git is designed to be used by multiple users. Thus, for one to get credit for the changes they make, identification is necessary. After installing git, the first thing one should do is sign in with their Github username and email address or any other ID of choice. The global variable can be used to make every project on the computer use the same name and email. This can be done using the following command.

```
git config
```

### Managing a folder with Git
The first thing to be done when managing a folder with git is initialize Git in that folder using the terminal or a suitable IDE. The following command is to be used.
```
git init
```

### Branching

Branching is a very useful feature of Git. For example, we want to implement any feature x but do not want it to affect the rest of the code in any way, then we will write that feature in a different branch.
A new branch can be created using this command:
```
git branch <name>
```
To switch to a specified branch, we can hit the following command:
```
git checkout <branch_name>
```
To make a new branch and switch directly to it, we can just do the following.
```
git checkout -b <branch_name>
```
No branch knows about or is affected by the content of other branches.
Once the code in a branch is verified ok, it can be moved into the main or master branch. We navigate to the destination branch and hit the following command for merging two branches.
```
git merge <source_branch_name>
```

### Staging and Committing
Before committing, changes need to be tracked added to the staging environment using the command:
```
git add <filename> 
```
All the files in the folder can be added to the staging environment by simply using the following command.
```
git add .
```
Once the files have been moved into staging, a commit can be registered, using the following command:
```
git commit -m '<commit_name>'
```
This will commit all the staged changes. The commit name needs to be passed in quotes and after the -m argument.
To review the commit prior to making it, we can do the following.
```
git commit --dry-run
```

### Using ".gitignore"
A file named ".gitignore", when present in the current working directory or repository, can be used to virtually hide files from Git. Files not supposed to be managed by Git should be named in this file. This will lead Git to ignoring these files while performing any operation.
".gitignore" itself can be mentioned in the .gitignore file and it will hide itself.

###  Miscellaneous commands
To see the entries and commits that have been made so far, the following command can be used:
```
git log
```

This provides the following information about a commit:
- Hash: Unique ID
- Which branch the head is currently in
- Author name and email address
- Date of commit
- git name

The changes/modifications that have been made so far in the folder or the repository can be fetched with the following command:
```
git status
```
If a file has been tracked previously but has then been modified, git status will show that it has been modified. If any files have been newly added to the folder or the repository, then git status will show them as untracked files.

```
git checkout <hash>
```
This command can be used to go to that particular commit, make changes, look around, whatever.

Sometimes, one may need to temporarily shelf (or stash) changes made to the working copy and switch to working on something else, and then come back to resume and re-apply their previous work. The following command enables one to do just that.
```
git stash
```
An example use case of this is a scenario in which an urgent bug fix is required in a different branch than what is currently being worked on. Current work can be stashed for the time being, and resumed after fixing the said bug.

## Pushing locally managed code or files to a remote repository
In a situation in which work that is or was being managed locally using Git has to be pushed to a remote Github repository, the following steps need to be taken.
1. Make a new repository on your github account or choose an existing one.
2. This repo has to be set as the remote repo for the locally hosted work. This can be done with the command: 
  ```
  git remote add <give any name to the remote repo> <remote repo url>
  ```
  We generally name the remote repo as "origin"
3. Navigate to the main branch with the command:
```
git branch -M <main branch name>
```
4. Push the code to the repo with the command:
```
git push -u origin master 
```
