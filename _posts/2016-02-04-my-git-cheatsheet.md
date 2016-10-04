---
title: "my git cheatsheet"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True

comments: true
subclass: 'post tag-speeches'
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-02-04 13:21:56 EST
---

Just to keep a note about some frequently used git commands:

## Push an existing project to a remote repository

```bash
# in your remote repo
git init --bare my-project.git

# in your local project folder
git init
git add .
git commit -m 'initial commit'
git remote add origin git@your-git-host:gitRepot/my-project.git
git push origin master
```


## Compare the difference between two branches

Display commits in branch-X, but not in master(or other branch you want to specify).

- [credit](http://stackoverflow.com/questions/13965391/how-do-i-see-the-commit-differences-between-branches-in-git)

```bash
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr)%Creset' --abbrev-commit --date=relative master..branch-X
```

## Squash multiple commits into one


```bash
git rebase -i HEAD~3 # 3 is the number of recent commits
```

The above rebase command will bring up the rebase editor

```bash
pick f392171 Added new feature X
pick ba9dd9a Added new elements to page design
pick df71a27 Updated CSS for new elements
```

Change your file to this:

```bash
pick f392171 Added new feature X
squash ba9dd9a Added new elements to page design
squash df71a27 Updated CSS for new elements
```

Once it's done, exit the editor and push the changes to the remote branch, using -f only when you are sure you are the only one who is making the change.
