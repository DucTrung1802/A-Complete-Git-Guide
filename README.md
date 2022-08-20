# A Complete Git Guide

## Cheat Sheet

## 1. What is Git ?
**`Git`** is a free and open source software for distributed version control: 
- Tracking changes in any set of files.
- Using for coordinating work among programmers collaboratively developing source code during software development.

## 2. Git Repositories
A **`Git repository / Git repo / repo`** is a virtual storage of your project. It allows you to save versions of your code, which you can access when needed.
There are 2 types of **`Git repository / Git repo / repo`**:
- **`Remote repository / Remote repo`**: A repository for sharing among many people and arranged on a server (Github, Gitlab, Bitbucket, Azure DevOps).
- **`Local repository / Local repo`**: A repository arranged on a machine, for a single person to use.

## 3. Git Components
Git includes **06** components as the following figure:

<br>

![](Images/Git%20Components.png)

<br>

Explanation:
- **`snapshot`**: Current state (including folders, files...) of the project at a specific point in time.

<br>

- **`remote branch`**: A series of **`snapshot`** on the server.
- **`remote-tracking reference`**: A copy of **`remote branch`** on your local machine.
- **`local branch`**: A series of **`snapshot`** on the local machine.
- **`index / staging area`**: The preparation space for a new **` snapshot`**.
- **`workspace`**: The current state of your project on local machine, may contains `committed files and uncommitted files` or `committed files` only.
- **`stash`**: a temporary local **`snapshot`** of the **`workspace`**, used to save the current state of the **`workspace`** while you work on another branch.

## 4. Git Commands

### 4.1 Getting and Creating Projects

#### 4.1.1 git init

##### a) Function

- Create an empty Git repository or reinitialize an existing one.

##### b) Syntax

```
git init [-q | --quiet] [--bare] [--template=<template-directory>]
	  [--separate-git-dir <git-dir>] [--object-format=<format>]
	  [-b <branch-name> | --initial-branch=<branch-name>]
	  [--shared[=<permissions>]] [<directory>]
```

##### c) Option

[git init](https://git-scm.com/docs/git-init#_options)

##### d) Useful full commands

`<something_something>` is the content to be filled.

- Create a new folder for a new repo
```
mkdir <new_repo_name>
cd <new_repo_name>
```

- Create a new bare repository (`already in folder of repository`)
```
git init --bare
```

- Create a new `local` repository with initial commit (`already in folder of repository`)
```
git init
echo # New Repo > README.md
git add README.md
git commit -m "Initial commit"
```

- Create a new `local + remote` repository with initial commit (`already in folder of repository`, `already logged in Github`) **(Recommend)**
```
git init
echo # New Repo > README.md
git add README.md
git commit -m "Initial commit"
git push -u origin master
```



#### 4.1.2 git clone







## Reference
- https://git-scm.com/docs
- https://ndpsoftware.com/git-cheatsheet.html
- https://backlog.com/git-tutorial/vn/intro/intro1_2.html
- 