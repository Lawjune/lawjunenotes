# Getting Started

## Installing Git

git-scm.com

```sh
git --version
```
## Configure Git

**SETTING**
- Name
- Email
- Default Editor
- Line Ending

**LEVELS**
- **SYSTEM** -> All users
- **GLOBAL** -> All repositories of the current user
- **LOCAL**  -> The current repository

```sh
git config --global user.name "Jun Luo"
git config --global user.email lawjune@163.com
```

VS Code -> Shell Command: Install ‘code’ command in PATH
```sh
git config --global core.editor "code --wait"
git config --global -e
```

**End of line:**
- WINDOWS: abc\r\n
	- \r: Carriage Return
	- \n: Line Feed
- macOS / Linux: abc\n
	- **ONLY** end with Line Feed.

To prevent the messup of EOL processing cross-platform


WINDOWS
```sh
git config --global core.autocrlf true 
```

macOS / Linux
```sh
git config --global core.autocrlf input 
```

## Getting Help

Google "git config"

```sh
git config --help
```

```sh
git config -h
```

## Cheat Sheet


# Creating Snapshots

## Intializing a Respository

```sh
mkdir ~/Projects/Moon
cd ~/Projects/Moon
```

```sh
git init
```
=> Initialized empty Git repository in /Users/mac/Projects/Moon/.git/
-> Check with ls -a

```sh
open .git
```
Access into the .git repository

**PLUG-IN TOOLS**
- Mac: Zsh with Git plugin
- Windows: posh-git

## Git Workflow

Project Repository -> **Index** -> Git Repository
			   (A hidden sub-repository)
			  (Or called **Staging Area**)

### Example

- Phase 1.0
	- Project Respository 
		- file1
		- file2
	- Staging Area
	- Git Repository

```sh
git add file1 file2
```
- Phase 1.1
	- Project Respository 
		- file1
		- file2
	- Staging Area
		- file1
		- file2
	- Git Repository


```sh
git commit -m "initial commit"
```
- Phase 1.2
	- Project Respository 
		- file1
		- file2
	- Staging Area
		- file1
		- file2
	- Git Repository
		- snapshot1
			- file1
			- file2

***Modified in file1 in working directory***
```sh
git add file1
```
- Phase 2.0
	- Project Respository 
		- (Modified)file1
		- file2
	- Staging Area
		- (Modified)file1
		- file2
	- Git Repository
		- snapshot1
			- file1
			- file2

```sh
git commit -m "Fixed the bug that..."
```
- Phase 2.1
	- Project Respository 
		- (Modified)file1
		- file2
	- Staging Area
		- (Modified)file1
		- file2
	- Git Repository
		- snapshot1
			- file1
			- file2
		- snapshot2
			- (Modified)file1
			- file2


***Deleted file2 in working directory***
```sh
git add file2
```
- Phase 3.0
	- Project Respository 
		- (Modified)file1
	- Staging Area
		- (Modified)file1
	- Git Repository
		- snapshot1
			- file1
			- file2
		- snapshot2
			- (Modified)file1
			- file2

```sh
git commit -m "Removed unused code"
```
- Phase 3.1
	- Project Respository 
		- (Modified)file1
	- Staging Area
		- (Modified)file1
	- Git Repository
		- snapshot1
			- file1
			- file2
		- snapshot2
			- (Modified)file1
			- file2
		- snapshot3
			- (Modified)file1

**COMMIT**
	- ID
	- Message
	- Date/time
	- Author
	- Complete snapshot

**GIT**
	- Compresses the content
	- Doesn't store duplicate content


### Staging Files

```sh
echo hello > file1.txt
echo hello > file2.txt
```

```sh
git status
```
```output
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
	file1.txt
	file2.txt

nothing added to commit but untracked files present (use "git add" to track)
```

```sh
git add file1.txt file2.txt
git add *.txt
git add .
```

Again
```sh
git status
```
```output 
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   file1.txt
	new file:   file2.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
```

Appen "world" under "hello"
```sh
echo world >> file1.txt 
```


Again
```sh
git status
```
```output 
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   file1.txt
	new file:   file2.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
```

```sh
git add file1.txt
```

Again
```sh
git status
```
```output 
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   file1.txt
	new file:   file2.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
```

### Committing Changes

```sh
git commit -m "Initial commit."
```
```output
[master (root-commit) 8b39523] Initial commit.
 2 files changed, 3 insertions(+)
 create mode 100644 file1.txt
 create mode 100644 file2.txt
```

=> **A very valuable constraints**
Just type
```sh
git commit
```
then edit the message in vs-code [COMMIT_EDITMSG]. 


### Committing Best Practices

**As you reach a state you want to record THEN make a commit**


### Skipping the Staging Area

** Do this when you 100% know what you are doing!**

```sh
echo test >> file1.txt
```

-a means all of the modified files
```sh
git commit -am "Fix the bug that preventd the users from signing up."
```
```output
[master ba9e95f] Fix the bug that preventd the users from signing up.
 1 file changed, 1 insertion(+)
```

**99% of the time you should stage your code before committing it.**


## Removing Files

```sh
rm file2.txt
```

```sh
git ls-files
```
```output
file1.txt
file2.txt
```

```sh
git add file2.txt
```

```sh
git ls-files
```
```output
file1.txt
```

```sh
git status
```
```output
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	deleted:    file2.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
```

```sh
git commit -m "Remove unused code."
```

Remove from both working directory and staging area
```sh
git rm file2.txt
```

## Renaming or Moving Files

```sh
mv file1.txt main.js
```

```sh
git status
``` 
```output
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    file1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
	main.js

no changes added to commit (use "git add" and/or "git commit -a")
```

```sh
git add file1.txt
git add main.js  
```

```sh
git status
```
```output
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    file1.txt -> main.js

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
```

**Faster method**

```sh
git mv main.js file1.js
git status
```
```output
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    file1.txt -> file1.js

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store

```

```sh
git commit -m "Refactor code."
```
```output
[master b0bf1bb] Refactor code.
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename file1.txt => file1.js (100%)
```

## Ignoring Files

```sh
mkdir logs
echo hello > logs/dev.log
```
```output
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
	logs/

nothing added to commit but untracked files present (use "git add" to track)
```

To avoid the "Untracked files:" statement

```sh
echo logs/ > .gitignore
```

Edit logs in .gitignore
```sh
code .gitignore
```
Then add included .log files in .gitignore

```gitignore
logs/
main.log
*.log
```

```sh
git add .gitignore
git commit -m "Add gitignore"
```
```output 
[master 1be63b3] Add gitignore
 1 file changed, 3 insertions(+)
 create mode 100644 .gitignore
```

### Remove Files in Statge Area

