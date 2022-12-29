# Git Guide

contribution text should come here

disclaimer should come here

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

6. Add your remote origin URL. You can find your remote URL from the "quick setup" screen right after you create an empty repository from Github

```
git remote add origin yourLinkHere
```

7. Push changes to remote

```
git push --set-upstream origin main
```

### Check remote URL attached to a local repository

```
git remote -v
```
