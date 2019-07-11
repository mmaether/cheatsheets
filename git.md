# Git

This file has some general git commands that I reuse pretty frequently.

## Revert Changes

`git reset --hard`

## Jenkins Pipeline

```
// Switch to master
git checkout master
git pull origin master
git cherry-pick (commit id), e.g. git cherry-pick 506880c
-- for conflicts, get the name of the file that has a merge conflict problem:
   git diff --name-only --diff-filter=U
-- you may then need to add files, git add <file>
-- git commit -m "Merged and cherry picked"
-- run update.php if needed
git push origin master

// Then switch to proprod and do the same
git checkout preprod
git pull origin preprod
...

// Then switch to production and do the same
```