```sh
git rm -h
```
```sh
usage: git rm [<options>] [--] <file>...

    -n, --dry-run         dry run
    -q, --quiet           do not list removed files
    --cached              only remove from the index(old terms of stage)
    -f, --force           override the up-to-date check
    -r                    allow recursive removal
    --ignore-unmatch      exit with a zero status even if nothing matched
    --pathspec-from-file <file>
                          read pathspec from file
    --pathspec-file-nul   with --pathspec-from-file, pathspec elements are separated with NUL character
```

Reuse the useful template in https://github.com/github/gitignore 


## Short Status

Modify an existing file and create a new file
```sh
echo sky >> file1.js
echo sky > file2.js
git status
```
```sh
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file1.js

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
	file2.js
```

```sh
it status -s
```
```sh
 M file1.js
?? file2.js
```

The 1st column -> working directory
The 2nd column -> staging area


```sh
git status -s
```
```sh
M  file1.js
?? file2.js
```

```sh
git add file2.js 
git status -s
```
```sh
M  file1.js
A  file2.js
```


## Viewing the Stage & Unstatge Changes

### Changes in Stage ONLY
```sh
git diff --cached
```

### Changes in wWrking Directory(Unstage) OBLY
```sh
git diff
```


## Visual Differ Tools 

- KDIFF3
- P4Merge
- WinMerge (Windows ONLY)
- VSCode

```sh
git config --global diff.tool vscode
```

Launch the diff tool of vscode
```sh
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
```

Then check the configuration in the default editor
```sh
git config --global -e
```

Make sure everything right in .gitconfig
```sh
[diff]
	tool = vscode
[difftool "vscode"]
	cmd = "code --wait --diff $LOCAL $REMOTE"
```

Check the diff result
```sh
git difftool --staged
```


## Viewing the History

```sh
git log
```

```sh
git log --oneline
```

```sh
git log --oneline --reverse
```


## Viewing a Commit

```sh
git show
```

```sh
git show {ID}
```

```sh
git show HEAD~1
```

```sh
git show HEAD~1:bin/app.bin
```

```sh
git show HEAD~1:,gitignore
```

List the git objects where we can find the id
```sh
git ls-tree HEAD~1
```

**GIT OBJECTS**
- Commits
- Blobs (Files)
- Trees (Directories)
- Tags


## Unstaging Files

```sh
git status -s
```
```sh
MM file1.js
A  file2.js
```

```sh
git restore --staged file1.js 
```

```sh
git status -s                
```
```sh
 M file1.js
A  file2.js
```


```sh
git restore --staged file2.js
git status -s  
```
```sh              
M  .gitignore
 M file1.js
```


## Discarding Local Changes

Undo all of the local changes and copy the staged version to working directory

```sh
git restore .
```
=>
```sh
git status -s
```
```sh
?? file2.js
```

?? means the untrack files which would not be restored


To "clean" the untrack files
```sh
git clean -h
usage: git clean [-d] [-f] [-i] [-n] [-q] [-e <pattern>] [-x | -X] [--] <paths>...

    -q, --quiet           do not print names of files removed
    -n, --dry-run         dry run
    -f, --force           force
    -i, --interactive     interactive cleaning
    -d                    remove whole directories
    -e, --exclude <pattern>
                          add <pattern> to ignore rules
    -x                    remove ignored files, too
    -X                    remove only ignored files
```
=>
```sh
git clean -fd
```

## Restoring a File to an Earlier Version

Example: To remove a file and add it back from the earlier version snapshot

```sh
git rm file1.js 
```
=>
```sh
it status -s
```
```sh
D  file1.js
```

```sh
git commit -m "Delete file1.js"
```  

```sh
it log --oneline
```
```sh
90e0096 (HEAD -> master) Delete file1.js
1be63b3 Add gitignore
b0bf1bb Refactor code.
b43d300 Remove unused code.
ba9e95f Fix the bug that preventd the users from signing up.
8b39523 Initial commit.
```

```sh
git restore --source=HEAD~1 file1.js
```
=>
```sh
git status -s
```
```sh
?? file1.js
```


## Creating Snapshots Using VSCode

## Creating Snapshots Using GitKraken


# Brwosing History

## Introduction 

- Search for commits (by author, date, message, etc)
- View a commit
- Restore your project to an earlier point
- Compare commits
- View the history of a file
- Find a bad commit that introduced a bug

## Viewing the History

In .../Venus/ directory

```sh
git log
```

```sh
git log --oneline
```

```sh
git log --oneline --stat
```

## Filtering the History

Check the last commits
```sh
git log --oneline
```

Filter by author name
```sh
git log --oneline --author="Mosh"
```

Filter by date
```sh
git log --oneline --after="2020-08-17"
git log --oneline --after="yesterday"
git log --oneline --after="one week ago"
git log --oneline --after="one month ago"
git log --oneline --after="one year ago"
```

Filter by keywords in commit
```sh
git log --oneline --grep="GUI"
```

Filter by content
```sh
git log -S"OBJECTIVES"
```

Filter by content
```sh
git log -S"OBJECTIVES" --patch
```

Filter by the range of IDs
```sh
git log --oneline 
a642e12 (HEAD -> master) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives
```

```sh
git log --oneline dad47ed..91f7d40       
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
```

Filter by the modified file
```sh
it log --oneline toc.txt         
a642e12 (HEAD -> master) Add header to all pages.
50db987 Include the first section in TOC.
ca49180 Initial commit.
```

```sh
git log --oneline --patch -- toc.txt
```

## Formatting the Log Output
```sh
git log --pretty=format:"hello %an" 
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
hello Moshfegh Hamedani
```

```sh
git log --pretty=format:"%an committed %H" 
Moshfegh Hamedani committed a642e1229e3cb69be9bf075d9fe5e752e9a17458
Moshfegh Hamedani committed 50db98710ed4330773f1df55b2a177600d523c9e
Moshfegh Hamedani committed 555b62e1ebb92c97fc69910ad0981a7d6dbbf8c6
Moshfegh Hamedani committed 91f7d40d6d5bbc336a271607a0488216aaf50cd7
Moshfegh Hamedani committed edb3594bfa5572d81e24b33aa928938e46907275
Moshfegh Hamedani committed 24e86ee2f15e47a0d7b51032d2dc5b684b33465a
Moshfegh Hamedani committed 36cd6db402cfd897810d4cb33d97ac1e9d1ce2d8
Moshfegh Hamedani committed 9b6ebfdac0e8a775f17418a63f1153ee74078163
Moshfegh Hamedani committed fa1b75e8d342a4cb507c28d5417ae6a9111ba81a
Moshfegh Hamedani committed dad47edb45fb6912ecbb9034daca59f0491da1ab
Moshfegh Hamedani committed fb0d184c7e31cbb00eed45c98ba502e466b60152
Moshfegh Hamedani committed 1ebb7a701c4e86331cc64fada6ac1057fdf2dcde
Moshfegh Hamedani committed ca4918083ec471878d58612142572f3367faf5fd
```

