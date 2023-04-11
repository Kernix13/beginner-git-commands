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
1. [gitignore](#gitignore)
1. [Important Notes about the `commit` command](#important-notes-about-the-commit-command)
1. [Reference links](#reference-links)
1. [Final notes](#final-notes)
   1. [Git keywords](#git-keywords)

## Download and Setup Git for Windows

You need to [download Git](https://git-scm.com/downloads 'Git download page') then open the `.exe` file to install Git. Accept all the defaults during the install with two exceptions:

1. _Choosing the default editor used by Git_. I chose VS Code but there is a way to set your default editor from Git Bash or the terminal (see below).
2. _Adjusting the name of the initial branch in new repositories_ by not choosing _Let Git decide_, and instead set it to _main_.

**NOTE**: You need Git Bash but that comes bundled with Git for Windows.

On the last screen you can select _Launch Git Bash_ then press finish or find Git Bash on your computer and open it. For me on Windows, there was a Git folder in my Start ment and Git bash was in there.

Open it then to verify that git is installed type `git --version` or `git -v` for short. If you see a version number then Git installed properly.

To close the Git Bash window just type `exit`. To open it again, you can hover over a folder in Windows Explorer, right-click and select _Git Bash Here_.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Authenticate with GitHub

On your first push ever to GitHub, you will need to authenticate your machine with GitHub. This is so Git/GitHub knows that you are who you say you are.

In the past you could just use `user.name` and `user.email` to verify your identity to GitHub. Now you have to generate an SSH key for authentification. I used the following docs to do that:

1. Link 1: [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
1. Link 2: [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

However, you still need to have `user.name` and `user.email` set. Here are the commands I used for my new laptop but I suggest using the 2 links above:

```sh
# Check to make sure Git installed by checking the version:
git --version
# or just
git -v

# To check to see if you have a name set already use:
git config user.name

# Set your user name and email
git config --global user.name "Name you want to be associated with"
git config --global user.email "Use the email you used for GitHub"

# Make VS Code your default editor
git config --global core.editor "code --wait"
```

The steps for creating your SSH key:

```sh
# 1. Generate your key
ssh-keygen -t ed25519 -C "myemail@somewhere.com"

# or if that doesn't work:
ssh-keygen -t rsa -b 4096 -C "myemail@somewhere.com"

# 2. Press ENTER for location and 3. for the passphrase then start the SSH agent:
eval "$(ssh-agent -s)"

# 4. Add your SSH private key to the ssh-agent
ssh-add ~/.ssh/id_ed25519

# 5. Copy the SSH public key to your clipboard.
clip < ~/.ssh/id_ed25519.pub
```

Those commands worked and I then cloned this repo.

I was then able to commit my changes but on my first `git push` I got a message about having to authenticate my GitHub account. There was a new tab open in Chrome where I clicked _Authenticate_ and I think I only had to enter my GitHub password. I should have taken better notes but I was more concerned on getting everything to work.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Pushing a local project to an empty repo on GitHub

After you created a project with files on your machine, you then need to push them to GitHub.

Don't worry if you do not know what the words _branch_, _staging_, _commit_ or _remote_ means - you will in time. You can use the commands that GitHub shows when you create the repo or use the following commands but make sure to copy the repo URL link (`https_url`).

Also note that step 4 requires you to add the URL for an empty repo on Github, so create an empty repo from your GitHub account. Choose to make it a public repo and DO NOT add a `README.md` file. The basic steps are:

```bash
# 1. Initiaze git tracking in the current folder:
git init
# 2. Add all your files to staging:
git add .
# 3. Commit the files in your staging area:
git commit -m "First commit"
# 4. Optionally rename the default branch from master to main:
git branch -M main
# 5. Set the remote to the optional name 'origin':
git remote add origin https_url
# 6. Push your commited changes to your repo:
git push -u origin master
```

An alternate way to add new or changed files to staging is to add the files individually:

```bash
# Use the following to add files individually to staging:
git add filename1.ext filename2.ext
```

**NOTE**: When you create an empty repo on GitHub, it's best practice to use the same name on GitHub as the folder on your local machine, though you can still push if the names do not match. I tend to make the names the same so that there is no confusion for repos/projects with similar names.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Commands after initial push

Now your local repo is connected to your remote repo on Github. After making some changes or creating new files use:

```bash
git add .
git status
git commit -m "Your next commit message"
git push
# Or
git push origin master
```

**NOTE**: You need to use `git push -u origin master` for the first commit. After that just use `git push`, although I believe you can still use `git push origin master` _AFTER_ the first commit and it won't have a negative effect.

Also, get in the habit of using `git status` as a way to check the status of your files and folders.

**NOTE**: You can add your files to staging and commit them in one command with the `-am` flag with the `commit` command:

```bash
git commit -am "Commit message"
```

Also, try not to make changes to any files on GitHub. If you do, you need to run either `git pull` or `git fetch`. The only time you may need to create a file on GitHub is adding a LICENSE file. See the INTERMEDIATE_GIT.md file for details on t hose commands.

<!-- Add notes on the following maybe: git log --oneline, git diff, clear -->

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Clone one of your existing GitHub repos

You would clone your own repo when you get a new computer/laptop or if you accidentally deleted one of your local repos.

Go to the main repo page and click on the green `Code` button and copy the _HTTPS_ link and replace `https_url` in the commands below with that link

```sh
# Go to the folder where you want your project folder and run
git clone https_url
# move into that folder
cd folder_name
# Check the remote location
git remote -v
```

**NOTE**: `git clone` automatically initializes Git and sets the remote so you do not need the commands `git init` and `git remote add origin https_url`. By running `git remote -v` you should see:

```bash
origin  https://github.com/You_User_Name/your_repo_name.git (fetch)
origin  https://github.com/You_User_Name/your_repo_name.git (push)
```

Then make some changes and run the standard commands:

```sh
git status
git add .
git commit -m "your commit message"
git push
# Or run
git push origin main
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Clone a repo that is not yours

These commands are for when you want to work on a repo that someone else created. The commands are the same as the section above except you want to change the remote location.

Go to GitHub and create an empty repo.

**NOTE**: `https_url` for the `git clone` command is the URL of the repo you want to clone, but `https_url` for the `git remote set-url origin` command should be the URL for the empty repo you created.

Then back in Git Bash or VS Code run these commands:

```sh
git clone https_url
cd folder_name
# Check to see where the remote is pointing to
git remote -v
# Set your GitHub repo as the remote
git remote set-url origin https_url
# Check to make sure it is now pointing to your account
git remote -v
git push -u origin master
```

Then for pushes after you set the upstream use:

```sh
git add .
git commit -m "your message"
git push origin master
# or just
git push
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## gitignore

There are some files that you do NOT want to push to a remoe public repository. The files you want Git to ignore include secrets, environmental variables, API keys, credentials, operating system files, log files, dependencies and packages, etc.

To have Git ignore any files that you do not want to push, create a file called `.gitignore`, usually in the root of your project folder. Add the paths and file names that you do not want to push:

```sh
index.html
js/test.js
*.log
```

For large repositories, this file will have a lot of entries. For some npm commands like `npx create-react-app` this file will be created for you.

If you want to ignore a folder you need to add `/` after the folder name or Git will think it is a file.Here is an example of a basic gitignore file. You _always_ want to add `node_modules` assuming you added node packages to your project:

```sh
# Dependencies
node_modules

# Production and other folders
/build
/dist

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

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Important Notes about the `commit` command

I originally would do massive changes to one or many files and `commit` all those changes, then `push` them to my GitHub repo. _THAT IS NOT WHAT YOU WANT TO DO!_

What you want to do is `commit` changes in related batches. You can have as many commits as you want when you run `git push`. Each `commit` should be for a specific change in case you need to _undo_ that commit.

**COMMIT MESSAGES**: you should use 1) present tense 2) imperative style when writing your commit mesages, although some people prefer past tense:

- `make thing do X` or past tense:
- `made thing do X`

**Atomic commits**:

- Atomic Commits – when possible a commit should encompass a single feature, change, or fix – focused on a single thing – that makes undo/rollback easier and makes your code easier to review

NOTE: If you forget to add `-m "msg"` with your `commit` command, you will be taken either into the Vim editor or VS Code if you added the global command for that. If you are in the Vim editor, type `:wq` to exit Vim.

## Reference links

FYI, it's difficult keeping this list up-to-date. I'll do my best to provide the best resources that I find and that work for me.

1. [Git reference docs](https://git-scm.com/docs 'Git documentation')
1. [GitHub for complete beginners MDN](https://developer.mozilla.org/en-US/docs/MDN/Contribute/GitHub_beginners 'MDN GitHub docs')
1. [Why Use Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/#why-use-conventional-commits 'Conventional Commits')
1. [Contribute to freeCodeCamp.org](https://contribute.freecodecamp.org/#/ 'freeCpdeCamp contribution docs')
1. [how-to-setup-freecodecamp-locally.md](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md 'How to setup freeCodeCamp locally')
1. [freeCodeCamp Conflicts on a pull request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md#making-changes-locally 'freeCodeCamp PR Conflicts')
1. [freeCodeCamp Introduction](https://contribute.freecodecamp.org/#/index 'freeCodeCamp contribution intro')
1. [freeCodeCamp How to work on coding challenges](https://contribute.freecodecamp.org/#/how-to-work-on-coding-challenges 'freeCodeCamp: Working on coding challenges')
1. [freeCodeCamp FAQs](https://contribute.freecodecamp.org/#/FAQ 'freeCodeCamp FAQs')
1. [freeCodeCamp How to open a Pull Request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-open-a-pull-request.md 'How to open a PR freeCodeCamp')
1. [freeCodeCamp How to contribute to open source](https://github.com/freeCodeCamp/how-to-contribute-to-open-source 'How to contribute to open source')
1. [How to contribute on GitHub](https://www.dataschool.io/how-to-contribute-on-github/ 'Step-by-step guide to contributing on GitHub')
1. [Contributing to MDN](https://developer.mozilla.org/en-US/docs/MDN/Contribute 'Contributing to MDN')
1. [Hostinger: Basic GIT Commands](https://www.hostinger.com/tutorials/basic-git-commands 'Basic GIT Commands')
1. [Frequently used Git Commands](https://codeburst.io/git-tutorial-a-beginners-guide-to-most-frequently-used-git-commands-2ab92bd22787 'Frequently used Git Commands')
1. [Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials)

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<p>_ _ _ _ _ _ _ _ _ _ _</p>

## Final notes

I may have errors or incorrect usage of commands in this file. I'll fix them as I find them. Or open an issue or create a pull request for any proposed changes.

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

### Git keywords

I'm wondering if putting in the following keywords will help beginners searching on GitHub to find this repo:

**Keywords**: git for beginners, basic git commands, basic git commands cheat sheet, basic git commands github, basic git commands for beginners, basic git commands list, basic commands for git, github basic commands, basic commands in git, basic git command, basic git commands to know, what are basic git commands, git guide command line, most basic git commands, basic commands of git, basic git workflow commands, basic git cheat sheet, git commands cheat sheet github.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>
