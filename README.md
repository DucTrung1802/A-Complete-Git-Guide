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

##### c) Options

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

##### c) Options

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

##### c) Options

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

##### c) Options

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

##### c) Options

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

##### c) Options

[git commit](https://git-scm.com/docs/git-commit#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

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

##### c) Options

[git reset](https://git-scm.com/docs/git-reset#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

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

##### c) Options

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

---

### 4.3 Branching and Merging

#### 4.3.1 git branch

##### a) Function

- List, create, or delete branches.
  
![](Images/git%20branch.png)

##### b) Syntax
```bash
git branch [--color[=<when>] | --no-color] [--show-current]
	[-v [--abbrev=<n> | --no-abbrev]]
	[--column[=<options>] | --no-column] [--sort=<key>]
	[--merged [<commit>]] [--no-merged [<commit>]]
	[--contains [<commit>]] [--no-contains [<commit>]]
	[--points-at <object>] [--format=<format>]
	[(-r | --remotes) | (-a | --all)]
	[--list] [<pattern>…​]
git branch [--track[=(direct|inherit)] | --no-track] [-f]
	[--recurse-submodules] <branchname> [<start-point>]
git branch (--set-upstream-to=<upstream> | -u <upstream>) [<branchname>]
git branch --unset-upstream [<branchname>]
git branch (-m | -M) [<oldbranch>] <newbranch>
git branch (-c | -C) [<oldbranch>] <newbranch>
git branch (-d | -D) [-r] <branchname>…​
git branch --edit-description [<branchname>]
```

##### c) Options

[git branch](https://git-scm.com/docs/git-branch#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Show current branches.
```bash
git branch
```

- Check out a branch.
```bash
git checkout <NAME_OF_EXISTING_BRANCH>
```

- Create a new local branch.
```bash
git branch <NEW_BRANCH_NAME>
```

- Create a new local + remote branch
```bash
git branch <NEW_BRANCH_NAME>
git push --set-upstream origin <NEW_BRANCH_NAME>
```

- Rename a branch on local + remote
```bash
git branch -m <OLD_BRANCH_NAME> <NEW_BRANCH_NAME>
git push origin HEAD
git push origin -d <OLD_BRANCH_NAME>
```

- Delete a branch

Checkout another branch before delete a branch !

```bash
git checkout <ANOTHER_BRANCH_NAME>
git branch -d <WANT_TO_DELETE_BRANCH_NAME>
git push origin -d <WANT_TO_DELETE_BRANCH_NAME>
```

---

#### 4.3.2 git checkout

##### a) Function

- Switch branches or restore working tree files.

![](Images/git%20checkout.png)

##### b) Syntax
```bash
git checkout [-q] [-f] [-m] [<branch>]
git checkout [-q] [-f] [-m] --detach [<branch>]
git checkout [-q] [-f] [-m] [--detach] <commit>
git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new-branch>] [<start-point>]
git checkout [-f|--ours|--theirs|-m|--conflict=<style>] [<tree-ish>] [--] <pathspec>…​
git checkout [-f|--ours|--theirs|-m|--conflict=<style>] [<tree-ish>] --pathspec-from-file=<file> [--pathspec-file-nul]
git checkout (-p|--patch) [<tree-ish>] [--] [<pathspec>…​]
```

##### c) Options

[git checkout](https://git-scm.com/docs/git-checkout#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Change branch.
```bash
git checkout <EXISTING_BRANCH_NAME>
```

- Restore a file in <HASHED_COMMIT>. Changes will be shown in **`index`**.
```bash
git checkout <HASHED_COMMIT> <FILE_NAME>
```

- Checkout a commit.

Show log in simple form to see all <HASHED_COMMIT>.
```bash
git log --oneline
```

Checkout a commit.
```bash
git checkout <HASHED_COMMIT>
```

Example
```bash
git checkout 981f4e7
```

Use `git checkout <EXISTING_BRANCH_NAME>` to return to a branch.

---

#### 4.3.3 git merge

##### a) Function

- Join two or more development histories together.

##### b) Syntax
```bash
git merge [-n] [--stat] [--no-commit] [--squash] [--[no-]edit]
	[--no-verify] [-s <strategy>] [-X <strategy-option>] [-S[<keyid>]]
	[--[no-]allow-unrelated-histories]
	[--[no-]rerere-autoupdate] [-m <msg>] [-F <file>]
	[--into-name <branch>] [<commit>…​]
git merge (--continue | --abort | --quit)
```

##### c) Options

[git merge](https://git-scm.com/docs/git-merge#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Merge `branch A` &rarr; `branch B`.
```bash
git checkout <BRANCH_B>
git merge <BRANCH_A>
git push
```

![](Images/git%20merge.png)

- Squash then Merge `branch A` &rarr; `branch B`.
```bash
git checkout <BRANCH_B>
git merge --squash <BRANCH_A>
git commit -m "<MESSAGE_OF_SQUASH_MERGE_COMMIT>"
git push
```
![](Images/git%20merge%20--squash.png)

---

#### 4.3.4 git log

##### a) Function

- Show commit logs.

##### b) Syntax
```bash
git log [<options>] [<revision-range>] [[--] <path>…​]
```

##### c) Options

[git log](https://git-scm.com/docs/git-log#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Show detail commit logs of current branch.
```bash
git log
```

Action with `git log`:

| Key | Description |
| :---: | ----------- |
| [ENTER] | Next line |
| w | Next page |
| [Spacebar] | Previous page |
| q | Quit |
| ?`keyword` | Find all commits containing `keyword` |
| n | Go to previous search result  |
| N | Go to next search result |

- Show a certain amount of logs.
```bash
git log -<NUMBER_OF_LOG>
```
Example:
```bash
git log -2
```

- Show changes of a certain amount of logs in detail.
```bash
git log -p -<NUMBER_OF_LOG>
```
Example:
```bash
git log -p -2
```

- Show changes of a certain amount of logs in brief.
```bash
git log --stat -<NUMBER_OF_LOG>
```
Example:
```bash
git log --stat -2
```

- Show logs in a line.
```bash
git log --oneline
```
Example:
```bash
git log --stat --oneline -10
```

- Filter logs by date
```bash
git log --after="<YEAR>-<MONTH>-<DAY>" --before="<YEAR>-<MONTH>-<DAY>"
```
Example: Filter logs in 2019.
```bash
git log --after="2019-1-1" --before="2019-12-31"
```

- Filter logs by author
```bash
git log --oneline --author="<NAME_OF_AUTHOR>"
```
Example:
```bash
git log --oneline --author="trungld11"
```

- Filter logs by merging commits.
```bash
git log --merges
```

- Filter logs by non-merging commits.
```bash
git log --no-merges
```

---

#### 4.3.5 git stash

##### a) Function

- Save the current state of **`working tree`** and **`index`** to a temporary commit to switch to another branch / task.

![](Images/git%20stash.png)

##### b) Syntax
```bash
git stash list [<log-options>]
git stash show [-u|--include-untracked|--only-untracked] [<diff-options>] [<stash>]
git stash drop [-q|--quiet] [<stash>]
git stash ( pop | apply ) [--index] [-q|--quiet] [<stash>]
git stash branch <branchname> [<stash>]
git stash [push [-p|--patch] [-S|--staged] [-k|--[no-]keep-index] [-q|--quiet]
	     [-u|--include-untracked] [-a|--all] [-m|--message <message>]
	     [--pathspec-from-file=<file> [--pathspec-file-nul]]
	     [--] [<pathspec>…​]]
git stash clear
git stash create [<message>]
git stash store [-m|--message <message>] [-q|--quiet] <commit>
```

##### c) Options

[git stash](https://git-scm.com/docs/git-stash#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

**`STASH = SAVE CURRENT WORKING TREE + INDEX`**

- Standard stash for current branch.
```bash
git stash save -a -m "<COMMENT_OF_COMMIT>"
```

- List all current stashes.
```bash
git stash list
```

- Pop stash of current branch (retreive old work).
```bash
git stash pop
```

- 











---


#### x.x.x git bla bla

##### a) Function


##### b) Syntax


##### c) Options

[git reset](https://git-scm.com/docs/git-reset#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.


## Reference
- https://git-scm.com/docs
- https://ndpsoftware.com/git-cheatsheet.html
- https://backlog.com/git-tutorial/vn/intro/intro1_2.html
- https://ndpsoftware.com/git-cheatsheet.html#loc=index