```sh
git log --pretty=format:"%an committed %h"
Moshfegh Hamedani committed a642e12
Moshfegh Hamedani committed 50db987
Moshfegh Hamedani committed 555b62e
Moshfegh Hamedani committed 91f7d40
Moshfegh Hamedani committed edb3594
Moshfegh Hamedani committed 24e86ee
Moshfegh Hamedani committed 36cd6db
Moshfegh Hamedani committed 9b6ebfd
Moshfegh Hamedani committed fa1b75e
Moshfegh Hamedani committed dad47ed
Moshfegh Hamedani committed fb0d184
Moshfegh Hamedani committed 1ebb7a7
Moshfegh Hamedani committed ca49180
```

```sh
it log --pretty=format:"%an committed %h on %cd"
Moshfegh Hamedani committed a642e12 on Tue Aug 18 09:23:19 2020 -0700
Moshfegh Hamedani committed 50db987 on Mon Aug 17 14:27:50 2020 -0700
Moshfegh Hamedani committed 555b62e on Mon Aug 17 14:26:49 2020 -0700
Moshfegh Hamedani committed 91f7d40 on Mon Aug 17 14:25:43 2020 -0700
Moshfegh Hamedani committed edb3594 on Mon Aug 17 14:24:38 2020 -0700
Moshfegh Hamedani committed 24e86ee on Mon Aug 17 14:23:52 2020 -0700
Moshfegh Hamedani committed 36cd6db on Mon Aug 17 14:22:51 2020 -0700
Moshfegh Hamedani committed 9b6ebfd on Mon Aug 17 14:22:17 2020 -0700
Moshfegh Hamedani committed fa1b75e on Mon Aug 17 14:21:30 2020 -0700
Moshfegh Hamedani committed dad47ed on Mon Aug 17 14:20:50 2020 -0700
Moshfegh Hamedani committed fb0d184 on Mon Aug 17 14:18:09 2020 -0700
Moshfegh Hamedani committed 1ebb7a7 on Mon Aug 17 14:17:31 2020 -0700
Moshfegh Hamedani committed ca49180 on Mon Aug 17 14:17:15 2020 -0700
```

```sh
git log --pretty=format:"%Cred%an%Creset committed %h on %cd"
```

## Creating Aliases

```sh
git config --global alias.lg "log --pretty=format:'%an committed %h'"
git config -e 
git lg
Moshfegh Hamedani committed a642e12
Moshfegh Hamedani committed 50db987
Moshfegh Hamedani committed 555b62e
Moshfegh Hamedani committed 91f7d40
Moshfegh Hamedani committed edb3594
Moshfegh Hamedani committed 24e86ee
Moshfegh Hamedani committed 36cd6db
Moshfegh Hamedani committed 9b6ebfd
Moshfegh Hamedani committed fa1b75e
Moshfegh Hamedani committed dad47ed
Moshfegh Hamedani committed fb0d184
Moshfegh Hamedani committed 1ebb7a7
Moshfegh Hamedani committed ca49180
```

```sh
git config --global alias.unstage "restore --staged ." 
git unstage
```

## Viewing a Commit

```sh
git show HEAD~2
commit 555b62e1ebb92c97fc69910ad0981a7d6dbbf8c6
Author: Moshfegh Hamedani <moshfegh@live.com.au>
Date:   Mon Aug 17 14:26:49 2020 -0700

    Include the note about committing after staging the changes.

diff --git a/sections/creating-snapshots/staging-changes.txt b/sections/creating-snapshots/staging-changes.txt
index bddf7bd..506a158 100644
--- a/sections/creating-snapshots/staging-changes.txt
+++ b/sections/creating-snapshots/staging-changes.txt
@@ -7,3 +7,5 @@ To stage the changes, run:
 You can add multiple files separated by a space. 
 You can use a . to add all the files and subdirectories recursively.
 
+Once you stage the changes, you need to commit them to store the 
+proposed snapshot permanently. 
\ No newline at end of file
```

```sh
git show HEAD~2:sections/creating-snapshots/staging-changes.txt
STAGING CHANGES 
===============
To stage the changes, run:

> git add <filename>

You can add multiple files separated by a space. 
You can use a . to add all the files and subdirectories recursively.

Once you stage the changes, you need to commit them to store the 
proposed snapshot permanently.
```

```sh
git show HEAD~2 --name-only
commit 555b62e1ebb92c97fc69910ad0981a7d6dbbf8c6
Author: Moshfegh Hamedani <moshfegh@live.com.au>
Date:   Mon Aug 17 14:26:49 2020 -0700

    Include the note about committing after staging the changes.

sections/creating-snapshots/staging-changes.txt
```

```sh
it show HEAD~2 --name-status
commit 555b62e1ebb92c97fc69910ad0981a7d6dbbf8c6
Author: Moshfegh Hamedani <moshfegh@live.com.au>
Date:   Mon Aug 17 14:26:49 2020 -0700

    Include the note about committing after staging the changes.

M       sections/creating-snapshots/staging-changes.txt
```

## Viewing the Changes Across Commits

```sh
(base) madeMacBook-Pro% git diff HEAD~2 HEAD
diff --git a/audience.txt b/audience.txt
index 6b3f8f5..4cfef55 100644
--- a/audience.txt
+++ b/audience.txt
@@ -1,2 +1,4 @@
+AUDIENCE 
+
 This course is for anyone who wants to learn Git. 
-No prior experience is required.
+No prior experience is required.
\ No newline at end of file
diff --git a/objectives.txt b/objectives.txt
index d31b40a..c882718 100644
--- a/objectives.txt
+++ b/objectives.txt
@@ -1,3 +1,4 @@
+OBJECTIVES 
 
(base) madeMacBook-Pro% git diff HEAD~2 HEAD
diff --git a/audience.txt b/audience.txt
index 6b3f8f5..4cfef55 100644
--- a/audience.txt
+++ b/audience.txt
@@ -1,2 +1,4 @@
+AUDIENCE 
+
 This course is for anyone who wants to learn Git. 
-No prior experience is required.
+No prior experience is required.
\ No newline at end of file
diff --git a/objectives.txt b/objectives.txt
index d31b40a..c882718 100644
--- a/objectives.txt
+++ b/objectives.txt
@@ -1,3 +1,4 @@
+OBJECTIVES 
```

```sh
it diff HEAD~2 audience.txt
diff --git a/audience.txt b/audience.txt
index 6b3f8f5..4cfef55 100644
--- a/audience.txt
+++ b/audience.txt
@@ -1,2 +1,4 @@
+AUDIENCE 
+
 This course is for anyone who wants to learn Git. 
-No prior experience is required.
+No prior experience is required.
\ No newline at end of file

```

