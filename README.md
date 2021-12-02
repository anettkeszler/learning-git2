# git-tutorial

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








