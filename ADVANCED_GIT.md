# Advanced Git Commnads

Some of these commands or actions on GitHub are intermediate level, others are advanced or very specific.

This file used to be very short but I added sections from the intermediate file, plus a lot of notes from [Colt Steele's Git Bootcamp course](https://www.udemy.com/course/git-and-github-bootcamp/). As a result, I believe I have duplicates and very _sloppy_ notes. I'll clean this file up when I get time.

✅: a green checkmark emoji means I revised/edited the section and it is 99-100% done.

<a id="back-to-top"></a>

## Table of contents

1. ✅ [Fixing mistakes](#fixing-mistakes)
   1. [Remove unstaged changes](#remove-unstaged-changes)
   1. [Remove staged changes](#remove-staged-changes)
   1. [Remove commits](#remove-commits)
   1. [Remove remote origin](#remove-remote-origin)
   1. [Remove a file from git tracking](#remove-a-file-from-git-tracking)
   1. [Remove a file from GitHub](#remove-a-file-from-github)
   1. [Remove git](#remove-git)
1. ✅ [git restore](#git-restore)
1. ✅ [git reset](#git-reset)
1. ✅ [git revert](#git-revert)
1. ✅ [git rebase](#git-rebase)
   1. [Comparing merging and rebasing](#comparing-merging-and-rebasing)
   1. [When not to rebase](#when-not-to-rebase)
   1. [Handling conflicts and rebasing](#handling-conflicts-and-rebasing)
   1. [Interactive rebase](#interactive-rebase)
1. ✅ [restore vs reset vs revert vs rebase](#restore-vs-reset-vs-revert-vs-rebase)
1. ✅ [git log](#git-log)
   1. [what is HEAD](#what-is-head)
1. [git diff](#git-diff)
1. [git show](#git-show)
1. ✅ [git reflog](#git-reflog)
1. ✅ [git tag](#git-tag)
   1. [Semantic Versioning](#semantic-versioning)
   1. [Viewing and searching tags](#viewing-and-searching-tags)
   1. [Comparing tags with git diff](#comparing-tags-with-git-diff)
   1. [Creating and working with tags](#creating-and-working-with-tags)
1. [GitHub Issues](#github-issues)
   1. [How to create an issue](#how-to-create-an-issue)
   1. [Closing an issue](#closing-an-issue)
1. [GitHub pull request process](#github-pull-request-process)
   1. [Pull request title](#pull-request-title)
   1. [Pull requests page notes](#pull-requests-page-notes)
   1. [Replies to your pull request](#replies-to-your-pull-request)
   1. [Code comments](#code-comments)
1. [Staying up to date](#staying-up-to-date)
1. ✅ [Terminal commands](#terminal-commands)
1. [GitHub Two Factor Authentication](#github-two-factor-authentication)
   1. [Two-factor authentication recovery codes](#two-factor-authentication-recovery-codes)
1. [Signed Commits](#signed-commits)
1. [ci cd pipeline](#ci-cd-pipeline)
1. [Code reviews](#code-reviews)

## Fixing mistakes

You will make mistakes from time to time. Here are ways to fix the most common mistakes.

### Remove unstaged changes

```sh
# Discard changes in a single file:
git checkout HEAD filename
# alternate syntax
git checkout -- file1
git checkout -- file1 file2

# or (newer Git versions prefer):
git restore filename

# restores the contents of filename to the state prior to HEAD
# use HEAD~# or 7-digit commit hash
git restore --source HEAD~1 filename
git restore --source abc1234 file1 file2

# Discard all unstaged changes: This resets files back to what’s in your most recent commit
# ⚠️ Careful: this will delete your work if you haven’t saved it elsewhere.
git restore .
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Remove staged changes

Remove **staged** changes: changes you’ve already added with `git add`, but haven’t committed yet

- With no commit reference, using just `git reset` Git assumes:
  - Reset the index (staging area) to match the current HEAD
  - Leave the working directory alone
- That means everything you staged gets unstaged, but your file changes stay on disk
- It's basically shorthand for `git reset --mixed HEAD`

```sh
# Unstage a single file
git reset HEAD filename

# or (newer Git):
# Unstage a single file
git restore --staged filename

# With filename and optional path
git reset path/filename.ext

# Unstage everything:
git reset
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Remove commits

Use git reset again but include HEAD which means the last commit. But to undo the last commit add ~1 to go back 1 commit past the last commit which will undo the last commit.

```sh
# Run the following to get a specific commit hash
git log --oneline
```

1. Undo the commit but keep changes staged - Useful if you committed too early but still want to keep all those changes staged for a new commit:

```sh
git reset --soft HEAD~1
```

2. Undo the commit and unstage changes (keep them in working directory) - If you want to undo the commit and put the changes back into your working directory - commit gone, staging cleared, but your edits still sit in your working directory:

```sh
# This is the default for git reset if you don’t specify --soft or --hard
git reset --mixed HEAD~1
# same as
git reset HEAD~1
# using a specific commit
git reset <commit-hash>
```

3. Undo the commit and discard changes completely - If you want to undo the commit and throw away all changes:

```sh
# ⚠️ This permanently deletes changes that weren’t pushed anywhere.
git reset --hard HEAD~1
# using a specific commit
git reset --hard <commit-hash>
```

But what if you want to go back a number of commits or to a specific commit. First use `git log` or `git log --oneline` which gives you a list of your commits in reverse chronological order. You can scroll down the log with <kbd>SPACEBAR</kbd>.

4. Undo a commit that’s already pushed (safe way) - If you’ve already pushed and want to undo without rewriting history:

```sh
# Use git reset with the commit HASH:
git reset <commit_hash>
git reset e220bfb1e34b8c6b6fce1deb7884244239284716
```

That will unstage any changes made to the file(s) AFTER that commit. The changes will be in your files but they will not be saved into git anymore. But how do you get rid of all the changes after a certain point? Use the same command but add the flag --hard:

```sh
git reset --hard e220bfb1e34b8c6b6fce1deb7884244239284716
```

**Git reset summary**:

- `git reset` (no args) = unstage all files
- `git reset HEAD <file>` = unstage just that file
- `git reset --mixed HEAD~1` = undo the last commit but keep changes (unstaged)

### Remove remote origin

I once pasted in my repo link ending in `.gi` instead of `.git` because I missed copying the `t`. Use the following to remove the origin and try again:

```sh
git remote remove origin
```

### Remove a file from git tracking

If you want Git to stop tracking a file but keep it locally, use:

```sh
git rm --cached filename.ext
```

Without the flag `--cached`, Git would remove the file (delete) from t he working directory.

Pair this with adding the file (or its pattern) to `.gitignore` so Git doesn’t stage it again. This is especially useful for sensitive files like `.env` or directories such as `node_modules/` that should stay local but not be version-controlled.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Remove a file from GitHub

> I'm not sure if this command is correct

I used the following command to remove a file from GitHub that had a different case from my local copy. I mistakenly created my file name as `errorMiddleWare.js` where the `W` should have been lowercase `w`. I made the change to my local filename but the filename on GitHub maintained the uppercase `W`. Here is the command I ran to fix that followed by an explanation of the command:

```sh
git rm -r --cached .
```

1. `git rm`: used to remove individual files or a collection of files
2. `-r`: shorthand for 'recursive'. When operating in recursive mode git rm will remove a target directory and all the contents of that directory
3. `--cached`: specifies that the removal should happen only on the staging index. Working directory files will be left alone

I thought the entire project was deleted and then added to staging because EVERY file was highlighted green in VS Code, but that not the case. I can't explain it but use this command if you also have a file where the case changed and the local file and GitHub file do not match.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Remove git

If you really messedthings up and you want to start over, you can remove git tracking from your project folder. To remove git tracking from a folder use the following command in git bash or the terminal in VS Code. Make sure you are in the root folder where you want Git removed:

```sh
rm -rf .git
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git restore

> These notes are not good!

- `git restore` helps with undoing operations
- Use `git restore --staged <file>` to unstage any files you added
- First, you can discard changes since the last commit
- `git restore <file-name>` - to restore the file to the contents in the HEAD – if you have uncommitted changes in the file, they will be lost – it replaces `git checkout HEAD <file-name>`
  - Use if you do not want to include the file in your next commit
- `git restore filename` restores using HEAD as the default source, but you can change that using the `--source` option
- SECOND, you can reference a particular commit
- `git restore --source HEAD~1 <file-name>` - restores the contents of `file-name` to the state prior to HEAD – you can also use a particular commit hash as the source
- So either a commit hash or `HEAD~num` – all the other files and branches are untouched

```sh
# or (newer Git versions prefer):
git restore filename
# NOTE: The above command is not undoable - any uncommited changes will be lost, git has no record of them after this command

# restores the contents of filename to the state prior to HEAD
# so HEAD~1 would be 2 commits prior - you have to use --source
# use HEAD~# syntax or 7-digit commit hash
git restore --source HEAD~1 filename
git restore --source abc1234 file1 file2
# To undo removing changes from the above 2 commands just do
# This goes back to the most recent commit
git restore filename

# Discard all unstaged changes
git restore .

# Remove a file from staging
git restore --staged filename
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git reset

- `git reset` restores a repo back to a specific commit – the commits are gone
  - Moves your project back to a previous commit
- Common if you did work on the master branch but you meant to do it on a new branch
- There are 2 versions: regular and a hard reset
- `git reset <commit-hash>` - restores a repo back to a specific commit, use the 7-digit hash from the `git log --oneline` command
- But that is a regular reset and that only removed the commits – the changes are still in the working directory – you just went back in time by removing commits – to Git, that's where the history stops – but for some reason it kept the changes in the file – WHY IS THAT?
- **Answer**: it's useful if you make commits on the wrong branch – you can keep that work and move it to another branch – how do you do that? By creating a new branch and then adding/committing the changes on that one – this may be what I did when I made a branch on a branch and made changes on that
- `git reset --hard <commit-hash>` - a hard reset that loses all the commits up to that commit hash – AND – the changes are removed from your working directory
- Like `git restore` you can use a commit hash or `HEAD~3` or whatever number
- YOU NEED TO BE CAREFUL USING `--hard`
- Note this is on a per-branch basis

```sh
# Restore a repo back to a specific commit
# This removes the commits but does not remove the work from those commits
# the changes are still in y our working directory
# this is good when you did work on the wrong branch so you want to keep the work but move it to another branch
git log --oneline
git reset <commit-hash>

# Hard reset: loses all the commits up to that commit hash, the changes are removed from your working directory
git reset --hard <commit-hash>
git reset --hard HEAD~1
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git revert

`git revert` is the first command that you would use when dealing specifically with remote repositories. All the commands up to this point are used with local and remote repos, but this one is only for remote repositories with 2 or more contributors.

- `revert` is similar to `reset` in that they both "undo" changes, but they do it in different ways
  - Undoes a previous commit by making a new commit on top of your history
- `git reset hash` actually moves the branch pointer backwards, eliminating commits – as if the commits NEVER occurred
- `git revert` instead creates a brand new commit which reverses/undos the changes from an earlier commit – because it results in a new commit, you have to enter a commit msg – instead of deleting everything, deleting history – that can be a problem if you are collaborating with other people
- With reset, you lose the commits that came after the one you used in the command – they are gone!
- With revert you get rid of the changes but you do not lose the commit for those changes – you have history!
- Sometimes reverting a commit can result in conflicts - manual merge conflict resolution

When to use `reset` and when to use `revert`?

- It has to do with collaboration:
  - If you want to reverse some commits that other people already have on their machines, you should use `revert`
  - If you want to reverse commits that you haven't shared with others, use `reset` and no one will ever know

```sh
git revert <commit-hash>
# This should open a file named COMMIT_EDITMSG to edit the commit msg, then:
git log --oneline

git revert HEAD~1
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git rebase

There are 2 ways to use the `git rebase` cmd:

1. as an alternative to merging – `git rebase` instead of `git merge`
2. as a cleanup tool

You will need to routinely merge changes for the `master` branch for an active open-source repo. As a result, your feature branch will have a lot of merge commits.

There are a lot to this commit to know, understand and think about. This is a huge topic....

1. `git rebase --abort`
1. `git rebase --continue`
1. `git rebase -i HEAD~4 `

Look into `git cherry-pick` for when someone accidentally creates a branch(es) on a branch instead of main, and rebase is not an option.

### Comparing merging and rebasing

The problem with merging, something that rebasing addresses that merging does not:

- You don't want to diverge from main for a long time without getting new changes but you are still working on your feature-branch
- You have to merge your branch with main resulting in a merge commit not a fast forward merge
- You may have to do that multiple times(very active main branch) - that's a bunch of merge commits from main and that muddies your feature-branch's history
- You can instead `rebase` the feature branch onto the main branch - this moves the entire feature branch so that it BEGINS at the tip of the main branch
- Instead of using a merge commit, rebasing rewrites history by creating new commits for each of the original feature branch commits
  - Remember: merge commits have 2 parents!
- Rebasing is another way of combining branches – rebasing rewrites history – you are creating new commits – git creates new commits based upon the original feature branch commits
- You rebase the feature branch onto the master branch
- "re-base" -> a new base for the feature branch
- Feature branch commits are added to the tip of the master branch
- Your feature branch has a new BASE at the tip of the master branch

```sh
# Switch to your feature branch
git switch feature
# rebase the feature branch onto the main branch
git rebase main
```

- `rebase` moves the entire feature branch so that it begins at the tip of the master branch
- Rebasing rewrites history by creating new commits for each of the feture branch commits
- So you still have your feature branch but it looks like its commits are on main – now the merge commits are gone and you have new commit hashes – new history!

**NOTE**: you rebase _ONTO_ master/main

Benefits:

1. It makes it easier for someone to review your feature branch commits
2. You get a cleaner & linear project history
3. No unnecessary merge commits

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### When not to rebase

- **The Golden Rule**: Because rebase rewrites commits, you should NEVER rebase commits that have been shared with others
  - If you already pushed commits to GitHub then **_DO NOT_** rebase them unless you are positive no one on the team is using those commits
  - If you do, it is really hard to reconcile the alternate histories
- You want to rebase commits that you have on your machine and other people don't – you don’t want to rebase the master branch – you can rebase your work onto the master branch – that is not changing the master branch
- The branch that you are on when you call `rebase` is the branch that is rebased
- Don't rewrite history that other people have!!!

> _You are not changing the branch you are rebasing onto The branch that you are on when you call rebase, is the branch that is rebased - you rebase ONTO master_

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Handling conflicts and rebasing

One way to fix a rebase conflict is to run `git rebase --abort` – or resolve the conflict like a normal merge conflict – do in vs code. I do not understand `rebase` that well, even less so for this section. Here are the commands I have:

```sh
# To reset back to before rebase:
git rebase --abort

# Run the following after fixing conflict:
git add/rm <conflicted_files>

# Then run:
git rebase --continue

# To skip this commit/patch:
git rebase --skip

# Run this to see the failed patch:
git am --show-current-path
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Interactive rebase

Use interactive rebase to clean up your git history, to edit commits, to change commit messages, change the contents of a commit, drop or delete an entire commit, ...:

- Common to do before you share your finished feature branch
  - If you have some half complete commits - you can streamline them down before you share the code with anyone
- To do this you do not specify a branch to rebase onto, instead you use the `-i` flag which enters the interactive mode which allows you to edit comments, files, drop commits, etc
- You need to specify how far back you want to rewrite commits – you are not rebasing onto another branch, you are rebasing a series of commits onto the HEAD they currently are based on:

```sh
git rebase -i HEAD~4
```

When you enter that cmd you will get a list of your commits preceded with a cmd:

- `pick`: use the commit (the default) – `p` – keep this commit as is
- `reword`: use the commit, but edit the commit msg – `pr`
- `edit`: use commit but stop for amending – `e`
- `squash`: use commit contents but meld it into previous commit – `s`
- `fixup`: like "squash", use commit contents but meld it into previous commit & discard the commit msg – `f`
- `drop`: remove commit – `d`
- Other less ommon types: exec, break, label, reset, merge
- NOTE: you can use the word or the letter, so `fixup` or just `f`
- Notice that the commits order is reversed - the first one is the last one

```sh
git log --oneline
git rebase -i HEAD~#

# Example output
pick 0e19c7a initial commit
pick cbee26b addproject files
pick 519aab6 add basic HTML boilerplate
pick 240827f add bootstrap
fixup 6e39a76 forgot to add bootstrap js script
pick 4ff2290 add top navbar
fixup 2a45e71 fix navbar typos
fixup 655204d fix another navbar typo
pick 63ff2f1 create README.md

# 1. The fixup for "forgot to add bootstrap js" will add that commit to the commit before it "add bootstrap" and remove the commit message for 6e39a76
# Result (I think t he commit hashes after the fixup are changed?!?)
pick 0e19c7a initial commit
pick cbee26b addproject files
pick 519aab6 add basic HTML boilerplate
pick 240827f add bootstrap
pick 4ff2290 add top navbar
fixup 2a45e71 fix navbar typos
fixup 655204d fix another navbar typo
pick 63ff2f1 create README.md

# 2. The 2 fixups for "fix another navbar typo" and "fix navbar typos" will have their commit messages removed and the commit content added to "4ff2290 add top navbar"
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## restore vs reset vs revert vs rebase

- `restore` = fix your working directory or staging area.
- `reset` = move your branch pointer (and maybe staging/working directory depending on flags).
- `revert` = create a new commit that undoes another.
- `rebase` = rewrite commit history by moving or combining commits onto a new base commit.

1. `restore`: Used to restore the contents of a file (or multiple files) from a commit, or to unstage changes without touching commit history.
   1. `git restore <file-name>` → throw away uncommitted changes in the working directory, restore file from HEAD.
   1. `git restore --source <commit-hash> <file-name>` → restore the file’s content from a specific commit.
   1. `git restore --staged <file-name>` → unstage the file (move it back to working directory, keep changes).
1. `reset`: Moves the branch pointer to a specific commit
   1. **`reset` rewrites history**.
   1. Can eliminate commits from history (if using `--hard` or `--mixed`).
   1. Can be destructive if those commits have been pushed and others depend on them.
   1. Think: "rewind history to this point."
   1. `git reset <commit-hash>` → default `--mixed`, moves branch pointer and keeps changes staged → unstaged.
   1. `git reset --soft <commit-hash>` → moves branch pointer but keeps changes staged (as if you hadn’t committed yet).
   1. `git reset --hard <commit-hash>` → moves branch pointer and wipes out changes (staged + working directory).
1. `revert`: Creates a new commit that undoes the changes from a previous commit (or range of commits).
   1. **`revert` preserves history**
   1. Does not move the branch pointer backwards.
   1. Safe for shared branches, because history is preserved.
   1. Think: "apply an opposite patch.""
   1. `git revert <commit-hash>` → creates a new commit that undoes the changes from that commit.
   1. `git revert -n <commit-hash>` → “no commit,” stages the revert so you can review/edit before committing.
   1. `git revert <old-commit>..<new-commit>` → revert a range of commits in one step.
1. `rebase`: An alternative to `git merge` or a cleanup tool for merge commits. Reapplies commits from your branch on top of another branch, creating a linear history instead of a merge commit. Can also be used interactively to clean up commit history.
   1. `git rebase main` (or `git rebase <branch-name>`) → replay commits from current branch onto the tip of `main`.
   1. `git rebase -i HEAD~4` → interactively edit, fixup, squash, reword, or drop the last 4 commits.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git log

> Lots of confusing notes in this section...

Check the [Git Docs](https://git-scm.com/docs).

- `git log` is a log of the commits for your local repo
- you need the commit hashes – you need those to redo a commit, to checkout, to look at a commit, etc
- to configure it so you can limit what you see for a very long commit msg (?)
- **_50_** characters or less – for more detail, keep it to **_72_** chars (Which one?)
- the 1st line is treated as the subject of the commit and the rest as the body
- the blank line separating the subject from the body is critical – cmds like `log`, `shortlog`, and `rebase` can get confused if you run the 2 together `???`
- explain the problem that the commit is solving – focus on **WHY** you are making the change as opposed to HOW
  - are there side effects or unintuitive consequences of the change
  - additional paragraphs should also be separated by blank lines
- `git log` shows commit logs – there are a lot of options but here is a common one: `--pretty`
- [Commit formatting](https://git-scm.com/docs/git-log#_commit_formatting)
- you can filter by who made the commit, when it was, sort them, …
- more commonly you will use `--oneline` – shorthand for `"--pretty=oneline --abbrev-commit"` used together: `git log --oneline`
- THAT ONE IS EXCELLENT!!!
- use `q` or `wq` to exit git log - same for git diff

```sh
git log
git log --oneline
git log --stat
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### what is HEAD

- when you do `git log` at the top commit you will see (`HEAD -> Master`) – _HEAD_ refers to master – but if you switch to a different branch like `new-feature` then you will see (`HEAD -> new-feature`) -
- `HEAD` is a pointer, is a reference to a branch pointer – a branch pointer is where a branch currently is
- `HEAD` points to whatever branch you are on
- So `HEAD` always points to the branch you are on which is pointing to the last commit for that branch – it points to the "Tip" of the branch - however there is an exception to that, which I think is from running `git rebase`

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git diff

- `git diff` is about showing changes – differences between files, between commits, between branches, on GitHub, ...
- often used with `git log` and `git status`
- use it when you don't remember all the changes you made!!!
- `git diff` will list ALL the changes in your working directory that are not staged for the next commit!
- I think it may not work with changes to untracked files, and it has to be changes within the branch you ran the command
- use `q` to exit `git diff` -
- `git diff`: shows ONLY unstaged changes
- `git diff HEAD`: shows staged AND unstaged changes, do not need `q` to exit
- `git diff --staged` and `git diff --cached`: shows only staged changes, do not need `q` to exit

I am unsure of all the commands, but I believe these are common ones you would use:

```sh
# differences between your working directory and the staging area
git diff

# differences between working directory vs. last commit
git diff HEAD
git diff HEAD [filename]

# differences between staging area vs. last commit
git diff --cached
git diff --staged
git diff --staged [filename]

# differences between A vs. B
git diff filename1..filename2
git diff branch1..branch2
git diff commit1..commit2
git diff <commithash1> <commithash2>

# Unsure about these
git diff HEAD~1 HEAD
git diff <commit-hash1>
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git show

Primarily used to display information about a single Git object, most commonly a commit. When used with a commit, it shows the commit message, author, date, and the full textual diff introduced by that specific commit

When given a commit ID, it presents a verbose output including the commit metadata and the patch (diff) for that commit

```sh
git show <commit-id>
git show abcd123
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git reflog

Reference logs record everything you do with your local branches.

- `reflog` is short for reference logs, is used to fix things
- Git keeps a record of when tips of branches were updated
- `git reflog`: is used to view and update the reference logs
- References are things like branch references (git switch), HEAD, remote branches, fetch HEAD, merge HEAD, ...
- Git keeps a record of when they change, e.g., a reflog for when HEAD changes
- Check `.git/logs` > `.git/logs/HEAD` – is readable - do not edit that file!
- Reflogs are only local, not shared with collaborators
- Reflogs also expire, cleaned out after 90 days
- They are used to fix mistakes, if you need to access a commit hash you no longer see in your git log, ...

```sh
git log --oneline
git reflog
```

1. Use `git reflog` to show everything you did in previous steps
2. Find the entry where you think you want to go back to.
3. Then use `git checkout HEAD@{12}` or `git reset HEAD@{3}` to get back to that state, where `HEAD@{12}` and `HEAD@{3}` are referring to the number of commits in the past.

- The `git reflog` command works with 4 different sub-commands, but `show` is the only one you want. The other three (`expire`, `delete`, `exists`) are not really used.
- `git reflog show HEAD` – or just `git reflog` because it defaults to HEAD
- `git reflog show` will show the log of a specific reference (defaults to HEAD)
- The output is similar to `git log` but shows things like
  - When you checked out a branch
  - When you used git reset, restore, revert, or rebase
  - Deleted a commit with the commit hash
  - When you were in detached HEAD
- You will see `HEAD@{#}`: that syntax refers to a particular entry in a reflog

```sh
git reflog show <reference>
# The output is similar to git log
git reflog show HEAD
```

**Passing reflog references around**:

- SYNTAX: `name@{qualifier}`
- We can access specific git refs using `name@{qualifier}` – they can be passed to other commands like `checkout`, `reset`, `diff`, and `merge`
  - `HEAD@{2}` is different that `HEAD~2` (involves commits)
  - `HEAD@{2}` means where HEAD was 2 moves ago
- `HEAD@{2}` shows all ref logs from the oldest to the one for 2
- The `#` qualifier stands for the # of moves ago so that could be something on another branch in the ref logs

```sh
# Checkout to HEAD 2 moves ago
git checkout HEAD@{2}
```

**Time-based reflog qualifiers**:

- Every reflog entry has a unix timestamp associated with it and also a commit hash and a user.email
- `git reflog main@{one.week.ago}`
- `git checkout bugfix@{2.days.ago}`
- `git difff main@{0} main@{yesterday}`

```sh
git reflog main@{one.week.ago}
git checkout bugfix@{2.days.ago}
git difff main@{0} main@{yesterday}
```

**Rescuing lost commits with reflog**:

You can lose commits when you do a hard reset but you can still retrieve the data from the reflog.

```sh
# Undo a commit
git reset --hard abcd123

# Find the hash for the commit removed above
git reflog show main
# You can access that with the commit hash abcd123 or main@{1}

# Checkout hash abcd123 (detached HEAD)
git checkout abcd123
git switch -
git reflog show main

# To restore the commit - undo the undo
git reset --hard abcd123
# or instead of abcd123 use main{1}
```

**Undoing a rebase with reflog**:

- Involves interactive rebasing – fixing it after the fact
- Use reflog to get the commit hash or HEAD #

```sh
# fixup
git rebase -i HEAD~4

# Show the lost commits
git reflog show branch-name

# Bring them back with
git reset --hard <commit-hash>
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git tag

- The concept of a tag is to mark or highlight some point in history (a commit) and have it be a static reference and it does not move
- Most often tags are used to mark different releases or versions like v7.0.1
- They are useful and simple to understand
- You can tag particular commits to mark a moment in time
- Think of tags as branch references that do not change – once a tag is created, it always refers to the same commit – it's just a label for a commit
- Tags are for specific points in a repos history that are important
  - _Mostly used for release points_
  - When a feature branch is merged into master
  - A radical change,
  - A bug fix,
  - New feature added, etc
- They can be named anything
- There are 2 types of tags:

1. Lightweight tags – just a name/label that points to a specific commit
2. Annotated tags: store extra meta-data including the author's name and email, the date, and a tagging message – _these are generally preferred_

- The basic command is `git tag`
- Tagging and versioning are kind of used together

```sh
git tag
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Semantic Versioning

- The mostt common use for tags is versioning
- The semantic versioning spec outlines a standardized versioning system for software releases – it provides a consistent way for devs to give meaning to their software release
- Versions consist of three numbers separated by periods:

Semantic Versioning pattern:

- Major-Release.Minor-Release.Patch-Release
- The first release is typically 1.0.0
- Example: 2.4.1
  - 2 = Major-Release
  - .4 = Minor-Release
  - .1 = Patch-Release

Patch Releases:

- Normally do not contain new features or significant changes
- They typically signify bug fixes and other changes that do not impact how the code is used
- They happen pretty frequently

Minor Release:

- Signify that new features or functionality have been added, but the project is still backwards compatible – no breaking changes
- The new functionality is optional and should not force users to rewrite their own code
- Whenever you have a minor release you should reset the patch number to 0

Major Release:

- Signify significant changes that are not backwwards compatible
- Features may be sunstantially removed or changed - breaking changes
- Then set minor and path releases numbers to 0

The new version makes it clear to a consumer or user how significant the change is.

- Go to Boostrap on Github and click on Tags above the listed files – then click on Releases to see the details for each tag/release
- You can also append after the patch number with things like beta: `v3.2.1-beta` or `-alpha3`
- Or go to the [changelog page on the React website](https://react.dev/versions#changelog) and click on a changelog link

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Viewing and searching tags

- The concept of a tag is to mark or highlight some point in history (a commit) and have it be a static reference and it does not move

How to view existing tags

- `git tag` will print a list of all the tags in the current repo
  - You may also see `v` prepended to the version number
  - They are tied to a specific commit
  - Type `q` to exit the list
- You can also filter and search the tags
  - `git tag -l` + wildcard pattern to search, `-l` is for list

```sh
# List all the tags in the current repo in ASCENDING order
git tag

# filter and search the tags
git tag -l "search criteria"

# Find all tags starting with v17
git tag -l "v17*"

# Find all tags with "beta"
git tag -l "*beta*"
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Comparing tags with git diff

- You can "checkout" particular tags, and a tag refers to a particular commit not a branch
- `git checkout <tag>` to view the state of a repo at a particular tag – this puts you in detached HEAD
- A tag is referring to a particular commit NOT a branch – and you go into detached HEAD because you are basically just checking out a commit
- `git checkout v15.3.1 `– but just takes you back, better to see the difference b\tw 2 tags
- `git diff v17.0.0 v17.0.1` – remember to do git switch master or git switch -

```sh
git checkout <tag>
git checkout v15.3.1

# See what changed between releases
git diff v17.0.0 v17.0.1
```

### Creating and working with tags

<br>

**Creating lightweight tags**:

- Lightweight tags: just a name and a label that points to a commit - lightwieght tags are frowned upon
- `git tag <tagname>`: by default it will reference the commit that `HEAD` is referencing/pointing to

```sh
# Create a tag:
git tag <tagname>
git tag v18.2.1
```

<br>

**Creating annotated tags**:

- Annotated tags: store extra meta data including the author's name and email, the data, and a tagging message.
- To create an anotated tag use the `-a` option
- `git tag -a <tagname>`: this also is based on the current HEAD position
  - You will get a prompt file in VS Code -> `TAG_EDITMSG` - add your description, save and close
  - You can also include `-m` option to write your description/message inline instead of in the text editor
- `git show <tagname>`: to see the meta info - use `q` to exit

```sh
# Create an annotated tag
git tag -a <tagname>
# Annotated tag with message
git tag -a <tagname> -m "tag description"

# See the meta data for an annotated tag
git show <tagname>
```

<br>

**Tagging previous commits**:

- You can go back and tag earlier commits
- `git tag <tagname> <commit>` - use `git log --online` to find a commit without a tag and copy the 9-digit commit hash
- You can do this for lightweight or annotated tags

```sh
git log --online
git tag <tagname> <commit>
```

<br>

**Replacing tags with force**:

- If you need to move a tag, have it refer to a different commit, use the `-f` flag for force to force that tag through
- You can't reuse a tag that is already referring to a commit - tag names need to be unique

```sh
git tag -f <tagname> <commit>
git tag <tagname> <commit> -f
```

<br>

**Deleting tags**:

```sh
git tag -d <tagname>
```

<br>

**Pushing tags**:

- `git push origin --tags`: by default, git push doesn't transfer tags to remote servers
- The `--tags` option used with `git push` is for when you have a lot of tags to push up at once
- This will transfer all your tags to the remote server that are not already there
- `git push origin v1.5.0` to push a single tag

```sh
# Push all tags to GitHub
git push origin --tags

# Push a single tag
git push origin v1.5.0
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## GitHub Issues

- Issues are for communicating or contributing through the GitHub website. They will not be in your local repo.
- The Issues tab is a place to leave a comment about a project, suggest a change, report a bug, etc.
- Reasons to create an issue: 1) bugs, 2) typos, 3) feature requests, 4) to ask a question, etc.

### How to create an issue

1. Click on the _Issues_ tab
1. Click the _New Issue_ button
1. Add a _Title_ and _Description_ about your issue
1. **Note**: You can take a screenshot and add it to your issue by copying it and then paste or drag it into the description field.
1. You can also add _Labels_ by clicking on the gear icon next to labels and checking the ones you want.
1. You can also add _Assignees_ to review your issue.
1. Then click the _Submit new issue_ button

If you click back on the issues tab you will see your issue and any other open issues. Pay attention to the `#` next to your issue title. That same number will appear in the address bar when you click into your issue. That is the issue number.

### Closing an issue

- Issues are _Open_ until they are resolved/closed
- Issues are _Closed_ when the person who owns the repo or who created the issue closes the issue.

When you make a change to a file in regards to an issue, add the issue `#` in your commit title, e.g.: `Making change as per issue #123`

When you go back into that issue you should see the commit that references the issue. If you are done click the _Close_ issue button. There are also keywords that will automatically close an issue and the main one is **_fixes_**.

So if you add the "`fixes`" keyword in your commit title it will close the issue AUTOMATICALLY: `This fixes #123`.

When you do that you will get a commit `#` for the closed issue. If you grab that commit hash from the url for the commit that closed an issue, you can create another issue and paste the hash into the description field. That will automatically create a link to that commit (Huh?)

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## GitHub pull request process

After you push your changes, go to your cloned copy of the repo on GitHub. You should see a green button labeled **_Compare & pull request_**. If you do not see it then click the Pull requests link to go to that tab.

Click the "**_Compare & pull request_**" button and notice the page title of **_Open a pull request_** and the paragraph in the section below the title saying **_Able to merge. These branches can be automatically merged._**

You can then edit your commit message if need be. In the body of your PR include a more detailed summary of the changes you made and why.

### Pull request title

The title convention has the following format:

`<type>([optional scope(s)]): <description>`

For example:

`fix(learn): tests for the do...while loop challenge`

| Type     | When to select                                                             |
| :------- | :------------------------------------------------------------------------- |
| fix      | Bug fix, changed/updated/improved functionality, tests, verbiage, etc.     |
| feat     | Introduction of a new functionality, feature, test, etc.                   |
| chore    | Not fix or feat, & don't modify src or test files (e.g. dependency update) |
| docs     | Changes to docs directory, README's, contributing guidelines, etc.         |
| refactor | Refactored code that neither fixes a bug nor adds a feature                |
| ci       | Continuous integration related                                             |
| perf     | Performance improvements                                                   |
| test     | Including new or correcting previous tests                                 |
| build    | Changes that affect the build system or external dependencies              |
| revert   | Reverts a previous commit                                                  |
| style    | Code formatting such as white-space, missing semi-colons, etc.             |

<br >

**Title:**

Keep it short (less than 30 characters) and simple. You can add more information in the PR description box and comments. Example: `fix(api,client): prevent CORS errors on form submission`.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Code Comments

You can make comments on the code you pushed. This only makes sense when you are contributing:

1. Click on the _Files changed_ tab when on the PR for the push
1. Click the `+` button that appears when you hover over a line of the code
1. Make a comment on a line of code.
1. You can add a description for the comment and also click the "_Resolve conversation_" button.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Staying up to date

Once you are done with your PR and start to work on something else, the repo has most likely had changes by other contributors so your copy is behind. You need to update your local copy of the repo before making new changes.

Use the following commands to update your local copy:

```sh
git checkout master
git pull upstream master
# Or use:
git pull origin master
```

I have also used `git fetch upstream` to update my local copy. I'm not sure if `git pull upstream master` is better or not. However, I had a PR fail because I was missing a command. `git fetch upstream` will only fetch the git data. To update your main fully, you should:

```sh
git checkout master
git fetch upstream
git merge upstream/master
# or use pull to fetch and merge in one step
git pull upstream master
```

So run `git merge upstream/master` every time before making your changes and doing a push if you chose to use `git fetch`. That will ensure you always have the latest state of `master` locally.

The main thing to know is that the master branch will most likely be updated regularly as you are working on your branch. You will want to pull those changes down to your local master branch.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### PR and merge conflict on GitHub

> I'm unsure why this section is here and unsure about the code block

- when you go into the pull request it will not have a Merge conflict btn – instead click the _Resolve Conflicts_ btn
- you get an option to do it in the browser but it is probably easier to resolve them on your own machine
- on the same page is a link titled "_command line instructions_":

```sh
# Step 1: from your project repository, bring in the changes and test
git fetch origin
git checkout -b new-branch origin/new-branch
# the above is to create new-branch and have it track origin/new-branch
# but insteead do:
git switch new-branch
git merge main

# Step 2: merge the changes and update on github
git checkout main
git merge --no-ff new-branch
git push origin main
```

- what `git merge main` is doing is merge `main` into `new-branch` and resolve the conflicts in that branch - so test things out and make sure it works
- then you save/add/commit the changes and switch to `main` and merge the branch into it
- `--no-ff` tells git to NOT fast-forward if it detects that it can. That will move the `HEAD` pointer forward but sometimes you want to prevent that (?)
- that is to preserve the history that a branch was merged in (???)
- back on GitHub everything should be good
- remember to do `git pull origin main`

## Terminal commands

Common terminal commands

```bash
# command [OPTIONS] arguments
# Arrow up will show the last command(s) ran so that you can run it again
# Bash scripts start with a shebang:
#!/bin/bash

# Use with any commands to see the flags
--help
# Display the current date:
date

# List the contents of the current directory: ls
# List files/directories in long form, displays detailed information
ls -l
# Show hidden files/folders
ls -a
# Sort output by last modified date
ls -t
# List only the directories
ls -d */
# List contents of folder_name
ls folder-name

# Display the present working directory:
pwd
# Go to home directory:
cd ~
# Go to last directory:
cd -
# Go up one directory
cd ..
# Go up two directories
cd ../..
# Go to folder-name
cd folder-name
# Go to your root directy
cd /

# FOLDERS
# Create filename.ext
touch filename.ext
# Used to create a directory: mkdir
mkdir folder_name
# Delete an empty folder
rmdir folder_name
# Delete all files & sub-directories of folder_name
rm -rf folder_name

# FILES
# Used to copy file(s):
cp filename destination
# Used to move or rename a file:
mv filename destination path
# Used to remove/delete: rm
rm filename.ext
# Ask user for confirmation
rm -i filename.ext

# Overwrite or create file with content
echo "foo" > bar.txt
# Append to file with content:
echo "foo" >> bar.txt

# Clear terminal output
clear
# Open default code editor:
code .
# Open Windows Explorer:
explorer .
# Open Notepad
notepad .

# Exit out of git diff
q

# Exit out of Vim
:wq

# Exit out of the shell prompt
CTRL+C

# Close bash terminal
exit
```

Others:

- rsync, read, cat, less, head, tail, wc, chmod, type, wget, which, whereis, locate, find, grep, sed, ln, zip, gzip, tar -c, unzip, gunzip, tar -x, df, du, free, apt, shutdown, reboot
- `~` indicates your home directory -
- `q`, `Q`, or `:q`: to exit out of VIM or Nano (I think)
- `.`, `./`, `../`: they stand for home, current directory, and up one directory
- `git` - shows other commands like `grep`, `show`, `rebase`, `switch`, `tag`
- `git help git` opens your local `git.html` file in the browser
- if you are in Vim use `i` to insert your message then `ESC` once to exit insert mode then `:wq` to exit Vim
- Use the up <kbd>&uarr;</kbd> and down <kbd>&darr;</kbd> arrow keys to cycle thru previous commands
- <kbd>CTRL</kbd>+<kbd>C</kbd> to exit REPLs like Node, Mongod, etc.
- <kbd>TAB</kbd> - auto fill in file and folder names
- `cls` to clear the screen in PowerShell/Command Prompt

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## GitHub Two Factor Authentication

> Starting in March 2023 and through the end of 2023, GitHub will gradually begin to require all users who contribute code on GitHub.com to enable one or more forms of two-factor authentication

The following notes are from GitHub pages:

- With two-factor authentication (2FA), you have to log in with your username and password and provide another form of authentication that only you know or have access to
- For GitHub, the second form of authentication is a code that's generated by an application on your mobile device or sent as a text message (SMS). After you enable 2FA, GitHub generates an authentication code any time someone attempts to sign into your account on GitHub.com. The only way someone can sign into your account is if they know both your password and have access to the authentication code on your phone
- After you configure 2FA, using a time-based one-time password (TOTP) mobile app, or via text message, you can add a security key - OR - you can add a passkey to your account. Passkeys are similar to security keys. However, passkeys satisfy both password and 2FA requirements, so you can sign in to your account in one step
- If you have already configured a security key for 2FA that is passkey eligible, you can easily upgrade the security key into a passkey in your account settings. For more information, see "[About passkeys](https://docs.github.com/en/authentication/authenticating-with-a-passkey/about-passkeys)" and "[Managing your passkeys](https://docs.github.com/en/authentication/authenticating-with-a-passkey/managing-your-passkeys)."
- You can also configure additional recovery methods in case you lose access to your two-factor authentication credentials. For more information on setting up 2FA, see "[Configuring two-factor authentication](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication)" and "[Configuring two-factor authentication recovery methods](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication-recovery-methods)."

> This is a PITA if you ask me, but I was able to get a number of _recovery codes_.

### Two-factor authentication recovery codes

> This is what I did:

- When you configure two-factor authentication, you'll download and save your 2FA recovery codes. If you lose access to your phone, you can authenticate to GitHub using your recovery codes. For more information, see "[Recovering your account if you lose your 2FA credentials](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/recovering-your-account-if-you-lose-your-2fa-credentials)."

Also check out:

- [Accessing GitHub using two-factor authentication](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/accessing-github-using-two-factor-authentication)
- [Recovering your account if you lose your 2FA credentials](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/recovering-your-account-if-you-lose-your-2fa-credentials)

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Signed Commits

> Notes from Eddie Jaoude YouTube video [Are YOUR git commits from you?](https://youtu.be/X1duT-4vKcI)

- In any of your Repos click on _Activity_ - not sure why he clicked there?!?
- If you want the verified badge on your git commits on GitHub, then you need to sign your commits

Check out: [About commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification)

- If a commit or tag has a GPG, SSH, or S/MIME signature that is cryptographically verifiable, GitHub marks the commit or tag "Verified" or "Partially verified."
- For most individual users, GPG or SSH will be the best choice for signing commits
- SSH signatures are the simplest to generate
- You can even upload your existing authentication key to GitHub to also use as a signing key
- Generating a GPG signing key is more involved than generating an SSH key, but GPG has features that SSH does not
- A GPG key can expire or be revoked when no longer used. GitHub shows commits that were signed with such a key as "Verified" unless the key was marked as compromised. SSH keys don't have this capability
- you can set up your repo to only allow signed commits on a certain branch though that will reduce potential contributors

### Generating a GPG Key

- [Generating a new GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key) - follow the steps and commands:

1. Download and install [the GPG command line tools](https://www.gnupg.org/download/) for your operating system. We generally recommend installing the latest version for your operating system
2. Open Git Bash
3. Generate a GPG key pair. Since there are multiple versions of GPG, you may need to consult the relevant [man page](https://en.wikipedia.org/wiki/Man_page) to find the appropriate key generation command
   1. If you are on version 2.1.17 or greater, paste the text below to generate a GPG key pair

```sh
gpg --full-generate-key
```

4. At the prompt, specify the kind of key you want, or press <kbd>Enter</kbd> to accept the default
5. At the prompt, specify the key size you want, or press <kbd>Enter</kbd> to accept the default
6. Enter the length of time the key should be valid. Press <kbd>Enter</kbd> to specify the default selection, indicating that the key doesn't expire. Unless you require an expiration date, we recommend accepting this default
7. Verify that your selections are correct
8. Enter your user ID information
9. Type a secure passphrase
10. Use the `gpg --list-secret-keys --keyid-format=long` command to list the long form of the GPG keys for which you have both a public and private key. A private key is required for signing commits or tags

```sh
gpg --list-secret-keys --keyid-format=long
```

11. From the list of GPG keys, copy the long form of the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:

```sh
gpg --list-secret-keys --keyid-format=long
/Users/hubot/.gnupg/secring.gpg
```

12. Paste the text below, substituting in the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`

```sh
gpg --armor --export 3AA5C34371567BD2
```

13. Copy your GPG key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----`.
14. [Add the GPG key to your GitHub account](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account)

Once you've generated the GPG key, you need to do 2 more things:

1. Add the GPG key to your GitHub account
2. Tell your local Git to use the same GPG key

### Add the GPG key to your GitHub account

1. Click your profile photo, then click Settings
2. In the "Access" section of the sidebar, click SSH and GPG keys.
3. Next to the "GPG keys" header, click New GPG key.
4. In the "Title" field, type a name for your GPG key.
5. In the "Key" field, paste the GPG key you copied when you generated your GPG key.
6. Click Add GPG key.
7. To confirm the action, authenticate to your GitHub account.

### Tell your local Git to use the same GPG key

If you have multiple GPG keys, you need to tell Git which one to use.

1. Open Git Bash
2. If you have previously configured Git to use a different key format when signing with `--gpg-sign`, unset this configuration so the default format of openpgp will be used

```sh
git config --global --unset gpg.format
```

3. Use the `gpg --list-secret-keys --keyid-format=long` command to list the long form of the GPG keys for which you have both a public and private key. A private key is required for signing commits or tags

```sh
gpg --list-secret-keys --keyid-format=long
```

4. From the list of GPG keys, copy the long form of the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`

```sh
gpg --list-secret-keys --keyid-format=long
/Users/hubot/.gnupg/secring.gpg
```

5. To set your primary GPG signing key in Git, paste the text below, substituting in the GPG primary key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`

```sh
git config --global user.signingkey 3AA5C34371567BD2
```

6. Optionally, to configure Git to sign all commits by default, enter the following command

```sh
git config --global commit.gpgsign true
```

Also check out [Telling Git about your SSH key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key#telling-git-about-your-ssh-key)

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## ci cd pipeline

> Continuous integration and continuous delivery (CI/CD) is a software development methodology that allows for rapid, frequent, and reliable code updates. It is a core component of DevOps, which is a set of practices that aims to foster collaboration and communication between development and operations teams

You can practice this on your projects hosted on Netlify or VErcel for example. It's a simple as puhing to GitHub and Netlify or Vercel will notice the change and redeploy your project/app/website.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Code reviews

Code reviews are not something you typically do as a developer.

Reviewing a Pull Request

- click on _Files changed_ in the PR
- You will all t he files that were changed - the changes are in green in the right pane, the changes are in red in the left pane
- If you hover over any line in either pane you will see a `+` symbol - click it to add a comment for that line of code
  - You can also select multiple rows by clicking the `+` icon then press `SHIFT` and drag
- When you click on a row, a textarea will open where you can add your comment
- You can click on the button _Add single comment_ - when you do that a notification will be sent to everyone following that PR - that will be for every comment you make that way
- Insteadclick _Start a review_ - that marks the comment as Pending
- When you are done, click the _Finish your review_ button at the top-right of the page where you can leave a final comment - you also have the choice to:
  - Commnet only
  - Approve the review
  - Request changes
- Then click _Submit review_

Making suggestions

- When you click on the `+` icon, above the textarea is a `+/-` icon - if you click it, it adds a suggestion in the textarea:

```suggestion
console.log('You code sux!')
```

````
```suggestion
console.log('You code sux!')
```
````

- then click Add review comment

Miscellaneous:

- You can mark a file as reviewed which will condense the file so the page is easier to navigate
- between comment, approve, or request changes, request changes will block them from being able to merge, but the comment option will not block that
- As a reviewer you can edit there PR title and description, but send it back asking them to be more descriptive.
- To better understand the PR, take a look at the commit history for it

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>