```sh
it diff HEAD~2 HEAD --name-only
audience.txt
objectives.txt
sections/creating-snapshots/init.txt
sections/creating-snapshots/staging-changes.txt
toc.txt
```

```sh
git diff HEAD~2 HEAD --name-status
M       audience.txt
M       objectives.txt
M       sections/creating-snapshots/init.txt
M       sections/creating-snapshots/staging-changes.txt
M       toc.txt
```

## Checking Out a Commit

```sh
git log --oneline
a642e12 (HEAD -> master) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```

```sh
git checkout dad47ed
Note: switching to 'dad47ed'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at dad47ed Write the first draft of initializing a repo.
```

```sh
git log --oneline   
dad47ed (HEAD) Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```

```sh
it log --oneline --all
a642e12 (master) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed (HEAD) Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```

```sh
it checkout master    
Previous HEAD position was dad47ed Write the first draft of initializing a repo.
Switched to branch 'master'
```

## Finding Bugs Using Bisect

```sh
git bisect start
git bisect bad 
```
=>
```sh
git log --oneline
a642e12 (HEAD -> master, refs/bisect/bad) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```
=>
```sh
git bisect good ca49180
Bisecting: 5 revisions left to test after this (roughly 3 steps)
[36cd6db402cfd897810d4cb33d97ac1e9d1ce2d8] Include the command prompt in code sample.
```
=>
```sh
git log --oneline      
36cd6db (HEAD) Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 (refs/bisect/good-ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```

```sh
it log --oneline --all
a642e12 (master, refs/bisect/bad) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db (HEAD) Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 (refs/bisect/good-ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```

The (HEAD) is in the middle as 36cd6db =>
Fetch the snapshot and run the automation testing on 36cd6db =>
If failed (bad commit) => bugs is within the commits before it (ca49180 ~ 24e86ee)
If success (good commit) => bugs is within the commits after it (edb3594 ~ a642e12)
=>
```sh
git bisect good        
Bisecting: 2 revisions left to test after this (roughly 2 steps)
[91f7d40d6d5bbc336a271607a0488216aaf50cd7] Explain various ways to stage changes.
```
=> 
```sh
git log --oneline --all
a642e12 (master, refs/bisect/bad) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 (HEAD) Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db (refs/bisect/good-36cd6db402cfd897810d4cb33d97ac1e9d1ce2d8) Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 (refs/bisect/good-ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```
=> *91f7d40 (HEAD) Explain various ways to stage changes.* is a good commit
```sh
git bisect good        
Bisecting: 0 revisions left to test after this (roughly 1 step)
[50db98710ed4330773f1df55b2a177600d523c9e] Include the first section in TOC.
```
=>
```sh
git log --oneline --all
a642e12 (master, refs/bisect/bad) Add header to all pages.
50db987 (HEAD) Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 (refs/bisect/good-91f7d40d6d5bbc336a271607a0488216aaf50cd7) Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db (refs/bisect/good-36cd6db402cfd897810d4cb33d97ac1e9d1ce2d8) Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 (refs/bisect/good-ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```
=> 
Then the bad commit should be *50db987 (HEAD) Include the first section in TOC.*
=>
```sh
git bisect bad         
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[555b62e1ebb92c97fc69910ad0981a7d6dbbf8c6] Include the note about committing after staging the changes.
```

```sh
it log --oneline --all
a642e12 (master) Add header to all pages.
50db987 (refs/bisect/bad) Include the first section in TOC.
555b62e (HEAD) Include the note about committing after staging the changes.
91f7d40 (refs/bisect/good-91f7d40d6d5bbc336a271607a0488216aaf50cd7) Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db (refs/bisect/good-36cd6db402cfd897810d4cb33d97ac1e9d1ce2d8) Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 (refs/bisect/good-ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```
=>
```sh
git bisect bad         
555b62e1ebb92c97fc69910ad0981a7d6dbbf8c6 is the first bad commit
commit 555b62e1ebb92c97fc69910ad0981a7d6dbbf8c6
Author: Moshfegh Hamedani <moshfegh@live.com.au>
Date:   Mon Aug 17 14:26:49 2020 -0700

    Include the note about committing after staging the changes.

 sections/creating-snapshots/staging-changes.txt | 2 ++
 1 file changed, 2 insertions(+)
```

## Finding Contributors Using Shortlog

```sh
git shortlog
Moshfegh Hamedani (11):
      Initial commit.
      Define the objectives.
      Define the audience.
      Write the first draft of initializing a repo.
      Include the warning about removing .git directory.
      Add a header to the page about initializing a repo.
      Include the command prompt in code sample.
      Add command line and GUI tools to the objectives.
      First draft of staging changes.
      Explain various ways to stage changes.
      Include the note about committing after staging the changes.
```

```sh
git shortlog -n -s
    11  Moshfegh Hamedani
```

```sh
git shortlog -n -s -e
    11  Moshfegh Hamedani <moshfegh@live.com.au>
```

## Viewing the History of a File

```sh
git log --oneline  toc.txt
ca49180 (refs/bisect/good-ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```

```sh
git log --oneline --stat toc.txt  
ca49180 (refs/bisect/good-ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
 toc.txt | 1 +
 1 file changed, 1 insertion(+)
```

```sh
it log --oneline --patch toc.txt
ca49180 (refs/bisect/good-ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
diff --git a/toc.txt b/toc.txt
new file mode 100644
index 0000000..8b13789
--- /dev/null
+++ b/toc.txt
@@ -0,0 +1 @@
+
```

## Restoring a Deleting File

```sh
git rm toc.txt
git commit -m "Remove toc.txt"
```

**Note: In the real world, we should never commit comments like this ever! The comment should be fixing bugs or adding new features!**

```sh
git log --oneline toc.txt
fatal: ambiguous argument 'toc.txt': unknown revision or path not in the working tree.
Use '--' to separate paths from revisions, like this:
'git <command> [<revision>...] -- [<file>...]'
```

```sh
git log --oneline -- toc.txt
55475c0 (HEAD) Remove toc.txt
ca49180 (refs/bisect/good-ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```
=>
```sh
git checkout ca49180 toc.txt
```
=>
```sh
git status -s
A  toc.txt
```

```sh
git commit -m "Restore toc.txt"
[detached HEAD 4f6b0df] Restore toc.txt
 1 file changed, 1 insertion(+)
 create mode 100644 toc.txt
```

## Finding the Author of Line Using Blame

```sh
it blame audience.txt
fb0d184c (Moshfegh Hamedani 2020-08-17 14:18:09 -0700 1) This course is for anyone who wants to learn Git. 
fb0d184c (Moshfegh Hamedani 2020-08-17 14:18:09 -0700 2) No prior experience is required.
```

