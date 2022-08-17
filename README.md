# Beginner Git commands

The basic steps you need in the beginning are:

1. Download and install Git (one time ony)
1. Create an empty repo on GitHub
1. Initialize Git in a project folder
1. Make changes or create a file
1. Add the changes to staging then commit the changes
1. Push your changes or project files to your empty repo

If you created any files on Github, then you will have to use `git pull` before you can do a `git push`. So in the beginning, don't create any files on GitHub.

<a id="back-to-top"></a>

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _</p>

## Table of contents

Section A:

1. [Download and setup Git](#download-and-setup-git)
1. [Pushing your local files to an empty repo](#pushing-your-local-files-to-an-empty-repo)
   1. [Commands after initial push](#commands-after-initial-push)
1. [Clone your own repo](#clone-your-own-repo)
1. [Clone an existing repo](#clone-an-existing-repo)
   1. [Push the cloned files up to your repo](#push-the-cloned-files-up-to-your-repo)

Section B:

[Intermediate Git Commands](#intermediate-git-commands)

1. [Branches](#branches)
   1. [Pushing branches to your repository](#pushing-branches-to-your-repository)
   1. [Common issues with branches](#common-issues-with-branches)
1. [Forking and cloning](#forking-and-cloning)
1. [GitHub pull request process](#github-pull-request-process)
   1. [Pull request title](#pull-request-title)
   1. [Pull requests page notes](#pull-requests-page-notes)
   1. [Replies to your pull request](#replies-to-your-pull-request)
   1. [Staying up to date](#staying-up-to-date)
   1. [Handling merge conflicts](#handling-merge-conflicts)
1. [Miscellaneous git commands](#miscellaneous-git-commands)
   1. [gitignore](#gitignore)
   1. [Mistakes](#mistakes)
1. [Reference links](#reference-links)
1. [Final notes](#final-notes)
   1. [Terminology](#terminology)

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _</p>

## Download and setup Git

It's been well over a year since I did this so I can't remember all the steps, but you will need to [download Git](https://git-scm.com/downloads "Git download page").

Check out this video from the YouTube channel LearnWebCode: [Git Tutorial Part 3: Installation, Command-line & Clone](https://youtu.be/UFEby2zo-9E "Git Tutorial"). I followed his steps to run the `config` commands below. Follow his instructions using Git Bash. Eventually, you will use VS Code for 99% of the commands in this guide.

**Note**: On your first push ever to GitHub, you will need to provide a `user name` and `email address` to git, the ones used when you created your GitHub account. This is so git knows that you are who you say you are.

Ater downloading Git, open the `.exe` file in your downloads folder. Then find Git Bash and open it. For me on Windows, there was a Git folder in my Start ment and Git bash was in there. Open it and in the command prompt that opens enter the following commands:

```bash
git config --global user.name "Github user name"
git config --global user.email "youremail@somewhere.com"
```

The `git config` command is used initially to configure the `user.name` and `user.email` fields. This specifies what email and username will be used from a local repository.

The `--global` flag tells Git that you're going to use the email above for all repos on your computer. Replace that with `--local` to use different emails for different repos.

Some people mention using an SSH key to validate your identity. An SSH key is another way to identify yourself to Github instead of using a username and password. I found that a little confusing so I prefer using username and password.

Also, try the following command to see all the configuration settings:

```bash
git config --list
```

Run that command and scroll down and look for `user.name="Yourname"` and `user.email="your-email@whatevs.com"`, though until you set those values you either will not see those fields or they will be set to empty strings.

> As of August 12th, 2022 I do not see the values with that command (?). Not in VS Code, Git Bash or the Windows Command Prompt.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _</p>

## Pushing your local files to an empty repo

Here are the commands followed by a brief definition. Make sure to know these because they are used for other sections in this file. By the way, you need to make changes to your files or create a file before running `git add .` unless you already have files in your project folder.

Go to GitHub and create an empty repo, meaning no README file. Then back in Git Bash or VS Code run:

```bash
git init
git add .
git commit -m "First commit"
git branch -M main
git remote add origin https_url
git push -u origin master
```

**NOTE**: I removed `git` from the commands in all the definition tables to make the table smaller. You should know to add `git` before the main commands (not for the parameters).

| _Basic_ Git Commands | Definition                                                                      |
| :------------------- | :------------------------------------------------------------------------------ |
| init                 | Initiates git tracking                                                          |
| status               | Checks the status of your changes/state                                         |
| add .                | Adds **_ALL_** (.) changes to staging                                           |
| commit -m "msg"      | Saves changes to local machine                                                  |
| remote add origin    | Adds URL as remote repo location                                                |
| `branch -M main`     | Changes default branch to 'main' (optional)                                     |
| push -u origin main  | Push changes to and sets remote                                                 |
| push                 | Push changes after upstream is set                                              |
| push origin main     | Used for 1st push if `-u` flag was not used                                     |
| `-u`                 | Parameter short for `upstream`                                                  |
| `upstream`           | the primary _branch_ on the original repository; where you cloned the repo from |

The `git init` command creates a new local GIT repository in the directory you ran that command.

The command `git branch -M main` is optional and I think the flag `-M` means changing the default branch name from master to the name **main**. I tried searching for it and I found that Git has changed the default branch name from `master` to `main` though GitHub still uses `master` by default. It's your choice.

The command `git remote add origin https_url` connects the local repository to a remote server (GitHub repo). `https_url` is the URL that is on the page when you create a new repo. It is also shown whn you click the `Code` button.

The `git push` command is used to send local commits to the master (or main) branch of the remote repository. But to use `git push` in the future you have to set something called an _upstream_, meaning where you want to push it to by default. That is why you use `-u`. The whole command `git push -u origin master` pushes your commits and sets the branch `master` as the origin for the location of `git push` in the future.

The keyword `origin` means the branch you want to push to. Replace `master` with the branch where you want to push your changes when you’re _not_ intending to push to the master branch (See the Branch section).

**NOTE**: You can add a second `-m` flag to your commit command to add a description:

```sh
git commit -m "commit msg" -m "commit description"
```

**NOTE**: When you create an empty repo on GitHub, I believe it's best practice to use the same name on GitHub for the folder of your local copy, though you can still push if the names do not match.

<!-- &#8627; -->
<!-- &#8640; -->
<!-- &#8674; -->
<!-- &#8702; -->
<!-- &#10230; -->
<!-- &#10511; -->

<!-- &#10551; -->
<!-- &#10559; -->

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="commands-after-initial-push">&#10551; Commands after initial push</h3>

Now your local repo is connected to your remote repo on Github. After making some changes or creating new files use:

```bash
git add .
git status
git commit -m "Created README file"
git push
```

**Note**: I'll repeat this again: You need to use `git push -u origin master` for the first commit. After that just use `git push`. Although I believe you can still use `git push origin master` and it won't have a negative effect it's just unnecessary.

Also, the flag `-u` is not needed if you are pushing to the default branch. And `-u` is short for `--set-upstream` which is what you would use when you are pushing a branch you created locally for the first time. By using that flag you set that as the default when you push the main or other branch to GitHub.

Also, I use `git status` as a habit to check the status of the files, though that command is not required. If you modified an existing file you can use `git commit -am "msg"` which combines **_add_** (`a`) amd **_message_** (`m`).

These commands work for me when pushing to a repo I created without a README file. If you have a README file, then you will get an error when trying to push, so you'll have to do a `git pull` command to pull the README to your local repo then you can use `git push`.

Here is a comparison of my commands vs. the commands you see on GitHub when you create an empty repo (there is only 1 difference). I am also tacking on the standard `add`, `commit`, and `push` commands.

Commands in detail:

| Command Description           |             My Git commands | GitHub commands             |
| :---------------------------- | --------------------------: | :-------------------------- |
| Initiate tracking             |                        init | init                        |
| Make changes                  |                           - | -                           |
| Add changes to staging        |                       add . | add README.md               |
| Save changes to local         |    commit -m "First commit" | commit -m "First commit"    |
| Change default branch to main |                           - | branch -M main              |
| Adds url as remote repo       | remote add origin https_url | remote add origin https_url |
| Verify repo url               |                   remote -v | remote -v                   |
| Push changes to remote        |       push -u origin master | push -u origin master       |
| Make changes                  |                           - | -                           |
| Add changes to staging        |                       add . | add .                       |
| Saves changes to local        |     commit -m "Next commit" | commit -m "Next commit"     |
| Push changes to remote        |       push -u origin master | push -u origin master       |
| Recurring pushes              |                        push | push                        |

NOTE: You can add your files to staging and commit them in one command with the `-am` flag with the `commit` command:

```bash
git commit -am "Commit message"
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _</p>

## Clone your own repo

Why would you do this? Use this when you created a repo and added a file on GitHub like a README.md file. Or if for some reason you have a commit and issues history that you want to copy, though who would have that? Regardless, the process is almost identical to cloning a repo that is not yours:

```sh
git clone https_url
cd folder_name
git remote -v
git remote add origin https_url
git remote -v
git push -u origin master
```

New commands in detail:

| _Clone_ Git Commands  | Definition                              |
| :-------------------- | :-------------------------------------- |
| clone                 | Copies repo at the URL to your machine  |
| remote -v             | Checks where your local copy points to  |
| remote set-url origin | Sets the URL to point towards your Repo |

The command `git clone` also initiates a git repo for the repo you want to clone, but git is installed in the downloaded/cloned folder, _NOT_ in the directory where you ran that command. But both initiate git tracking.

`git clone` is used on its own or when you Fork a repo. Use `cd` to switch to that folder.

Use `git remote -v` to list the remote repository that is connected to this project. That is to check if you are pointing to the cloned URL or the copy of the repo in your account. Did you fork and clone to contribute, or to work on your own version of the repo?

`remote set-url origin` here sets your repo as the source URL as opposed to changing the URL if cloned from a different account (see next section). It's function is similar to `remote add origin` in the first section.

Then make some changes and run the standard commands:

```sh
git status
git add .
git commit -m "First commit"
git push
```

That all works for your repos, but eventually you will want to clone, or fork and clone a repo so that you can contribute to it. You will then need to use the `git clone` again, and various `branch` git commands. You will also need to add additional parameters to your git commands (see [Forking and cloning](#forking-and-cloning) section)

**NOTE**: This is an alterate way of initializing a local git repo than what is in the section [Pushing your local files to an empty repo](#pushing-your-local-files-to-an-empty-repo). The differece though is that this method installs git in the cloned file folder and not in the directory where you run `git clone url`, whereas in the section linked above it installs git in that folder.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _</p>

## Clone an existing repo

For when you want to work on a repo that someone else created. Go to GitHub and create an empty repo. Then back in Git Bash or VS Code run:

```sh
git clone https_url
cd folder_name
git remote -v
```

You can also clone a specific branch with:

```sh
git clone -branch_name https_url
```

You can also clone the repo into a folder name that you want to use by adding that parameter to the end of the command:

```sh
git clone https_url app_folder_name
```

Once again, since you did not fork this repo, but instead you want a copy of it to work on for yourself, you need to first push it up to your empty GitHub repo. See the next section for the details on that...

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="push-the-cloned-files-up-to-your-repo"> &#10551; Push the cloned files up to your repo</h3>

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

Where `origin` stands for the default branch of your repo.. Then after making changes use:

```sh
git add .
git commit -m "First commit"
git push -u origin master
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<br />

<img align="center" src="https://github.com/Kernix13/Kernix13/blob/main/assets/divider-github.png" alt="divider" title="Testing a 16px high gradient PNG image as a divider and spacer, should be 8px maybe and change the gradient colors" />

# Intermediate Git Commands

From here the commands are a little more involved and are for when you start creating your own branches and/or contributing to open source projects.

<!-- <p>_ _ _ _ _ _ _ _ _ _</p> -->
<br>

## Branches

A branch is a version of your project. `master` or `main` is the primary or live or production version of your project. `main` is the preferred default name for your production branch.

You usually do not want to commit work-in-process (WIP) code to the master/main branch. Instead, create a new branch for each new feature of your project.

Before you create `new_branch`, you want to make sure that you have a clean working directory (no uncommitted changes). So do `git status` and your other basic push commands before creating a new branch.

Here are common commands you'll often use when working with braches:

```sh
git branch
git branch -a
git checkout branch_name
git checkout -b new_branch
git merge new_branch
git diff new_branch
```

I did not create branches until I started contributing for _freeCodeCamp_. If you are going to contrinute then you will have to learn about branches. Eventually you will want to create branches for your own projects.

New commands in detail (`git` removed for brevity):

| _Branch_ Git Commands  | Definition                                              |
| :--------------------- | :------------------------------------------------------ |
| branch                 | Shows the branch you are working on                     |
| branch branch_name     | create branch_name                                      |
| branch -a              | Lists all the branch names in your repo                 |
| checkout branch_name   | Switches to branch_name                                 |
| checkout -b new_branch | Creates then switches to new_branch                     |
| merge new_branch       | Merges 2 branches locally                               |
| diff new_branch        | To check the differences between the two before merging |
| push origin new_branch | push just the branch with the changes                   |

After you merge your branck into main/master, push the master branch up to github as you normally would: `git push origin master` or `git push`.

> I think that is wrong. Merging into master is a local merge. I had problems doing that.

If you push the branch with `git push origin new_branch`, back in your repo on GitHub you will see something like "...`new_branch` had recent pushes 2 minutes ago" and a button labeled _Compare and pull request_.

Miscellaneous (not sure what this is): `git branch --sort=-committerdate # DESC` and `git branch -r --sort=-committerdate # DESC` where the flag `-r` is for just remotes.

Recap:

```sh
# check what branch you are on
git branch
# create new branch
git checkout -b new_branch
# make changes, add, commit, push
git status
git add .
git commit -m "commit msg"
git push --set-upstream origin new_branch
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="pushing-branches-to-your-repository">&#10551; Pushing branches to your repository</h3>

You can merge branches locally, but more commonly you will push the changes to GitHub then make a PR (pull request) whether you are contributing or working on your own project. Make sure you **switch from main/master back to your branch** before doing that!.

For a new branch, `git push` won't work because git doesn't know what branch you are pushing to, so run:

```sh
git push --set-upstream origin branch_name
```

**Note**: Using `--set-upstream` is the same thing as using `-u` in the sections above. Actually, `-u` is short-hand for `--set-upstream`.

Then after setting the upstream for your new branch you can do the usual:

```sh
git add .
git commit -m "fixes on new_branch"
git push
```

Remember, you push the changes for your branch _from_ your branch, not from `master`.

Then back on your repo main page you should see the **Compare & Pull Request** button. Clicking it takes you to a page titled "_Open a pull request_" where you can add a description. Then click the "_Create pull request_" button. That takes you to the "_Pull requests_" tab where you can click the _Merge pull request_ button and click _Confirm merge_ if you are done, or you can continue to push changes from your branch.

If you have multiple commits for that branch, select _Squash and merge_ option from the dropdown list under _Compare and merge_. You can also click on the Files changed tab, and click the `+` button that appears when you hover over the code, and make a comment on a line of code. You can add a description for the comment and also click the "Resolve conversation" button. Or click Merge pull request.

**Note**: A PR from your branch to the master branch is a request to have your code merged with the master branch. You can, and should (see below), delete your branch when your code/changes are merged.

If you go back to your local project and switch to master, the changes won’t be there because they are only on GitHub and you need to pull them down to your local machine. To pull changes from GitHub to your machine use:

```sh
git pull origin master
```

Or just `git pull` if you set the upstream already. **Make sure you are on the master branch**. What `git pull` does is merge all the changes present in the remote repository to the local working directory (See the section [Staying up to date](#staying-up-to-date)).

**NOTE**: Do `git status` to check the status of your local repo but it should also show a message of `Your branch is up to date with 'origin/master'` if you have the default set as the origin.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="common-issues-with-branches">&#10551; Common issues with branches</h3>

You may run into issues when you start working with branches. Here are some that I encountered.

<br>

**--> Checkout to other branches before pushing**:

If you continue working on your branch, you can't just checkout to `master` or some other branch. Thankfully, Git will warn you that switching to a different branch will result in the loss of your changes:

> error: Your local changes to the following files would be overwritten by checkout: <br>
> README.md <br>
> Please commit your changes or stash them before you switch branches. <br>
> Aborting

The `stash` command is an advanced command IMO, so run `git add .` and `git commit -m "message"` before switching to a different branch.

**NOTE**: I did that, switched back to my branch, then ran `git push` and there was nothing on my Github page? I'm not sure why, but you do not get a message for pull requests after you click the "_Create pull request_" button...(Double check that)

<br>

**--> Continue to work after pushing changes**:

...but because I already pushed and continued working, I had to go to the _Conversation_ tab and click _Merge pull request_ (I was 5 commits behind).

So don't merge until you are done making changes and push the changes. Or don't push until you are done with the branch!

> These notes are questionable. There is a drop-down list with the option of **Squash and merge** so you can keep working on your branch after pushing. Keep pushing on the same branch until you are done.

<br>

**--> Deleting branches**:

Once the PR is merged, you generally delete your branch and switch back to the master branch. To delete a branch use:

```sh
# check the branch you are on:
git branch
# checkout to master if not on master
git checkout master
# delete the new branch that you pushed and merged
git branch -d branch_name
```

If you get this error when trying to delete a branch:

> error: The branch `branch-name` is not fully merged.
> If you are sure you want to delete it, run `git branch -D branch-name`.

It's probably because something in your local branch has not actually made it to the remote repository. To find out what commits have not been merged from your source branch to a target branch run:

```sh
git log branch_name --not main
```

That will show you what has been changed and what has not been pushed to main (or maybe has not been merged). If you are fine with the differences then replace `-d` with `-D`.

It appears that after the PR from your branch has been merged and you _do not_ delete it, there is not a way to delete it from GitHub. When that happens run:

```sh
#  delete branch remotely
git push origin --delete branch_name
```

When you create a branch, push the changes, merge it into master, then delete it from GitHub, locally the branch will show when you run `git branch -a` even after you delete it. To get rid of the local branch use:

```sh
git fetch -p
```

From freeCodeCamp, here is what the `-p` flag does:

> The `-p` flag means "prune". After fetching, branches which no longer exist on the remote will be deleted.

Double-check that the branch is gone with `git branch`.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ </p>

## Forking and cloning

<dl>
  <dt><strong>Fork</strong>:</dt>
  <dd>Copies the forked repo into your account</dd>
</dl>

To fork a repo, go to the repository main page, then click the `Fork` button to the left of the `Star` button (upper right). I'm going to use the <a href="https://github.com/freeCodeCamp/freeCodeCamp" target="_blank">freeCodeCamp repo</a> as an example.

After you fork a repo, open up a terminal with Git Bash and navigate to the folder where you want the cloned repo. Then enter the following commands:

```bash
git clone --depth=1 https://github.com/User_Name/freeCodeCamp
cd folder-name
```

Next, add a remote reference to the main freeCodeCamp repo, or whatever repo you are cloning after forking, then check the configuration:

```sh
git remote add upstream https://github.com/freeCodeCamp/freeCodeCamp.git
# check the location
git remote -v
```

Then use `git status` and `git checkout main` if not on main. Next:

1. Update your local copy of the freeCodeCamp upstream repository,
1. Hard reset your main branch with the freeCodeCamp main,
1. Push your main branch to your origin to have a clean history on your fork on GitHub,
1. And validate your current main matches the upstream/main by performing a diff:

```sh
git fetch upstream
git reset --hard upstream/main
git push origin main --force
git diff upstream/main
```

The 1st command is necessary for the clone to fetch the files, the 4th is optional. Use #2 & #3 with caution - read up on them. The commands above are from freeCodeCamp docs.

**NOTE**: `git fetch upstream` is used to fetch all objects from the remote repo that don’t currently reside in the local working directory. You'll also often see`git fetch origin`. `git diff upstream` checks for a difference between a branch and its upstream source.

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

New commands in detail:

| _Fork_ Commands            | Definition                                            |
| :------------------------- | :---------------------------------------------------- |
| `--depth=1 `               | Creates a shallow copy of the repo                    |
| remote add upstream        | Pull changes from the original repo...                |
| ...                        | &#10551; into the local clone of your fork            |
| fetch upstream             | Update local repo with source repo objects            |
| reset --hard upstream/main | Erases uncommitted changes                            |
| `--hard`                   | Resets the index and working tree                     |
| `--force`                  | reserved for a case where you do mean to lose history |
| ...                        | &#10551; use with caution                             |

**NOTES**:

> `git reset --hard upstream/main` erases any uncommitted changes. This is not a required command used every time you need to push changes to the remote repo - use it wisely and when needed. Or **ONLY** run as part of the original fetch process.

> `git push origin main --force`, you don’t need to add the `--force`. Just doing a regular git push is fine. Or **ONLY** do it on the first push.

> You only use the `--set-upstream` parameter when you need to add **your LOCAL** branch to **your REMOTE** branch. But once the new branch is added to the remote repo, then you don’t need to use `--set-upstream` each time.

MY FINAL COMMANDS (clone, fetch, push):

```sh
git clone --depth=1 https_url
git remote add upstream https_url
git fetch upstream
git remote -v
git push origin main
```

THEN: create branch, make changes, and push them

```sh
git checkout -b fix/branch-name
git add .
git commit -m "short description"
git push --set-upstream origin fix/branch-name
```

Use that last `git push` only for the first time, then use `git push origin fix/something-typos`. Here is the last command AFTER you set the upstream:

```sh
git push origin fix/branch-name
```

If you realize that you need to edit a file or update the commit message after making a commit you can do so after editing the files with:

`git commit --amend`

This will open up a default text editor like `nano` or `vi` where you can edit the commit message title and add/edit the description.

Here is a comparison of cloning your repo vs. cloning someone else's repo vs. forking then cloning:

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

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ </p>

## GitHub pull request process

After you push your changes, go to your cloned copy of the repo on GitHub. You should see a green button labeled **_Compare & pull request_**. If you do not see it then click the Pull requests link to go to that tab.

Click the "Compare & pull request" button and notice the page title of **_Open a pull request_** and the paragraph in the section below the title saying **_Able to merge. These branches can be automatically merged._**

You can then edit your commit message if need be. In the body of your PR include a more detailed summary of the changes you made and why.

Large repos will have various form fields to fill out. Here is an example of the steps you need to do from freeCodeCamp:

1. Put an `x` in the checkboxes,
1. Remove all the comment fields,
1. You can preview the message if you like,
1. Remove the phrase "Closes #XXXXX"
1. When done, click the green button **_Create pull request_**.

REMEMBER TO USE `fix: what-you-fixed` or `fix(curriculum)` in the PR Title or other prefixes like `feat`, `bug`, `chore`, `revert`, etc. And you can add to those, e.g. `fix(tools)` or `chore(deps)`.

If the PR is meant to address an existing GitHub Issue then, at the end of your PR's description body, use the keyword `Closes` with the issue number: `Closes #123`

Indicate if you have tested on a local copy of the site or not. Here are some of the notes from their PR page:

> This is very important when making changes that are not just edits to text content like documentation or a challenge description. Examples of changes that need local testing include JavaScript, CSS, or HTML which could change the functionality or layout of a page.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="pull-request-title">&#10551;    Pull request title</h3>

The convention has the following format:

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

Keep it short (less than 30 characters) and simple, you can add more information in the PR description box and comments. Example: `fix(api,client): prevent CORS errors on form submission`.

**QUESTION**: What creates CHANGELOGs? Is it the use of the colon `:`? Learn more: [Why Use Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/#why-use-conventional-commits "Conventional Commits").

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="pull-requests-page-notes">&#10551;  Pull request page notes</h3>

Check the values for the fields labeled `base fork` and `head fork`.

1. The `base repository` is the original source, the repo you forked and cloned, the public version.
1. The `head repository` is your local copy of the base repo.

Those fields should be correct but just be aware of the values. You will also see fields labeled just `base` which shows the branch of the original repo that you pushed to, and `compare` which shows the name of the branch you created and pushed.

**Note**: Large repos like the one for freeCodeCamp will have fields created in the pull request text area that I reference in the steps above. A smaller repo that you are contributing to may not have that setup. In the latter case, be as descriptive but concise as possible.

Also, if you scroll further down on the page you will see all the changes you made. And after clicking the "Create pull request" button you will be taken to the source repo showing your pull request, other pull requests, the conversations for each, etc. Also, check the tabs **Checks**, **Files changed** and **Commits**.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="replies-to-your-pull-request">&#10551; Replies to your pull request</h3>

> Our moderators will now take a look and leave you feedback. You will get a message when a reviewer for the source repo adds a comment about your pull request...

Regardless, your changes will either be accepted or rejected. When the owner of the repo accepts your changes they will do so by clicking the **Merge pull request** button. If it is your repo you will then see a green button **Confirm merge**.

Then you will get a message that you can delete your local branch - do that.

<h3 id="staying-up-to-date">&#10551; Staying up to date</h3>

Once you are done with your PR and start to work on something else, the repo has most likely had changes by other contributors so your copy is behind. You need to update your local copy of the repo before making new changes:

```sh
git checkout master
git pull upstream master
```

I actually use `git fetch upstream` to update my local clone. I'm not sure if `git pull upstream master` is better or not. However, I had a PR fail because I was missing a command. `git fetch upstream` will only fetch the git data. To update your main fully, you should:

```sh
git checkout master
git fetch upstream
git merge upstream/master
```

So run `git merge upstream/master` every time before making your changes and doing a push. That will ensure you always have the latest state of `master` locally.

The main thing to know is that the master branch will most likely updated regularly as you are working on your branch. You will want to pull those changes down to your local master branch. Then you will want to checkout to your branch and use `git merge master` to keep your branch up to date with what is going on with master. This is where you may get a merge conflict.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="handling-merge-conflicts">&#10551; Handling merge conflicts</h3>

I'm a little fuzzy on this process. There are a few of ways to handle merge conflicts: 1) on Github, 2) in your terminal, or 3) the easiest is directly in your code.

Read more here: [Conflicts on a pull request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md#making-changes-locally "Making changes locally").

A merge conflict is when 2 or more people change the same code/content but with different values. However, I don't think a beginner contributor would actually run `git merge branch_name`.

But if you did ad there was a conflict, in VS Code you will see something like:

```sh
<<<<<<< HEAD (Current Change)
<p>some change here</p>
=======
<p>different change here</p>
>>>>>>> Branch-Name (Incoming Change)
```

Where `HEAD` is your current branch, usually main/master. Once again, this would only be done by the owner of the repo, but what you would do is:

1. Decide which change you want to keep,
1. Delete EVERYTHING else -> the change you don't want and the equal, less than, and greater than signs along with the text like `HEAD` and `Current Change`. Everything other than the actual change that you want.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _</p>

## Miscellaneous git commands

### gitignore

To have git ignore any files that you do not want to push, create a file called `.gitignore` in the root of your project file. Add the paths and file names for those files:

```git
index.html
js/test.js
```

For large repositories, this file will have a lot of entries. For some npm commands like `npx create-react-app` this file will be created for you. Here is the ignore file from a project where I used that command:

```sh
# dependencies
/node_modules
/.pnp
.pnp.js

# testing
/coverage

# production
/build

# misc
.DS_Store
.env.local
.env.development.local
.env.test.local
.env.production.local

npm-debug.log*
yarn-debug.log*
yarn-error.log*
```

Here is an example of a basic gitignore file. You want to always add `node_modules` even if you have not added any NPM packages. You might in the future and accidentally push that folder:

```sh
# Packages
node_modules

# Ignore /build and docs directories
/build
docs/

# Numerous always-ignore extensions
*.diff
*.err
*.orig
*.log
*.rej
*.swo
*.swp
*.vi
*~
*.sass-cache

# ignore all files starting with . or ~
.*
~*

# ignore composer vendor directory
/vendor

# ignore Editor files
*.sublime-project
*.sublime-workspace
*.komodoproject

# ignore log files and databases
*.log
*.sql
*.sqlite

# ignore compiled files
*.com
*.class
*.dll
*.exe
*.o
*.so

# ignore packaged files
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip

# ignore private/secret files
*.der
*.key
*.pem

# track these files, if they exist
!.editorconfig
!.env.example
!.gitignore
!.nvmrc
!.phpcs.xml.dist
```

That's a lot. Try this as a beginner template:

```sh
# Dependencies
node_modules

# Production and other folders
/build
/dist

### VisualStudioCode ###
.vscode/*

# Windows thumbnail cache files
Thumbs.db
Thumbs.db:encryptable
ehthumbs.db
ehthumbs_vista.db

# Numerous always-ignore extensions
*.diff
*.env
*.err
*.log
*.sass-cache
*.tmp
```

### Mistakes

**Undo Staging**: If you accidentally added a file with `git add .`, to remove it from the staging area, use:

```sh
# without arguments
git reset
# with filename and optional path
git reset path/filename.ext
```

**Undo a Commit**: Use use `git reset` again but include `HEAD` which means the last commit. But to undo the last coomit add `~1` to go back 1 commit past the last commit which will undo the last commit:

```sh
git reset HEAD~1
```

But what if you want to go back a number of commits or to a specific commit. First use `git log` which gives you a list of your commits in reverse chronological order. You can scroll down the log with SPACEBAR.

You will see the commit hash and the commit message along with other information. To go back to a specific commit, use the hash for it:

```sh
# use git reset HASH:
git reset e220bfb1e34b8c6b6fce1deb7884244239284716
```

That will unstage any changes made to the file(s) AFTER that commit. The changes will be in your files but they will not be saved into git any more. But how do you get rid of all the changes after a certain point? USe the same command but add the flag `--hard`:

```sh
git reset --hard e220bfb1e34b8c6b6fce1deb7884244239284716
```

**Remove Git**: To remove git tracking from a folder use the following command in `git bash`, the command prompt or in VS Code:

```sh
rm -rf .git
```

Here is an interesting one: `gitk` shows the graphical interface for a local repository.

Here are variations of some of the commands above or common ones you may see:

```sh
git log
git add -A
git add *.ext
git add filename
git --version
git rm –cached filename
git merge --abort
git diff filename.ext
git fetch
```

Here are some command prompt commands you may need: `clear`, `q`, `Q`, `exit`, `ESC`, `:WQ`, `ENTER`, `pwd`, <kbd>CTRL</kbd>+<kbd>C</kbd>.

I am not sure what these commands do, mostly because I believe these are advanced git commands but I have either used them with help from other people, or they are from my many pages of git notes:

```sh
git push -f
git reflog
git archive
git prune
git reset HEAD
git revert id
git config -l
git log --graph --decorate –oneline
git stash
git stash pop
git tag
git show
git branch login
git branch -vv
git remote update --prune
git rebase -i
git rebase -i HEAD~n
git bisect start
git bisect bad
git bisect good
git config --global core.editor "code –wait"
git config --global core.autocrlf true
git command --help
```

Reference logs record everything you do with your local branch. Use `git reflog` to show everything you did in previous steps - find the entry where you think you want to go back to. Then use `git checkout HEAD@{12}` or`git reset HEAD@{3}` to get back to that state, where `HEAD@{12}` and `HEAD@{3}` are just using example numbers. Just run it and you'll see what I mean.

I had to run the following to fix one of my mistakes:

```sh
git checkout fix/some-branch-name
git fetch upstream
git rebase -i upstream/main
git push -f
```

Is this how you add a description?

```sh
git commit -m "Title" -m "Description .........."
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _</p>

## Reference links

FYI, it's difficult keeping this list up-to-date. I'll do my best to provide the best resources that I find and that work for me.

To search for a gist on GitHub: `https://gist.github.com/username/`

1. [Git reference docs](https://git-scm.com/docs "Git documentation")
1. [GitHub for complete beginners MDN](https://developer.mozilla.org/en-US/docs/MDN/Contribute/GitHub_beginners "MDN GitHub docs")
1. [Why Use Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/#why-use-conventional-commits "Conventional Commits")
1. [Contribute to freeCodeCamp.org](https://contribute.freecodecamp.org/#/ "freeCpdeCamp contribution docs")
1. [how-to-setup-freecodecamp-locally.md](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md "How to setup freeCodeCamp locally")
1. [freeCodeCamp Conflicts on a pull request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md#making-changes-locally "freeCodeCamp PR Conflicts")
1. [freeCodeCamp Introduction](https://contribute.freecodecamp.org/#/index "freeCodeCamp contribution intro")
1. [freeCodeCamp How to work on coding challenges](https://contribute.freecodecamp.org/#/how-to-work-on-coding-challenges "freeCodeCamp: Working on coding challenges")
1. [freeCodeCamp FAQs](https://contribute.freecodecamp.org/#/FAQ "freeCodeCamp FAQs")
1. [freeCodeCamp How to open a Pull Request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-open-a-pull-request.md "How to open a PR freeCodeCamp")
1. [freeCodeCamp How to contribute to open source](https://github.com/freeCodeCamp/how-to-contribute-to-open-source "How to contribute to open source")
1. [How to contribute on GitHub](https://www.dataschool.io/how-to-contribute-on-github/ "Step-by-step guide to contributing on GitHub")
1. [Contributing to MDN](https://developer.mozilla.org/en-US/docs/MDN/Contribute "Contributing to MDN")
1. [Hostinger: Basic GIT Commands](https://www.hostinger.com/tutorials/basic-git-commands "Basic GIT Commands")
1. [Frequently used Git Commands](https://codeburst.io/git-tutorial-a-beginners-guide-to-most-frequently-used-git-commands-2ab92bd22787 "Frequently used Git Commands")
1. [Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials)

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<p>_ _ _ _ _ _ _ _ _ _ _</p>

## Final notes

I may have errors or incorrect usage of commands in this file. I'll fix them as I find them. Or contact me and let me know what needs to be changed at [Kernix Web Design](https://kernixwebdesign.com/contact/ "Contact page").

I am also looking to find 3-4 entry-level designers and developers to start a project or two. I have some ideas about how we can help each other land a job!

To-Do List:

- What are **Actions**?
- What are **Packages**? NPM packages?
- What are **Environments**?
- What is a **Releases** exactly?
- What exactly do you put on the **Projects** tab?
- Go into your Repo settings and add:
  - Description
  - Website link
  - Topic tags
  - Deselect Releases and Packages if you do not have any

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="terminology">&#10551; Terminology</h3>

Here are some common terms. These notes are from git, MDN, and other sources:

1. **`upstream`**: the primary _branch_ on the original repository; where you cloned the repo from.
1. **`origin`**: The default upstream repository - a reference to the remote repository from where a project was initially cloned.
1. **`remote` / `remote repository`**: the version of a repository or branch that is hosted on a server (like GitHub), a shared repository that all team members use to exchange their changes.
1. **`fetch`**: adding changes from the remote repository to your local working branch without committing them.
1. **`pull`**: Pulling a branch means to fetch it and merge it; fetches and merges changes on the remote server to your working directory.
1. **`push`**: To send your committed changes to a remote repo, to upload local repo content to a remote repo.
1. **`clone`**: used to make a copy of the target repository; a copy of a repo that lives on your computer.
1. **`merge`**: bring the contents of another branch into the current branch; to take the data created on a separate branch and integrate them into a single branch.
1. **`head`**: A named reference to the commit at the tip of a branch.
1. **`HEAD`**: your current branch, or a defined commit of a branch, usually the most recent commit at the tip of the branch, or refers to the current commit you are viewing. `HEAD` is a reference to one of the heads in your repository.
1. **`blob`**: (Binary Large OBject) Untyped object, e.g. the contents of a file, is the object type used to store the contents of each file in a repository.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Git keywords

I'm wondering if putting in the following keywords will help beginners searching on GitHub to find this repo:

**Keywords**: git for beginners, basic git commands, basic git commands cheat sheet, basic git commands github, basic git commands for beginners, basic git commands list, basic commands for git, github basic commands, basic commands in git, basic git command, basic git commands to know, what are basic git commands, git guide command line, most basic git commands, basic commands of git, basic git workflow commands, basic git cheat sheet, git commands cheat sheet github, ...

<!-- [Back to Top](#back-to-top "Table of contents") -->

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<!-- Ignore this line, experimenting with markdown comments -->
