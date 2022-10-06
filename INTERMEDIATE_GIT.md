# Intermediate and Advanced Git Commands

These are commands that you will encounter when you start contributing to open-source projects and creating branches. Some people may view branches as beginner-level git, but I am putting them here because even though they are basic commands, they can create problems if done incorrectly.

<a id="back-to-top"></a>

## Table of contents

1. [Branches](#branches)
   1. [Pushing branches to your repository](#pushing-branches-to-your-repository)
   1. [Common issues with branches](#common-issues-with-branches)
1. [Forking and cloning](#forking-and-cloning)
1. [GitHub Issues](#github-issues)
   1. [How to create an issue](#how-to-create-an-issue)
   1. [Closing an issue](#closing-an-issue)
1. [GitHub pull request process](#github-pull-request-process)
   1. [Pull request title](#pull-request-title)
   1. [Pull requests page notes](#pull-requests-page-notes)
   1. [Replies to your pull request](#replies-to-your-pull-request)
   1. [Staying up to date](#staying-up-to-date)
   1. [Handling merge conflicts](#handling-merge-conflicts)
1. [Miscellaneous git commands](#miscellaneous-git-commands)
   1. [gitignore](#gitignore)
   1. [Mistakes](#mistakes)
1. [Creating a GitHub gist](#creating-a-github-gist)
   1. [Clone or fork a gist](#clone-or-fork-a-gist)
   1. [Editing a gist](#editing-a-gist)

## Intermediate Git Commands

From here the commands are a little more involved and are for when you start creating your own branches and/or contributing to open source projects.

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

Recap:

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

Miscellaneous (not sure what this is): `git branch --sort=-committerdate # DESC` and `git branch -r --sort=-committerdate # DESC` where the flag `-r` is for just remotes.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<h3 id="pushing-branches-to-your-repository">&#10551; Pushing branches to your repository</h3>

After you push the changes to GitHub you would then make a PR (pull request) whether you are contributing or working on your own project.

Remember, you push the changes for your branch _from_ your branch, not from `master`.

Then back on your repo main page:

1. Click the **Compare & Pull Request** button.
1. Clicking it takes you to a page titled "_Open a pull request_" where you can add a description.
1. Then click the "_Create pull request_" button.
1. That takes you to the "_Pull requests_" tab where you can click the _Merge pull request_ button
1. And finally, click _Confirm merge_ if you are done working on your branch, or you can continue to work and push changes from your branch.

**Squash**:

If you have multiple commits for that branch, select _Squash and merge_ option from the dropdown list under _Compare and merge_.

**Code Comments**:

1. Click on the Files changed tab
1. Click the `+` button that appears when you hover over the code
1. Make a comment on a line of code.
1. You can add a description for the comment and also click the "Resolve conversation" button.

**Note**: A PR from your branch to the master branch is a request to have your code merged with the master branch. You can, and should (see below), delete your branch when your code/changes are merged.

If you go back to your local project and switch to master, the changes won’t be there because they are only on GitHub and you need to pull them down to your local machine. To pull changes from GitHub to your machine use:

```sh
git pull
```

Or just `git pull origin master` if you have not set the upstream already.

> **Make sure you are on the master branch**

What `git pull` does is merge all the changes present in the remote repository to the local working directory (See the section [Staying up to date](#staying-up-to-date)).

**NOTE**: Run `git status` to check the status of your local repo but it should also show a message of `Your branch is up to date with 'origin/master'`.

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

The `stash` command is when you are working on a branch but are not finished with your work and you need to switch back to master. The questions is did you make commits or not? If you did not then git won't let you switch branches unless you make a commit or stash.

Stash: "stashing" uncommitted changes so that you can return to them later without having to make unnecessary commits. It's better than a half-complete commit. Running `git stash` (or `git stash save`) will take all uncommited changes (staged and unstaged) and stash them, reverting the changes in your working copy.

When you want to go back to your branch and see your changes from befoe you stashed them, run `git stash pop`. There is also `git stash list` to see all your stashes and `git stash clear` to clear your stashes.

```sh
git stash
git stash pop
```

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

This will open up a default text editor like `nano` or `vim` where you can edit the commit message title and add/edit the description. I had a hard time figuring out how to quit out of that editor, but I think `CTRL + X` may do it. If that doesn't work try any of the following: `q`, `Q`, `exit`, `ESC`, `:WQ`, `ENTER`, or `CTRL + C`. Hopefully, one of those work.

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

## GitHub Issues

- Issues are for collaborating thru the GitHub website. They will not be in your local repo.
- The Issues tab is a place to leave a comment about a project
- Reasons to create an issue: 1) bugs, 2) typos, 3) feature requests, 4) to ask a question, etc.

### How to create an issue

1. Click on the Issues tab
1. Click the New Issue button
1. Add a Title and Description about your issue
1. Note: You can take a screenshot and add it to your issue by copying it and then paste or drag it into the description field.
1. You can also add labels by clicking on the gear icon next to labels and checking the ones you want.
1. Then click the Submit new issue button

If you click back on the issues tab you will see your issue and any other open issues. Pay attention to the # next to your issue title. That same number will appear in the address bar when you click into your issue. That is the issue number.

- Issues are Open until they are resolved/closed
- Issues are Closed when the person who owns the repo or who created the issue can close the issue.

### Closing an issue

When you make a change to a file in regards to an issue, add the issue # in your commit title, e.g.:

> Making change as per issue #3

When you go back into that issue you should see the commit that references the issue. If you are done click the Close issue button. But there are also keywords that will automatically close an issue and the main one is **_fixes_**.

So if you add the "fixes" in your commit title it will close the issue: `This fixes #3`. When you do that you will get a commit # for the closed issue. If you grab that commit hash from the url for the commit that closed an issue, you can create another issue and paste the hash into the description field. That will automatically create a link to that commit. Perhaps you feel the issue should not have been closed and there are still unresolved issues.

So referencing Issue numbers and commit hashes for more functionality in the collaboration process.

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

Note: you should use `git switch branch_name` as opposed to `git checkout` but this is a new command that I am no familiar with. Check out the article [What's the Difference Between Git Switch and Checkout](https://linuxhandbook.com/git-switch-checkout/).

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

You can also remove a specific file from staging by using `git rm –cached filename.ext` where `rm` is short for remove.

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
git merge --abort
git diff filename.ext
git fetch
```

Here are some terminal commands you may need:

- `clear`: to clear the terminal
- `q`, `Q`, or `:q`: to exit out of VIM or Nano
- `cd` - change directory
- `.`, `./`, `../`: they stand for home, current directory, and up one directory
- `pwd` - print working directory
- `ls` - list the contents of the current working directory, `ls -all`
- `TAB` - auto fill in file and folder names
- `git` - shows other commands like `grep`, `show`, `rebase`, `switch`, `tag`
- `log` - shows your local history
- up and down arrow to cycle thru previous commands
- `open .`: open file explorer in Windows from bash or command prompt
- `code .`: open your default text editor
- <kbd>CTRL</kbd>+<kbd>C</kbd>,
- `exit`, `ESC`, `:WQ`, `ENTER`: not sure what these are for

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
git tag
git show
git stash apply
git stash -u
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

## Creating a GitHub gist

**<ins>What is a Gist?</ins>**

They are basically code snippets to save/store and share. Gists do not have Issues, PR's, Projects or Actions. If you have a simple JavaScript function that is not part of a project, then that would be something you could add to its own gist. From Github:

> Every gist is a Git repository, which means that it can be forked and cloned...and you will see it in your list of gists when you navigate to your gist home page. They're also searchable, so you can use them if you'd like other people to find and see your work.

1. Navigate to your [gist home page](https://gist.github.com/) - OR -
1. Click the down arrow next to your profile image thumbnail > click _New Gist_
1. Type a description and file name with extension for your gist (you want the extension for code highlighting).
1. Optionally, you can change the Indent Mode, Indent Size, and if you want it to Wrap or not.
1. Type the text of your gist into the gist text box
1. When done Click either `Create secret gist` or `Create public gist`

**NOTE**: For the gist filename just make something up. For example, if you have a JavaScript function that takes a blog post title and converts it to a URL string, then give it a name like `BlogTitleUrl.js`.

Then you can get the Share link for the gist to share with people or to add to an online article. When you choose `Embed` and add the link to an HTML page it will output is a formatted code block (not for all sites though).

You can add code blocks for your gist by clicking _Add file_.

**Public gists** can be found by other users on the Discover page. Just click _All gists_ from the menu bar and they are listed in reverse chronologial order of creation date. You can also search for gists by keywords, add comments on gists you found and have comments on your gists.

**NOTE**: You can create a gist if you are not signed into GitHub but it will be an anonymous gist which you will not be able to edit or delete. I don't know why you would want to do that but you can if you want to.

### Clone or fork a gist

Your options from the dropdown list after creating your gist are to _Embed_, _Share_ or _Clone_ the gist. If you want to clone the gist then in your terminal do:

```shell
git clone gist_url
```

If you choose to _fork_ someone else's gist then it will show upon your gist home page similar to how forked repos will show in your repositories.

### Editing a gist

Just click the Edit button while in your gist and edit the code as you see fit. There is also a delete button next to edit if you want to delete your gist.

When done editing click the _Update public gist_ button. Click the _Revisions_ link to see your changes. Remember that your gists are also repositories. You can go pulls and pushes.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>