```sh
git blame -e audience.txt
fb0d184c (<moshfegh@live.com.au> 2020-08-17 14:18:09 -0700 1) This course is for anyone who wants to learn Git. 
fb0d184c (<moshfegh@live.com.au> 2020-08-17 14:18:09 -0700 2) No prior experience is required.
```

```sh
git blame -e -L 1,2 audience.txt
fb0d184c (<moshfegh@live.com.au> 2020-08-17 14:18:09 -0700 1) This course is for anyone who wants to learn Git. 
fb0d184c (<moshfegh@live.com.au> 2020-08-17 14:18:09 -0700 2) No prior experience is required.

```

## Tagging

```sh
git tag v1.0 55475c0            
git log --oneline   
4f6b0df (HEAD) Restore toc.txt
55475c0 (tag: v1.0) Remove toc.txt
555b62e (refs/bisect/bad) Include the note about committing after staging the changes.
91f7d40 (refs/bisect/good-91f7d40d6d5bbc336a271607a0488216aaf50cd7) Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db (refs/bisect/good-36cd6db402cfd897810d4cb33d97ac1e9d1ce2d8) Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 (refs/bisect/good-ca4918083ec471878d58612142572f3367faf5fd) Initial commit.
```

To check the current tags
```sh
git tag
```

```sh
git tag -a v1.1 -m "My version 1.1"
```

```sh
git tag -n                         
v1.0            Remove toc.txt
v1.1            My version 1.1
```

```sh
git show v1.1
```

Delete a tag
```sh
git tag -d v1.1
```

## Browsing History Using VSCode

Install the ***GitLens*** plugin

##   17- 

# Branching

## Introduction
- Use branches
- Compare brances
- Meerge brances
- Resolve conflicts
- Undo a faulty merge
- Essential tool (stashing, cheery packing)

## Working with Branches

```sh
git branch bugfix
it branch
```
```output
  bugfix
* master
```

Switch to bugfix branch
```sh
git switch bugfix
```

Check current branch by
```sh
git status
```

In reality that there will be hundreds or thousands of other bugs to fix.
It's better to use a more a specific name. To rename this branch:
```sh
it branch -m bugfix/signup-form
```

Modify the codes by opening the editor.
```sh
code audience.txt
```
=>
```txt
WHO THIS COURSE IS FOR 
======================
This course is for anyone who wants to learn Git. 
```

```sh
 git status       
On branch bugfix/signup-form
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   audience.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

```sh
git add .
git commit -m "Fix the bug that prevented the users from signing up."
```

```sh
git log --oneline
8169691 (HEAD -> bugfix/signup-form) Fix the bug that prevented the users from signing up.
a642e12 (master) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```

Swith back to Master Branch, not see the bugfix/signup-form branch's modification.
```sh
git switch master
```

```sh
git log --oneline
a642e12 (HEAD -> master) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```

```sh
git log --oneline --all
8169691 (bugfix/signup-form) Fix the bug that prevented the users from signing up.
55475c0 (tag: v1.1, tag: v1.0, tag: v1,0) Remove toc.txt
a642e12 (HEAD -> master) Add header to all pages.
50db987 Include the first section in TOC.
555b62e Include the note about committing after staging the changes.
91f7d40 Explain various ways to stage changes.
edb3594 First draft of staging changes.
24e86ee Add command line and GUI tools to the objectives.
36cd6db Include the command prompt in code sample.
9b6ebfd Add a header to the page about initializing a repo.
fa1b75e Include the warning about removing .git directory.
dad47ed Write the first draft of initializing a repo.
fb0d184 Define the audience.
1ebb7a7 Define the objectives.
ca49180 Initial commit.
```

Git prevents us to accidently delete the branch
```sh
it branch -d bugfix/signup-form
error: The branch 'bugfix/signup-form' is not fully merged.
If you are sure you want to delete it, run 'git branch -D bugfix/signup-form'.
```
=> Using "D" can delete the branch by force.

## Comparing Branches

Show the bugfix/signup-form branch and are not in master.
```sh
it log master..bugfix/signup-form
commit 816969112e5f20ac0516ab32e7d88b13b64fbf0e (bugfix/signup-form)
Author: JunLuo <lawjune@163.com>
Date:   Tue Jul 6 21:20:23 2021 +0800

    Fix the bug that prevented the users from signing up.
```

```sh
git diff master..bugfix/signup-form
```
```sh -output
diff --git a/audience.txt b/audience.txt
index 4cfef55..5957d53 100644
--- a/audience.txt
+++ b/audience.txt
@@ -1,4 +1,3 @@
-AUDIENCE 
-
-This course is for anyone who wants to learn Git. 
-No prior experience is required.
\ No newline at end of file
+WHO THIS COURSE IS FOR 
+======================
+This course is for anyone who wants to learn Git. 
\ No newline at end of file
```

Check the difference between bugfix/ and the current directory.
```sh
git diff bugfix/signup-form 
```

```sh
git diff --name-only bugfix/signup-form
audience.txt
```

## Stashing 

Modify the audience.txt then

```sh
git switch bugfix/signup-form
error: Your local changes to the following files would be overwritten by checkout:
	audience.txt
Please commit your changes or stash them before you switch branches.
Aborting
```

- In this case, we don't want to commit the changes because we're note done yet. 
- So in situtations like this, we should ***stash*** our changes.
- Stashing something means storing it in a safe place.
- So we're going to store this sowewhere in our Git respository. But this is not going to be part of our history.

```sh
git stash push -m "New tax rules."
```
Saved working directory and index state On master: New tax rules.


By defaukt, new ontrack files are not included in your stash.
So as an example:
```sh
echo hello > newfile.txt
```

You **HAVE TO** use "-a" which means "all"
```sh
git stash push -am "My new stash."
```

```sh
git stash list
```
```sh -output
stash@{0}: On master: My new stash.
stash@{1}: On master: New tax rules.
```

```sh
it stash drop 1
```
Dropped refs/stash@{1} (546e9129ca0d8ae82b93cd8d861f3e586e8e46ec)


## Merging 

- Fast-fordward merges (if branches have not diverged)
It simply brings the pointer MASTER forword to the target branch. Then remove teh point of BRANCH once we completed the testing.

- 3-ways merges (if branches have diverged)

### Fast-forward Merges

It's better to add "--graph"
```sh
git log --oneline --all --graph 
```
```sh output
| * 8169691 (bugfix/signup-form) Fix the bug that prevented the users from signing up.
|/  
* a642e12 (HEAD -> master) Add header to all pages.
```


```sh
git merge bugfix/signup-form
```

```sh output
| * 8169691 (HEAD -> master, bugfix/signup-form) Fix the bug that prevented the users from signing up.
```

***Disable Fast-forward Merges***

Modifications => 

-C means "Create"
```sh
git switch -C bugfix/login-form
```
```sh output
Switched to a new branch 'bugfix/login-form'
```

```sh
code toc.txt
git add.
git commit -m "Update toc.txt"
```
=> Modify the file

```sh
(base) madeMacBook-Pro% git switch master
Switched to branch 'master'
(base) madeMacBook-Pro% git merge --no-ff bugfix/login-form
Merge made by the 'recursive' strategy.
 toc.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

