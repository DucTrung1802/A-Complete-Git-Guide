# A Complete Git Guide

## Link to headers

#### [4.1 Getting and Creating Projects](#41-getting-and-creating-projects)
##### [4.1.1 git init](#411-git-init)
##### [4.1.2 git clone](#412-git-clone)

#### [4.2 Basic Snapshotting](#42-basic-snapshotting)
##### [4.2.1 git add](#421-git-add)
##### [4.2.2 git status](#422-git-status)
##### [4.2.3 git commit](#423-git-commit)
##### [4.2.4 git reset](#424-git-reset)
##### [4.2.5 git mv](#425-git-mv)

#### [4.3 Branching and Merging](#43-branching-and-merging)
##### [4.3.1 git branch](#431-git-branch)
##### [4.3.2 git checkout](#432-git-checkout)
##### [4.3.3 git merge](#433-git-merge)
##### [4.3.4 git stash](#434-git-stash)

#### [4.4 Sharing and Updating Projects](#44-sharing-and-updating-projects)
##### [4.4.1 git fetch](#441-git-fetch)
##### [4.4.2 git pull](#442-git-pull)
##### [4.4.3 git push](#443-git-push)

#### [4.5 Inspection and Comparison](#45-inspection-and-comparison)
##### [4.5.1 git show](#451-git-show)
##### [4.5.2 git log](#452-git-log)
##### [4.5.3 git diff](#453-git-diff)

#### [4.6 Patching](#46-patching)
##### [4.6.1 git cherry-pick](#461-git-cherry-pick)
##### [4.6.2 git rebase](#462-git-rebase)

#### [5. Undo changes in Git](#5-undo-changes-in-git)
##### [5.1 Undoing local changes that have not been committed](#51-undoing-local-changes-that-have-not-been-committed)
##### [5.2 Undoing local changes that have been committed (BUT NOT PUSHED)](#52-undoing-local-changes-that-have-been-committed-but-not-pushed)
##### [5.3 Undoing a specific sommit (THAT HAS BEEN PUSHED)](#53-undoing-a-specific-sommit-that-has-been-pushed)


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

- Add specific file(s) / folder(s) into **`index`**
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

#### 4.2.3 git commit

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

#### 4.2.4 git reset

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

- Reset a specific file in **`index`** back to **`working tree`**.
```bash
git reset <FILE_NAME_1> <FILE_NAME_2>
```

- Reset to a commit and `does not touch the index file or the working tree at all`.
```bash
git reset --soft <HASH_COMMIT>
```
Example:
> git reset --soft bd33c1


- Reset to a commit and **`reset the index but not the working tree`**.
```bash
git reset <HASH_COMMIT>
```
or
```bash
git reset --mixed <HASH_COMMIT>
```

- Reset to a commit and **`reset the index and working tree`**.
```bash
git reset --hard <HASH_COMMIT>
```

---

#### 4.2.5 git mv

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

- Restore a file in <HASH_COMMIT>. Changes will be shown in **`index`**.
```bash
git checkout <HASH_COMMIT> <FILE_NAME>
```

- Checkout a commit.

Show log in simple form to see all <HASH_COMMIT>.
```bash
git log --oneline
```

