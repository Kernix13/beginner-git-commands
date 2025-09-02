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
   1. [Remove git](#remove-git)
   1. [Remove remote origin](#remove-remote-origin)
   1. [Remove a file from git tracking](#remove-a-file-from-git-tracking)
   1. [Remove a file from GitHub](#remove-a-file-from-github)
1. [GitHub Issues](#github-issues)
   1. [How to create an issue](#how-to-create-an-issue)
   1. [Closing an issue](#closing-an-issue)
1. [GitHub pull request process](#github-pull-request-process)
   1. [Pull request title](#pull-request-title)
   1. [Pull requests page notes](#pull-requests-page-notes)
   1. [Replies to your pull request](#replies-to-your-pull-request)
   1. [Code comments](#code-comments)
1. [Staying up to date](#staying-up-to-date)
1. [Handling merge conflicts](#handling-merge-conflicts)
   1. [More on merge conflicts](#more-on-merge-conflicts)
   1. [Another section on merge conflicts](#another-section-on-merge-conflicts)
   1. [The steps to resolve a merge conflict](#the-steps-to-resolve-a-merge-conflict)
   1. [using vs code to resolve conflicts](#using-vs-code-to-resolve-conflicts)
1. [Terminal commands](#terminal-commands)
1. [Git Log](#git-log)
   1. [what is HEAD](#what-is-head)
1. [Git Diff](#git-diff)
1. [git restore](#git-restore)
   1. [un-staging changes with git restore](#un-staging-changes-with-git-restore)
1. [git reset](#git-reset)
1. [git revert](#git-revert)
1. [git rebase](#git-rebase)
1. [restore vs reset vs revert vs rebase](#restore-vs-reset-vs-revert-vs-rebase)
1. [GitHub Two Factor Authentication](#github-two-factor-authentication)
   1. [Two-factor authentication recovery codes](#two-factor-authentication-recovery-codes)
1. [Signed Commits](#signed-commits)
1. [ci cd pipeline](#ci-cd-pipeline)

## Fixing mistakes

You will make mistakes from time to time. Here are ways to fix the most common mistakes.

Git reset summary:

- `git reset` (no args) = unstage all files
- `git reset HEAD <file>` = unstage just that file
- `git reset --mixed HEAD~1` = undo the last commit but keep changes (unstaged)

### Remove unstaged changes

```sh
# Discard changes in a single file:
git checkout HEAD filename
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

You can also remove a specific file from staging by using git rm –cached filename.ext.

### Remove commits

Use git reset again but include HEAD which means the last commit. But to undo the last commit add ~1 to go back 1 commit past the last commit which will undo the last commit.

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
```

3. Undo the commit and discard changes completely - If you want to undo the commit and throw away all changes:

```sh
# ⚠️ This permanently deletes changes that weren’t pushed anywhere.
git reset --hard HEAD~1
```

But what if you want to go back a number of commits or to a specific commit. First use `git log` or `git log --oneline` which gives you a list of your commits in reverse chronological order. You can scroll down the log with <kbd>SPACEBAR</kbd>.

4. Undo a commit that’s already pushed (safe way) - If you’ve already pushed and want to undo without rewriting history:

```sh
# Use git reset with the commit HASH:
git revert <commit_hash>
git reset e220bfb1e34b8c6b6fce1deb7884244239284716
```

That will unstage any changes made to the file(s) AFTER that commit. The changes will be in your files but they will not be saved into git anymore. But how do you get rid of all the changes after a certain point? Use the same command but add the flag --hard:

```sh
git reset --hard e220bfb1e34b8c6b6fce1deb7884244239284716
```

### Remove git

To remove git tracking from a folder use the following command in git bash, the command prompt, or the terminal in VS Code. Make sure you are in the root folder where you want Git removed:

```sh
rm -rf .git
```

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

Pair this with adding the file (or its pattern) to `.gitignore` so Git doesn’t stage it again. This is especially useful for sensitive files like `.env` or directories such as `node_modules/` that should stay local but not be version-controlled.

### Remove a file from GitHub

I used the following command to remove a file from GitHub that had a different case from my local copy. I mistakenly created my file name as `errorMiddleWare.js` where the `W` should have been lowercase `w`. I made the change to my local filename but the filename on GitHub maintained the uppercase `W`. Here is the command I ran to fix that followed by an explanation of the command:

```sh
git rm -r --cached .
```

1. `git rm`: used to remove individual files or a collection of files
2. `-r`: shorthand for 'recursive'. When operating in recursive mode git rm will remove a target directory and all the contents of that directory
3. `--cached`: specifies that the removal should happen only on the staging index. Working directory files will be left alone

I thought the entire project was deleted and then added to staging because EVERY file was highlighted green in VS Code, but that not the case. I can't explain it but use this command if you also have a file where the case changed and the local file and GitHub file do not match.

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

## Handling merge conflicts

> This section definitely needs to be edited and rewritten - I'm a little fuzzy on this process.

Read more here: [Conflicts on a pull request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md#making-changes-locally 'Making changes locally').

A merge conflict is when 2 or more people change the same code/content but with different values. However, I don't think a beginner contributor would actually handle merge conflicts.

But if you have a conflict, in VS Code you will see something like:

```sh
<<<<<<< HEAD (Current Change)
<p>some change here</p>
=======
<p>different change here</p>
>>>>>>> Branch-Name (Incoming Change)
```

Where `HEAD` is pointing to the last commit for your current branch, usually main/master. What you would do is:

1. Decide which change you want to keep,
1. Delete EVERYTHING else -> the change you don't want and the equal (`=`), less than (`<`), and greater than (`>`) signs along with the text like `HEAD` and `Current Change`. Everything other than the actual change that you want.

Although, that is the hard way to do it.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### More on merge conflicts

Git can NOT automatically merge the branches when there is a merge conflict – they have to manually be resolved

- when you merge a branch into main or another branch where the same line was changed on both branches, you will get a warning in the terminal AND the file with the conflict will open with conflict marrkers and the line(s) in question -
- `HEAD` starts with `<<<<` and ends/includes `=====`, below that is the file changes you are trying to merge into main – do you want just the main changes, just the branch changes or BOTH or some combination of both?
- so make that choice and remove the conflict markers then save the file(s) – my file is red-orange with a green btn `Resolve in Merge Editor` - what is that?
- add `git status` before step 4 – runniing that shows the terminal msg

```bash
You have unmerged paths.
(fix conflicts and run "git commit")
(use "git merge --abort" to abort the merge)
```

- so `git add` modified file > `git commit -m "merged test-branch"`

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Another section on merge conflicts

When a line in the same file was changed in the branch you are trying to merge _AND_ in master, then you will get a merge conflict with a message:

> CONFLICT (content): Merge conflict in file.ext
> Automatic merge failed; fix conflicts then commit the result.

This is a multi-step process

1. You have to open the files where there are conflicts
2. "Fix" the conflicts
3. Commit the change

The files that are conflicting have new content - many `<`, `>`, and `=` symbols and `HEAD` and the other branch name

It shows the content that came from the `HEAD` branch, the branch you are on, indicated by `<<<<<< HEAD`, followed by the content then `=======`.

Then below the equal signs is the content from the branch followed by `>>>>> branch-name` (usually main/master).

You have to figure out which to keep and which to delete, then get rid of all the extra symbols and keywords and save the file. Then you `add` and `commit` the changes.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### The steps to resolve a merge conflict

1. Open the file(s)
2. Edit the file(s)
3. Remove the conflict markers
4. Run `git status` to see terminal messages
5. Add your changes and then commit them

> This is the line I will test changing! This sentence is from test-branch.

This sentence will not be in conflict with the `main` branch.

Terminal messages you see with a merge conflict:

> You have unmerged paths.
> (fix conflicts and run “git commit”)
> (use “git merge --abort” to abort the merge)

- I think it may not work with changes to untracked files,
- And it has to be changes within the branch you ran the command

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### using vs code to resolve conflicts

- use `git status` on each brach as a check
- in VS Code there is a built in interface – you don't have to manually delete everything -
- I did not get a conflict – terminal msg: `"Merge made by the 'ort' strategy."`

> `ort` is much faster than recursive
> `ort` has a better performance, and it's now the default merge strategy in newer Git versions

above the HEAD line are 4 options you can click:

1. `Accept Current Change` – that is for `main` or whichever branch you are merging into
2. `Accept Incoming Change`
3. `Accept Both Changes`
4. `Compare Changes`

Notes:

- if you click Compare Changes, it looks like whatever was changed last is highlighted red, and the first file is highlighted green
- but sometimes you need to add code and work with both files to resolve the conflict

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

| Command              | Use                                            |
| :------------------- | :--------------------------------------------- |
| `cd`                 | change directory                               |
| `cd folder-name`     | move into folder-name                          |
| `cd ..`              | cd to folder one level up                      |
| `cd ~`               | go to your home directory                      |
| `cd /`               | go to your root directory                      |
| `--help`             | use with any cmd for all the flags             |
| `ls`                 | list files & folders in current directory      |
| `ls -a `             | list hidden files as well using `-a`           |
| `ls folder-name`     | list contents of folder_name                   |
| `code .`             | Opens up VS Code                               |
| `pwd`                | print working directory                        |
| `touch filename.ext` | create filename.ext                            |
| `mkdir folder_name`  | to make a directory/folder                     |
| `rm filename.ext`    | to delete/remove a file - it's GONE!           |
| `rmdir folder-name`  | only deletes an empty folder                   |
| `rm -rf folder_name` | to delete a folder, e.g. `rm -rf .git`         |
| r                    | recursive                                      |
| f                    | force                                          |
| `exit`               | close terminal                                 |
| `clear`              | Clear the terminal                             |
| `exit`               | To close the terminal                          |
| `code .`             | To open your default text editor               |
| -                    | -                                              |
| `cls`                | to clear the terminal in cmd prompt/powershell |
| `start . `           | Opens up windows explorer                      |
| `dir`                | the ls version for command prompt              |
| `ni filename.ext `   | create using cmd prompt/powershell             |
| `open .`             | open file explorer in Windows                  |

- `~` indicates your home directory -
- `q`, `Q`, or `:q`: to exit out of VIM or Nano (I think)
- `.`, `./`, `../`: they stand for home, current directory, and up one directory
- `git` - shows other commands like `grep`, `show`, `rebase`, `switch`, `tag`
- `git help git` opens your local `git.html` file in the browser
- if you are in Vim use `i` to insert your message then `ESC` once to exit insert mode then `:wq` to exit Vim
- Use the up <kbd>&uarr;</kbd> and down <kbd>&darr;</kbd> arrow keys to cycle thru previous commands
- <kbd>CTRL</kbd>+<kbd>C</kbd> to exit REPLs like Node, Mongod, etc.
- <kbd>TAB</kbd> - auto fill in file and folder names

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Git Log

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

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### what is HEAD

- when you do `git log` at the top commit you will see (`HEAD -> Master`) – _HEAD_ refers to master – but if you switch to a different branch like `new-feature` then you will see (`HEAD -> new-feature`) -
- `HEAD` is a pointer, is a reference to a branch pointer – a branch pointer is where a branch currently is
- `HEAD` points to whatever branch you are on
- So `HEAD` always points to the branch you are on which is pointing to the last commit for that branch – it points to the "Tip" of the branch - however there is an exception to that, which I think is from running `git rebase`

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Git Diff

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
git diff HEAD [filename]
git --diff staged [filename]
git diff --cached
git diff --staged
git diff filename1..filename2
git diff branch1..branch2
git diff commit1..commit2
git diff HEAD HEAD~1
git diff hash#
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git restore

> These notes are not good!

- `git restore` helps with undoing operations
- use `git restore --staged <file>` to unstage any files you added
- FIRST, you can discard changes since the last commit
- `git restore <file-name>` - to restore the file to the contents in the HEAD – if you have uncommitted changes in the file, they will be lost – it replaces `git checkout HEAD <file-name>`
- `git restore filename` restores using HEAD as the default source, but you can change that using the `--source` option
- SECOND, you can reference a particular commit
- `git restore --source HEAD~1 <file-name>` - restores the contents of `file-name` to the state prior to HEAD – you can also use a particular commit hash as the source
- so either a commit hash or `HEAD~num` – all the other files and branches are untouched

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### un-staging changes with git restore

- `git restore --staged <file-name>` - to unstage files that you staged – use that if you do not want to include the file in your next commit

## git reset

- `git reset` restores a repo back to a specific commit – the commits are gone
- common if you did work on the master branch but you meant to do it on a new branch
- there are 2 versions: regular and a hard reset
- `git reset <commit-hash>` - restores a repo back to a specific commit, use the 7-digit hash from the `git log --oneline` command
- but that is a regular reset and that only removed the commits – the changes are still in the working directory – you just went back in time by removing commits – to Git, that's where the history stops – but for some reason it kept the changes in the file – WHY IS THAT?
- **Answer**: it's useful if you make commits on the wrong branch – you can keep that work and move it to another branch – how do you do that? By creating a new branch and then adding/committing the changes on that one – this may be what I did when I made a branch on a branch and made changes on that
- `git reset --hard <commit-hash>` - a hard reset that loses all the commits up to that commit hash – AND – the changes are removed from your working directory
- like `git restore` you can use a commit hash or `HEAD~3` or whatever number
- YOU NEED TO BE CAREFUL USING `--hard`
- note this is on a per-branch basis

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git revert

`git revert` is the first command that you would use when dealing specifically with remote repositories. All the commands up to this point are used with local and remote repos, but this one is only for remote repositories with 2 or more contributors.

- `revert` is similar to `reset` in that they both "undo" changes, but they do it in different ways
- `git reset hash` actually moves the branch pointer backwards, eliminating commits – as if the commits NEVER occurred
- `git revert` instead creates a brand new commit which reverses/undos the changes from an earlier commit – because it results in a new commit, you have to enter a commit msg – instead of deleting everything, deleting history – that can be a problem if you are collaborating with other people
- with reset, you lose the commits that came after the one you used in the command – they are gone!
- with revert you get rid of the changes but you do not lose the commit for those changes – you have history!

> When to use `reset` and when to use `revert`?

- it has to do with collaboration – if you want to reverse some commits that other people already have on their machines, you should use `revert` – if you want to reverse commits that you haven't shared with others, use `reset` and no one will ever know

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

## restore vs reset vs revert vs rebase

1. `restore`: to restore the contents of a **_file_** to a specific point or to unstage files
   1. `git restore <file-name> `
   1. `git restore --source HEAD~1 <file-name>`
   1. `git restore --staged <file-name>`
1. `reset`: reset a repo back to a specific **_commit_**
   1. `git reset <commit-hash>`
   1. `git reset --hard <commit-hash>`
1. `revert`: similar to `reset`, **_undo changes_**, moves the branch pointer backwards, eliminating commits
   1. `git revert <commit-hash>`
1. `rebase`: an alternative to `git merge` or a cleanup tool for merge commits
   1. `git rebase main` or `git rebase <branch-name`
   1. `git rebase --continue`

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