```sh
(base) madeMacBook-Pro% git log --oneline --all --graph    
*   63f02de (HEAD -> master) Merge branch 'bugfix/login-form'
|\  
| * 9ce7389 (bugfix/login-form) Update toc.txt
|/  
* 8169691 (bugfix/signup-form) Fix the bug that prevented the users from signing up.
```

**WHY DISABLE FF**
- **CONS**
	- Pollutes the history

- **PROS**
	- True reflection of history
	- Allow reverting a feature


Disable Fast-forward only in the current repository
```sh
git config ff no
```
-> Apply to all of the repository
```sh
git config --global ff no
```

### Three-way Merges

To create a new branch to develop the new feature
```sh
(base) madeMacBook-Pro% git switch -C feature/change-password
Switched to a new branch 'feature/change-password'
```

```sh
(base) madeMacBook-Pro% git log --oneline --all --graph      
*   63f02de (HEAD -> feature/change-password, master) Merge branch 'bugfix/login-form'
|\  
| * 9ce7389 (bugfix/login-form) Update toc.txt
|/  
* 8169691 (bugfix/signup-form) Fix the bug that prevented the users from signing up.
| *   01ec230 (refs/stash) On master: My new stash.
|/|\  
| | * 6dc8977 untracked files on master: a642e12 Add header to all pages.
| * 6cc330c index on master: a642e12 Add header to all pages.
|/  
* a642e12 Add header to all pages.
* 50db987 Include the first section in TOC.
| * 55475c0 (tag: v1.1, tag: v1.0, tag: v1,0) Remove toc.txt
|/  
* 555b62e Include the note about committing after staging the changes.
* 91f7d40 Explain various ways to stage changes.
* edb3594 First draft of staging changes.
```

Currently we are in the "feature" branch
```sh
(base) madeMacBook-Pro% git status
On branch feature/change-password
nothing to commit, working tree clean
```

```sh
(base) madeMacBook-Pro% echo hello > change-password.txt
(base) madeMacBook-Pro% git add .
(base) madeMacBook-Pro% git commit -m "Build the change password form."
[feature/change-password 0b4b301] Build the change password form.
 1 file changed, 1 insertion(+)
 create mode 100644 change-password.txt
```

```sh
(base) madeMacBook-Pro% git log --oneline --all --graph                
* 0b4b301 (HEAD -> feature/change-password) Build the change password form.
*   63f02de (master) Merge branch 'bugfix/login-form'
|\  
| * 9ce7389 (bugfix/login-form) Update toc.txt
|/  
* 8169691 (bugfix/signup-form) Fix the bug that prevented the users from signing up.
```

```sh
(base) madeMacBook-Pro% git switch master
Switched to branch 'master'
(base) madeMacBook-Pro% code objectives.txt 
```

Modify the file.

```sh
(base) madeMacBook-Pro% git add .                            
(base) madeMacBook-Pro% git commit -m "Update objectives.txt"
[master 6dafed7] Update objectives.txt
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Now both branch and master committed.
```sh
(base) madeMacBook-Pro% git log --oneline --all --graph      
* 6dafed7 (HEAD -> master) Update objectives.txt
| * 0b4b301 (feature/change-password) Build the change password form.
|/  
*   63f02de Merge branch 'bugfix/login-form'
|\  
| * 9ce7389 (bugfix/login-form) Update toc.txt
```

*How to merge or combine the changes into a new merge commit?*
```sh
(base) madeMacBook-Pro% git merge feature/change-password
Merge made by the 'recursive' strategy.
 change-password.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 change-password.txt
```

```sh
(base) madeMacBook-Pro% git log --oneline --all --graph  
*   3b2973b (HEAD -> master) Merge branch 'feature/change-password'
|\  
| * 0b4b301 (feature/change-password) Build the change password form.
* | 6dafed7 Update objectives.txt
|/  
*   63f02de Merge branch 'bugfix/login-form'
|\  
| * 9ce7389 (bugfix/login-form) Update toc.txt
|/  
* 8169691 (bugfix/signup-form) Fix the bug that prevented the users from signing up.
```

## Viewing Merged and Unmerged Branches
```sh
(base) madeMacBook-Pro% git branch --merged
  bugfix/login-form
  bugfix/signup-form
  feature/change-password
* master
```

```sh
(base) madeMacBook-Pro% git branch -d bugfix/login-form
Deleted branch bugfix/login-form (was 9ce7389).
```

```sh
git branch --no-merge
```

## Merge Conflicts

**CONFLICTS**
- Change1, Change2
- Change, Delete
- Add1, Add2 (Contents are differnent)

```sh
(base) madeMacBook-Pro% git switch -C bugfix/change-password
Switched to a new branch 'bugfix/change-password'

(base) madeMacBook-Pro% code change-password.txt 
```
Modify the file.
```sh
(base) madeMacBook-Pro% git add .
(base) madeMacBook-Pro% git commit -m "Update change-password.txt"
[bugfix/change-password 872df1f] Update change-password.txt
 1 file changed, 1 insertion(+)
```

```sh
(base) madeMacBook-Pro% git switch master
Switched to branch 'master'
(base) madeMacBook-Pro% code change-password.txt 
```
Modify the file **AGAIN**.

```sh
(base) madeMacBook-Pro% git add .
(base) madeMacBook-Pro% git commit -m "Update change-password.txt"
[master d82dea8] Update change-password.txt
 1 file changed, 1 insertion(+)
```

```sh
(base) madeMacBook-Pro% git merge bugfix/change-password
Auto-merging change-password.txt
CONFLICT (content): Merge conflict in change-password.txt
Automatic merge failed; fix conflicts and then commit the result.
```

```sh
(base) madeMacBook-Pro% git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   change-password.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

```sh
code change-password.txt
```
=> We'll see in the editor.
```sh
hello
<<<<<<< HEAD
Change in the master branch.
=======
Change in the bug fix.
>>>>>>> bugfix/change-password
```
=> To select the options in vs-code.
- Accept Current Change
- Accept Incoming Change
- Accpet Both CHanges

```sh
(base) madeMacBook-Pro% git add change-password.txt 
(base) madeMacBook-Pro% git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
	modified:   change-password.txt
```

```sh
(base) madeMacBook-Pro% git commit
[master 0b45063] Merge branch 'bugfix/change-password'
```

## Graphical Merge Tools

**MERGE TOOLS**
- Kdiff
- P4Merge: https://www.perforce.com/downloads/visual-merge-tool
- WinMerge (Windows Only)

