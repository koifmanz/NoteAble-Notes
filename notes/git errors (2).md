---
tags: [Notebooks/DevOps]
title: git errors
created: '2020-08-19T06:45:15.026Z'
modified: '2020-08-19T06:50:24.083Z'
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

*Source: [stackoverflow.com](https://stackoverflow.com/questions/24114676/git-error-failed-to-push-some-refs-to-remote)*

