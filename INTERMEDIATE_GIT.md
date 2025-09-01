# Intermediate Git Commands File

Some of the git commands below can be considered beginner but they involve using branches. Many people think that branches are beginner as well, but you can easily make mistakes when working with branches. I also added notes on creating GitHub Gists and GitHub pages at the bottom of the file.

<a id="back-to-top"></a>

## Table of contents

1. [Branches](#branches)
   1. [Merge branches locally](#merge-branches-locally)
   1. [generating merge commits](#generating-merge-commits)
   1. [Pushing branches to your repository](#pushing-branches-to-your-repository)
   1. [Squashing commits](#squashing-commits)
1. [Stashing your changes](#stashing-your-changes)
1. [Miscellaneous git stuff](#miscellaneous-git-stuff)
   1. [Use the raw link](#use-the-raw-link)
   1. [git reflog](#git-reflog)
   1. [Download a folder from GitHub](#download-a-folder-from-github)
1. [Creating a GitHub gist](#creating-a-github-gist)
   1. [Clone or fork a gist](#clone-or-fork-a-gist)
   1. [Editing a gist](#editing-a-gist)
1. [GitHub pages](#github-pages)

## Branches

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

# To switch/return to the previously active branch (make sure to commit or stash your changes)
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

**NOTE**: `git branch branch-name` will create and switch to `branch-name` assuming you pulled a new remote branch from GitHub which you do not have locally.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Merge branches locally

Most of the time you will push your branches with the changes on it to your own repo, or to a repo that you are contributing for. But sometimes you will merge branches locally:

```bash
# Switch to the branch you want to merge into (the receiving branch) and run
git merge branch-name
# To abort a merge you performed:
git merge --abort
```

### generating merge commits

> This section is sloppy and needs editing and a rewrite

**MERGING**: Incorporating changes from one branch to another – 2 merging concepts:

1. You merge branches not specific commits
2. You always merge to the current HEAD branch – you merge to where you are, to where `HEAD` is

- not Fast-forward merges – changes on master that are not on the branch and changes on the branch that are not on master – git may not automatically be able to do the merge for us – it depends on conflicts – if the same line(s) were changed in both – if the same lines were not edited that it can happen automatically -
- when that happens a merge commit is generated and we need a `msg –
- and that commit will have 2 different parent commits -
- when you do that a file will open in VS Code – git made a commit and created the message `merge branch branch-name` –
- you could change that, but all you need to do is close the file to finalize the merge commit – ‘recursive' strategy -
- conflicts are much more difficult to perform

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Pushing branches to your repository

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

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Miscellaneous git stuff

### Use the raw link

**Tip**: `raw` link - If you want to copy the code for a file, click the `raw` button. That will load all the code onto a white/blank webpage and you just need to do <kbd>CTRL</kbd>+<kbd>C</kbd> to copy all the contents. That is way easier than trying to select the code and maybe missing some of it.

### git reflog

Reference logs record everything you do with your local branch.

1. Use `git reflog` to show everything you did in previous steps
2. find the entry where you think you want to go back to.
3. Then use `git checkout HEAD@{12}` or`git reset HEAD@{3}` to get back to that state, where `HEAD@{12}` and `HEAD@{3}` are referring to the number of commits in the past.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Download a folder from GitHub

This does not involve any git commands but it can be useful if you need images from a repo but do not want to clone the entire repo or download a zip file.

Go to [GitHub Download on GitKraken](https://www.gitkraken.com/learn/git/github-download) and scroll down to _How to Download a Folder from GitHub_. There is a link to [download-directory](https://download-directory.github.io/) where all you have to do is paste in the link to the folder you want to download.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Creating a GitHub gist

These are not git commands, rather they are a way to have code on GitHub that is not a stand-alone repository. People ceate them because they are chunks of code that other people can use.

To search for a gist on GitHub: `https://gist.github.com/username/` or just `https://gist.github.com/`

**<ins>What is a Gist?</ins>**

They are basically code snippets to save/store and share. Gists do not have Issues, PR's, Projects or Actions. If you have a simple JavaScript function that is not part of a project, then that would be something you could add to its own gist. From Github:

> Every gist is a Git repository, which means that it can be forked and cloned...and you will see it in your list of gists when you navigate to your gist home page. They're also searchable, so you can use them if you would like other people to find and see your work.

1. Navigate to your [gist home page](https://gist.github.com/) - OR -
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

There are 2 types: 1. user sites, and 2. project sites

- Project sites: for every repo you can have a corresponding website
- URL pattern: `username.github.io/repo-name` – one per project
- User site: `username.github.io` – you can only have 1 per GitHub account
- You can have a website or just markdown files like docs
- To setup a website go into one of your repos > select a branch (`main`/`master` most likely)
- You need to tell GitHub that the branch contains a website, specificall an `index.html` file
- Then go to the Repo _Settings_ tab > in the left sidebar look for _Pages_ under _Code and automation_ > go the the _Branch_ subheading where it says:

> "GitHub Pages is currently disabled. Select a source below to enable GitHub Pages for this repository"

- Then select the branch you want
- The old convention was to name the branch `gh-pages` so use that and keep main for your `project/portfolio` – but you can name the branch anything
- Make sure your `index.html` file is either in the root or a `/docs` folder – tell GitHub where it is
- Any time you update `gh-pages` branch your website will update

> I'm not positive about these commands:

```bash
# Go to the folder where you want your project, and clone the new repo
git clone https://github.com/username/username.github.io
# go into the folder
cd username.github.io
# add, commit, push
git add --all
git commit -m "Initial commit"
git push -u origin main
# Open a browser and go to https://username.github.io
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>
