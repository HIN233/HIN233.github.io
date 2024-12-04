---
title: Learn Git the Hard Way
date: 2024-11-30
summary: 对Git最基础的介绍，快速上手Git
category: 电子扫盲课
tags: [教程笔记, Git]
---

# Basic Git Syntax

## The Most Basic Syntax

Have a quick check the commands below.

1. `git clone`
2. `git add`
3. `git commit`
4. `git push` `git pull`
5. `git reset`
6. `git rebase`
7. `git checkout`

## Git Workflow

### Personal Workflow

1. `git add`
2. `git commit`
3. `git push`

### Collabration

1. `git clone` clone the remote repository to your PC
2. `git checkout -b fixbugs1` create a new branch and switch to it
3. Make change on the code
4. Check your work on a visualization window or by `git diff`
5. `git add` add changes in the working directory to the staging area (preparing them to be included in the next commit)
6. `git commit` commits the changes in the staging area to local git repository
7. `git push <remote repository name> <branch name>` upload local branch changes to github

If you find the remote repository had been changed (**a**) before your _push_

1. `git checkout main` switch (HEAD) to the _main_ branch [same as`git switch main`]
2. `git pull <remote repository name> master(main)` pull the remote changes to your PC
3. `git checkout <your own branch name>` switch to your change
4. `git rebase main` when the HEAD points to your branch (4.), it will take the changes from _your change branch_ and reapply them on the _master(main) branch_. The result is like that you modified the **a** files

```
remote main -- before -- a
local main -- before -- b1 -- b2

->
remote main -- before -- a
local main -- before -- a -- b1' -- b2'
```

5. `git push -f <remote repository name> <your branch name>` (**f**orce) push
6. the master use _squash and merge_ in _pull request_ to integrate all the commit

After the remote update

1. `git branch -d <your own branch name>` delete local branch
2. `git pull <remote repository name> master(main)` get the latest version

---

The following are basically scattered notes, mainly for personal use.

## Commands

### Branch

create a new branch by `git branch fixbugs1`
switch to it `git checkout fixbugs1` and `git commit`

or `git checkout -b fixbugs1` and `git commit`

`git merge`
`git rebase`
`git cherry-pick`

`git reset`
`git rebase`

### Remote work

`git pull` = `git fetch` + `git merge`
`git pull --rebase` = `git fetch` + `git rebase`

`git pull --rebase`+`git push`

## Syntax Anaysis & Examples Notes

- `git add .` where `.` is all the files changed.
- `git checkout -b <name>` create a new branch and switch to it
- `git commit -m` `-m` means message

### Updating...