```sh
git config --global merge.tool p4Merge
git config --global mergetool.p4Merge.path "/Applications/p4merge.app/Contents/MacOS/p4merge"
```

Run merge tool
```sh
git mergetool
```

## Aborting a Merge

```sh
git merge --abort
```


## Undoing a Faulty Merge

```sh
(base) madeMacBook-Pro% git reset -h
usage: git reset [--mixed | --soft | --hard | --merge | --keep] [-q] [<commit>]
   or: git reset [-q] [<tree-ish>] [--] <pathspec>...
   or: git reset [-q] [--pathspec-from-file [--pathspec-file-nul]] [<tree-ish>]
   or: git reset --patch [<tree-ish>] [--] [<pathspec>...]

    -q, --quiet           be quiet, only report errors
    --mixed               reset HEAD and index
    --soft                reset only HEAD
    --hard                reset HEAD, index and working tree
    --merge               reset HEAD, index and working tree
    --keep                reset HEAD but keep local changes
    --recurse-submodules[=<reset>]
                          control recursive updating of submodules
    -p, --patch           select hunks interactively
    -N, --intent-to-add   record only the fact that removed paths will be added later
    --pathspec-from-file <file>
                          read pathspec from file
    --pathspec-file-nul   with --pathspec-from-file, pathspec elements are separated with NUL character
```

```sh
git reset --hard HEAD~1
```

```sh
(base) madeMacBook-Pro% git reset --hard HEAD~1
HEAD is now at d82dea8 Update change-password.txt
(base) madeMacBook-Pro% git log --oneline --all --graph           
* d82dea8 (HEAD -> master) Update change-password.txt
| * 872df1f (bugfix/change-password) Update change-password.txt
|/  
*   3b2973b Merge branch 'feature/change-password'
|\  
| * 0b4b301 (feature/change-password) Build the change password form.
* | 6dafed7 Update objectives.txt
|/  
*   63f02de Merge branch 'bugfix/login-form'
|\  
| * 9ce7389 Update toc.txt
|/  
* 8169691 (bugfix/signup-form) Fix the bug that prevented the users from signing up.
| *   01ec230 (refs/stash) On master: My new stash.
|/|\  
| | * 6dc8977 untracked files on master: a642e12 Add header to all pages.
| * 6cc330c index on master: a642e12 Add header to all pages.
|/  

zsh: suspended  git log --oneline --all --graph
(base) madeMacBook-Pro% git reset --hard 3b2973b       
HEAD is now at 3b2973b Merge branch 'feature/change-password'
(base) madeMacBook-Pro% git log --oneline --all --graph
* 872df1f (bugfix/change-password) Update change-password.txt
*   3b2973b (HEAD -> master) Merge branch 'feature/change-password'
|\  
| * 0b4b301 (feature/change-password) Build the change password form.
* | 6dafed7 Update objectives.txt
|/  
*   63f02de Merge branch 'bugfix/login-form'
|\  
| * 9ce7389 Update toc.txt
|/  
* 8169691 (bugfix/signup-form) Fix the bug that prevented the users from signing up.
| *   01ec230 (refs/stash) On master: My new stash.
|/|\  
| | * 6dc8977 untracked files on master: a642e12 Add header to all pages.
| * 6cc330c index on master: a642e12 Add header to all pages.
|/  
* a642e12 Add header to all pages.
* 50db987 Include the first section in TOC.
```

```sh
(base) madeMacBook-Pro% git revert -m 1 HEAD
Removing change-password.txt
[master dbd7f52] Revert "Merge branch 'feature/change-password'"
 1 file changed, 1 deletion(-)
 delete mode 100644 change-password.txt
```

```sh
(base) madeMacBook-Pro% git log --oneline --all --graph
* dbd7f52 (HEAD -> master) Revert "Merge branch 'feature/change-password'"
| * 872df1f (bugfix/change-password) Update change-password.txt
|/  
*   3b2973b Merge branch 'feature/change-password'
|\  
| * 0b4b301 (feature/change-password) Build the change password form.
* | 6dafed7 Update objectives.txt
```

## Squash Merging

You should use it in short-lived branches with bad history.
Like bug fixes or features that you can implement in a few hours or in a day.

*The first commit*
```sh
(base) madeMacBook-Pro% git switch -C bugfix/photo-upload
Switched to a new branch 'bugfix/photo-upload'
(base) madeMacBook-Pro% echo >> audience.txt
(base) madeMacBook-Pro% git status
On branch bugfix/photo-upload
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   audience.txt

no changes added to commit (use "git add" and/or "git commit -a")
(base) madeMacBook-Pro% git commit -am "Update audience.txt" 
[bugfix/photo-upload 19accd1] Update audience.txt
 1 file changed, 1 insertion(+), 1 deletion(-)
```

*The second commit*
```sh
(base) madeMacBook-Pro% echo bugfix >> toc.txt
(base) madeMacBook-Pro% git status
On branch bugfix/photo-upload
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   toc.txt

no changes added to commit (use "git add" and/or "git commit -a")
(base) madeMacBook-Pro% git commit -am "Update toc.txt"
[bugfix/photo-upload 69a53a9] Update toc.txt
 1 file changed, 1 insertion(+), 1 deletion(-)
```

```sh
(base) madeMacBook-Pro% git log --oneline --graph
* 69a53a9 (HEAD -> bugfix/photo-upload) Update toc.txt
* 19accd1 Update audience.txt
* dbd7f52 (master) Revert "Merge branch 'feature/change-password'"
*   3b2973b Merge branch 'feature/change-password'
```

```sh
(base) madeMacBook-Pro% git switch master
Switched to branch 'master'
(base) madeMacBook-Pro% git merge --squash bugfix/photo-upload
Updating dbd7f52..69a53a9
Fast-forward
Squash commit -- not updating HEAD
 audience.txt | 2 +-
 toc.txt      | 2 +-
 2 files changed, 2 insertions(+), 2 deletions(-)
```

```sh
(base) madeMacBook-Pro% git status -s
M  audience.txt
M  toc.txt
(base) madeMacBook-Pro% git commit -m "Fix the bug on the photo upload page."
[master bdfcbb4] Fix the bug on the photo upload page.
 2 files changed, 2 insertions(+), 2 deletions(-)
```

```sh
(base) madeMacBook-Pro% git log --oneline --graph                            
* bdfcbb4 (HEAD -> master) Fix the bug on the photo upload page.
* dbd7f52 Revert "Merge branch 'feature/change-password'"
*   3b2973b Merge branch 'feature/change-password'
```

```sh
(base) madeMacBook-Pro% git branch --merged
  bugfix/signup-form
  feature/change-password
* master
(base) madeMacBook-Pro% git branch --no-merged
  bugfix/change-password
  bugfix/photo-upload
```

