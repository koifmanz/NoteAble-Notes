---
tags: [Notebooks/DevOps]
title: git errors
created: '2020-08-19T06:45:15.026Z'
modified: '2020-08-19T06:48:41.323Z'
---

# git errors

### failed to push some refs to remote

If the GitHub repo has seen new commits pushed to it, while you were working locally:

```shell
git pull --rebase origin master
git push origin master
```
or 
```shell
git pull --rebase
git push
```

