## New repository from folder

create new repository on GitHub (do not initialize the new repo with README, licence or gitignore)
change current working directory to local project
initialize the local directory as a Git repository `git init`
add the files in the local repository `git add .`
commit the files  `git commit -m "First commit"`
copy remote repository URL (at the top of GitHub repository's Quick Setup)
Add the URL for the remote repository where local repository will be pushed.
```
git remote add origin remoteRepositoryURL
# Sets the new remote
git remote -v
# Verifies the new remote URL
```
push the changes in local repository to GitHub `git push origin master`

## clone repository
`git clone https..... ./` will clone all files from repository into this folder (do not create repository folder!!!)


## Push to repository
`git add .`
`git commit -m "some message"`
`git push origin master`

## Pull

## commands
git log --oneline   *list of what was changed added ???*
git status  *gives me info about branche, commits, ...*

## Branches
`git branch newbranch`  **will create a new branch**
`git bramch -a` **will list all branches** the colored with star is current branch I'm working at
`git checkout somebranch` will change my current branch
`git branch -d someBranch` will delete branch only if it is marged
`git branch -D someBranch` will 'hard' delete branch
`git checkout -b someBranch` will maybe merge and delete branch

`git push origin branchName`

`git branch -d branchName` will delete branch if it is fully marged 

changes will commit only to branch I'm currently working at, when I switch to other branch, changes wont be there
https://www.youtube.com/watch?v=QV0kVNvkMxc

## Setting config
In order not to have type user and password every time I'm pushing or pulling, I can edit `.git/config`

```
[remote "origin"]
	url = https://user:password@github.com/MojaCZ/Notes.git
	fetch = +refs/heads/*:refs/remotes/origin/*
	pushurl = https://user:password@github.com/MojaCZ/Notes.git
```