But we'll get an error while deleting the bugfix/photo-upload
```sh
(base) madeMacBook-Pro% git branch -d bugfix/photo-upload
error: The branch 'bugfix/photo-upload' is not fully merged.
If you are sure you want to delete it, run 'git branch -D bugfix/photo-upload'.
```
-> To use "D"
```sh
(base) madeMacBook-Pro% git branch -D bugfix/photo-upload
Deleted branch bugfix/photo-upload (was 69a53a9).
```

## Rebasing
Another technique for bringing changes from one branch into another.

**REBASING REWRITINGS HISTORY**

===============================


## Cherry Picking

===============================

## Picking a File from Another Branch

===============================




# Collaboration

## Introduction
- Collaboration
- Pushing, fetching and pulling
- Pull requests, issues and milestones
- Contributing to open-source projects

## Workflows

- **CENTRALIZED** -> Single repository
- **DISTRIBUTED** -> Every dev has one repository
- **CENTRALIZED WORKFLOW** PUSH -> PULL
- **INTEGRATION-MANAGER** FORK -> PULL -> PUSH -> PULL REQUEST ...

## Creating a GitHub Repository

## Adding Collaborators

## Cloning the 

```sh
(base) madeMacBook-Pro% git clone https://github.com/Lawjune/Mars.git
Cloning into 'Mars'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```

```sh
(base) madeMacBook-Pro% git log --oneline --all --graph
* 84d0e24 (HEAD -> master, origin/master, origin/HEAD) Initial commit
```

```sh
(base) madeMacBook-Pro% git switch origin/master
fatal: a branch is expected, got remote branch 'origin/master'
(base) madeMacBook-Pro% git branch
* master
(base) madeMacBook-Pro% git remote
origin #It's not in the current directory
(base) madeMacBook-Pro% git remote -v # Get more details of the repository
origin	https://github.com/Lawjune/Mars.git (fetch)
origin	https://github.com/Lawjune/Mars.git (push)
```


## Fetching 

Edit the README.md in github online.

1. 
**LOCAL**
	**MASTER** -> (A)
**REMOTE**
	**MASTER** -> (A)

2.
**LOCAL**
	**MASTER** -> (A)
**REMOTE**
	**MASTER** -> (B) -> (A)

3. `git fetch`
**LOCAL**
	**MASTER** -> (A)
	**ORIGIN/MASTER** -> (B) -> (A)
**REMOTE**
	**MASTER** -> (B) -> (A)

4. `git merge origin/master` in **MASTER** branch
=> Fast Forward Merge
**LOCAL**
	**MASTER** -> (B) => Resolve the confict for divergence
	**ORIGIN/MASTER** -> (B) -> (A)
**REMOTE**
	**MASTER** -> (B) -> (A)

```sh
(base) madeMacBook-Pro% git log --oneline --all --graph
* 84d0e24 (HEAD -> master, origin/master, origin/HEAD) Initial commit
(base) madeMacBook-Pro% git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
(base) madeMacBook-Pro% git fetch
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 646 bytes | 323.00 KiB/s, done.
From https://github.com/Lawjune/Mars
   84d0e24..cbe3cf0  master     -> origin/master
(base) madeMacBook-Pro% git log --oneline --all --graph
* cbe3cf0 (origin/master, origin/HEAD) Update README.md
* 84d0e24 (HEAD -> master) Initial commit
```

```sh
(base) madeMacBook-Pro% git branch -vv
* master 84d0e24 [origin/master: behind 1] Initial commit
```

```sh
(base) madeMacBook-Pro% git merge origin/master
Updating 84d0e24..cbe3cf0
Fast-forward
 README.md | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
```

```sh
(base) madeMacBook-Pro% git log --oneline --all --graph
* cbe3cf0 (HEAD -> master, origin/master, origin/HEAD) Update README.md
* 84d0e24 Initial commit
(base) madeMacBook-Pro% git branch -vv                 
* master cbe3cf0 [origin/master] Update README.md
(base) madeMacBook-Pro% cat README.md                  
# Mars
A new line of code
```


## Pulling

**Pull = Fetch + Merge**


1. 
**LOCAL**
	**MASTER** -> (A)
	**ORIGIN/MASTER** -> (A)
**REMOTE**
	**MASTER** -> (A)

2. 
**LOCAL**
	**MASTER** -> (B) -> (A)
	**ORIGIN/MASTER** -> (A)
**REMOTE**
	**MASTER** -> (C) -> (A)

3. `git pull`
**LOCAL**
	**MASTER** -> (M) -> (B) -> (A)
	**ORIGIN/MASTER** -> (C) -> (A)
**REMOTE**
	**MASTER** -> (C) -> (A)

4. `git pull --rebase`

**LOCAL**
	**MASTER** -> (B) -> (C) -> (A)
	**ORIGIN/MASTER** -> (C) -> (A)
**REMOTE**
	**MASTER** -> (C) -> (A)


To modify on github and then
```sh
(base) madeMacBook-Pro% echo hello > file1.txt
(base) madeMacBook-Pro% git add .
(base) madeMacBook-Pro% git commit -m "Add file1"
[master 97aac5e] Add file1
 1 file changed, 1 insertion(+)
 create mode 100644 file1.txt
```

```sh
(base) madeMacBook-Pro% git log --oneline --all --graph
* 97aac5e (HEAD -> master) Add file1
* cbe3cf0 (origin/master, origin/HEAD) Update README.md
* 84d0e24 Initial commit
```


## Pushing
1. 
**LOCAL**
	**MASTER** -> (C) -> (B) -> (A)
	**ORIGIN/MASTER** -> (B) -> (A)
**REMOTE**
	**MASTER** -> (B) -> (A)

2. `git push`
**LOCAL**
	**MASTER** -> (C) -> (B) -> (A)
	**ORIGIN/MASTER** -> (C) -> (B) -> (A)
**REMOTE**
	**MASTER** -> (C) -> (B) -> (A)

***Never ever use `git push -f`***


## Storing Credetials

```sh
git config --global credential.helper cache
```

**CREDENTIAL HELPER**
- Mac: Keychain
- Windows: Windows Credential Store

```sh
(base) madeMacBook-Pro% git credential-osxkeychain
usage: git credential-osxkeychain <get|store|erase>
```

```sh
git config --global credential.helper osxkeychain
```


## Sharing Tags

```sh
git tag v1.0
git push origin v1.0
```

```sh
git push origin --delete v1.0
git tag -d v1.0
```


## Releases

A github feature


## Sharing Branches

```sh
git switch -C feature/change-password
git push -u origin feature/change-password
```

Remove the branch
```sh
git push -d origin feature/change-password
```
```sh
git switch master
git branch -d feature/change-password
```


## Collaboration Workflow






# Rewriting History






































