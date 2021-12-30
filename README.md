# Beginner Git commands

**Note**: On your first push ever to GitHub, you may need to provide a user name and email address, I assume the ones used when you created your GitHub account. I think the commands are something like this:

```
git config --global user.name "any user name"

git config --global user.email "someone@someone.com"
or is it this:
git config --global user.email <email id>
```

The git config command is used initially to configure the user.name and user.email. This specifies what email id and username will be used from a local repository. When git config is used with --global flag, it writes the settings to all repositories on the computer.

## Table of contents

1. [Pushing your local files to an empty repo](#pushing-your-local-files-to-an-empty-repo)
1. [Commands after initial push](#commands-after-initial-push)
1. [Clone an existing repo](#clone-an-existing-repo)
   1. [Push the cloned files up to your repo](#push-the-cloned-files-up-to-your-repo)
1. [Branches and merging](#branches-and-merging)
1. [Forking and cloning](#forking-and-cloning)
1. [GitHub pull request process](#github-pull-request-process)
   1. [Pull request title](#pull-request-title)
   1. [Pull requests page notes](#pull-requests-page-notes)
   1. [Replies to your pull request](#replies-to-your-pull-request)
1. [Handling merge conflicts](#handling-merge-conflicts)
1. [Miscellaneous git commands](#miscellaneous-git-commands)
1. [Create a repo from the command line](#create-a-repo-from-the-command-line)
1. [Reference links](#reference-links)
1. [Final notes](#final-notes)

## Pushing your local files to an empty repo

This works for me when pushing to a repo I created without a README file. If you hve a README file, then you will get an error when trying to push, so you'll have to do a git pull command. It's easier to have an empty repo:

```
git init
git add .
git commit -m "First commit"
git remote add origin https_url
git push origin master
```

But these are the commands GitHub shows you when you create an empty repo:

```
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https_url
git push -u origin main
```

I know the first code block works, but I remember following the GitHub commands exactly and it worked as well - it's your choice.

## Commands after initial push

after making some changes do:

```
git add .
git status
git commit -m "Reason for commit"
git push -u origin master
```

**Note**: You need to use `git push -u origin master` for the next commit only after the initial push (don't ask me why). After that just use `git push`, although I believe you could do `git push origin master` and it won't have a negative effect. Also, I'm adding `git status` as a habit to check the status of the files. That command is not necessary.

## Clone your own repo

Why would you do this?

## Clone an existing repo

```
git clone https_url
```

### Push the cloned files up to your repo

Because you cloned this repo from an existing repo, git will try to push it to its original destination. For example, if you type `git remote -v` you will get their repo address where git thinks you want to push to.

You need to update the address. Copy the address from the overview page for the repo you created for the clone, then use:

```
git remote set-url origin https_url
git remote -v
```

Now git knows that the origin is your repo. Using `git reomote -v` again is to check that git is pointing to your repo adddress. Then to push the cloned repo files to your repo use:

```
git push origin master
```

## Branches and merging

Here are common commands:

```
git branch
git branch -a
git checkout branch_name
git checkout -b new_branch
git merge branch_name
git diff branch_name
```

The 1st command shows the branch you are working on. The 2nd one lists all the branch names in your repo. The next two switches to the branch and creates then switches to that branch, respectively. The merge command merges the branch into whatever branch you are currently in, most likely master.

More commonly you will push the changes to github then make a PR (push request).. For a new branch, git push wont work because git doesn’t know what branch you are pushing to – so do:

```
git push --set-upstream origin branch-name
```

To pull changes from GitHub to your machine use `git pull origin master`

To delete a branch use `git branch -d branch_name`

If you get this error when trying to delete a branch:

> error: The branch 'fix/branch-name' is not fully merged.
> If you are sure you want to delete it, run 'git branch -D fix/branch-name'.

It's probably because something in your local branch has not actually made it to the remote repository. To find out what commits have not been merged from your source branch to a target branch try:

```
git log fix/branch-name --not main
```

That will show you what has been changed that has not been pushed to main, or maybe has not been merged. If you are fine with the differences then replace `-d` with `-D`.

## Forking and cloning

Here is a list of commands from [how-to-setup-freecodecamp-locally.md](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md). After you fork a repo:

```
git clone --depth=1 https://github.com/User_Name/freeCodeCamp
```

**Note**: `--depth=1` creates a shallow clone of your fork, with only the most recent history/commit.

Next, add a remote reference to the main freeCodeCamp repo, or whatever repo you are cloning after forking, then check the configuration:

```
git remote add upstream https://github.com/freeCodeCamp/freeCodeCamp.git
git remote -v
```

Then use `git status` and `git checkout main` if not on main. Then:

1. Update your local copy of the freeCodeCamp upstream repository,
1. Hard reset your main branch with the freeCodeCamp main,
1. Push your main branch to your origin to have a clean history on your fork on GitHub,
1. And validate your current main matches the upstream/main by performing a diff:

```
git fetch upstream
git reset --hard upstream/main
git push origin main --force
git diff upstream/main
```

> **MAJOR QUESTION**: Do you run those 4 commands EVERY time you work on the repo or just once in the beginning?

**ANSWER**: #1 is necessary for the clone to fetch the files. #4 is optional. Use #2 & #3 with caution - read up on them.

Finally, create a branch matching your contribution, make your changes, and then commit and push:

```
git checkout -b fix/catphotoapp-typos
git status
git add .
git status
git commit -m "short description"
git push origin fix/catphotoapp-typos
```

**Note**: The link above mentions keeping commit messages to 50 or less characters. My first commit message was about 74 characters. On the freeCodeCamp repo it looks like it cut off my message at either 69 or 70 characters, so I think keeping to a max of 69 or 70 characters will work but don't quote me on that.

Before covering the Pull Request back on GitHub, here is a reply from the freeCodeCamp forum about the process:

```
git clone https://github.com/User_Name/freeCodeCamp
git checkout -b fix/catphotoapp-typos
git status
git add .
git commit -m "write some commit message here"
git push --set-upstream origin fix/catphotoapp-typos
```

Why the difference with the first way with `git push origin fix/catphotoapp-typos` and the second with `git push --set-upstream origin fix/catphotoapp-typos`?

NOTES:

> `git reset --hard upstream/main` erases any uncommitted changes. This is not a required command used everytime you need to push changes to the remote repo - use it wisely and when needed.

> `git push origin main --force`, you don’t need to add the `--force`. Just doing a regular git push is fine.

> You only use the `--set upstream` when you need to add your local branch to the remote branch. But once the new branch is added to the remote repo, then you don’t need to use `--set upstream` each time

MY FINAL COMMANDS:

```
git clone --depth=1 https_url
git remote add upstream https_url
git fetch upstream
git push origin main
git checkout -b fix/branch-name
git add.
git commit -m "short description"
git push --set-upstream origin fix/branch-name
```

With that last `git push` only for the first time, then use `git push origin fix/catphotoapp-typos`. Also add `git remote -v` after the fetch command, and of course `git status` as needed.

If you realize that you need to edit a file or update the commit message after making a commit you can do so after editing the files with:

`git commit --amend`

This will open up a default text editor like `nano` or `vi` where you can edit the commit message title and add/edit the description.

## GitHub pull request process

After you push your changes go to your cloned copy of the repo on GitHub and refresh the page if necessary. You should see a green button labeled **_Compare & pull request_**. If you do not see it then click the Pull requests link to go to that tab.

Click "Compare & pull request" button and notice the page title of **_Open a pull request_** and the paragraph in the section below the title saying **_Able to merge. These branches can be automatically merged._**

You can then edit your commit message if need be. In the body of your PR include a more detailed summary of the changes you made and why.

In the text area field:

1. Put an `x` in the checkboxes,
1. Remove all the comment fields,
1. You can preview the message if you like,
1. Remove the phrase "Closes #XXXXX"
1. Click the green button **_Create pull request_**.

DONE, DONE AND DONE - NOW WAIT. REMEMBER TO USE fix: what-you-fixed or fix(curriculum) in the PR Title!!!!!!!!!

If the PR is meant to address an existing GitHub Issue then, at the end of your PR's description body, use the keyword Closes with the issue number: `Closes #123`

Indicate if you have tested on a local copy of the site or not. This is very important when making changes that are not just edits to text content like documentation or a challenge description. Examples of changes that need local testing include JavaScript, CSS, or HTML which could change the functionality or layout of a page.

### Pull request title

The convention has the following format:

`<type>([optional scope(s)]): <description>`

For example:

`fix(learn): tests for the do...while loop challenge`

| Type  | When to select                                                                   |
| :---- | :------------------------------------------------------------------------------- |
| fix   | Changed or updated/improved functionality, tests, the verbiage of a lesson, etc. |
| feat  | Only if you are adding new functionality, tests, etc.                            |
| chore | Changes that are not related to code, tests, or verbiage of a lesson.            |
| docs  | Changes to `/docs` directory or the contributing guidelines, etc.                |

**Description:**

Keep it short (less than 30 characters) and simple, you can add more information in the PR description box and comments. Example: `fix(api,client): prevent CORS errors on form submission`.

**QUESTION**: What creates CHANGELOGs? Is it the use of the colon `:`? Here is a quote from [Why Use Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/#why-use-conventional-commits):

> Automatically generating CHANGELOGs.

Will using `fix:`, `feat:`, `docs:`, etc. create CHANGELOGs where fix, feat, or docs without the colon not do that?

### Pull requests page notes

Check the values for the fields labeled `base fork` and `head fork`.

1. The base repository is the original source, the repo you forked and cloned, the public version.
1. The head repository is your local copy of the base repo.

Those fields should be correct but just be aware of the values. You will also see fields labeled just `base` which shows the branch of the original repo that you pushed to, and `compare` which shows the name of the branch you created and pushed.

**Note**: Large repos like the one for freeCodeCamp will have fields created in the pull request text area that I reference in the steps above. A smaller repo that you are contributing to may not have that setup. In the latter case, be as descriptive but concise as possible - don't write a book!

Also, if you scroll further down on the page you will see all the changes you made. And after clicking the "Create pull request" button you will be taken to the source repo showing your pull request, other pull requests, the conversations for each, etc.

### Replies to your pull request

Our moderators will now take a look and leave you feedback. You will get a message when a reviewer for the source repo adds a comment about your pull request.

Regardless, your changes will either be accepted or rejected. When the owner of the repo accepts your changes they will do so by clicking the **Merge pull request** button.

## Handling merge conflicts

Here is where I'm a little fuzzy on the steps. I think you may have to do a pull request to get changes from other contributors. Make sure you are on the `master` or `main` branch then do `git pull`.

Read more here: [Conflicts on a pull request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md#making-changes-locally).

A merge conflict is when 2 or more people change the same code/content but with different values and you run the command `git merge branch-name`. However, I don't think a contributor would actually run that command.

But if you did, in VS Code you will see something like:

```
<<<<<<< HEAD (Current Change)
<p>some change here</p>
=======
<p>different change here</p>
>>>>>>> Branch-Name (Incoming Change)
```

Where `HEAD` is your current branch, usually main/master I think. Once again, this would only be done by the owner of the repo, but what you would do is:

1. Decide which change you want to keep,
1. Delete EVERYTHING else -> the change you don't want and the equal, less than, and greater than signs along with the text like HEAD and Current Change. Everything other than the actual change that you want.

## Miscellaneous git commands

To remove git tracking from a folder use the following command in git bash or from the command prompt, it does not work in VS Code:

`rm -rf .git`

I (mostly) know what these commands do:

```
git init
git commit -am
git log
git add -A
git add *.ext
git --version
git remote -v
git remote add upstream remote-url
git push --set-upstream origin branch-name
git rm –cached filename
git merge --abort
git branch -a
clear, q, Q, exit
```

I am not sure what these commands do, mostly because I believe these are advanced git commands:

```
git reset
git reset filename.ext
git reset HEAD
git revert id
git config -l
git diff filename.ext
git fetch
git fetch upstream
gitreflog
git log --graph --decorate –oneline
git stash
git stash pop
git branch login
git branch -vv
git remote update --prune
git rebase
git bisect start
git bisect bad
git bisect good
git config --list
git config --global core.editor "code –wait"
git config --global core.autocrlf true
git rebase -i HEAD~n
ESC | :WQ | ENTER, pwd
```

Is this how you add a description?

```
- git commit -m "Title" -m "Description ..........";
```

## Create a repo from the command line

I don't think anyone does this. Everyone seems to just create an empty repo. But you can try using this link:
[Adding an existing project to GitHub using the command line](https://docs.github.com/en/github/importing-your-projects-to-github/importing-source-code-to-github/adding-an-existing-project-to-github-using-the-command-line).

```
git init -b main
git add . && git commit -m "initial commit"
gh repo create project-name
```

I get an error for the use of `&&` and `gh` so just create an empty repo. You need to install something called GitHub CLI (not interested).

## Reference links

1. [Git reference docs](https://git-scm.com/docs)
1. [GitHub for complete beginners MDN](https://developer.mozilla.org/en-US/docs/MDN/Contribute/GitHub_beginners)
1. [Why Use Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/#why-use-conventional-commits)
1. [how-to-contribute-to-open-source](https://github.com/freeCodeCamp/how-to-contribute-to-open-source)
1. [Contribute to freeCodeCamp.org](https://contribute.freecodecamp.org/#/)
1. [how-to-setup-freecodecamp-locally.md](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md)
1. [freeCodeCamp Conflicts on a pull request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md#making-changes-locally)
1. [freeCodeCamp Introduction](https://contribute.freecodecamp.org/#/index)
1. [freeCodeCamp How to work on coding challenges](https://contribute.freecodecamp.org/#/how-to-work-on-coding-challenges)
1. [freeCodeCamp FAQs](https://contribute.freecodecamp.org/#/FAQ)
1. [freeCodeCamp How to open a Pull Request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-open-a-pull-request.md)

## Final notes

I may have errors in here. I'll fix them as I find them.

> Last updated December 30th, 2021.