Checkout a commit.
```bash
git checkout <HASH_COMMIT>
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

#### 4.3.4 git stash

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

Output:
> stash@{0}: On feature_1: comment of feature 1 branch
> stash@{1}: On feature_2: comment of feature 2 branch
> stash@{2}: On main: comment of main branch

- Retrieve old work of `current` branch and **`REMOVE`** the stashed state (the top stash in the stash list).
```bash
git stash pop # ~ git stash pop stash@{0}
```

- Retrieve old work of `a specific` branch and **`REMOVE`** the stashed state (the top stash in the stash list).
```bash
git stash pop stash@{<ORDER_OF_STASH>}
```

- Retrieve old work of `current` branch and **`DO NOT REMOVE`**  the stashed state.
```bash
git stash apply
```

- Retrieve old work of `a specific` branch and **`DO NOT REMOVE`**  the stashed state.
```bash
git stash apply stash@{<ORDER_OF_STASH>}
```

- Show brief change of newest stash.
```bash
git stash show # ~ git stash show stash@{0} 
```

- Show detail change of newest stash.
```bash
git stash show -p # ~ git stash show -p stash@{0} 
```

- Show brief change of `a specific` branch and **`DO NOT REMOVE`**  the stashed state.
```bash
git stash show stash@{<ORDER_OF_STASH>}
```

- Create a new branch with the changes of last stash.
```bash
git stash branch <NAME_OF_NEW_BRANCH> # ~ git stash branch <NAME_OF_NEW_BRANCH> stash@{0}
```

- Create a new branch with the changes of a specific stash.
```bash
git stash branch <NAME_OF_NEW_BRANCH> stash@{<ORDER_OF_STASH>}
```

- ⚠️ **DELETE THE LAST STASH (DANGEROUS - CANNOT RESTORE)**. 
```bash
git stash drop # ~ git stash drop stash@{0}
```

- ⚠️ **DELETE A SPECIFIC STASH (DANGEROUS - CANNOT RESTORE).**
```bash
git stash drop stash@{<ORDER_OF_STASH>}
```

- ⚠️ **DELETE ALL STASHSES (DANGEROUS - CANNOT RESTORE).**
```bash
git stash clear
```

---

### 4.4 Sharing and Updating Projects

#### 4.4.1 git fetch

##### a) Function

- Download objects and refs from **`remote branch`** to **`remote-tracking reference`** (Update **`remote-tracking reference`** to the newest state of **`remote branch`** without changing **`local branch`**).

![](Images/git%20fetch.png)

##### b) Syntax
```bash
git fetch [<options>] [<repository> [<refspec>…​]]
git fetch [<options>] <group>
git fetch --multiple [<options>] [(<repository> | <group>)…​]
git fetch --all [<options>]
```

##### c) Options

[git fetch](https://git-scm.com/docs/git-fetch#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Download all objects and refs of all branches.
```bash
git fetch origin
```

```bash
git fetch --all
```

- Download all objects and refs of a specific branch.
```bash
git fetch origin <NAME_OF_BRANCH>
```

---

#### 4.4.2 git pull

##### a) Function

- Fetch from and integrate with another repository or a local branch.

![](Images/git%20pull.png) 

##### b) Syntax
```bash
git pull [<options>] [<repository> [<refspec>…​]]
```

##### c) Options

[git pull](https://git-scm.com/docs/git-pull#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Update current **`working tree`** and **`local branch`** from corresponding **`remote branch`**. ATTENTION: **`working tree`** and **`index`** must be the same!
```bash
git pull
```

---

#### 4.4.3 git push

##### a) Function

- Update **`remote branch`** using **`local branch`**.

![](Images/git%20push.png)


##### b) Syntax
```bash
git push [--all | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>]
	   [--repo=<repository>] [-f | --force] [-d | --delete] [--prune] [-v | --verbose]
	   [-u | --set-upstream] [-o <string> | --push-option=<string>]
	   [--[no-]signed|--signed=(true|false|if-asked)]
	   [--force-with-lease[=<refname>[:<expect>]] [--force-if-includes]]
	   [--no-verify] [<repository> [<refspec>…​]]
```

##### c) Options

[git push](https://git-scm.com/docs/git-push#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Push current **`local branch`** to **`remote branch`** **FOR THE FIRST TIME**.
```bash
git push -u origin <NAME_OF_BRANCH>
```

- Push current **`local branch`** to **`remote branch`**.
```bash
git push
```

- Push a specific **`local branch`** to its **`remote branch`**.
```bash
git push origin <NAME_OF_BRANCH>
```

- Push all **`local branch`** to **`remote branch`**.
```bash
git push origin --all
```

- Delete a specific **`remote branch`**.
```bash
git push origin --delete <NAME_OF_BRANCH>
```

- Double check all **`remote branch`**.
```bash
git branch -a
```

- ⚠️ Overwrite current **`remote branch`** with current **`local branch`** **(DANGEROUS - CANNOT RESTORE)**.
```bash
git push -f 
```

- ⚠️ Overwrite corresponding **`remote branch`** with a specific **`local branch`** **(DANGEROUS - CANNOT RESTORE)**. 
```bash
git push -f <NAME_OF_BRANCH>
```

--- 

### 4.5 Inspection and Comparison

#### 4.5.1 git show

##### a) Function

- Show various types of objects.

##### b) Syntax
```bash
git show [<options>] [<object>…​]
```

##### c) Options

[git show](https://git-scm.com/docs/git-show#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Show detail of current checkout commit.
```bash
git show
```

- Show detail of a specific commit.
```bash
git show <HASH_COMMIT>
```

Example:
> git show 99b0f3

- Show customized detail of commit.
```bash
git show <HASH_COMMIT> --pretty=<TYPE_OF_FORMAT>
```

- Table type of format

| TYPE OF FORMAT |
| :---: |
| "oneline" |
| "short" |
| "medium" |
| "full" |
| "fuller" |
| "email" |

-  Actions in a **`git show`** command.

| Key | Description |
| :---: | ----------- |
| [Up arrow] | Previous line |
| [Down arrow] | Next line |
| q | Quit |

--- 

#### 4.5.2 git log

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

- Show a specific amount of logs.
```bash
git log -<NUMBER_OF_LOG>
```
Example:
```bash
git log -2
```

- Show changes of a specific amount of logs in detail.
```bash
git log -p -<NUMBER_OF_LOG>
```
Example:
```bash
git log -p -2
```

- Show changes of a specific amount of logs in brief.
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

#### 4.5.3 git diff

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

- Show differences between HASH commit 1 and HASH commit 2.
```bash
git diff <HASH_COMMIT_1> <HASH_COMMIT_2>
```
Example:
> git diff 981f4e 79c9bf

- Show differences between branch 2 and branch 1.
```bash
git diff <BRANCH_1_NAME> <BRANCH_2_NAME>
```

---

### 4.6 Patching

#### 4.6.1 git cherry-pick

##### a) Function

- Apply the changes introduced by some existing commits.

##### b) Syntax
```bash
git cherry-pick [--edit] [-n] [-m <parent-number>] [-s] [-x] [--ff]
		  [-S[<keyid>]] <commit>…​
