---
tags: [Notebooks/DevOps]
title: git Cheat Sheet
created: '2020-01-29T12:25:45.600Z'
modified: '2020-01-29T12:36:32.420Z'
---

# git Cheat Sheet

### Working Directory
- Area where all our files, dirs and changes are living
- use git status to check what need to be add
- to add to stage 
```shell
git add <name> / *
```

### Staging Area
- Files and dirs we add to the staging area
- use git status to check what need to be commit
```shell
git status
```
- use git commit to move to repostitory
```shell
git commit -m "Message"
```

### Git Repository
- Where all our snapshots are stored
- use git log to view repository history
```shell
git log
```
- the log commit id can use to view diffrences between commits

### Branches
- use git branch to list all branches. The green branch is the current one
```shell
git branch
```
- use git checkout with -b flag to create new branches
```shell
git checkout -b <branch name>
```
- use git checkout to switch between branches. Master is a branch too.
```shell
git checkout <branch name>
```

### Branches - Merge
- Merging will take one branch and insert it to another
```shell
git merge <branch name to merge>
```
- It is not recomended to remove a branch, it does not take a lot of space. It is possible
```shell
git branch -d <branch name>
```

### Push to github 
- first add github link.
```shell
git remote add origin https://github.com/<username>/<github rep name>.git
```
- then use git push to upload
```shell
git push -u origin master
```




