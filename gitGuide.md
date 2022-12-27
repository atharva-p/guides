# Git Guide

contribution text should come here

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
