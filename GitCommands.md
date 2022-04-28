# Git

## git commit --amend
Allows you to modify the most recent commit in your repository or add changes to the last commit. 
[Rewriting history](https://www.atlassian.com/git/tutorials/rewriting-history).

```bash
git commit --amend
git duet-commit --amend

# update the message on the last commit.
git commit --amend -m "an updated message"
git duet-commit --amend -m "an updated message"

# If you make a commit but forget to add a change you can...
git add --all | git add -p | git add file.js

# Then add the changes to the last commit
git commit --amend --no-edit
git duet-commit --amend --no-edit
```

## git checkout

```bash
## Checkouts the specified branch
git checkout [branch]

## the - flag alternates between your last two branches
git checkout -
```

## git diff

```bash
## Compares changes with last commit
git diff

## Compares changes between specified branches
git diff [branch-1] [branch-2]

```


## git grep

Look for specified search patterns within your repository work tree. [More on git grep here](https://git-scm.com/docs/git-grep).

```bash
git grep "your search term"
```
## Rebasing from feature branch
```bash
# Checkout your feature branch and then commit and push your changes
git checkout [feature-branch]
git commit -m "your changes with a relevant comment"
git push

# squash feature branch down to one commit
git merge-base master HEAD
git rebase -i <insert result from git merge-base above>

# Choose which commits to pick and squash.
# The following command will prompt you at each instance
# of the word pick, and will allow you to replace it with the word squash.
# In most circumstances, we pick the first commit, and squash all subsequent commits (from top top bottom):
:%s/pick/squash/gc

# Write and Save the file
:wq

# Set the comment for the commit to <Title of Story> [#<ID of Story>], then save
:wq

# Switch to master and pull with rebase
git checkout master
git pull -r

# Switch to feature branch
git checkout [feature-branch]

# Rebase with commit
git rebase master
# at this stage, resolve any merge conflicts and use git rebase --continue if required

# Switch to master
git checkout master

# Merge with master and push
git merge [feature-branch]
# **********
# IMPORTANT: Check that 'Fast-forward' has been mentioned in the git output. If it hasn't, something has gone wrong!
# **********

# Do another rebase pull before pushing to prevent a merge commit
git pull -r

# Pushi it!
git push
```

## Deleting branches

```bash
# Lists branches that can be deleted/pruned on local (requires --dry-run)
git remote prune origin --dry-run

# Prunes cleans up branches on your local.
git remote prune origin

# Deletes specified local branch. The -d flag will only delete branch if you have no uncommitted changes
git branch -d [feature-branch]

# Deletes specified local branch. The -D flag will force delete branch whether it has changes or not.
git branch -D [feature-branch]

# Deletes specified branch on origin.
git push origin --delete [feature-branch]
```

## Patching changes
```bash

# Allows you to commit your changes in patches
git add -p

# Allows you to add new files to be committed in patches
git add -N .
git add -p

# Or, add specific new files to be commited in patches
git add -N [your-file-to-add.ext]
git add -p

```

## Adding, commiting and pushing commits using duet
```bash
# Add your changes in patches
git add -p

# Set your authors. Your author list is available in [your-git-root]/.git-authors
git duet [a1] [a2]

# Add your commit message
git duet-commit -m "your commit message here"

# Push your changes
git push
```

## Useful git aliases

The following aliases should be placed in your ``` [your-git-root]/.gitconfig ``` file.

```bash

# Different print out variations for git log. 
lol = log --graph --decorate --pretty=oneline --abbrev-commit
lola = log --graph --decorate --pretty=oneline --abbrev-commit --all
plog = log --graph --pretty='format:%C(red)%d%C(reset) %C(yellow)%h%C(reset) %ar %C(green)%aN%C(reset) %s'
tlog = log --stat --since='1 Day Ago' --graph --pretty=oneline --abbrev-commit --date=relative
lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

# Shows number of commits by author in descending order
rank = shortlog -sn --no-merges

# Lists your git aliases
aliases=!git config -l | grep alias | cut -c 7-
```