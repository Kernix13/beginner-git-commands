# Beginner Git commands

The basic steps you need in the beginning are:

- Download and setup Git (one time ony)
- Create an empty repo on GitHub
- Initialize Git in a project folder
- Make changes or create a file
- Add the changes to staging then commit the changes
- Push your changes or project files to your empty repo


If you created any files on Github, then you will have to use `git clone` and `git pull` before you can do a `git push`. So don't create any files on GitHub in the beginning.

<a id="back-to-top"></a>

<p>----------------------------</p>

## Table of contents

1. [Download and setup Git](#download-and-setup-git)
1. [Pushing your local files to an empty repo](#pushing-your-local-files-to-an-empty-repo)
1. [Commands after initial push](#commands-after-initial-push)
1. [Clone your own repo](#clone-your-own-repo)
1. [Clone an existing repo](#clone-an-existing-repo)
   1. [Push the cloned files up to your repo](#push-the-cloned-files-up-to-your-repo)
1. [Branches](#branches)
1. [Forking and cloning](#forking-and-cloning)
1. [GitHub pull request process](#github-pull-request-process)
   1. [Pull request title](#pull-request-title)
   1. [Pull requests page notes](#pull-requests-page-notes)
   1. [Replies to your pull request](#replies-to-your-pull-request)
   1. [Staying up to date](#staying-up-to-date)
   1. [Handling merge conflicts](#handling-merge-conflicts)
1. [Create a repo from the command line](#create-a-repo-from-the-command-line)
1. [Miscellaneous git commands](#miscellaneous-git-commands)
1. [Reference links](#reference-links)
1. [Final notes](#final-notes)
   1. [Terminology](#terminology)
   1. [Git keywords](#git-keywords)

<div>----------------------------------------</div>

## Download and setup Git

It's been well over a year since I did this so I can't remember all the steps. But first, you need to first [download Git](https://git-scm.com/downloads 'Git download page').

Check out this video from the YouTube channel LearnWebCode: [Git Tutorial Part 3: Installation, Command-line & Clone](https://youtu.be/UFEby2zo-9E 'Git Tutorial'). I followed his steps to run the `config` commands below. Follow his instructions using Git Bash. Eventually, you will use VS Code for 99% of the commands in this guide.

**Note**: On your first push ever to GitHub, you will need to provide a `user name` and `email address` to git, I assume the ones used when you created your GitHub account. This is so git knows that you are who you say you are. 

Check your GitHub profile to see what name you entered. Click your thumbnail image in the top right and select Settings. It will be the first field.

Ater downloading Git, open the `.exe` file in your downloads folder. Then find Git Bash and open it. For me on Windows there was a Git folder in my Start ment and Git bash was in there. Open in and in the commpand prompt that opens enter the following commands:

```
git config --global user.name "Github user name"
git config --global user.email "youremail@somewhere.com"
```

The `git config` command is used initially to configure the `user.name` and `user.email` fields. This specifies what email and username will be used from a local repository.

The `--global` flag tells Git that you're going to use the email above for all repos on your computer. Replace that with `--local` to use different emails for different repos.

Some people mention using an SSH key to validate your identity. I found that a little confusing so I prefer the method above.

Also, try the following command to see all the configuration settings:

```
git config --list
```

Run that command and scroll down and look for `user.name="Yourname"` and `user.email="your-email@whatevs.com"`, though until you set those values you either will not see those fields or they will be set to empty strings.

[Back to Top](#back-to-top "Table of contents")
<p>-------------------------------------------------------------------</p>

## Pushing your local files to an empty repo

Here are the commands followed by a brief definition. Make sure to know these because they are used for other sections in this file:

```
git init
git add .
git commit -m "First commit"
git branch -M main (optional)
git remote add origin https_url
git push -u origin master
```
**NOTE**: I removed 'git' from the commands in the definition tables to make the table smaller. You should know to add `git` before the main commands (not for the parameters).

**Definitions**:

| *Basic* Git Commands | Definition |
| :--------------- | :---------- |
| init             | Initiates git tracking |
| status           | Check the status of your changes/state |
| add .            | Adds ***ALL*** (.) changes to staging |
| commit           | Saves changes to local copy |
| remote add origin | Adds URL as remote repo location |x`
| `branch -M main`   | Changes default branch to 'main' (this is optional) |
| push -u origin main | Push changes to remote |
| push             | Push changes after upstream is set | 
| push origin main | Used for 1st push if `-u` not used |
| -u               | Parameter short for `upstream` |
| upstream         | the primary *branch* on the original repository; where you cloned the repo from |

The command `git remote add origin https_url` connects the local repository to a remote server (GitHub repo). `https_url` is the URL that is on the page when you create a new repo. It is also shown whn you click the `Code` button.

The `git push` command is used to send local commits to the master (or main) branch of the remote repository. But to use `git push` in the future you have to set something called an *upstream*, meaning where you want to push it to by default. That is why you use `-u`.

Replace **master** with the branch where you want to push your changes when you’re *not* intending to push to the master branch. 

[Back to Top](#back-to-top "Table of contents")

## Commands for initial push

after making some changes use:

```
git add .
git status
git commit -m "Created README file"
git push -u origin master
```

**Note**: You need to use `git push -u origin master` for the next commit only after the initial push. After that just use `git push` unless you used `-u` as mentioned above (DOUBLE CHECK THAT). Although I believe you can run `git push origin master` and it won't have a negative effect. Also, I use `git status` as a habit to check the status of the files, though that command is not required.

These commands work for me when pushing to a repo I created without a README file. If you have a README file, then you will get an error when trying to push, so you'll have to do a `git pull` command to pull the README to your local repo then you can use `git push`.

The only difference is `git branch -M main` and I think the flag `-M` means changing the master branch to the name **main**. The `add README.md` command is not necessary. Just create and edit your README in VS Code and push it to your repo.

[Back to Top](#back-to-top "Table of contents")

## Clone your own repo

Like `git init`, the command `git clone` also initiates a git repo for a repo you want to clone, but git is installed in the downloaded/cloned folder, *NOT* in the directory where you ran that command. But both initiate git tracking.

That all works for your repos, but eventually you will want to clone, or fork and clone a repo so that you can contribute to it. You will then need to use the `git clone` again, and various `branch` git commands. You will also need to add additional parameters to your git commands:

<dl>
  <dt>Clone</dt>
  <dd>Copies repo at the URL to your machine</dd>
  <dd>Used on its own or with Fork</dd>
  <dd>It's best to use this with Git Bash</dd>
</dl>

| *Clone* Commands | Definition |
| :--------------- | :--------- |
| clone            | Copies repo at the URL to your machine |
| remote set-url origin | Change your remote's URL |
| | |

[Back to Top](#back-to-top "Table of contents")

## Clone an existing repo

Use `git remote -v` to list any remote repositories that you have connected to this repo. That is to check if you are pointing to the cloned URL or the repo in your account. Did you clone to contribute, or to work on your own version of the repo?

[Back to Top](#back-to-top "Table of contents")

### Push the cloned files up to your repo


[Back to Top](#back-to-top "Table of contents")

## Branches

<dl>
  <dt><strong>Branch</strong>:</dt>
  <dd>...</dd>
</dl>

| *Branch* Commands | Definition |
| :--- | :--- |
| branch -a | ... |
| checkout branch_name | |
| checkout -b new_branch | |
| merge new_branch | |
| diff new_branch | |
| | |

[Back to Top](#back-to-top "Table of contents")

## Forking and cloning

<dl>
  <dt><strong>Fork</strong>:</dt>
  <dd>Copies the forked repo into your account</dd>
</dl>

| *Fork* Commands | Definition |
| :-------------- | :--------- |
| --depth=1             | Creates a shallow copy of the repo |
| remote -v        | A check to make sure the URL is correct |
| remote add upstream   | Pull changes from the original repo...  |
| -                     | ...into the local clone of your fork |
| fetch upstream        | ... |
| reset --hard upstream/main | |
| --hard                | |
| push origin main --force | |
| --force               | |
|                       | |

[Back to Top](#back-to-top "Table of contents")

## GitHub pull request process


[Back to Top](#back-to-top "Table of contents")

### Pull request title



### Pull requests page notes



### Replies to your pull request



### Staying up to date



### Handling merge conflicts



## Create a repo from the command line



## Miscellaneous git commands



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

## Final notes

I may have errors or incorrect usage of commands in this file. I'll fix them as I find them. Or contact me and let me know what needs to be changed at [Kernix Web Design](https://kernixwebdesign.com/contact/ 'Contact page').

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

### Terminology

Here are some common terms. These notes are from git, MDN, and other sources:

1. **upstream**: the primary *branch* on the original repository; where you cloned the repo from.
1. **origin**: The default upstream repository - a reference to the remote repository from where a project was initially cloned.
1. **remote / remote repository**: the version of a repository or branch that is hosted on a server (like GitHub), a shared repository that all team members use to exchange their changes.
1. **fetch**: adding changes from the remote repository to your local working branch without committing them.
1. **pull**: Pulling a branch means to fetch it and merge it; fetches and merges changes on the remote server to your working directory.
1. **push**: To send your committed changes to a remote repo, to upload local repo content to a remote repo.
1. **clone**: used to make a copy of the target repository; a copy of a repo that lives on your computer.
1. **merge**: bring the contents of another branch into the current branch; to take the data created on a separate branch and integrate them into a single branch.
1. **head**: A named reference to the commit at the tip of a branch.
1. **HEAD**: your current branch, or a defined commit of a branch, usually the most recent commit at the tip of the branch, or refers to the current commit you are viewing. `HEAD` is a reference to one of the heads in your repository.
1. **blob**: (Binary Large OBject) Untyped object, e.g. the contents of a file, is the object type used to store the contents of each file in a repository.

### Git keywords

I'm wondering if putting in the following keywords will help beginners searching on GitHub to find this repo:

**Keywords**: git for beginners, basic git commands, basic git commands cheat sheet, basic git commands github, basic git commands for beginners, basic git commands list, basic commands for git, github basic commands, basic commands in git, basic git command, basic git commands to know, what are basic git commands, git guide command line, most basic git commands, basic commands of git, basic git workflow commands, basic git cheat sheet, git commands cheat sheet github, ...

<!-- Ignore this line, experimenting with markdown comments -->
