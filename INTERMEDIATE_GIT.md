# Intermediate Git Commands File

Some of the git commands below can be considered beginner but they involve using branches. Many people think that branches are beginner as well, but you can easily make mistakes when working with branches. I also added notes on creating GitHub Gists and GitHub pages at the bottom of the file.

✅: a green checkmark emoji means I revised/edited the section and it is 99-100% done.

<a id="back-to-top"></a>

## Table of contents

1. ✅ [Branches](#branches)
   1. [Branches and HEAD](#branches-and-head)
   1. [Checking out old commits](#checking-out-old-commits)
1. ✅ [Merge branches locally](#merge-branches-locally)
   1. [Generating merge commits locally](#generating-merge-commits-locally)
   1. [Merge conflicts](#merge-conflicts)
   1. [Resolving merge conflicts](#resolving-merge-conflicts)
   1. [Using VS Code to resolve conflicts](#using-vs-code-to-resolve-conflicts)
1. ✅ [Pushing branches to your repository](#pushing-branches-to-your-repository)
   1. [Squashing commits](#squashing-commits)
   1. [Deleting branches](#deleting-branches)
   1. [Branch Protection Rules](#branch-protection-rules)
   1. [Remote Tracking Branches](#remote-tracking-branches)
1. ✅ [Stashing your changes](#stashing-your-changes)
1. ✅ [Forking](#forking)
   1. [Fork and Clone Workflow](#fork-and-clone-workflow)
1. [Pull Requests](#pull-requests)
1. [git fetch](#git-fetch)
1. [git pull](#git-pull)
1. [git fetch vs git pull](#git-fetch-vs-git-pull)
1. [Miscellaneous git stuff](#miscellaneous-git-stuff)
   1. [Git config files](#git-config-files)
   1. [Use the raw link](#use-the-raw-link)
   1. [Download a folder from GitHub](#download-a-folder-from-github)
   1. [githubuser](#githubuser)
1. ✅ [Creating a GitHub gist](#creating-a-github-gist)
   1. [Clone or fork a gist](#clone-or-fork-a-gist)
   1. [Editing a gist](#editing-a-gist)
1. ✅ [GitHub pages](#github-pages)

## Branches

![alt text](image.png)

In the beginning you will be working on your default branch which will most likely be `master`, or `main` if you changed the default name. You will definitely be working with branches when you start contributing to other people's repositories, but it would be a good idea to experiment with branches on your own projects.

In the past you would use `checkout` to switch to and/or create branches, but now you should be using the newer `switch` command. Here are common git commands you will use when working with branches:

```bash
# Check which branch you are on and to see all branches:
git branch

# Switch to an existing branch:
git switch branch-name
# Checkout to an existing branch
git checkout branch-name

# Create new_branch and switch to it
git switch -c new_branch

# "Old" way to create and switch/checkout to a new branch
git checkout -b new_branch

# To see the last commit hash and msg on each branch
git branch -v

# Rename a branch but you have to be on the branch you want to rename
git branch -m new-name

# To switch/return to the previously active branch (you may have to commit or stash your changes)
git switch -

# Delete a branch but make sure to switch to a different branch first
# 1. Check what branch you are on
git branch
# 2. Switch to the main branch
git switch main
# 3. Delete "branch-name"
git branch -d branch-name

# 4. Force delete a branch, to delete the branch if it is not fully merged
git branch -D branch-name
```

**NOTE**: `git branch branch-name` will create and switch to `branch-name` assuming you pulled a new remote branch from GitHub which you do not have locally. That won't make sense until you have the opportunity to do it, so ignore this if it is confusing.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Branches and HEAD

- When you make a commit, each commit gets a hash to identify it
- Each commit references at least 1 parent commit that came before it
- Contexts: large projects often work in multiple contexts, e.g.: bug fixes, feature adds, redesign, etc
- You need branches (different contexts) to do all that – and merges will be required
- `HEAD -> Main, origin/main`: `HEAD` refers to `main` – but if you switch to a different branch like `new-feature` then you will see (`HEAD -> new-feature`)
- `HEAD` is a pointer, is a reference to a branch pointer – a branch pointer is where a branch currently is - `HEAD` points to whatever branch you are on
- A branch is just a reference to some commit - the last commit for that branch but `HEAD` follows the current branch being worked on
  - Each branch has a branch reference pointing to where you left off
  - `HEAD` always points to the branch you are on which is pointing to the last commit for that branch – it points to the "Tip" of the branch
- The branch with an asterisk (`*`) is the branch you are currently on
- When you create a new branch it is based off of the `HEAD`, where you currently were on `main`
- If you run `git log` you will see (`HEAD -> main, newbranch`) – you see the `new-branch` because it is at the same commit, it is pointing to the same commit as main
- When you make a change on `new-branch` and add, commit and then do `git log`, you will see `HEAD` pointing to `new-branch`

```sh
# See detailed information on commits:
git log
# Abbreviated version
git log --oneline
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Checking out old commits

```sh
# to view a previous commit
git checkout abc1234
# switch to a branch to reattach HEAD
git switch main
```

- `git checkout abc1234`: to view a previous commit – you can use `git log` or `git log --oneline` to view commit hashes – you need the first 7 digits of a commit hash

**detached HEAD**:

Any checkout of a commit that is not the name of one of your branches will result in **_detached HEAD_**. When we run git checkout origin/blah, we are no longer on a local branch. HEAD is pointing to a floating commit that is not rooted to any local branch

- If you do git log, you won't see any commits after the one you checked out with
- If you do git status you see HEAD detached at 0db14ae
- Normally, HEAD points to a particular branch reference – amd the branch reference points to the tip of the branch, the most recent commit – HEAD is always pointing to a branch – the branch you are currently on – HEAD refers to a branch reference NOT to a commit - the branch reference points to a commit
- But when you run `git checkout commithash` you have HEAD refer to a commit NOT to a branch reference – it’s not a normal "state" – you are technically now NOT on a branch

You have 3 options at this point:

1. You can examine the contents of the old commit – leave and go back to wherever you were before – or create a new branch and switch to it; and make and save changes
2. Leave and go back to main - reattach HEAD
3. Create a new branch and switch to it and do work from that point - you can pick a previous commit then branch off at that point to try something else - you will not have any of the changes from commits that happened after that commit

- To go back to main/master you just have to switch/checkout to main/master

```sh
# Go to the commit before current HEAD
# Puts you back into detached HEAD
# Same as git checkout abc1234
git checkout HEAD~1
# go back 2
git checkout HEAD~2
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Merge branches locally

Most of the time you will push your branches with the changes on it to your own repo, or to a repo that you are contributing for which creates a Pull Request (PR). But sometimes you will merge branches locally.

2 merging concepts:

- You merge branches not specific commits
- You always merge to the current `HEAD` branch – you merge to where you are

1. checkout/switch to master/main or the branch you want to merge to -> move over to the RECEIVING branch
2. `git merge branch-name` – `main` is catching up to the same commit as the new branch – so now `main` and `branch-name` are both ponting to the same commit

```sh
# MERGING BRANCHES
# 1. Move to the receiving branch
git switch main

# 2. Merge branch-name into receiving branch (main)
git merge branch-name
```

- That is called a "Fast Forward Merge", and that is what you will see in the terminal - no merge commit is needed with fast forward merges
- A fast forward merge is a simpler merge to perform - when nothing has been changed on `main` so you just merge in the changes from the new branch
- All git does is move the `HEAD` pointer up the number of commits
- After the merge `branch-name` still exists and you can continue working on it

**`git merge` is one of the most important features of git**

> Look into `Merge made by the 'ort' strategy.`

### Generating merge commits locally

You will have a merge commit when there are changes on main that are not on your branch and/or changes on your branch that are not on main.

- git may not automatically be able to do the merge for us – it depends on conflicts.
  - if the same line(s) were changed in both
  - if the same lines were not edited then it can happen automatically
- git makes a commit for us: when that happens a merge commit is generated and we need a msg – and that commit will have 2 different parent commits
- a file will open in VS Code – git made a commit and created the message _merge branch branch-name_ – you could change that, but all you need to do is close the file to finalize the merge commit
- this happens automatically if there are no conflicting lines.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Merge conflicts

Git can NOT automatically merge the branches when there is a merge conflict – they have to manually be resolved. If there are conflicts after running git merge, you will see a msg like this:

```sh
Auto-merging filename.md
CONFLICT(content): Merge conflict in filename.md
Automatic merge failed; fix conflicts and then commit the result.
```

- This is a multi-step process
  - Git tells us that there are conflicts
  - Then we have to open the files & fix the conflicts
  - Then commit those changes
- The files where there are conflicts are decorated red. Here is an example of what you will see:

```
<<<<<< HEAD
blah blah blah
=======
blah blah blah blah blah blah
>>>>>> branch-name
```

- The content below `<<<<<<< HEAD` and above `=======` is content that came from your `HEAD` branch - the branch you are trying to merge into (Content A)
- The content below `=======` and above `>>>>>> branch-name` is the content from `branch-name` that you are trying to merge in (Content B)
- You need to decide which to keep then delete:
  - `<<<<<<< HEAD`
  - `=======`
  - `>>>>>> branch-name`
  - Content A or Content B

Here are the steps:

1. Open the file(s) with conflicts
2. Edit the file(s) - decide which content to keep (or keep both)
3. Remove the conflict markers (`<`, `=`, `>`, `HEAD`, and `branch-name`)
4. Add changes then commit

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Resolving merge conflicts

When you merge a branch into main or another branch where the same line was changed on both branches, you will get a warning in the terminal AND the file(s) with the conflict will open with conflict marrkers and the line(s) in question

- `HEAD` starts with `<<<<` and ends with `=====`
- Below that is the file changes you are trying to merge into main – do you want:
  - Just the main changes
  - Just the branch changes
  - Or BOTH or some combination of both?
- Make that choice and remove the conflict markers then save the file(s)
- Run `git status` which shows the terminal msg: "_You have unmerged paths. (fix conflicts and run "`git commit`") (use "`git merge --abort`" to abort the merge)_"

```sh
git add modifiedfilename
git commit -m "merged test-branch"

# Abort the merge
git merge --abort
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Using vs code to resolve conflicts

- Use `git status` on each brach as a check
- In VS Code there is a built in interface – you don’t have to manually delete the conflict markers
- Above the `HEAD` line are 4 options you can click:

1. Accept Current Change
2. Accept Incoming Change
3. Accept Both Changes
4. Compare Changes

If you click _Compare Changes_, whatever was changed last is highlighted red, and the first file is highlighted green. Sometimes you need to add code and work with both files to resolve the conflict.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Pushing branches to your repository

Use these commands when pushing the committed changes for your new branch:

```sh
# check what branch you are on
git branch
# create and check out to new_branch
git checkout -b new_branch
# make changes, add, commit, push
git status
git add .
git commit -m "commit msg"
git push --set-upstream origin new_branch
```

See details.md for notes on `--set-upstream`. Then after setting the upstream for your new branch you can do the usual commands. This is assuming that you have additional work on your new branch after your initial push:

```sh
git add .
git commit -m "fixes on new_branch"
git push
```

Then back on the repo main page:

1. Click the **Compare & Pull Request** button.
1. Clicking it takes you to a page titled "_Open a pull request_" where you can add a description.
1. Then click the "_Create pull request_" button.
1. That takes you to the "_Pull requests_" tab where you can click the _Merge pull request_ button
1. And finally, click _Confirm merge_ if you are done working on your branch, or you can continue to work and push changes from your branch. In that case, you do not want to merge and confirm.

**Note**: A _Pull Request_ from your branch to the master branch is a request to have your code merged with the master branch. You can, and should (see below), delete your branch when your code/changes are merged.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Squashing commits

If you have multiple commits for that branch, select _Squash and merge_ option from the dropdown list under _Compare and merge_:

- Click `Squash and merge` btn > click `Confirm squash and merge` then delete the branch
- Go back to the code view for the repo and you will see a new hash

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Deleting branches

Once you are done working on a branch, and merged it locally or pushed the final changes to GitHub, then you should delete the branch.

- `git branch -d branch-name`: you can’t be on that branch and it must be fully merged with master
- `git branch -D branch-name`: to delete it if it is not fully merged
- `git branch -m new-name`: to rename a branch but you have to switch to the branch you want to rename
- `-d` = `--delete`
- `-D `= `--delete --force`
- `-m` = `--move` -> move/rename
- To delete a remote branch, use git `push --delete` or just `-d`

```sh
# Delete branch, must be fully merged with main, must not be on that branch
git branch -d branch-name

# Delete it if it is not fully merged
git branch -D branch-name

# Rename a branch, you have to switch to the branch you want to rename
git branch -m new-name

# Delete a remote branch
git push origin --delete branch-to-delete
# or this
git push origin -d "branch-to-delete"
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Branch Protection Rules

> _Define branch rules to disable force pushing, prevent branches from being deleted, or require pull requests before merging. Learn more about repository rules and protected branches_.

You want to add branch protection rules if you have collaborators. If you are just starting out with Git/GitHub, skip this section until you are more comfortable with the whole process

- Go into Settings > Branches Click _Add branch ruleset_ or _Add classic branch protection rule_

**Add classic branch protection rule** option:

- The first thing you are asked is a branch name pattern - it can be complicated for large repos but just do `main` or `master`
- Check "_Require pull request reviews before merging_" - that means commits have to be made to a non-protected branch and then submitted via PR
  - Then select the number of people needed to approve the PR

**Add Ruleset** option:

- Enter _Ruleset Name_ (required)
- Select option for Enforcement status: either Disabled (default) or Active
- Bypass list: Exempt roles, teams, and apps from this ruleset
- Target branches: Which branches should be matched?
- Rules > Branch rules: check/uncheck for what you need.
  - _Restrict deletions_ and _Block force pushes_ are checked by default.
- Click Create

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Remote Tracking Branches

- `git fetch` and `git pull` both deal with getting changes from a public repo
- When you clone a repo you get all the commits, the files, and the branches + git is initiated
- But there are 2 branch references for main/default – and the one basic one is just main
  - The remote has just `main`, but your local cloned repo has main and `origin/main`
  - `origin/main` is the "Remote Tracking Branch" - a reference and it points back to the last commit on the origin remote
- When you have origin/main, that is a "remote tracking brach reference" – it's just a pointer but it doesn’t move because it is pointing back at the last known commit on the main branch from the origin remote
- As you make commits on your local version, main and origin/main will diverge – main will move with the local commits but origin/main will not
- Remote Tracking Branch: the bookmark/pointer that remembers at the last time you communicated with this remote repo, here is where the default branch was pointing on that github repo on origin – they follow this pattern
  - `<remotename>/<branchname>`:

1. origin/main references the state of the main branch on the remote repo named origin
2. upstream/logo references the state of the logo branch on the remote repo named upstream

- `upstream` is another common remote name besides `origin`
- Use `git branch -r` to view the remote branches your local repo knows about: origin/main

> `origin/main` is the remote tracking branch

```sh
# View the remote branches your local repo knows about, shows all the remote branches from the clone
git branch -r
```

**checking out remote tracking branches**:

> "_Your branch is ahead of 'origin/master' by 1 commit._"

- Now main and origin/main are not pointing at the same thing – that's normal – it's so you know how far ahead you are – run `git checkout origin/main`:

```sh
# See where you were before making commits
# puts you in detached HEAD
git checkout origin/main
```

Then you will see:

> "_You are in 'detached HEAD' state. You can look around, make experimental changes and commit them, and you can discard any commits you make in this state without impacting any branches by switching back to a branch._"

- You can undo this operation with `git switch`
- If you want to reference where the remote is use origin/main or whatever name/branch you have
- Whenever you clone, whatever the default branch is that is what you get – you get all the data including the branches but it’s not all in your workspace at once

How do you make a local branch connected to origin/branch-name?

- When you do `git switch branch-name`, git will create a branch with that name and automatically track the remote branch `origin/branch-name`
- Normally when you try to switch to a branch that does not exist you get "fatal: invalid reference ...", but not for branches that exist on the remote repo you cloned

```sh
# This shows all the remote branches from the clone
git branch -r

# This creates a local branch named branch-name and track origin/branch-name
git switch branch-name

# The old way of doing that
git checkout --track origin/branch-name

# Switch your local to to a commit/state for a remote-tracking branch
# Results in "detached HEAD", you are no longer on a local branch, but directly on a commit
git checkout origin/branch-name
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Stashing your changes

The `git stash` commands are easy and should be in the beginner file, but you only use them when you start working with branches. Creating and merging braches locally are also beginner level _unless_ you make a mistake. That's why stashing and branches are in this file.

The `git stash` command is used when you have more than 1 branch and you need to switch to a different branch. It's doubtful you will need this command unless you are contributing.

There are 2 scenarios when you try to checkout/switch without committing your changes:

1. the changes come with you to the destination branch-name
2. git won't let you switch if there are potential conflicts

If you have changes in your files, you will not be able to switch to a different branch unless you `commit` or `stash` those changes. If you are not ready to `commit` your changes then you should `stash` them.

Actually, Git won't let you switch if there are potential conflicts between files and you will see the following message in the teminal:

> Please commit your changes or stash them before you switch branches.

These are the main commands ou will use:

```sh
# Stash your changes with:
git stash
# FYI, that command is short for
git stash save
# Then to bring the changes back (un-stash them) use:
git stash pop
```

Other useful stash commands are:

```bash
# Show all your stashed files
git stash list
# cleasr your stash (be careful using this one)
git stash clear
```

- `git stash` or `git stash save` – takes uncommited changes, staged or unstaged, and stashes/hides them and it reverts those changes in your working copy – you can retrieve them later
  - It removes your changes but saves them for later
- `git stash pop` – to remove the most recently stashed changes in your stash and reapply them to your working copy – or you can reapply them to a different branch
- NOTE: `index` is what git calls the staging area
- Run `git stash` and in the terminal you will see:

> "Saved working directory and index state WIP on test: 0282ecd Added Colt's notes to new files"

- The 7-digit hash is the first 7 chars on your last commit

**git stash apply & git stash list**:

- 90% of the time he only uses `git stash` and `git stash pop`
- `git stash apply` – to apply whatever is stashed away WITHOUT removing it from the stash – useful if you want to apply stashed changes to multiple branches

```sh
# Run on a different branch but you may get conflicts
git stash apply
```

- You can add multiple stashes onto the stack of stashes – they will be stashed in the order you added them – he rarely does this – SKIP
- `git stash list` – to view all your stashes – terminal shows stash@{0}...stash@{1}
- It starts at 0 so zero-based and it gives the most recent commit when you made the stash
- However, no one really does multiple stashes on the same branch -

- If you do git stash pop, that will pop off the stash with the highest index #, or the first stash you did, not the latest stash – you may not want that so do:
  - `git stash apply stash@{2}` – where 2 is the stash ID -

```sh
git stash list
# where 2 is the stash ID
git stash apply stash@{2}
```

**dropping & clearing the stash**:

- `git stash drop stash@{2}` to delete the stash with an ID/Index of 2
- `git stash clear` to empty out everything in the stash

```sh
git stash drop stash@{2}
git stash clear
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Forking

This is another workflow – instead of one centralized github repo, every developer has their own github repo in addition to the "main" repo. Read the GitHub page [Fork a repo](https://docs.github.com/en/get-started/quickstart/fork-a-repo) for the same steps as shown below.

> **_Developers make changes and push to their own forks/versions before making pull requests_**

- This is common on large open source projects where there may be 1000’s of contributors but only a few maintainers
- The Fork & Clone workflow enables ANYBODY to try and make a contribution – you don't need permission because you make your own copy – then you make a PR
- FORKS: a personal copy of someone else's repos in your account – the copy is called a "fork"
- It's your repo now and you can do whatever you want or you can start making open-source contributions

If you only clone a repo, you can't make changes and commits then push them up to that repo - you don't have permission. If you want to make changes and push them up to GitHub, then fork the repo and push to your forked version. Then you can clone your fork and the remote will be set to push to your copy of the repo. If y ou only cloned, pushing changes would go to the original repo.

How to fork:

1. Go to a repo that you like and click the Fork button on the top right. You will be taken to a copy/fork of that repo but in your account.
2. You clone it which sets up the remote to push to your copy

After you fork a repo, open up a terminal and navigate to the folder where you want the cloned repo and run:

```sh
# Create local clone
git clone https://github.com/Your_User_Name/repo_name

# Move into that folder
cd folder_name
```

Next, check the remote reference then add a remote reference to the main forked repo:

```sh
# Check to see that the remote origin is set to your fork
git remote -v

> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)

# Sync your fork with the upstream repository
git remote add upstream https://github.com/ORIGINAL_OWNER/their-repo-name.git
```

`git remote -v` for a clone shows the source repo but for fork & clone it shows your copy.

**NOTE**: `git fetch` is typically used to get the latest changes from the remote repo without merging them into the main branch.

To verify the new upstream repository you have specified for your fork, type `git remote -v` again:

```sh
git remote -v
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
> upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
> upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)
```

My final commands:

```sh
git clone https_url
cd folder_name
git remote -v
git remote add upstream https_url
git remote -v
git status
git switch main
```

Finally:

1. Check the branch you are on and switch to main/master if not on that branch,
2. Create a new branch for your contributions, make your changes then
3. Check the status, add your changes, check status again, commit the changes, and then push the changes:

```sh
git branch
git checkout -b fix/something
# or
git switch -c fix/something
git status
# make changes then the usual
git add .
git status
git commit -m "short description"
git push --set-upstream origin fix/something
# or
git push -u origin fix/something
```

Then just use `git push` for future pushes.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Fork and Clone Workflow

In your forked copy you will see messages like "This branch is 1 commit ahead of username:master", or whatever the number is based on your commits. You can ignore that and not do anything with the original repo. Or you can attempt to share your work by making a PR to the source repo.

1. Click the _Pull request_ link/button
2. Click the green _Create pull request_ button
3. Add any information you feel is important for the repo owner about your PR

Then the repo owner can choose to merge your PR or close it without merging.

> THAT IS THE POINT OF FORKING - TO CONTRIBUTE TO AN OPEN-SOURCE PROJECT!

Or you may see that you are "X" number of commits behind "username:master", in which case you should update your version.

Remember, for `git clone` you need to set the remote for your github repo or else you will push to the repo you cloned. Recap:

1. First you fork which creates a copy in your GitHub acct
2. Then you clone the forked repo in your account down to your machine and it will point to your remote copy when you push and pull

- **ORIGIN** = refers to your forked copy in your github acct – origin is the default remote name
- But you want to set up a second remote, normally you call it `upstream` hich refers to the original repo your forked
- **UPSTREAM** = to the source, where you forked it from – you need to set up a 2nd remote – you need to get the changes from the source down to your machine – you can't push but you can pull
- You push to your origin in your acct

Fork & clone allows a project maintainer to accept contributions from developers all around the world without having to add them as actual owners of the main project repo or worry about giving them all permission to push to the repo.

The process:

1. Make changes locally then push to your fork
2. Make a Pull Request to the source repo
3. Update your local copy with git pull for changes on the source repo
4. Continue working and repeat

> Pull from source > Push to your copy > make PR > Repeat

1. Fork the project
2. Clone the fork
3. Add upstream remote
4. Do some work
5. Push to origin
6. Open PR

You don't need to create a fork for every project you are working on. It's a good idea to go this route if you don't want to give contributors access to your repo.

To add the upstream, go to the source repo and copy the URL:

```sh
# Set upstream so you can pull changes to your machine
git remote add upstream original_url

# Check the remotes
git remote -v
# You will have 2 origin remotes pointing to your acct (fetch & push) and 2 upstream remotes pointing to the original/source (fetch & push)

# Then to get changes
git pull upstream main

# Then make changes to your local copy and
git add .
git commit -m "message"

# Push to your copy
git push origin main
# Or
git push
```

Now you are ahead of the last known copy of the original source repo. Then create a pull request to the original source – from your fork to the original.

`git remote -v` will show:

```sh
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
> origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
> upstream  https://github.com/SOURCE_USERNAME/THEIR_REPO_NAME.git (fetch)
> upstream  https://github.com/SOURCE_USERNAME/THEIR_REPO_NAME.git (push)
```

To make a pull request to the original project:

1. Click _Pull request_
2. Add description for the PR
3. Click the green button _Create pull request_

It's then up to the source repo owner to merge the PR in or not.

> Make sure you are going from `feature_branch` to `main` (or whatever branch to branch you want) by looking at the fields _base repository_ and _head repository_ at the top of the "Open a pull request page".

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Pull Requests

> coming soon - check the section on PRs in `ADVANCED_GIT.md`

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git fetch

> COMING SOON

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git pull

> COMING SOON

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git fetch vs git pull

> COMING SOON

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Miscellaneous git stuff

### Git config files

Git looks for the following config files:

1. LOCAL config file: `.git/config` and applies only to that repo - OR
2. GLOBAL config file: `~/.gitconfig` or `~/config/git/config` - OR
3. SYSTEM config file: if you have multiple users on one machine, config settings applies to all of those users

GLOBAL:

- Any config variables you change in the file or from the command line will be applied across all git repos, e.g.: `git config --global user.name "Your name"`
- The global config file is in a `~/.gitconfig` file and in the home directory by default – `C:\Users\pc\.gitconfig`
- You can open it up to edit or print it out using `cat ~/.gitconfig`
- Also try `git config --list` to see all the settings
- Aliases are the most important thing to update in that file – but most commonly you will set `user.name`, `user.email`, `init.defaultBranch` and `code.editor`

```sh
# Example of the contents in ~/.gitconfig
cat ~/.gitconfig
[user]
        email = somename@gmail.com
        name = Some Name
[core]
        editor = code --wait
[init]
        defaultBranch = main
[color]
        ui = auto
```

LOCAL:

- The LOCAL config file is inside the .git folder for each of your repos: `.git/config`
- Every repo has that file - if you put something in that file it will only be for that one repo
- This is also where you can add git aliases for a particular repo
- You can have customization for one repo that won't affect other repos
- Check out [Git Config docs](https://git-scm.com/docs/git-config)
- `--global` for global settings and `--local` for local/repo settings

```sh
# Set user.name globally (what you should have already done)
git config --global user.name "name"

# Set user.name in local config file
git config --local user.name "name"
```

> Developers often share their config files so look at what other people set

### Use the raw link

**Tip**: `raw` link - If you want to copy the code for a file, click the `raw` button. That will load all the code onto a white/blank webpage and you just need to do <kbd>CTRL</kbd>+<kbd>C</kbd> to copy all the contents. That is way easier than trying to select the code and maybe missing some of it.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Download a folder from GitHub

This does not involve any git commands but it can be useful if you need images from a repo but do not want to clone the entire repo or download a zip file.

Go to [GitHub Download on GitKraken](https://www.gitkraken.com/learn/git/github-download) and scroll down to _How to Download a Folder from GitHub_. There is a link to [download-directory](https://download-directory.github.io/) where all you have to do is paste in the link to the folder you want to download.

### githubuser

If you need to paste a screenshot into an issue or pull request description field, you can just copy the screenshot and paste into the field. In the past, if you inspected the image `src` it had `githubuser`. However, that must have

I just did that on the Discussions tab for a new post and got this:

```html
<!-- github.com/user-attachments -->
<img
  width="208"
  height="298"
  alt="image"
  src="https://github.com/user-attachments/assets/38221e73-db58-4b84-bf04-bc1180cb752b"
/>
```

I don't know when they changed it but now part of the `src` is `github.com/user-attachments`. That's better than pushing up images only for your markdown files, but then you will have to edit the markdown file(s) on GitHub!

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Creating a GitHub gist

These are not git commands, rather they are a way to have code on GitHub that is not a stand-alone repository. People ceate them because they are chunks of code that other people can use.

To search for a gist on GitHub: `https://gist.github.com/username/` or just `https://gist.github.com/`

**<ins>What is a Gist?</ins>**

They are basically code snippets to save/store and share. Gists do not have Issues, PR's, Projects or Actions. If you have a simple JavaScript function that is not part of a project, then that would be something you could add to its own gist. From Github:

> Every gist is a Git repository, which means that it can be forked and cloned...and you will see it in your list of gists when you navigate to your gist home page. They're also searchable, so you can use them if you would like other people to find and see your work.

Besides being able to fork and clone gists, you can also:

- Leave comments
- Star them
- Download them
- Share them
- Embed them
- Have collaborators
- See revisions and diffs (history)

1. Navigate to your [gist home page](https://gist.github.com/) and click the `+` button - OR -
1. Click the down arrow next to your profile image thumbnail > click _New Gist_
1. Type a description and file name with extension for your gist (you want the extension for code highlighting).
1. Optionally, you can change the Indent Mode, Indent Size, and if you want it to Wrap or not.
1. Type or copy the code/text of your gist into the gist text box
1. When done Click either `Create secret gist` or `Create public gist`

**NOTE**: For the gist filename just make something up. For example, if you have a JavaScript function that takes a blog post title and converts it to a URL string, then give it a name like `BlogTitleUrl.js`.

Then you can get the Share link for the gist to share with people or to add to an online article. When you choose `Embed` and add the link to an HTML page it will output as a formatted code block (not for all sites though).

You can add code blocks or other files for your gist by clicking _Add file_.

**Public gists** can be found on the Discover page. Just click _All gists_ from the menu bar and they are listed in reverse chronologial order of creation date. You can also search for gists by keywords, add comments on gists you found, and have comments on your gists.

**NOTE**: You can create a gist if you are not signed into GitHub but it will be an anonymous gist which you will not be able to edit or delete. I don't know why you would want to do that but you can if you want to.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Clone or fork a gist

Your options from the dropdown list after creating your gist are to _Embed_, _Share_ or _Clone_ the gist. If you want to clone the gist then in your terminal do:

```shell
git clone gist_url
```

If you choose to _fork_ someone else's gist then it will show on your gist home page similar to how forked repos will show in your repositories.

### Editing a gist

Just click the Edit button while in your gist and edit the code as you see fit. There is also a delete button next to edit if you want to delete your gist.

When done editing click the _Update public gist_ button. Click the _Revisions_ link to see your changes. Remember that your gists are also repositories. You can go pulls and pushes.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## GitHub pages

Use [GitHub Pages](https://pages.github.com/) to host your portfolio or a live version of your app(s). Other options would be to use Netlify or Vercel. Portfolios, personal websites, projects, documentation all are good reasons to use these

Links:

- **NOTE**: https://pages.github.com/ redirects to [GitHub Pages documentation](https://docs.github.com/en/pages)
- [Quickstart for GitHub Pages](https://docs.github.com/en/pages/quickstart)
- [Creating a GitHub Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)

There are 2 types:

1. User sites, and
2. Project sites

> Because https://pages.github.com/ redirects to a new page, I'm not sure if ths is true anymore, or the page describing both is unavailable at this time?!?

- Project sites: for every repo you can have a corresponding website
  - URL pattern: `username.github.io/repo-name` – one per project
- User site: `username.github.io` – you can only have 1 per GitHub account
- You can have a website or just markdown files like docs
- To setup a website go into one of your repos > select a branch (`main`/`master` but it could be any branch)
  - It would be good to have a branch solely for the GitHub page and the main branch is for your code and docs
- You need to tell GitHub that the branch contains a website, specificall an `index.html` file
- Then go to the Repo _Settings_ tab > in the left sidebar look for _Pages_ under _Code and automation_ > go the the _Branch_ subheading where it says:

> "GitHub Pages is currently disabled. Select a source below to enable GitHub Pages for this repository"

- Then select the branch you want
- The old convention was to name the branch `gh-pages` so use that and keep main for your `project/portfolio` – but you can name the branch anything
- Make sure your `index.html` file is either in the root or a `/docs` folder – tell GitHub where it is
- Any time you update the `gh-pages` branch (or whatever page you chose) your website will update

> Open a browser and go to https://username.github.io

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>
