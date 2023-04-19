# Detailed descriptions on the commands

This is meant to be details and descriptions of the main files. I wanted to keep the main files as brief as possible, with explanations and insights on the commands placed here.

As of now the detailed notes are not orderly so do a search for the command you are looking for. Eventually I will add better structure. Also, the `git checkout` section is unique only to this file. That section was originally in the advanced file.

<a id="back-to-top"></a>

## Table of contents

1. [Beginner file notes](#beginner-file-notes)
   1. [Table of basic commands](#table-of-basic-commands)
   1. [Clone notes](#clone-notes)
1. [Intermediate file notes](#intermediate-file-notes)
   1. [branches](#branches)
   1. [Deleting branches](#deleting-branches)
   1. [Git Remotes](#git-remotes)
1. [Advanced file notes](#advanced-file-notes)
   1. [Forking and cloning](#forking-and-cloning)
   1. [GitHub Issues](#github-issues)
   1. [How to create an issue](#how-to-create-an-issue)
   1. [Closing an issue](#closing-an-issue)
   1. [GitHub pull request process](#github-pull-request-process)
   1. [Pull request title](#pull-request-title)
   1. [Replies to your pull request](#replies-to-your-pull-request)
   1. [Other commands](#other-commands)
   1. [git checkout](#git-checkout)
   1. [checking out old commits](#checking-out-old-commits)
   1. [re-attaching our detached HEAD](#re-attaching-our-detached-HEAD)
   1. [referencing commits relative to HEAD](#referencing-commits-relative-to-HEAD)
   1. [discarding changes with git checkout](#discarding-changes-with-git-checkout)
   1. [More miscellaneous commands](#more-miscellaneous-commands)
   1. [Terminology](#terminology)

## Beginner file notes

The `git config` command is used initially to configure the `user.name` and `user.email` fields. This specifies what email and username will be used from a local repository.

The `--global` flag tells Git that you're going to use the email above for all repos on your computer. Replace that with `--local` to use different emails for your projects/repos, although that is not recommended if you are new to Git.

1. `git config --global core.editor "code --wait" `– to set VS Code as Git default editor, the `--wait` flag waits for you to close the file that opens for you to type your msg

### Table of basic commands

| _Basic_ Git Commands    | Definition                                      |
| :---------------------- | :---------------------------------------------- |
| git init                | Initiates git tracking                          |
| git status              | Checks the status of your changes/state         |
| git add .               | Adds **_ALL_** (.) changes to staging           |
| git add file1 file2 ... | Adds specific files to staging                  |
| git commit -m "msg"     | Saves changes to local machine with a message   |
| git remote add origin   | Adds URL as remote repo location                |
| git `branch -M main`    | Changes default branch to 'main' (optional)     |
| git push -u origin main | Push changes to and sets remote                 |
| git push                | Push changes after upstream is set              |
| `-u`                    | Parameter short for `upstream`                  |
| `upstream`              | the primary _branch_ on the original repository |

The `git init` command creates a new local GIT repository in the directory you ran that command.

You tend to use `git add .` to commit all your changes to the staging area, but you do not have to do that. You could individually add some files to staging while not adding others. You would do that by specifying the files you want to add: `git add filename1.ext filename2.ext`, etc.

- `git add .` is not good when you have a lot of changes – be more exact than that

The command `git branch -M main` is optional and I think the flag `-M` means changing the default branch name from master to the name **main**. I tried searching for it and I found that Git has changed the default branch name from `master` to `main` though GitHub still uses `master` by default. It's your choice. To see the branch you are on, look to the far left of the bottom bar in VS Code or run `git branch`.

The command `git remote add origin https_url` connects the local repository to a remote server (GitHub repo). `https_url` is the URL that is on the page when you create a new repo. It is also shown when you click the `Code` button in your GitHub repo.

Also, the flag `-u` is not needed if you are pushing to the default branch. The flag `-u` is short for `--set-upstream` which is what you would use when you are pushing a branch you created locally for the first time. By using that flag you set that as the default when you push to GitHub

The `git push` command is used to send local commits to the _master_ (or _main_) branch of the remote repository. But to use `git push` in the future you have to set something called an _upstream_, meaning where you want to push it to by default. That is why you use `-u`. The whole command `git push -u origin master` pushes your commits and sets the branch `master` as the origin for the location of `git push` in the future.

The keyword `origin` means the branch you want to push to. Replace `master` with the branch where you want to push your changes when you're _not_ intending to push to the master branch (See the Branch section in INTERMEDIATE_GIT.md).

Other commands you may find useful are:

1. `git log`: this shows your commit history for the day with the hash you would use to undo a commit with some of the advanced git commands. Type `q` to exit the screen.
1. `git log --oneline`: show your commit hashes and messages on one line.
1. `git diff`: this shows you the file(s) that changed and the actual changes by showing the before and after pictures of your files. Type `q` to exit the screen.
1. `clear`: to clear the console/terminal. That is a terminal command, not a Git command.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Clone notes

The `git remote set-url` command here changes an existing remote repository URL from it's original source to whatever you used for `https_url`.

Now git knows that the origin is your repo. Using `git remote -v` again is to check that git is pointing to the repo address you want.

**Cloning your own repo**:

New commands in detail:

| _Clone_ Git Commands      | Definition                                 |
| :------------------------ | :----------------------------------------- |
| git clone                 | Copies the repo at the URL to your machine |
| git remote -v             | Checks where your local copy points to     |
| git remote set-url origin | Sets the URL to point to when pushing      |

The command `git clone` also initiates a git repo for the repo you want to clone, but git is installed in the downloaded/cloned folder, _NOT_ in the directory where you ran that command. So when cloning you do not need `git init`.

`git clone` is used on its own or when you Fork a repo. Use `cd` to switch to the folder cloned repo.

Use `git remote -v` to list the remote repository that is connected to this project. That is to check if you are pointing to the cloned URL or the copy of the repo in your account. Did you fork and clone to contribute, or to work on your own version of the repo?

`remote set-url origin` here sets your repo as the source URL as opposed to changing the URL if cloned from a different account (see next section). It's function is similar to `remote add origin` in the first section.

That all works for your repos, but eventually you will want to clone, or fork and clone a repo so that you can contribute to it. You will then need to use the `git clone` again, and various `branch` git commands. You will also need to add additional parameters to your git commands (see the Forking and cloning section in INTERMEDIATE_GIT.md)

**NOTE**: This is an alterate way of initializing a local git repo than what is in the section [Pushing your local files to an empty repo](#pushing-your-local-files-to-an-empty-repo). The differece though is that this method installs git in the cloned file folder and not in the directory where you ran `git clone url`, whereas in the section above it installs git in that folder.

- `git clone` works with any hosted PUBLIC repo

**Cloning a repo that is not yours**:

Because you cloned this repo from an existing repo, git will try to push it to its original destination. For example, if you type `git remote -v` you will get the address of the cloned repo where Git thinks you want to push to.

That is fine if you are contributing, otherwise you need to update the address. Copy the **https_url** from the overview page for the repo you created for the clone, then use:

```sh
git remote set-url origin https_url
git remote -v
```

The `git remote set-url` command here changes an existing remote repository URL from it's original source to whatever you used for `https_url`.

Now git knows that the origin is your repo. Using `git remote -v` again is to check that git is pointing to the repo address you want.

Then to push the cloned repo files to _your_ repo use:

```sh
git push origin master
```

Where `origin` stands for the default branch of your repo.

You can also clone a specific branch with:

```sh
git clone -branch_name https_url
```

You can also clone the repo into a folder name that you want to use by adding that parameter to the end of the command:

```sh
git clone https_url app_folder_name
```

<!-- > I NEED NOTES ABOUT ORIGIN VS UPSTREAM HERE MAYBE -->

## Intermediate file notes

- <ins>Fast Forward Merge</ins>: is when the main branch does not have any changes so there are no merge conflicts and the merge happens automatically.
- <ins>Merge commits</ins>: happens when the merge is not a fast forward and there may or may not be conflicts. Regardless, main has commits that the branch does not have, have vice versa.

### branches

A branch is a version of your project. `master` or `main` is the primary or live or production version of your project. FYI, `main` is the preferred default name for your production branch.

You usually do not want to commit work-in-process (WIP) code to the master/main branch. Instead, create a new branch for each new feature of your project.

Before you create `new_branch`, you want to make sure that you have a clean working directory (no uncommitted changes). So do `git status` and your other basic commands before creating a new branch.

> If you don't do that, you are in for problems such as merge conflicts, so just check and then push.

Here are common commands you'll often use when working with branches:

```sh
git branch
git branch -a
# Should be git switch
git checkout branch_name
git checkout -b new_branch
git merge new_branch
git diff new_branch
```

I did not create branches until I started contributing for _freeCodeCamp_. If you are going to contrinute then you will have to learn about branches. Eventually you will want to create branches for your own projects.

New commands in detail (`git` removed for brevity):

| _Branch_ Git Commands      | Definition                                              |
| :------------------------- | :------------------------------------------------------ |
| git branch                 | Shows the branches in your repo                         |
| git branch branch_name     | create branch_name                                      |
| git checkout branch_name   | Switches to branch_name                                 |
| git checkout -b new_branch | Creates then switches to new_branch                     |
| git switch branch_name     | Switches to branch_name                                 |
| git switch -c new_branch   | Creates then switches to new_branch                     |
| git merge new_branch       | Merges 2 branches locally (don't do this!)              |
| git diff new_branch        | To check the differences between the two before merging |
| git push origin new_branch | push just the branch with the changes                   |
| git branch -d branch_name  | Delete the specified branch                             |
| git branch -D branch_name  | Force delete the specified branch                       |

**NOTE**: the branch with an asterisk (`*`) before it's name indicates that it is your current branch - the branch you are on.

If you push the branch with `git push origin new_branch`, back in your repo on GitHub you will see something like "...`new_branch` had recent pushes 2 minutes ago" and a button labeled _Compare and pull request_.

For a new branch, `git push` won't work because git doesn't know what branch you are pushing to, so run:

```sh
git push --set-upstream origin branch_name
```

**Note**: Using `--set-upstream` is the same thing as using `-u` mentioned in the BEGINNER_GIT file. Once again, `-u` is short-hand for `--set-upstream`.

When you push the changes for your branch to GitHub a PR (pull request) is created whether you are contributing to an open source repo or working on your own project.

> **Remember, you push the changes for your branch _from_ your branch, not from `master`.**

What `git pull` does is merge all the changes present in the remote repository to the local working directory (See the section [Staying up to date](#staying-up-to-date)).

NOTE: I used `git push origin fix/branch-name` instead of `git push --set-upstream origin fix/branch-name` and I got the above error when trying to delete the branch after it was merged and main updated.

- Squash your PR's - if something goes wrong then you can pull that commit out using `git revert commit_hash` - so squash will combine the commits into one and give a new commit hash
- if you have to use `git revert commit_hash` that will make a new commit which will undo the previous commit but the history of it will be there

If you go back to your local project and switch to master, the changes won't be there because they are only on GitHub. Assuming your PR was merged with the master branch, you need to pull the changes down to your local machine. To pull changes from GitHub to your machine use:

```sh
# if you have not set the upstream
git pull origin master
# After setting the remote
git pull
```

> **Make sure you are on the master branch when you run that command**

**NOTE**: Run `git status` to check the status of your local repo but it should also show a message of `Your branch is up to date with 'origin/master'`.

Miscellaneous commands that I am unsure of:

1. `git branch --sort=-committerdate # DESC`
1. `git branch -r --sort=-committerdate # DESC` where the flag `-r` is for just remotes.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Deleting branches

Once the PR is merged, you generally delete your branch and switch back to the master branch. To delete a branch use:

Check out the freeCodeCamp article [Git Delete Remote Branch – How to Remove a Remote Branch in Git](https://www.freecodecamp.org/news/git-delete-remote-branch/) for a great guide on the whole process.

### Git Remotes

- before we can push anything to GitHub, we need to tell Git about our remote repo on GitHub – we need to setup a "destination" to push up to – these "destinations" are knows as remotes – each remote is a URL where a hosted repository lives -
- `git remote` or `git remote -v` – display a list of remotes or nothing if you haven't added any remotes
- `git remote add <name> <url>` - to make a remote use, used when you clone – `name` = `origin` is the standard name or `upstream` for contributing, "Git, please remember this URL using this NAME"
- origin is just a convention, it is not a special keyword -
- `git remote rename <old> <new>` - to rename a remote but is not common to do -
- `git remote remove <name>` - to remove a remote
- it's common to have multiple remotes especially when working on open source projects

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Advanced file notes

### Forking and cloning

<dl>
  <dt><strong>Fork</strong>:</dt>
  <dd>Copies the forked repo into your account</dd>
</dl>

To fork a repo, go to the repository main page, then click the `Fork` button to the left of the `Star` button (upper right). I'm going to use the <a href="https://github.com/freeCodeCamp/freeCodeCamp" target="_blank">freeCodeCamp repo</a> as an example.

You will be taken to a page where you can rename the fork but leave it as it is and click _Create fork_. You will be redirected to the forked repo on your account with the note "_forked from user/repo-name_".

New commands in detail:

| _Fork_ Commands                | Definition                                            |
| :----------------------------- | :---------------------------------------------------- |
| `--depth=1 `                   | Creates a shallow copy of the repo                    |
| git remote add upstream        | Pull changes from the original repo...                |
| ...                            | &#10551; into the local clone of your fork            |
| git fetch upstream             | Update local repo with source repo objects            |
| git reset --hard upstream/main | Erases uncommitted changes                            |
| `--hard`                       | Resets the index and working tree                     |
| `--force`                      | reserved for a case where you do mean to lose history |
| ...                            | &#10551; use with caution                             |

**NOTES**:

- `git reset --hard upstream/main` erases any uncommitted changes. This is not a required command used every time you need to push changes to the remote repo - use it wisely and when needed. Or **ONLY** run as part of the original fetch process.
- `git push origin main --force`, you don't need to add the `--force`. Just doing a regular git push is fine. Or **ONLY** do it on the first push.
- You only use the `--set-upstream` parameter when you need to add **your LOCAL** branch to **your REMOTE** branch. But once the new branch is added to the remote repo, then you don't need to use `--set-upstream` each time.

> NOTE: Remember to add a label!

If you realize that you need to edit a file or update the commit message after making a commit use: `git commit --amend`

This will open up a default text editor like `nano` or `vim` where you can edit the commit message title and add/edit the description. I had a hard time figuring out how to quit out of that editor, but I think `CTRL + X` may do it. If that doesn't work try any of the following: `q`, `Q`, `exit`, `ESC`, `:WQ`, `ENTER`, or `CTRL + C`. One of those should work.

Actually, I believe to exit VIM use <kbd>ESC</kbd> + `:wq` or just `wq`.

Here is a comparison of cloning your repo vs. cloning someone else's repo vs. forking then cloning with the keyword `git` removed to save space:

| Command Description            |        Clone (Yours)        |      Clone (Not Yours)      |              Fork then Clone               |
| :----------------------------- | :-------------------------: | :-------------------------: | :----------------------------------------: |
| Fork                           |              -              |              -              |             Click Fork button              |
| Copy forked repo               |              -              |              -              |         clone --depth=1 https_url          |
| Copy repo at the URL           |       clone https_url       |       clone https_url       |                     -                      |
| Switch into cloned folder      |       cd folder_name        |       cd folder_name        |               cd folder_name               |
| Verify repo url                |              -              |          remote -v          |                 remote -v                  |
| Pull changes from the original |              -              |              -              |       remote add upstream https_url        |
| Add changes to staging         |            add .            |            add .            |                     -                      |
| Save changes to local          |  commit -m "First commit"   |  commit -m "First commit"   |                     -                      |
| Change your remote's URL       | remote add origin https_url | remote add origin https_url |                     -                      |
| Verify repo url                |          remote -v          |          remote -v          |                 remote -v                  |
| Fetch source                   |              -              |              -              |               fetch upstream               |
| Reset                          |              -              |              -              |         reset --hard upstream/main         |
| Push changes to remote         |    push -u origin master    |    push -u origin master    |          push origin main --force          |
| Check for differences          |              -              |              -              |             diff upstream/main             |
| Create branch                  |              -              |              -              |        checkout -b fix/branch-name         |
| Make changes                   |              -              |              -              |                     -                      |
| Add changes to staging         |            add .            |            add .            |                   add .                    |
| Save changes to local          |       commit -m "msg"       |       commit -m "msg"       |              commit -m "msg"               |
| Push changes to remote         |    push -u origin master    |    push -u origin master    |                     -                      |
| Initial branch push            |              -              |              -              | push --set-upstream origin fix/branch-name |
| Recurring pushes               |              -              |              -              |        push origin fix/branch-name         |

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### GitHub pull request process

Large repos will have various form fields to fill out. Here is an example of the steps you need to do from freeCodeCamp:

1. Put an `x` in the checkboxes,
1. Remove all the comment fields,
1. You can preview the message if you like,
1. Remove the phrase "Closes #XXXXX" unless your change closes an issue,
1. When done, click the green button **_Create pull request_**.

REMEMBER TO USE `fix: what-you-fixed` or `fix(curriculum)` in the PR Title or other prefixes like `feat`, `bug`, `chore`, `revert`, etc. And you can add to those, e.g. `fix(tools)` or `chore(deps)`.

If the PR is meant to address an existing GitHub Issue then, at the end of your PR's description body, use the keyword `Closes` with the issue number: `Closes #123`

Indicate if you have tested on a local copy of the site or not. Here are some of the notes from their PR page:

> This is very important when making changes that are not just edits to text content like documentation or a challenge description. Examples of changes that need local testing include JavaScript, CSS, or HTML which could change the functionality or layout of a page.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="pull-request-title">&#10551; Pull request title</h3>

**QUESTION**: What creates CHANGELOGs? Is it the use of the colon `:`? Learn more: [Why Use Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/#why-use-conventional-commits 'Conventional Commits').

<h3 id="pull-requests-page-notes">&#10551;  Pull request page notes</h3>

Check the values for the fields labeled `base fork` and `head fork`.

1. The `base repository` is the original source, the repo you forked and cloned, the public version.
1. The `head repository` is your local copy of the base repo.

Those fields should be correct but just be aware of the values. You will also see fields labeled just `base` which shows the branch of the original repo that you pushed to, and `compare` which shows the name of the branch you created and pushed.

**Note**: Large repos like the one for freeCodeCamp will have fields created in the pull request text area that I reference in the steps above. A smaller repo that you are contributing to may not have that setup. In the latter case, be as descriptive but also as brief as possible.

Also, if you scroll further down on the page you will see all the changes you made. After clicking the "Create pull request" button you will be taken to the source repo showing your pull request, other pull requests, the conversations for each, etc. Also, check the tabs **Checks**, **Files changed** and **Commits**.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="replies-to-your-pull-request">&#10551; Replies to your pull request</h3>

> Our moderators will now take a look and leave you feedback. You will get a message when a reviewer for the source repo adds a comment about your pull request...

Your changes will either be accepted or rejected. When the owner of the repo accepts your changes they will do so by clicking the **Merge pull request** button (or Squash for multiple commits pushed). If it is your repo you will then see a green button **Confirm merge**.

Then you will get a message that you can delete your local branch. Do that and also delete your local branch.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Other commands

Here is an interesting one: `gitk` shows the graphical interface for a local repository.

Here are variations of some of the commands above or common ones you may see:

```sh
git add -A
git add *.ext
```

I am not sure what these commands do, mostly because I believe these are advanced git commands but I have either used them with help from other people, or they are from my many pages of git notes:

```sh
git push -f
git reflog
git archive
# I think I've used prune before
git prune
git reset HEAD
git revert id
git config -l
git log --graph --decorate –oneline
git tag
git show
git stash -u
git branch login
git branch -vv
git remote update --prune
git rebase -i
git rebase -i HEAD~n
git bisect start
git bisect bad
git bisect good
git config --global core.autocrlf true
git command --help
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### git checkout

Various commands and topics using `checkout`

#### checking out old commits

- `git checkout` is like a swiss army knife – but the overloaded nature of `git checkout` is what led to the addition of `git switch` and `git restore` cmds -
- checkout can be used to 1. create branches, 2. switch to branches, 3. restore files, & 4. undo history
- `git checkout abc1234` – to view a previous commit – you can use `git log` to view commit hashes – you need the first 7 digits of a commit hash
- but you get the msg: error:

```bash
Your local changes to the following files would be overwritten by checkout: … Please commit your changes or stash them before you switch branches. Aborting.
```

- "Detached HEAD state" - I don't see that

> Any checkout of a commit that is not the name of one of your branches will result in detached HEAD. When we run `git checkout origin/blah`, we are no longer on a local branch. HEAD is pointing to a floating commit that is not rooted to any local branch

- I think with `git checkout hash` you can make experimental changes and commit them, you can discard any commits you make in this state w\o impacting any branches by switching back to a branch -
- you can go back many commits to see what things looked like back then -
- use `git log --oneline` to get the 7-digit hash -
- but basically that cmd jumps back in time -
- Normally, HEAD points to a particular branch reference – amd the branch reference points to the tip of the branch, the most recent commit – HEAD is always pointing to a branch – the branch you are currently on – HEAD refers to a branch reference NOT to a commit -
- but when you run this cmd you have HEAd refer to a commit NOT to a branch reference – it's not a normal "state" – you are technically now NOT on a branch -
- the file `.git/HEAD` normally shows `ref: refs/heads/main` – but now it has a commit hash in it -

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

#### re-attaching our detached HEAD

- you can examine the contents of the old commit – leave and go back to wherever you were before – or create a new branch and switch to it; and make and save changes -
- to go back to master you just have to switch/checkout to master -

> OH, you can do this (although it does not work for me), branch off and try something new – and you will not have any of the changes form commits that happened after that commit

#### referencing commits relative to HEAD

- `git checkout HEAD~1` or another num – `HEAD~1` will refer to the commit that comes before HEAD or the parent, `HEAD~2` is 2 commits before HEAD or the grandparent -
- HEAD / Master → last commit – then commit before is `HEAD~1`, before that is `HEAD~2`, before that is `HEAD~3`, etc
- for me `git checkout HEAD~1` had a lot of msgs in the terminal and the last line is: `HEAD is now at f12de6f Stash test` which is my last commit
- being that HEAD is now at `HEAD~1` you can again do `git checkout HEAD~1` to go back 1 commit from there – use `git switch master` to get back to the current state -
- another option to get out of this mode and go back to master or another branch is `git switch -` which will take you back to whatever branch you were on last

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

#### discarding changes with git checkout

- `git checkout HEAD <filename(s)>` - to revert a file back to what it looked like before you committed – that discards any changes in the file, reverting back to HEAD -
- because HEAD is pointing at the last commit thru the brach and your saved changes (not committed) are not there -
- `git checkout -- <file1> <file2>` - is an alternate way to do the same thing

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### More miscellaneous commands

These are mainly to undo changes or to go back in time.

| cmd                                       | use    |
| :---------------------------------------- | :----- |
| git checkout                              | varied |
| git checkout abc1234                      |        |
| git checkout hash                         |        |
| git checkout HEAD~1                       |        |
| git checkout HEAD `<filename(s)>`         |        |
| git checkout -- `<file1>` `<file2>`       |        |
| git checkout HEAD `<file-name>`           |        |
| git restore                               |        |
| git restore --staged `<file>`             |        |
| git restore `<file-name>`                 |        |
| git restore filename                      |        |
| git restore --source HEAD~1 `<file-name>` |        |
| git restore --staged `<file-name>`        |        |
| git reset                                 |        |
| git reset `<commit-hash>`                 |        |
| git reset --hard `<commit-hash>`          |        |
| --hard                                    |        |
| git revert                                |        |
| -                                         | -      |
| git rebase                                |        |

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Terminology

Here are some common terms. These notes are from git, MDN, and other sources:

1. **Staging area**: From Git SCM, "_Staged means that you have marked a modified file in its current version to go into your next commit snapshot_".
1. **`push`**: To send your committed changes to a remote repo, to upload local repo content to a remote repo.
1. **`pull`**: Pulling a branch means to fetch it and merge it; fetches and merges changes on the remote server to your working directory.
1. **`fetch`**: adding changes from the remote repository to your local working branch without committing them.
1. **`upstream`**: the primary _branch_ on the original repository; where you cloned the repo from.
1. **`origin`**: The default upstream repository - a reference to the remote repository from where a project was initially cloned.
1. **`remote` / `remote repository`**: the version of a repository or branch that is hosted on a server (like GitHub), a shared repository that all team members use to exchange their changes.
1. **`clone`**: used to make a copy of the target repository; a copy of a repo that lives on your computer.
1. **`merge`**: bring the contents of another branch into the current branch; to take the data created on a separate branch and integrate them into a single branch.
1. **`head`**: A named reference to the commit at the tip of a branch.
1. **`HEAD`**: your current branch, or a defined commit of a branch, usually the most recent commit at the tip of the branch, or refers to the current commit you are viewing. `HEAD` is a reference to one of the heads in your repository.
1. **`blob`**: (Binary Large OBject) Untyped object, e.g. the contents of a file, is the object type used to store the contents of each file in a repository.

Here are some terms I need to look into or need to understand better:

1. detached HEAD
1. upstream vs origin
1. `git tag`: most often tags are used to mark different releases or versions
1. `git show`
1. `git branch login`
1. `git bisect`

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>
