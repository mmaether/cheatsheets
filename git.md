# Git Cheat Sheet

This cheatsheet is a Markdown-ified version of [GitHub's cheatsheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf) for easy access.

Git is the open source distributed version control system that facilitates GitHub activities on your laptop or desktop. This cheat sheet summarizes commonly used Git command line instructions for quick reference.

## Install Git

GitHub provides desktop clients that include a graphical user interface for the most common repository actions and an automatically updating command line edition of Git for advanced scenarios.

### GitHub for Windows

[htps://windows.github.com](htps://windows.github.com)

### GitHub for Mac

[htps://mac.github.com](htps://mac.github.com)

Git distributions for Linux and POSIX systems are available on the official Git SCM web site.

### Git for All Platforms

[htp://git-scm.com](htp://git-scm.com)

## Configure Tooling

Configure user information for all local repositories

| Command | Explanation|
|---------|------------|
|`$ git config --global user.name "[name]"`| Sets the name you want atached to your commit transactions|
|`$ git config --global user.email "[email address]"`| Sets the email you want atached to your commit transactions |
|`$ git config --global color.ui auto`| Enables helpful colorization of command line output

## Create Repositories

Start a new repository or obtain one from an existing URL

| Command | Explanation|
|---------|------------|
|`$ git init [project-name]`| Creates a new local repository with the specified name
|`$ git clone [url]` | Downloads a project and its entire version history

## Make Changes

Review edits and craf a commit transaction

| Command | Explanation|
|---------|------------|
|`$ git status`| Lists all new or modified files to be commited
|`$ git diff`| Shows file differences not yet staged
|`$ git add [file]`| Snapshots the file in preparation for versioning
|`$ git diff --staged`| Shows file differences between staging and the last file version
|`$ git reset [file]`| Unstages the file, but preserve its contents
|`$ git commit -m "[descriptive message]"`| Records file snapshots permanently in version history

## Group Changes

Name a series of commits and combine completed efforts

| Command | Explanation|
|---------|------------|
|`$ git branch`| Lists all local branches in the current repository
|`$ git branch [branch-name]`| Creates a new branch
|`$ git checkout [branch-name]`| Switches to the specified branch and updates the working directory
|`$ git merge [branch]`| Combines the specified branch's history into the current branch
|`$ git branch -d [branch-name]`| Deletes the specified branch

## Refactor Filenames

Relocate and remove versioned files

| Command | Explanation|
|---------|------------|
|`$ git rm [file]`| Deletes the file from the working directory and stages the deletion
|`$ git rm --cached [file]`| Removes the file from version control but preserves the file locally
|`$ git mv [file-original] [file-renamed]`| Changes the file name and prepares it for commit

## Suppress Tracking

Exclude temporary files and paths

| Command | Explanation|
|---------|------------|
|`*.log` <br>  `build/` <br> `temp-\*` | A text file named `.gitignore` suppresses accidental versioning of files and paths matching the specified paterns
|`$ git ls-files --other --ignored --exclude-standard`| Lists all ignored files in this project

## Save Fragments

Shelve and restore incomplete changes

| Command | Explanation|
|---------|------------|
|`$ git stash`| Temporarily stores all modified tracked files
|`$ git stash pop`| Restores the most recently stashed files
|`$ git stash list`| Lists all stashed changesets
|`$ git stash drop`| Discards the most recently stashed changeset

## Review History

Browse and inspect the evolution of project files

| Command | Explanation|
|---------|------------|
|`$ git log`| Lists version history for the current branch
|`$ git log --follow [file]`| Lists version history for a file, including renames
|`$ git diff [first-branch]...[second-branch]`| Shows content differences between two branches
|`$ git show [commit]`| Outputs metadata and content changes of the specified commit

## Redo Commits

Erase mistakes and craf replacement history

| Command | Explanation|
|---------|------------|
|`$ git reset [commit]`| Undoes all commits afer `[commit]`, preserving changes locally
|`$ git reset --hard [commit]`| Discards all history and changes back to the specified commit

## Synchronize Changes

Register a repository bookmark and exchange version history

| Command | Explanation|
|---------|------------|
|`$ git fetch [bookmark]`| Downloads all history from the repository bookmark
|`$ git merge [bookmark]/[branch]`| Combines bookmark’s branch into current local branch
|`$ git push [alias] [branch]`| Uploads all local branch commits to GitHub
|`$ git pull`| Downloads bookmark history and incorporates changes

## Revert Changes

`git reset --hard`

## Jenkins Pipeline

To push code via the Jenkins CI/CD pipeline, we commit according to the following general steps.

1. Switch to a branch.
2. Pull the latest code changes.
3. Add the updated code via cherry-pick
4. Push the code
5. Switch to the next branch and repeat.

```
// Make changes to master.
git checkout master
git pull origin master
git cherry-pick (commit id), e.g. git cherry-pick xxxxxxx
git push origin master

// Switch to proprod (sandbox) and do the same.
git checkout preprod
git pull origin preprod
git cherry-pick (commit id), e.g. git cherry-pick xxxxxxx
git push origin preprod

// Switch to production (live) and do the same.
git checkout production
git pull origin production
git cherry-pick (commit id), e.g. git cherry-pick xxxxxxx
git push origin production


-- For conflicts, get the name of the file that has a merge conflict problem.
git diff --name-only --diff-filter=U
-- You may then need to add those merge conflicted files.
git add <file>
-- And then commit.
git commit -m "Merged and cherry picked"
-- For Drupal you may want to run update.php if needed.
```
