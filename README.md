# Git and GitHub tutorial

### Git
Git is a version control system, that allows one or more people to work on the same code

### Github 
Hosting provider, that allows us to host our project

### How git works

- from Working Directory to Staging Area
```aidl
git add <filename>
```
- from Staging Area to Commit History
```aidl
git commit -m "commit message"
```

![img.png](img.png)

This is happening on our local machine. <br> 
We want to store our project on a remote server. <br>
From Commit History (local server) to Remote Server (GitHub, BitBucket, AWS, GitLab): <br>
```aidl
git push
```

To gain the changes on the remote server to the local machine: 
```aidl
git pull
```

##### What is a commit? 
It captures a snapshot of the project's currently staged changes, it is a safe point. 



### Verify git
```aidl
git --version
```
- if you get the below response back there is no git installed on your computer
```aidl
ksh: git: not found, No such file or directory
```

### Git setup
List options:
```aidl
git config
```
```aidl
git config --global user.name "anettkeszler"
git config --global user.email "anett.dr.keszler@gmail.com"
git config --global color.ui auto
```

- List all settings:
```aidl
git config -l
```

### Initialize git on your repository
- Repositories in git contain a collection of files of various different versions of a project.
- If you have a folder project, and you want to make it visible for git (you want to tell that the working directory is a git repository) we have to initialize the working directory

- Desktop: 
```aidl
mkdir learning git
cd learning git
git init .
```

Now you can issue git commands
Git init is mainly for brand-new projects. If you want to work on an existing project on GitHub, you have to clone it and this is already initialized with git.

```
rm -rf .git
```
This will delete git from the repository, it will no longer a git repository

### Git status
```aidl
git status
```
- Git status shows the currant state of your git working directory and staging area
- Untracked files: files which are in Working Directory and with 'git add' you can add them to Staging Area (tracked files)

- If you want to revert your files from staging area to working directory (tracked --> untracked)
```aidl
git rm -r --cached .
git rm --cached index.html
```

### Git add
```aidl
git add index.html
git add.
git add -A
```
'git add .' command will add all files from the current directory downwards (so if you have changes in another directory upwards, those files won't be added). <br>
'git add -A' : if you want to add ALL files

### Git commit 
```aidl
git commit -m "commit message"
```
```aidl
git log
```
```aidl
git show <hash of the commit>
```
```aidl
vim index.js // it opens vim editor, you can add js code now
```
press 'i' to insert
```aidl
console.log("hello Anett");
```
press 'esc + :x!' --> it will save the changes
```aidl
cat index.js // it will display the file's content
```
```aidl
git diff // diff is what I have changed/added a line, it gives you the diff of last commit and what you have in the working directory
```
Remove console.log from index.js, then:
```aidl
git restore index.js
```
Git restore will reset the last committed status of the file

### Amend commit message
The best practice is to have meaningful commit messages
```aidl
git commit --amend -m "amend is to modify the last commit message"
```

### GitHub
- Remote server, where we can host git projects

#### How to push an existing repository from the command line to GitHub
First, create an empty repository on GitHub
```aidl
git remote add origin git@github.com:anettkeszler/learning-git.git
git branch -M main --> it will change master to main
git push -u origin main --> it will fail first
```
- "Permission denied (publickey)"

#### SSH key setup
- you need to configure SSH key
- Settings --> SSH and GPG keys --> generating SSH key
- Follow the instructions
- Add your generated SSH key to your GitHub account
- now you are able to push from local to remote


### Branches
- main = master branch
- a branch represents an independent line of development
- check the branches in your local machine
```aidl
git branch
```
- check the branches in the remote server
```aidl
git branch -r
```
- check all branches:
```aidl
git branch -a
```
- create a new branch:
```aidl
git branch feature-a
```
- switch brances:
```aidl
git checkout feature-a
```
- switch to the previous branch:
```aidl
git checkout -
```
- if you go back to main, and check logs (git log), you cannot see the last committed new file, because that is on another branch (feature-a)
- this feature branch doesn't exist in GitHub yet
- push the changes on the local feature branch to the remote feature branch:
```aidl
git push
```
fatal: The current branch feature-a has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin feature-a

--> this is because feature-a branch haven't exist on remote yet.

- create a new branch and checkout to that branch in 1 step
```aidl
git checkout -b feature-b
```
- delete a branch:
```aidl
git checkout main
git branch -d feature-b
```

### Merging and Pull Requests
- when you want to push a feature branch to main, best practice is to do it through a PR, as it can be reviewed before merging
- you could merge it through bash:
```aidl
git checkout main
git merge feature-a
```
- create pull request from feature-a to main in GitHub, merge it
- go back to terminal
```aidl
git log
```
- you cannot see the changes on main, because first you need to pull it
- if you delete the feature branch in GitHub after merging, it is still exists on your local machine, you need to delete it

### Git Workflow
- when you start to work on a new feature, the first thing you do is to pull the latest changes from master to your local machine 
- from that point you create a new branch (git checkout -b feature-a), start working on your feature, make commits
- it is advisable to rebase your changes against master, especially if you have been working on the feature for days, as you know, master will move on.
- so what you want to do is to bring the latest changes from master into your local machine and when you rebase you might not have conflicts
- if you have conflicts you have to resolve all of your conflicts
- if you have 10 commits, then you have to resolve the conflicts for each commit. So what is advisable to do is to squash all of your local commits first, and rebase master
- you squash your commits, so on your local branch you have one single squashed commit, and when you rebase, you need to remove this commit, this action is called stash, this means that you put your commit aside, than you bring all the changes from master with rebase, and then you put your commit back on the top of it
- then you push to remote and raise a pull request
- if this is approved, then you merge your commit into master

### Dealing with conflicts
- merge conflict occur when 2 developers work on the same line of the file
- you need to pull the changes first from the same file then resolve the conflict

### Rebase
- you have a feature branch, and you are working on that branch
- during that time, main branch may have multiple commits, main branch has moved on, and you don't have that commits from main
- what rebase does: it takes all of your new commits away, it will bring all the commits from master into your branch, than it will apply your changes on top of it.

```aidl
git pull --rebase
git pull -r origin main // remote main/master/master-staging
```
- open intellij or open the file in vim
- resolve first merge conflict, then:
```aidl
git add .
git rebase --continue
```
- open intellij or the file in vim again, and resolve the second commit, than:
```aidl
git add .
git rebase --continue
```
- continue it until all conflicts will be resolved, than:
```aidl
git push
```
It will give you an error message:
```aidl
To github.com:anettkeszler/learning-git2
 ! [rejected]        feature-xyz -> feature-xyz (non-fast-forward)
error: failed to push some refs to 'git@github.com:anettkeszler/learning-git2'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
```aidl
git push -f
```
- create pull request from feature branch to main

### Squash commits
- you are working on your feature branch, and you have 10 commits.
- before you rebase, it is better to squash that 10 commits into 1 commit, than you do not need to resolve 10 commits' merge conflicts, only 1.








