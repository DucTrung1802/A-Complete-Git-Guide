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
- **`working tree`**: The current state of your project on local machine, may contains `committed files and uncommitted files` or `committed files` only.
- **`stash`**: a temporary local **`snapshot`** of the **`working tree`**, used to save the current state of the **`working tree`** while you work on another branch.

## 4. Git Commands

### 4.1 Getting and Creating Projects

#### 4.1.1 git init

##### a) Function

- Create an empty Git repository or reinitialize an existing one.

##### b) Syntax

```bash
git init [-q | --quiet] [--bare] [--template=<template-directory>]
	  [--separate-git-dir <git-dir>] [--object-format=<format>]
	  [-b <branch-name> | --initial-branch=<branch-name>]
	  [--shared[=<permissions>]] [<directory>]
```

##### c) Option

[git init](https://git-scm.com/docs/git-init#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Create a new folder for a new repo
```bash
mkdir <REPO_NAME>
cd <REPO_NAME>
```

- Create a new `local + remote` repository with initial commit (`already in folder of repository`)

**Make sure you already initialized a remote repo with name <REPO_NAME> on Github.**

```bash
git init
echo # New Repo > README.md
git add README.md
git commit -m "Initial commit"
git branch -M main
```
```bash
git remote add origin https://github.com/<GIT_USERNAME>/<REPO_NAME>.git
```
```bash
git push -u origin main
```

---

#### 4.1.2 git clone

##### a) Function

- Clone a repository into a new directory.

![](Images/git%20clone.png)


##### b) Syntax

```bash
git clone [--template=<template-directory>]
	  [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
	  [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
	  [--dissociate] [--separate-git-dir <git-dir>]
	  [--depth <depth>] [--[no-]single-branch] [--no-tags]
	  [--recurse-submodules[=<pathspec>]] [--[no-]shallow-submodules]
	  [--[no-]remote-submodules] [--jobs <n>] [--sparse] [--[no-]reject-shallow]
	  [--filter=<filter> [--also-filter-submodules]] [--] <repository>
	  [<directory>]
```

##### c) Option

[git clone](https://git-scm.com/docs/git-clone#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Copy a local repo to current folder.
```bash
git clone <LOCAL_REPO_PATH>
```

- Copy a local repo to a cetain folder.
```bash
git clone <LOCAL_REPO_PATH> <DESTINATION_FOLDER_PATH>
```

- Copy a remote repo to current folder (ssh method)
```bash
git clone <USER>@<HOST>:<PATH_TO_REPO>.git
```

- Copy a remote repo to current folder (https method)
```bash
git clone <URL_REPO>
```

---

### 4.2 Basic Snapshotting

#### 4.2.1 git add

##### a) Function

- Add file contents to the **`index`**.

![](Images/git%20add.png)

##### b) Syntax

```bash
git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p]
	  [--edit | -e] [--[no-]all | --[no-]ignore-removal | [--update | -u]] [--sparse]
	  [--intent-to-add | -N] [--refresh] [--ignore-errors] [--ignore-missing] [--renormalize]
	  [--chmod=(+|-)x] [--pathspec-from-file=<file> [--pathspec-file-nul]]
	  [--] [<pathspec>…​]
```

##### c) Option

[git add](https://git-scm.com/docs/git-add#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Add certain file(s) / folder(s) into **`index`**
```bash
git add <NAME_FILE_1> <NAME_FILE_2> <NAME_FOLDER_1> <NAME_FOLDER_2>
```

- Add all file in **`working tree`** into **`index`**
```bash
git add -all
```
or
```bash
git add -A
```

- Add all file in current folder into **`index`**
```bash
git add .
```

##### e) ATTENTION

- **`git add`** does not add file described in **`.gitignore`** !

---

#### 4.2.2 git status

##### a) Function

- Show the **`working tree`** status.

![](Images/git%20status.png)

##### b) Syntax

```bash
git status [<options>…​] [--] [<pathspec>…​]
```

##### c) Option

[git status](https://git-scm.com/docs/git-status#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Show the **`working tree`** status
```bash
git status
```

- Show the **`working tree`** status in simple form
```bash
git status -s
```

- Output for short format
> [X][Y] PATH
> 
> [X][Y] ORIGINAL_PATH -> PATH

Explain:
[X]: The status of the **`index`**.
[Y]: The status of the **`working tree`**.

Example:
```bash
A  abcd.txt
```
&rarr; `abcd.txt` is added in **`index`** and unmodified in **`working tree`**.
```bash
AD  abcd.txt
```
&rarr; `abcd.txt` is added in **`index`** and deleted in **`working tree`**.

- Table of [X] or [Y]

| Arbitrary | Description |
| :---: | ----------- |
| " " | Unmodified |
| M | modified |
| T | File type changed |
| A | Added |
| D | Delete |
| R | Renamed |
| C | Copied |
| U | Updated but unmerged |

---

#### 4.2.3 git diff

##### a) Function
- Show changes between commits, commit and **`working tree`**, etc

![](Images/git%20diff.png)

##### b) Syntax
```bash
git diff [<options>] [<commit>] [--] [<path>…​]
git diff [<options>] --cached [--merge-base] [<commit>] [--] [<path>…​]
git diff [<options>] [--merge-base] <commit> [<commit>…​] <commit> [--] [<path>…​]
git diff [<options>] <commit>…​<commit> [--] [<path>…​]
git diff [<options>] <blob> <blob>
git diff [<options>] --no-index [--] <path> <path>
```

##### c) Option

[git diff](https://git-scm.com/docs/git-diff#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Show differences of EXISTING files between **`working tree`** and **`index`**.
```bash
git diff
```

- Show differences of staged files between **`index`** and last commit of current branch.
```bash
git diff --cached
```

- Show differences of staged files between **`index`**, tracking files (modificated files) in **`working tree`** and last commit of current branch.
```bash
git diff head
```

- Show differences of staged files between **`index`**, modificated files in **`working tree`** and last commit of <BRANCH_NAME> branch.
```bash
git diff <BRANCH_NAME>
```

- Show differences between hashed commit 1 and hashed commit 2.
```bash
git diff <HASHED_COMMIT_1> <HASHED_COMMIT_2>
```
Example:
> git diff 981f4e 79c9bf

- Show differences between branch 2 and branch 1.
```bash
git diff <BRANCH_1_NAME> <BRANCH_2_NAME>
```

---

#### 4.2.4 git commit

##### a) Function

- Record changes to the repository.

![](Images/git%20commit.png)

##### b) Syntax
```bash
git commit [-a | --interactive | --patch] [-s] [-v] [-u<mode>] [--amend]
	   [--dry-run] [(-c | -C | --squash) <commit> | --fixup [(amend|reword):]<commit>)]
	   [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
	   [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
	   [--date=<date>] [--cleanup=<mode>] [--[no-]status]
	   [-i | -o] [--pathspec-from-file=<file> [--pathspec-file-nul]]
	   [(--trailer <token>[(=|:)<value>])…​] [-S[<keyid>]]
	   [--] [<pathspec>…​]
```

##### c) Option

[git commit](https://git-scm.com/docs/git-commit#_options)

##### d) Useful commands

- Create a new commit with all changes in **`index`**.
```bash
git commit -m <COMMENT_OF_THIS_COMMIT>
```

- Create a new commit with all changes in **`index`** and tracking files (modificated files) in **`working tree`**.
```bash
git commit -a -m <COMMENT_OF_THIS_COMMIT>
```

- Change comment of the last UNPUSHED commit.
```bash
git commit --amend -m <COMMENT_OF_THIS_COMMIT>
```

---

#### 4.2.5 git reset

##### a) Function

- Reset current HEAD to the specified state

![](Images/git%20reset.png)

##### b) Syntax
```bash
git reset [-q] [<tree-ish>] [--] <pathspec>…​
git reset [-q] [--pathspec-from-file=<file> [--pathspec-file-nul]] [<tree-ish>]
git reset (--patch | -p) [<tree-ish>] [--] [<pathspec>…​]
git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]
```

##### c) Option

[git reset](https://git-scm.com/docs/git-reset#_options)

##### d) Useful commands

- Reset all files in **`index`** back to **`working tree`** (inverse of **`git add`**).
```bash
git reset
```

- Reset a certain file in **`index`** back to **`working tree`**.
```bash
git reset <FILE_NAME_1> <FILE_NAME_2>
```

- Reset to a commit and `does not touch the index file or the working tree at all`.
```bash
git reset --soft <HASHED_COMMIT>
```
Example:
> git reset --soft bd33c1


- Reset to a commit and **`reset the index but not the working tree`**.
```bash
git reset <HASHED_COMMIT>
```
or
```bash
git reset --mixed <HASHED_COMMIT>
```

- Reset to a commit and **`reset the index and working tree`**.
```bash
git reset --hard <HASHED_COMMIT>
```

---

#### 4.2.6 git mv

##### a) Function

- Move or rename a file, a directory, or a symlink.

##### b) Syntax
```bash
git mv [-v] [-f] [-n] [-k] <source> <destination>
git mv [-v] [-f] [-n] [-k] <source> ... <destination directory>
```

##### c) Option

[git mv](https://git-scm.com/docs/git-mv#_options)


##### d) Useful commands

- Rename file
```bash
git mv <OLD_FILE_NAME> <NEW_FILE_NAME>
```

- Move file
```bash
git mv <FILE_NAME> <FOLDER_NAME>
```






#### x.x.x git bla bla

##### a) Function


##### b) Syntax


##### c) Option

[git reset](https://git-scm.com/docs/git-reset#_options)

##### d) Useful commands






## Reference
- https://git-scm.com/docs
- https://ndpsoftware.com/git-cheatsheet.html
- https://backlog.com/git-tutorial/vn/intro/intro1_2.html
- https://ndpsoftware.com/git-cheatsheet.html#loc=index