git cherry-pick (--continue | --skip | --abort | --quit)
```

##### c) Options

[git cherry-pick](https://git-scm.com/docs/git-cherry-pick#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Append a single commit from branch A to branch main.
```bash
git checkout main
git cherry-pick <HASH_COMMIT_OF_BRANCH_A>
```

Example:
Append commit `f9b494h` of branch A to branch main.
> git checkout main
> git cherry-pick f9b494h

- Append multiple, **not continuous** commits from branch A to branch main.
```bash
git checkout main
git cherry-pick <HASH_COMMIT_OF_BRANCH_A> <ANOTHER_HASH_COMMIT_OF_BRANCH_A>
```

Example:
Append continuous commits `9nzx9du`, `46yn0hw`, `1rmbtd1`, `tnps7pn` of branch A to branch main.
> git checkout main
> git cherry-pick 9nzx9du 46yn0hw 1rmbtd1 tnps7pn

- Append multiple, **continuous** commits from branch A to branch main.
```bash
git checkout main
git cherry-pick <START_CHAIN_HASH_COMMIT_BRANCH_A>^..<END_CHAIN_HASH_COMMIT_BRANCH_A>
```

Example:
Append continuous commits `f9b494h`, `dj2389r`, `3jkfe9s`, `sdu3oi2` of branch A to branch main.
> git checkout main
> git cherry-pick f9b494h^..sdu3oi2

- One commit for 2 branches.
```bash
# Current in branch X, create a new commit
git add file_X
git commit -m " new commit branch X"

# Checkout branch Y and use git cherry-pick
git checkout branch_Y
git cherry-pick branch_X
```

---

#### 4.6.2 git rebase

##### a) Function

- Reapply commits on top of another base tip

![](Images/git%20rebase.png)

##### b) Syntax
```bash
git rebase [-i | --interactive] [<options>] [--exec <cmd>]
	[--onto <newbase> | --keep-base] [<upstream> [<branch>]]
git rebase [-i | --interactive] [<options>] [--exec <cmd>] [--onto <newbase>]
	--root [<branch>]
git rebase (--continue | --skip | --abort | --quit | --edit-todo | --show-current-patch)
```

##### c) Options

[git rebase](https://git-scm.com/docs/git-rebase#_options)

##### d) Useful commands

`<SOMETHING_SOMETHING>` is the content to be filled.

- Rebase branch B on branch A (branch A is base of branch B).
```bash
git checkout <BRANCH_B>
git rebase <BRANCH_A>
```

- Interactively rebase branch B on branch A (branch A is base of branch B).
```bash
git checkout <BRANCH_B>
git rebase --interactive <BRANCH_A>
```
A text editor will be opened along with detail instruction and a list of commits. 

---

### 5. Undo changes in Git

Sometimes you make a mistake and want to go back to a previous version. Here's how to rollback changes.


#### 5.1 Undoing local changes that have not been committed

- Check status.
```bash
git status
```

- Undo change for specific `modified` and `deleted` files.
```bash
git restore <FILE_A> <FILE_B> 
```

- Undo change for all `modified` and `deleted` files.
```bash
git restore .
```

- Undo change for `completely new` (untracked) files.
```bash
git clean -f <FILE_A> <FILE_B>
```

- Undo change all `completely new` (untracked) files.
```bash
git clean -f .
```

#### 5.2 Undoing local changes that have been committed (BUT NOT PUSHED)

- Check status.
```bash
git status
```

- Check hash commits.
```bash
git log --oneline
```

Each commit has a unique hash (which looks something like `2f5451f`). You need to find the hash for the last good commit (the one you want to revert back to).


- Revert to a commit and `does not touch the index file or the working tree at all` (replacing `2f5451f` with your commit's hash).
```bash
git reset --soft 2f5451f
```


- Revert to a commit and **`reset the index but not the working tree`** (replacing `2f5451f` with your commit's hash).
```bash
git reset 2f5451f
```
or
```bash
git reset --mixed 2f5451f
```

- Revert to a commit and **`reset the index and working tree`** (replacing `2f5451f` with your commit's hash).
```bash
git reset --hard 2f5451f
```

#### 5.3 Undoing a specific sommit (THAT HAS BEEN PUSHED)

- Check status.
```bash
git status
```

- Check hash commits.
```bash
git log --oneline
```

- Revert with default comment (Revert <old_comment>) (replacing `2f5451f` with your commit's hash)
```bash
git revert 2f5451f --no-edit
```

- Revert with editing comment (replacing `2f5451f` with your commit's hash)
```bash
git revert 2f5451f
```

## Reference
- https://git-scm.com/docs
- https://ndpsoftware.com/git-cheatsheet.html
- https://backlog.com/git-tutorial/vn/intro/intro1_2.html
- https://ndpsoftware.com/git-cheatsheet.html#loc=index
- https://xuanthulab.net/git-va-github/