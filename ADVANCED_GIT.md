# Advanced Git Commnads

Some of these commands or actions on GitHub are intermediate level, others are advanced or very specific.

This file used to be very short but I added section from the intermediate file, plus a lot of notes I took from [Colt Steele's Git Bootcamp course](https://www.udemy.com/course/git-and-github-bootcamp/). As a result, I believe I have duplicates and very _sloppy_ notes.

<a id="back-to-top"></a>

## Table of contents

1. [Forking and cloning](#forking-and-cloning)
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
   1. [merge conflicts](#merge-conflicts)
   1. [More on Merge conflicts](#more-on-merge-conflicts)
   1. [The steps to resolve a merge conflict](#the-steps-to-resolve-a-merge-conflict)
   1. [using vs code to resolve conflicts](#using-vs-code-to-resolve-conflicts)
1. [Mistakes](#mistakes)
   1. [Undo Staging](#undo-staging)
   1. [Undo a Commit](#undo-a-commit)
   1. [Remove Git](#remove-git)
   1. [Remove remote origin](#remove-remote-origin)
   1. [Undo git add](#undo-git-add)
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

## Forking and cloning

After you fork a repo, open up a terminal with Git Bash and navigate to the folder where you want the cloned repo.

```bash
git clone https://github.com/User_Name/freeCodeCamp
cd folder-name
```

Next, add a remote reference to the main forked repo then check the configuration:

```sh
git remote add upstream https://github.com/other-account/their-repo-name.git
# check the location
git remote -v
```

Then use `git status` and `git checkout main` if not on main.

My final commands:

```sh
git clone --depth=1 https_url
# or just
git clone https_url
git remote add upstream https_url
git fetch upstream
git remote -v
git push origin main
```

> The following set of commands are questionable. They are from when I contributed to freeCodeCamp.

Next:

1. Update your local copy of the upstream repository,
1. Hard reset your main branch with the freeCodeCamp main,
1. Push your main branch to your origin to have a clean history on your fork on GitHub,
1. And validate your current main matches the upstream/main by performing a diff:

```sh
git fetch upstream
git reset --hard upstream/main
git push origin main --force
```

The 1st command is necessary for the clone to fetch the files. Use #2 & #3 with caution - read up on them. The commands above are from freeCodeCamp docs.

**NOTE**: `git fetch upstream` is used to fetch all objects from the remote repo that don't currently reside in the local working directory. You'll also often see`git fetch origin`. `git diff upstream` checks for a difference between a branch and its upstream source.

Finally:

1. Check the branch you are on and switch to main/master if not on that branch,
1. Create a new branch for your contributions, make your changes then
1. Check the status, add your changes, check status again, commit the changes, and then push the changes:

```sh
git branch
git checkout -b fix/something-here
git status
git add .
git status
git commit -m "short description"
# shouldn't it be --set-upstream?
git push origin fix/something-here
```

THEN: create and checkout to your branch, make changes, add and commit your changes, and push them.

```sh
git checkout -b fix/branch-name
git add .
git commit -m "short description"
git push --set-upstream origin fix/branch-name
```

Use that last `git push` only for the first time, then use `git push origin fix/something-typos`. Although, I believe once you set the `upstream` and/or `origin`, you only need to do `git push` similar to a regualr push. Here is the last command AFTER you set the upstream:

```sh
git push origin fix/branch-name
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
1. Then click the _Submit_ new issue button

If you click back on the issues tab you will see your issue and any other open issues. Pay attention to the `#` next to your issue title. That same number will appear in the address bar when you click into your issue. That is the issue number.

- Issues are _Open_ until they are resolved/closed
- Issues are _Closed_ when the person who owns the repo or who created the issue closes the issue.

### Closing an issue

When you make a change to a file in regards to an issue, add the issue `#` in your commit title, e.g.: `Making change as per issue #3`

When you go back into that issue you should see the commit that references the issue. If you are done click the _Close_ issue button. But there are also keywords that will automatically close an issue and the main one is **_fixes_**.

So if you add the "`fixes`" keyword in your commit title it will close the issue AUTOMATICALLY: `This fixes #3`.

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

**Description:**

Keep it short (less than 30 characters) and simple. You can add more information in the PR description box and comments. Example: `fix(api,client): prevent CORS errors on form submission`.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Code Comments

You can make comments on the code you pushed. This only makes sense when you are contributing:

1. Click on the _Files changed_ tab when on the PR for the push
1. Click the `+` button that appears when you hover over the code
1. Make a comment on a line of code.
1. You can add a description for the comment and also click the "_Resolve conversation_" button.

## Staying up to date

Once you are done with your PR and start to work on something else, the repo has most likely had changes by other contributors so your copy is behind. You need to update your local copy of the repo before making new changes.

Use the following commands to update your local copy:

```sh
git checkout master
git pull upstream master
```

I actually use `git fetch upstream` to update my local copy. I'm not sure if `git pull upstream master` is better or not. However, I had a PR fail because I was missing a command. `git fetch upstream` will only fetch the git data. To update your main fully, you should:

```sh
git checkout master
git fetch upstream
git merge upstream/master
```

So run `git merge upstream/master` every time before making your changes and doing a push. That will ensure you always have the latest state of `master` locally.

The main thing to know is that the master branch will most likely be updated regularly as you are working on your branch. You will want to pull those changes down to your local master branch. Then you will want to checkout to your branch and use `git merge master` to keep your branch up to date with what is going on with master. If you don't do that then this is where you _may_ get a merge conflict.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Handling merge conflicts

> This section definitely needs to be edited and rewritten

I'm a little fuzzy on this process. There are a few of ways to handle merge conflicts: 1) on Github, 2) in your terminal, or 3) directly in your code. However, try not to make any mistakes so you don't have to deal with conflicts.

Read more here: [Conflicts on a pull request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md#making-changes-locally 'Making changes locally').

A merge conflict is when 2 or more people change the same code/content but with different values. However, I don't think a beginner contributor would actually run `git merge branch_name`.

But if you did and there was a conflict, in VS Code you will see something like:

```sh
<<<<<<< HEAD (Current Change)
<p>some change here</p>
=======
<p>different change here</p>
>>>>>>> Branch-Name (Incoming Change)
```

Where `HEAD` is your current branch, usually main/master. Once again, this would only be done by the owner of the repo, but what you would do is:

1. Decide which change you want to keep,
1. Delete EVERYTHING else -> the change you don't want and the equal (`=`), less than (`<`), and greater than (`>`) signs along with the text like `HEAD` and `Current Change`. Everything other than the actual change that you want.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### merge conflicts

- git can NOT automatically merge the branches when there is a merge conflict – they have to manually be resolved
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

### More on Merge conflicts

When a line in the same file were changed in the branch you are trying to merge and in master, then you will get a merge conflict with a message:

> CONFLICT (content): Merge conflict in file.ext
> Automatic merge failed; fix conflicts then commit the result.

This is a multi-step process

1. You have to open the files where there are conflicts
2. "Fix" the conflicts
3. Commit the change

The files that are conflicting have new content - many `<`, `>`, and `=` symbols and `HEAD` and the other branch name

It shows the content that cam from the HEAD branch, the branch you are on indicated by `<<<<<< HEAD`, followed by the content then `=======`.

Then below the equal signs is the content from the branch followed by `>>>>> branch-name`.

You have to figure out which to keep and which to delete, then get rid of all the extra symbols and keywords and save the file. Then you add and commit the changes.

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

This is a line from the 'luna' branch.

WTF, `git diff` not working?

- I think it may not work with changes to untracked files,
- And it has to be changes within the branch you ran the command

### using vs code to resolve conflicts

- use `git status` on each brach as a check
- in VS Code there is a built in interface – you don't have to manually delete everything -
- I did not get a conflict – terminal msg: `"Merge made by the 'ort' strategy."`

> `ort` is much faster than recursive
> `ort` has a better performance, and it's now the default merge strategy in newer Git versions

above the HEAD line are 4 options you can click:

1. `Accept Current Change` – that is for main or whatver you are merging into
2. `Accept Incoming Change`
3. `Accept Both Changes`
4. `Compare Changes`

Notes:

- if you click Compare Changes, it looks like whatever was changed last is highlighted red, and the first file is highlighted green
- but sometimes you need to add code and work with both files to resolve the conflict

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### PR and merge conflict on GitHub

> I'm unsure why this section is here

- when you go into the pull request it will not have a Merge conflict btn – instead click the _Resolve Conflicts_ btn
- you get an option to do it in the browser which he has never done, but it is probably easier to resolve them on your own machine
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

- what `git merge main` is doing is merge `main` into `new-branch` and resolve the conflicts in that branch - so test things out and make sure it works -
- then you save/add/commit the changes and switch to `main` and merge the branch into it -
- `--no-ff` tells git to NOT fast-forward if it detects that it can which will move the HEAD pointer forward but sometimes you want to prevent that -
- that is to preserve the history that a branch was merged in (???)
- back on GitHub everything should be good
- remember to do `git pull origin main`

## Mistakes

You will undoubtedly make mistakes when working with Git. Here are common mistakes that I have made and how to fix/undo them.

### Undo Staging

If you accidentally added a file with `git add .`, to remove it from the staging area, use:

```sh
# without arguments
git reset
# with filename and optional path
git reset path/filename.ext
```

- use `git restore --staged <file>` to unstage any files you added -

### Undo a Commit

Use `git reset` again but include `HEAD` which means the last commit. But to undo the last commit add `~1` to go back 1 commit past the last commit which will undo the last commit:

```sh
git reset HEAD~1
```

But what if you want to go back a number of commits or to a specific commit. First use `git log` which gives you a list of your commits in reverse chronological order. You can scroll down the log with <kbd>SPACEBAR</kbd>.

You will see the commit hash and the commit message along with other information. To go back to a specific commit and undo it, use the hash for it:

```sh
# use git reset HASH:
git reset e220bfb1e34b8c6b6fce1deb7884244239284716
```

That will unstage any changes made to the file(s) AFTER that commit. The changes will be in your files but they will not be saved into git anymore. But how do you get rid of all the changes after a certain point? Use the same command but add the flag `--hard`:

```sh
git reset --hard e220bfb1e34b8c6b6fce1deb7884244239284716
```

You can also remove a specific file from staging by using `git rm –cached filename.ext` where `rm` is short for remove.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Remove Git

To remove git tracking from a folder use the following command in `git bash`, the command prompt, or the terminal in VS Code:

```sh
rm -rf .git
```

### Remove remote origin

I once pasted in my repo link ending in `.gi` instead of `.git` because I missed copying the `t`. Use the following to remove the origin and try again:

```sh
git remote remove origin
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Undo git add

If you accidentally push your `node_modules` directory for your first push (when you forgot about `.gitignore`), just use `git reset`to unstage all changes. You could also remove a single file with `git reset <file>`.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

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
- `q`, `Q`, or `:q`: to exit out of VIM or Nano
- `.`, `./`, `../`: they stand for home, current directory, and up one directory
- `git` - shows other commands like `grep`, `show`, `rebase`, `switch`, `tag`
- `git help git` opens your local `git.html` file
- if you are in Vim use `i` to insert your message then `ESC` once to exit insert mode then `:wq` to exit Vim
- Use the up <kbd>&uarr;</kbd> and down <kbd>&darr;</kbd> arrow keys to cycle thru previous commands
- <kbd>CTRL</kbd>+<kbd>C</kbd> to exit REPLs like Node, Mongod, etc
- <kbd>TAB</kbd> - auto fill in file and folder names

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Git Log

- `git log` is a log of the commits for your local repo -
- to configure it so you can limit what you see for a very long commit msg – we need the commit hashes – you need those to redo a commit, to checkout, to look at a commit, etc
- 50 chars or less – for more detail, keep it to 72 chars – the 1st line is treated as the subject of the commit and the rest as the body -
- the blank line separating the subject from the body is critical – cmds like `log`, `shortlog`, and `rebase` can get confused if you run the 2 together `???`
- explain the problem that the commit is solving – focus on WHY you are making the change as opposed to HOW – are there side effects or unintuitive consequences of the change – additional paragraphs should also be separated by blank lines
- options for git log, https://git-scm.com/docs – git log shows commit logs – there are a lot of options but here is a common one: --pretty |
- Commit formatting: https://git-scm.com/docs/git-log#_commit_formatting -
- you can filter by who made the commit, when it was, sort them, …
- more commonly you will use `--oneline` – shorthand for `"--pretty=oneline --abbrev-commit"` used together – `git log --oneline`
- THAT ONE IS EXCELLENT!!!

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### what is HEAD

- when you do `git log` at the top commit you will see (`HEAD -> Master`) – HEAD refers to master – but if you switch to a different branch like new-feature then you will see (`HEAD -> new-feature`) -
- `HEAD` is a pointer, is a reference to a branch pointer – a branch pointer is where a branch currently is
- `HEAD` points to whatever branch you are on -
- "A branch is just a reference to some commit" - ???
- So `HEAD` always points to the branch you are on which is pointing to the last commit for that branch – it points to the "Tip" of the branch - how ever this is an exception to that, which I think is from running `git rebase`

## Git Diff

- `git diff` is about showing changes – diffs b\tw files, b\tw commits, b\tw branches, on GitHub, ...
- often used with `git log` and `git status` -
- use it when you don't remember all the changes you made!!!
- `git diff` will list ALL the changes in your working directory that are not staged for the next commit!
- I think it may not work with changes to untracked files, and it has to be changes within the branch you ran the command
- use `q` to exit `git diff` -
- `git diff`: shows ONLY unstaged changes
- `git diff HEAD`: shows staged AND unstaged changes, do not need `q` to exit
- `git diff --staged` and `git diff --cached`: shows only staged changes, do not need `q` to exit

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git restore

- `git restore` helps with undoing operations -
- use `git restore --staged <file>` to unstage any files you added -
- FIRST, you can discard changes since the last commit -
- `git restore <file-name>` - to restore the file to the contents in the HEAD – if you have uncommitted changes in the file, they will be lost – it replaces `git checkout HEAD <file-name>` -
- SECOND, you can reference a particular commit – `git restore filename` restores using HHEAD as the default source, but you can change that using the --source option -
- `git restore --source HEAD~1 <file-name>` - restores the contents of file-name to the state prior to HEAD – you can also use a particular commit hash as the source -
- so either a commit hash or HEAD~num – all the other files and branches are untouched -

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### un-staging changes with git restore

- `git restore --staged <file-name>` - to unstage files that you staged – use that if you do not want to include the file in your next commit -

## git reset

- `git reset` restores a repo back to a specific commit – the commits are gone
- common if you did work on the master branch but you meant to do it on a new branch -
- there are 2 versions: regular and a hard reset
- `git reset <commit-hash>` - restores a repo back to a specific commit, use the 7-digit hash from `git log --oneline` -
- but that is a regular reset and that only removed the commits – the changes are still in the working directory – but we just went back in time by removing commits – in git's mind, that's where the history stops – butt for some reason it kept the changes in the file – WHY IS THAT?
- **Answer**: it's useful if you make commits on the wrong branch – you can keep that work and move it to another branch – how do you do that? By creating a new branch and then adding/committing thee changes on that one – this may be what I did when I made a branch on a branch and made changes on that
- `git reset --hard <commit-hash>` - a hard reset that loses all the commits up to that commit hash – AND – the changes are removed from your working directory -
- like `git restore` you can use a commit hash or HEAD~3 or whatever number
- YOU NEED TO BE CAREFUL USING `--hard`
- note this is on a per-branch basis -

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git revert

`git revert` is the first command that you would use when dealing specifically with remote repositories. All the commands up to this point are used with local and remotte repos, but this one is only for remote repositories with 2 or more contributors.

- `revert` is similar to `reset` in that they both "undo" changes, but they do it in different ways -
- `git reset` hash actually moves the branch pointer backwards, eliminating commits – as if they commits NEVER occurred -
- `git revert` instead creates a brand new commit which reverses/undos the changes from an earlier commit – because it results in a new commit, you have to enter a commit msg – instead of deleting everything, deleting history – that can be a problem if you are collaborating with other people
- with reset, you lose the commits that came after the one you used it the cmd – they are gone!
- with revert you get rid of the changes but you do not lose the commit for those changes – you have history!

> When to use `reset` and when to use `revert`?

- it has to do with collaboration – if you want to reverse some commits that other people already have on their machines, you should use `revert` – if you want to reverse commits that you haven't shared with others, use `reset` and no one will ever know -

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## git rebase

> Geez, I need some notes here...

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
