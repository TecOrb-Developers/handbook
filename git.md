# Contents

* [Installing Git](#install-git)
* * [GitHub Desktop](#github-desktop)
* * [Git for all platforms](#git-for-all-platforms)
* [Initial setup](#initial-setup)
* [Creating a repository](#create-a-repository)
* [Alteration](#alteration)
* [Teamwork](#teamwork)
* [File operations](#file-operations)
* [Ignoring some files](#ignore-some-files)
* [Saving fragments](#saving-fragments)
* [View history](#view-history)
* [Reverting commits](#rollback-commits)
* [Synchronization with a remote repository](#synchronize-with-a-remote-repository)

# Install Git

> GitHub provides a windowed GUI for basic repository operations, and a console version of Git with automatic updates for advanced workflows.

## GitHub Desktop

[desktop.github.com](https://desktop.github.com/)

Git distributions for Linux and POSIX systems are available from the official Git SCM website.

## Git for all platforms

[git-scm.com](https://git-scm.com/)

# Initial setup

> Setting user information for all local repositories

```bash
git config --global user.name "[name]"
```

Sets the name that will appear in the author field of commits you make

```bash
git config --global user.email "[email address]"
```

Sets the email address that will be shown in the commits you make

# Create a repository

> Create a new repository or fetch it from an existing URL

```bash
git init [project name]
```

Creates a new local repository with the given name

```bash
git clone [url]
```
Downloads a repository along with its entire change history

# Alteration

> Review changes and create commits (commit changes)

```bash
git status
```

Lists all new or changed files that need to be committed

```bash
git diff
```

Shows differences by changes made in files not yet indexed

```bash
git add [file]
```

Indexes the specified file for later commit

```bash
git diff --staged
```

Shows differences between indexed and last committed versions of files

```bash
git reset [file]
```

Cancels the indexing of the specified file, while preserving its contents

```bash
git commit -m "[description message]"
```

Commits indexed changes and saves them to version history

# Teamwork

> Named series of commits and aggregation of work results

```bash
git branch
```

List of named commit branches, indicating the selected branch

```bash
git branch [branch name]
```

Creates a new branch

```bash
git switch -c [branch name]
```

Switches to the selected branch and updates the working directory to its state

```bash
git merge [branch name]
```

Commits the changes of the specified branch to the current branch

```bash
git branch -d [branch name]
```

Deletes the selected branch

# File operations

> Moving and deleting repository file versions

```bash
git rm [file]
```

Removes a specific file from the working directory and indexes its removal

```bash
git rm --cached [file]
```

Removes a specific file from version control, but physically leaves it in its place

```bash
git mv [original file] [new name]
```

Moves and renames the specified file, immediately indexing it for later commit

# Ignore some files

> Exclusion of temporary and secondary files and directories

```bash
*.log
build/
temp-*
```

Git will ignore files and directories listed in `.gitignore` file using wildcard syntax

```bash
git ls-files --others --ignored --exclude-standard
```

List of all ignored files in the current project

# Saving fragments

> Save and restore pending changes

```bash
git stash
```

Temporarily saves all uncommitted changes to monitored files

```bash
git stash pop
```

Restores the state of previously saved versions of files

```bash
git stash list
```

Lists all temporary saves

```bash
git stash drop
```

Resets the last temporarily saved changes

# View history

> View and study the history of changes to project files

```bash
gitlog
```

Commit history for the current branch

```bash
git log --follow [file]
```

Change history of a particular file, including its renaming

```bash
git diff [first branch]...[second branch]
```

Shows the difference between the contents of the commits of two branches

```bash
git show [commit]
```

Prints information and shows changes in the selected commit

# Rollback commits

> Deleting errors and correcting the created history

```bash
git reset [commit]
```

Reverts all commits after the given one, leaving all changes in the working directory

```bash
git reset --hard [commit]
```

Resets the entire history, along with the state of the working directory, up to the specified commit.

# Synchronize with a remote repository

> Register remote repository and share changes

```bash
git fetch [remote repository]
```

Downloads the entire history from a remote repository

```bash
git merge [remote repository]/[branch]
```

Commits changes from the remote repository branch to the current local repository branch

```bash
git push [remote repository] [branch]
```

Downloads all changes from the local branch to the remote repository

```bash
git pull
```

Downloads a history from a remote repository and merges it with the local one. pull = fetch + merge
