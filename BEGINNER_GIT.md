# Git Commands for Beginners

NOTE: I alternately use `main` or `master` when referring to your default branch name in the commands in this file and in the other files.

<a id="back-to-top"></a>

## Table of contents

1. [Download and Setup Git for Windows](#download-and-setup-git-for-windows)
1. [Authenticate with GitHub](#authenticate-with-github)
1. [Pushing a local project to an empty repo on GitHub](#pushing-a-local-project-to-an-empty-repo-on-github)
   1. [Commands after initial push](#commands-after-initial-push)
1. [Clone one of your existing GitHub repos](#clone-one-of-your-existing-github-repos)
1. [Clone a repo that is not yours](#clone-a-repo-that-is-not-yours)
1. [Important Notes about the `commit` command](#important-notes-about-the-commit-command)
   1. [Atomic commits](#atomic-commits)
   1. [Commit messages](#commit-messages)
   1. [Ammending a commit](#ammending-a-commit)
   1. [Conventional Commits](#conventional-commits)
1. [gitignore](#gitignore)
1. [Reference links](#reference-links)
1. [Final notes](#final-notes)
1. [Git keywords](#git-keywords)

## Download and Setup Git for Windows

If you have not done so already, then you need to [download Git](https://git-scm.com/downloads 'Git download page') open the `.exe` file to install Git. Accept all the defaults during the install with the following two exceptions:

1. _Choosing the default editor used by Git_. I chose VS Code from the select list but there is a way to set your default editor from Git Bash or the terminal (see below).
2. _Adjusting the name of the initial branch in new repositories_ by not choosing _Let Git decide_, and instead set it to `main`.

**NOTE**: You need Git Bash but that comes bundled with Git for Windows.

On the last screen you can select _Launch Git Bash_ then press _Finish_ or find Git Bash on your computer and open it.

To verify that git is installed, type `git --version` or `git -v` for short. If you see a version number then Git installed properly.

**NOTE**: To close the Git Bash window just type `exit`. To open it again, you can hover over a folder in Windows Explorer, right-click and select _Git Bash Here_. But don't close it yet because you have to authenticate with GitHub (next section).

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Authenticate with GitHub

On your first push ever to GitHub from your machine, you will need to authenticate your machine with GitHub. This is so Git/GitHub knows that you are who you say you are.

In the past you could just use `user.name` and `user.email` to verify your identity to GitHub. Now you have to generate an SSH key for authentification. I used the following docs to do that:

However, you still need to have `user.name` and `user.email` set. Here are the commands I used but I suggest using the 2 links above as they are the offical source and the commands or syntax may change over time:

```sh
# Verify that git is installed by checking the version
# Installation worked if you see a version
git --version
# or use -v which is short for --version
git -v

# CONFIG
# See all settings
git config --list

# check your name and email
git config user.name
git config user.email

# Set (or change) your user name and email
git config --global user.name "Name you want to be known as"
git config --global user.email "Use the email you used for GitHub"

# Check the name of your default branch
git config init.defaultBranch

# Change your default branch to "main"
git config --global init.defaultBranch main

# Make VS Code your default editor
git config --global core.editor "code --wait"
```

You may need to create an SSH key and add it to your GitHub account as an additional step to authentication. I followed the steps from the following links and I had no problems:

1. Link 1: [Checking for existing SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)

Here are the steps for creating your SSH key on Windows using.

```sh
# Check to see if you already have an SSH key
ls -al ~/.ssh
```

2. Link 2: [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

**NOTE**: Even though I am on Windows, I chose to use Git Bash and the commands from the tab for _Linux_. I chose NOT to enter a passphrase:

```sh
# 1. Generate your key (use the email you set with user.email above)
ssh-keygen -t ed25519 -C "myemail@somewhere.com"

# or if that doesn't work:
ssh-keygen -t rsa -b 4096 -C "myemail@somewhere.com"

# 2. Press ENTER to accept the default file location
# 3. Enter Passphrase or press ENTER for no passphrase, then repeat - that generates the .pub key
# 4. Then start the ssh-agent in the background (in Git Bash/Linux):
eval "$(ssh-agent -s)"
# you should see: Agent pid 59566

# 5. Add your SSH private key to the ssh-agent
ssh-add ~/.ssh/id_ed25519

# 6. Copy the SSH public key to your clipboard.
clip < ~/.ssh/id_ed25519.pub
```

3. Link 3: [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

All those commands above worked and I then back on GitHub:

1. Click your profile photo, then click Settings.
2. In the "_Access_" section of the sidebar, click _SSH and GPG keys_.
3. Click the _New SSH key_ or _Add SSH key_ button.
4. In the "_Title_" field, add a descriptive label for the new key, e.g. "Personal Laptop" but the title is not important.
5. Leave the default for the dropdown for Key type set to Authentification key
6. Paste your public key into the "Key" field.
7. Click _Add SSH key_. If prompted, confirm access to your account on GitHub.

To test to make sure that worked run:

```sh
ssh -T git@github.com
# you should see the message "Hi YourName! You've successfully authenticated, but GitHub does not provide shell access."

# if that doesn't work run
eval `ssh-agent -s`

# You should see some pis number (not "1234")
Agent pid 1234
```

On my first `git push` to GitHub I got a message about having to authenticate my GitHub account. There was a new tab open in Chrome where I clicked _Authenticate_ and I think I only had to enter my GitHub password.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Pushing a local project to an empty repo on GitHub

After you created a project with files on your machine, you then need to push them to GitHub. But first you need to create a repo on GitHub:

1. Create a new repo on GitHub by clicking the `+` icon and choose "New repository"
2. Enter the name and set it to public
3. **_DO NOT_** add a `README.md` file
4. Click "Create repository"

You can use the commands that GitHub shows when you create the repo or use the following commands but make sure to copy the repo URL link (`https_url`).

The basic commands are:

```bash
# 1. Initialize git in current folder:
git init

# 2. Add all changed files to staging (-A, --a):
git add .

# 3. Commit all staged files (--message):
git commit -m "first commit"

# 4. Connect your remote/GitHub repo to your local repo, & set the remote to the alias 'origin':
# SYNTAX: git remote add [alias] [url]
git remote add origin https://github.com/YOUR_USER_NAME/YOUR_REPO_NAME.git

# 5. Push your commits and connect your local to your remote repo (--set-upstream)
# SYNTAX: git push [alias] [branch]
git push -u origin main

# NOTE: the -u flag is short for --set-upstream
# For any future commits just use:
git push

# If you do not use the -u flag then do the following each time you push
git push origin main

# In case origin is pointing to the wrong GitHub repo
git remote remove origin

# Get help on commands
git help
git help -m
git help -a
```

When you run `git init` you will see your brnach name in the lower left corner of VS Code. You will also see all your file names turn green with a `U` next to them. The `U` stands for "untracked".

An alternate way to add new or changed files to staging is to add the files individually:

```bash
# Use the following to add files individually to staging:
git add filename1.ext filename2.ext filename3.ext
```

For the above command you can use <kbd>TAB</kbd> once you have typed a few characters of your filename.

**NOTE**: When you create an empty repo on GitHub, it's best practice to use the same name on GitHub as the folder on your local machine, though you can still push if the names do not match.

The `git log` is a log of the commits for your local repo. It shows the commit hash, author, date, and message.

```sh
# See log of all your commits
git log

# Put logs on one line, only shows first 7 characters of the commit hash and the message
git log --oneline
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Commands after initial push

Now your local repo is connected to your remote repo on Github. After making some changes or creating new files use:

```bash
git add .
git status
git commit -m "Your next commit message"
git push
```

**NOTE**: You need to use `git push -u origin main` for the first push. After that just use `git push`, although you can still use `git push origin main` _AFTER_ the first push and it won't have a negative effect.

Also, get in the habit of using `git status` as a way to check the status of your files and folders, which branch you are on, and more.

**NOTE**: You can add your files to staging and commit them in one command with the `-am` flag with the `commit` command:

```bash
git commit -a -m "Commit message"
git commit -am "Commit message"
```

Another way to do that is with `&&`:

```bash
git add index.html && git commit -m "Update index.html"
```

Also, try not to make changes to any files on GitHub. If you do, you need to run either `git pull` or `git fetch`. The only time you may need to create a file on GitHub is adding a LICENSE file. See the INTERMEDIATE_GIT.md file for details on those commands.

### Commands GitHub shows with new repo

NOTE: Ignore the commands `git add README.md` and `git branch -M main`. If you want to add a README file, then do it manually in your local repo and add content to it. And you should have already configured your default branch name.

```sh
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/YOUR_USER_NAME/YOUR_REPO_NAME.git
git push -u origin main

# or push an existing repository from the command line
git remote add origin https://github.com/YOUR_USER_NAME/YOUR_REPO_NAME.git
git branch -M main
git push -u origin main
```

<!-- Add notes on the following maybe: git diff, clear -->

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Clone one of your existing GitHub repos

You would clone your own repo when you get a new computer/laptop or if you accidentally deleted one of your local repos.

Go to the main repo page and click on the green `Code` button and copy the _HTTPS_ link and replace `https_url` in the commands below with that link

```sh
# Go to the folder where you want your project folder and run
git clone [url]
git clone https://github.com/YOUR_USER_NAME/YOUR_REPO_NAME.git

# Move into that folder
cd folder_name

# Check the remote location (name/alias and URL)
git remote -v
```

<!-- Add notes somewhere on git remote, git remote add, git remote remove, git remote rename - maybe INTERMEDIATE -> Branches? -->

**NOTE**: `git clone` automatically initializes Git and sets the remote so you do not need the commands `git init` and `git remote add origin https_url`. By running `git remote -v` you should see:

```bash
origin  https://github.com/YOUR_USER_NAME/YOUR_REPO_NAME.git (fetch)
origin  https://github.com/YOUR_USER_NAME/YOUR_REPO_NAME.git (push)
```

Then make some changes and run the standard commands:

```sh
git status
git add .
git commit -m "your commit message"
# No need to set upstream because cloning automatically does that
git push
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Clone a repo that is not yours

These commands are for when you want to work on a repo that someone else created and either contribute to the repo, or work on it yourself. The commands are the same as the section above except you want to change the remote location.

If you intend to work on the repo yourself, go to GitHub and create an empty repo. This is where you will push so give it a relevant name.

Then back in Git Bash or VS Code run these commands:

```sh
# Use the source repo address to clone
git clone https://github.com/THEIR_USER_NAME/THEIR_REPO_NAME.git

# Switch into the folder and open VS Code
cd folder_name
code .

# Check to see where the remote is pointing to
git remote -v

# Set your GitHub repo as the remote if you do not intent to contribute
git remote set-url origin https://github.com/YOUR_USER_NAME/YOUR_REPO_NAME.git

# Check to make sure it is now pointing to your account
git remote -v

# Make changes, add, commit, tthen push
git add .
git commit -m "message"
git push -u origin main
```

Then for pushes after you set the upstream use the usual commands:

```sh
git add .
git commit -m "your message"
git push origin main
# or just if you used the -u flag
git push
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Important Notes about the commit command

NOTE: If you forget to add `-m "msg"` with your `commit` command, you will be taken either into the Vim editor or VS Code if you added the global command for that. If you are in the Vim editor:

1. if you are in Vim type `i` (insert mode) to insert your message then
2. <kbd>ESC</kbd> once to exit insert mode then
3. Type `:wq` (or just `wq`) to exit Vim, `w` = write, `q` = quit

### Atomic commits

I originally would do massive changes to one or many files and `commit` all those changes, then `push` them to my GitHub repo. _THAT IS NOT WHAT YOU WANT TO DO!_

What you want to do is `commit` changes in related batches. You can have as many commits as you want when you run `git push`. Each `commit` should be for a specific change in case you need to _undo_ that commit.

- Atomic Commits – when possible a commit should encompass a single feature, change, or fix. It should be focused on a single thing. That makes undo/rollback easier and makes your code easier to review.

### Commit messages

When composing the text for your commit message, you should use 1) _present tense_ and 2) _imperative style_, although some people prefer past tense:

- `make thing do X` or past tense:
- `made thing do X`

### Ammending a commit

Use the following command when you need to change something about your last commit:

- `git commit --amend` to change your commit message or when you forgot to add a file to a commit.

```sh
# If you need to edit a commit msg
git commit --amend

# Change PREVIOUS commit by adding a file you forgot
git add forgotten-file.md
```

### Conventional Commits

Link: [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/#why-use-conventional-commits)

Commit messages should start with the `<type>`

```
<type>[optional scope]: <description>

[optional body]

[optional footer]
```

Common types:

- `fix:`, `feat;`, `chore:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:`, `improvement:`, and others

Read the notes on the Conventional Commits page.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## gitignore

There are some files that you do NOT want to push to a remoe public repository. Some examples of files you want Git to ignore are environmental variables, API keys, credentials, operating system files, log files, dependencies and packages, etc.

To have Git ignore any files that you do not want to push, create a file called `.gitignore`, usually in the root of your project folder. Add the paths and file names that you do not want to push:

```sh
index.html
js/test.js
*.log
```

For large repositories, this file will have a lot of entries. For some npm commands like `npx create-react-app` this file will be created for you.

If you want to ignore a folder you need to add `/` after the folder name or Git will think it is a file. Here is an example of a basic gitignore file. You _always_ want to add `node_modules` assuming you added node packages to your project, the other files are just suggestions.

```sh
# Dependencies
/node_modules

# Production and other folders
/build
/dist
/images

### VisualStudioCode ###
.vscode/*

# misc
.env
.env.local
.env.development.local
.env.test.local
.env.production.local

# Numerous always-ignore extensions
*.diff
*.env
*.err
*.log
*.sass-cache
*.tmp
```

You can add anything you want in the gitignore file for your repos. If you are contributing, then do not touch that file unless the repo owner asked you to.

> When do you add the `/` before the folder name vs after, such as `/node_modules` vs `images/`?

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Reference links

FYI, it's difficult keeping this list up-to-date. I'll do my best to provide the best resources that I find and that work for me.

1. [Git reference docs](https://git-scm.com/docs 'Git documentation')
1. [GitHub for complete beginners MDN](https://developer.mozilla.org/en-US/docs/MDN/Contribute/GitHub_beginners 'MDN GitHub docs')
1. [Why Use Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/#why-use-conventional-commits 'Conventional Commits')
1. [How to contribute on GitHub](https://www.dataschool.io/how-to-contribute-on-github/ 'Step-by-step guide to contributing on GitHub')
1. [Contributing to MDN](https://developer.mozilla.org/en-US/docs/MDN/Contribute 'Contributing to MDN')
1. [Hostinger: Basic GIT Commands](https://www.hostinger.com/tutorials/basic-git-commands 'Basic GIT Commands')
1. [Frequently used Git Commands](https://codeburst.io/git-tutorial-a-beginners-guide-to-most-frequently-used-git-commands-2ab92bd22787 'Frequently used Git Commands')
1. [Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials)

Contributing to freeCodeCamp:

1. [Contribute to freeCodeCamp.org](https://contribute.freecodecamp.org/#/ 'freeCpdeCamp contribution docs')
1. [how-to-setup-freecodecamp-locally.md](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md 'How to setup freeCodeCamp locally')
1. [freeCodeCamp Conflicts on a pull request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md#making-changes-locally 'freeCodeCamp PR Conflicts')
1. [freeCodeCamp Introduction](https://contribute.freecodecamp.org/#/index 'freeCodeCamp contribution intro')
1. [freeCodeCamp How to work on coding challenges](https://contribute.freecodecamp.org/#/how-to-work-on-coding-challenges 'freeCodeCamp: Working on coding challenges')
1. [freeCodeCamp FAQs](https://contribute.freecodecamp.org/#/FAQ 'freeCodeCamp FAQs')
1. [freeCodeCamp How to open a Pull Request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-open-a-pull-request.md 'How to open a PR freeCodeCamp')
1. [freeCodeCamp How to contribute to open source](https://github.com/freeCodeCamp/how-to-contribute-to-open-source 'How to contribute to open source')

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Final notes

I may have errors or incorrect usage of commands in this file. I'll fix them as I find them. Or if you find any errors, open an issue or create a pull request for any proposed changes.

I am also looking to find 3-4 entry-level designers and developers to start a project or two. I have some ideas about how we can help each other land a job!

To-Do List:

- What are **Actions**?
- What are **Environments**?
- What are **Milestones**?
- What is a **Releases** exactly?
- What exactly do you put on the **Projects** tab?
- What about the other **Insights** and **Security** tabs.
- What else can you do to make full use of all the GitHub tabs?

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Git keywords

I'm wondering if putting in the following keywords will help beginners searching on GitHub to find this repo:

**Keywords**: git for beginners, basic git commands, basic git commands cheat sheet, basic git commands github, basic git commands for beginners, basic git commands list, basic commands for git, github basic commands, basic commands in git, basic git command, basic git commands to know, what are basic git commands, git guide command line, most basic git commands, basic commands of git, basic git workflow commands, basic git cheat sheet, git commands cheat sheet github.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>
