# Git Guide

_If you find any errors or if you would like to make improvements or add to this, **please consider contributing** by opening pull requests_

_This is **not** meant for complete beginners to git and is not a substitute for a proper tutorial. This is meant to be used as a quick reference and contains a list of basic commands (that i think are commonly used) with brief discriptions on how to use them._

_An amazing site to learn git in an interactive way is [learnGitBranching](https://learngitbranching.js.org/). You can also try the sandbox version of the same [here](https://learngitbranching.js.org/?NODEMO)_

## First time setup

If you haven't already, [click here to install git for windows](https://git-scm.com/download/win) from the official git website. Select git bash

### Set up username

Your username will be used to associate you with the commits that you make. You will need to assign a username before you can make any commits

```
git config --global user.name "Your name here"
```

This sets your username globally for all repositories. To set your username for only a single repository, run the same command with your desired name, without the `--global` tag.

### Sign in to your remote git service provider

When you use git to perform a task that requires signing in (such as cloning using HTTPS), you will be prompted to sign in. Git will locally save your login info for your convenience. This will **NOT** happen if you use SSH to connect to your provider. [Click here for more information](https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git).

## Basic terminal commands

_These commands use for git bash and other UNIX based shells_

`ls` list all files in the directory

`ls -all` list all files in the directory including hidden files (like git files)

`mkdir` to create a folder

`cd` to change directory (change the folder you're currently viewing in terminal)

`touch filename.fileExtension` to create a new file of the given name and the extension (.md, .txt, etc)

## Creating a git repository and connecting to remote

1. Initialize an empty git repository

```
git init
```

2. It is recommended to add at least one file to your repository before connecting it to remote. If your repository is empty, add a readme file

```
touch README.md
```

3. Stage all of your files

```
git add .
```

4. Commit all files

```
git commit -m "first commit"
```

5. Rename your [master branch to main](https://git-scm.com/docs/git-branch)

```
git branch -M main
```

6. Add your remote URL (origin). You can find your remote URL from the "quick setup" screen right after you create an empty repository from Github

```
git remote add origin origin-url-here
```

7. Push changes to remote

```
git push --set-upstream origin main
```

### Check remote URL attached to a local repository

```
git remote -v
```

## Cloning repository (using HTTPS)

1. Copy your HTTPS clone URL by going to the "code" section of your main repository page
2. Use the git clone command in the location you want to clone into

```
git clone pasteYourLinkHere
```

## HEAD, working tree and the index

HEAD - pointer that points to a branch or commit that is the the last checked out. When a make a new commit, the HEAD will be updated to point at the new commit. (\*) symbol denotes the HEAD

Working tree - Files that you are currently working on

Index - staging area

Visit [this stackoverflow answer](https://stackoverflow.com/questions/3689838/whats-the-difference-between-head-working-tree-and-index-in-git) for more information.

## Origin and upstream URLs conventions

`origin` - URL of any repository (whether folked or not) that you own or can directly make changes to is called as origin URL. Use `git remote add origin origin-URL-here`.

`upstream` - URL from where a project has been forked is known as upstream URL. By setting upstream in git, the local branches can track the remote branches. This makes pulling changes from the remote repository very easy. Use `git remote add upstream upstream-url-here`.

## Status

To check status of your git repository, use `git status`

## Staging changes

To stage only a single file

```
git add filename.fileExtension
```

To stage all files that have been modified

```
git add .
```

### Unstage (restore)

```
git restore --staged filename.fileExtension
```

Or to unstaged changes the uncommited and preserve them from all files

```
git restore --staged .
```

Unstage changes from file and **delete** the uncommited changes or discard the unstaged changes in the working directory. **_needs verification_**

```
git restore filename.fileExtension
```

## Commits

To commit files already staged

```
git commit -m "your commit message here"
```

To automatically stage files that have been modified and then commit, use the `-a` or `-all` tag

```
git commit -a -m "your commit message here"
```

To see all commits, use `git log`

### Removing commits (reset)

To remove commits without losing changes made in them, use the commitID for the commit you want to reset to, and the reset command. Changes from the removed commits will move to the unstaged area

```
git reset commitID
```

To remove commits and delete changes in them, use the commitID for the commit you want to reset to, and the reset command with the `--hard` tag. Changes from the removed commits will be **deleted and will not be unstaged**

```
git reset --hard commitID
```

### Removing changes of commits while preserving the history (revert)

_yet to be added_

## Reset, restore and revert

`revert` - is about making a new commit that reverts the changes made by other commits.

`restore` - is about restoring files in the working tree from either the index or another commit. This command does not update your branch. The command can also be used to restore files in the index from another commit.

`reset` - is about updating your branch, moving the tip in order to add or remove commits from the branch. This operation changes the commit history.

For more information, visit [official docs](https://git-scm.com/docs/git#_reset_restore_and_revert)

## Stash

To stash changes that are staged

```
git stash
```

To pull changes back to working directory from the stash. Popped changes will be unstaged

```
git stash pop
```

To **delete** stashed changes

```
git stash clear
```

## Branches

For listing all branches, use `git branch`

For listing all remote branches, use `git branch -r`

For creating a new branch

```
git branch branchName
```

For deleting an existing branch, use `--delete` tag or the `-d` shorhand

```
git branch -d branchName
```

For switching (or "checking out") branches

```
git checkout branchName
```

## Pushing changes

To push changes, specify your URL (origin) and the branch you want to push changes to

```
git push origin branchName
```

### Set upstream tag

To push changes and specify an upstream for further argument less push / pull commands, use the `--set-upstream` or the shorthand `-u` tag. This sets the upstream association for any future push/pull attempts automatically.

```
git push -u origin branchName
```

### Force pushing

Git will prevent any changes to be pushed to remote if the local is using an outdated version of remote's commit history. This ensures that you are not overwriting changes made by someone else because your local was not in sync. [Read this article for more info](https://www.git-tower.com/blog/force-push-in-git/).

```
git push --force
```

This is a destructive command as it overwrites any changes in the remote with your local changes so **data could be lost**. Use only when you're sure about what you're doing.

A good use case is when you want to remove commits from a branch or an already open pull request. You can use [git-reset](#removing-commits-reset) and remove commits from your local git copy. However, git won't allow you to push it to remote because the remote now has extra commits (these are the commits you just removed) that your local copy does not have. You will have to force push to overwrite the remote commits with your version.

## Fetching changes

Downloads data from remote but does not force those changes to be merged into your local work.

## Pulling changes

_yet to be added_

## Contributing to Open Source

_This section describes git and ways to use it for contributing to open source. **This section requires improvement**_

### Open source and forking

You do not have permissions to make changes to a repository that you do not own / not a part of. In order you contribute, you should create a copy of that repository that you will own that is, a fork. You can make changes to your fork and then open pull request to push those changes to the original repository (or upstream).

### Open source and working with branches

There can be **only one open pull request** per branch. Github will combine all commits into the pull request that's currently open.Therefore, a separate pull request cannot be created for every commit made to a branch.

To fix this, create a new branch for every new feature / change so you can create separate pull requests for being reviewed by other contributors.

### Making local repository up to date with remote