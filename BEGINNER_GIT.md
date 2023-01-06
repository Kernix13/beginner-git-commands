# Git Commands for Beginners

Get these commands down in the beginning, then move to the intermediate commands.

<a id="back-to-top"></a>

## Table of contents

1. [Download and setup Git](#download-and-setup-git)
1. [Pushing your local files to an empty repo](#pushing-your-local-files-to-an-empty-repo)
   1. [Commands after initial push](#commands-after-initial-push)
1. [Clone your own repo](#clone-your-own-repo)
1. [Clone an existing repo](#clone-an-existing-repo)
   1. [Push the cloned files up to your repo](#push-the-cloned-files-up-to-your-repo)
1. [Reference links](#reference-links)
1. [Final notes](#final-notes)
   1. [Terminology](#terminology)

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _</p>

## Download and setup Git

It's been a long time since I did this so I can't remember all the steps, but you will need to [download Git](https://git-scm.com/downloads 'Git download page').

Check out this video from the YouTube channel LearnWebCode: [Git Tutorial Part 3: Installation, Command-line & Clone](https://youtu.be/UFEby2zo-9E 'Git Tutorial'). I followed his steps to run the `config` commands below. Follow his instructions using Git Bash. Eventually, you will use VS Code for 99% of the commands in this guide.

**Note**: On your first push ever to GitHub, you will need to provide a `user name` and `email address` to git, the ones used when you created your GitHub account, or accounts on GitLab or BitBucket. This is so git knows that you are who you say you are.

Ater downloading Git, open the `.exe` file to install Git. Then find Git Bash and open it. For me on Windows, there was a Git folder in my Start ment and Git bash was in there. Open it...

In the past you could just use `user.name` and `user.email` to verify your identity to GitHub. Now you have to generate an SSH key to let GitHub know you are who you say you are. I used the following docs for the commands I used:

1. Link 1: [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
   Link 2: [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

Here are the commands I used:

```sh
# Generate your key
ssh-keygen -t ed25519 -C "myemail@somewhere.com"

# or if that doesn't work:
ssh-keygen -t rsa -b 4096 -C "myemail@somewhere.com"

# Press ENTER for location and for the passphrase start the SSH agent:
eval "$(ssh-agent -s)"

# Add your SSH private key to the ssh-agent
ssh-add ~/.ssh/id_ed25519

# Copy the SSH public key to your clipboard.
clip < ~/.ssh/id_ed25519.pub

# error on git commit:
# Author identity unknown
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

Those worked and I cloned this repo. Then I made a change and tried to commit it but I got an error in the command (see the last 4 lines in the code block above). So you still need to use `user.name` and `user.email`:

```sh
git config --global user.name "Github user name"
git config --global user.email "youremail@somewhere.com"
```

The git `config` command is used initially to configure the `user.name` and `user.email` fields. This specifies what email and username will be used from a local repository.

The `--global` flag tells Git that you're going to use the email above for all repos on your computer. Replace that with `--local` to use different emails for different repos.

I was then able to commit my changes but on `git push` I got a message about having to authenticate my GitHub account. There was a new tab open in Chrome where I clicked _Authenticate_ and I had to enter my GitHub password (something like that). I should have taken better notes but I was more concerned on getting everything to work.

Check out my SSH markdown file in my repo `bash-shell-scripts`, specifically the section [Generate SSH keys](https://github.com/Kernix13/bash-shell-scripts/blob/main/SSH.md#generate-ssh-keys) to learn more about that method.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _</p>

## Pushing your local files to an empty repo

Here are the commands followed by a brief definition on each. Make sure to know these because they are used for other sections in this file. By the way, you need to make changes to your files or create a file before running `git add .` unless you already have files in your project folder.

Go to GitHub and create an _empty_ repo, meaning _do not_ add a README file. Then back in Git Bash or VS Code and run:

```bash
git init
git add .
git commit -m "First commit"
git branch -M main
git remote add origin https_url
git push -u origin master
```

**NOTE**: I removed `git` from the commands in all the definition tables to make the table smaller. You should know to add `git` before the main commands (not for the parameters/flags).

| _Basic_ Git Commands | Definition                                                                      |
| :------------------- | :------------------------------------------------------------------------------ |
| init                 | Initiates git tracking                                                          |
| status               | Checks the status of your changes/state                                         |
| add .                | Adds **_ALL_** (.) changes to staging                                           |
| commit -m "msg"      | Saves changes to local machine with a message                                   |
| remote add origin    | Adds URL as remote repo location                                                |
| `branch -M main`     | Changes default branch to 'main' (optional)                                     |
| push -u origin main  | Push changes to and sets remote                                                 |
| push                 | Push changes after upstream is set                                              |
| `-u`                 | Parameter short for `upstream`                                                  |
| `upstream`           | the primary _branch_ on the original repository; where you cloned the repo from |

The `git init` command creates a new local GIT repository in the directory you ran that command.

You tend to use `git add .` to commit all your changes to the staging area, but you do not have to do that. You could individually add some files to staging while not adding others. You would do that by specifying the files you want to add: `git add filename1.ext filename2.ext`, etc.

The command `git branch -M main` is optional and I think the flag `-M` means changing the default branch name from master to the name **main**. I tried searching for it and I found that Git has changed the default branch name from `master` to `main` though GitHub still uses `master` by default. It's your choice. To see the branch you are on, look to the far left of the bottom bar in VS Code.

The command `git remote add origin https_url` connects the local repository to a remote server (GitHub repo). `https_url` is the URL that is on the page when you create a new repo. It is also shown whn you click the `Code` button. And you do not have to use the keyword _origin_, that is just common practice to use that word.

The `git push` command is used to send local commits to the master (or main) branch of the remote repository. But to use `git push` in the future you have to set something called an _upstream_, meaning where you want to push it to by default. That is why you use `-u`. The whole command `git push -u origin master` pushes your commits and sets the branch `master` as the origin for the location of `git push` in the future.

The keyword `origin` means the branch you want to push to. Replace `master` with the branch where you want to push your changes when you’re _not_ intending to push to the master branch (See the Branch section in INTERMEDIATE_GIT.md).

**NOTE**: You can add a second `-m` flag to your commit command to add a description, though I never do that:

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

**Note**: I'll repeat this again => You need to use `git push -u origin master` for the first commit. After that just use `git push`. Although I believe you can still use `git push origin master` _AFTER_ the first commit and it won't have a negative effect, though it's totally unnecessary to do that.

Also, the flag `-u` is not needed if you are pushing to the default branch. And `-u` is short for `--set-upstream` which is what you would use when you are pushing a branch you created locally for the first time. By using that flag you set that as the default when you push the main or other branch to GitHub.

Also, I use `git status` as a habit to check the status of the files, though that command is not required.

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

**NOTE**: You can add your files to staging and commit them in one command with the `-am` flag with the `commit` command:

```bash
git commit -am "Commit message"
```

If you modified an existing file you can use `git commit -am "msg"` which combines **_add_** (`a`) amd **_message_** (`m`). That combines the `git add .` and `git commit -m "msg"` into one command.

Other commands you may find useful are:

1. `git log`: this shows you your commit history with the hash you would use to undo a commit with some of the advanced git commands.
1. `git diff`: this shows you the file(s) that changed and the actual changes by showing the before and after pictures of y our files.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _</p>

## Clone your own repo

> Why would you clone your own repo?

The one reason I will clone my repos is when I want to do more than just a refactoring of my code, but rather a total rewrite of the code. Regardless, the process is almost identical to cloning a repo that is not yours:

```sh
git clone https_url
cd folder_name
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

> I remove the command below for this process (EDIT TO-DO)

`remote set-url origin` here sets your repo as the source URL as opposed to changing the URL if cloned from a different account (see next section). It's function is similar to `remote add origin` in the first section.

Then make some changes and run the standard commands:

```sh
git status
git add .
git commit -m "First commit"
git push
```

That all works for your repos, but eventually you will want to clone, or fork and clone a repo so that you can contribute to it. You will then need to use the `git clone` again, and various `branch` git commands. You will also need to add additional parameters to your git commands (see the Forking and cloning section in INTERMEDIATE_GIT.md)

**NOTE**: This is an alterate way of initializing a local git repo than what is in the section [Pushing your local files to an empty repo](#pushing-your-local-files-to-an-empty-repo). The differece though is that this method installs git in the cloned file folder and not in the directory where you run `git clone url`, whereas in the section above it installs git in that folder.

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

Once again, since you did not fork this repo, but instead you want a copy of it to work on for yourself (assuming that is your intention), you need to first push it up to your empty GitHub repo. See the next section for the details on that...

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

Where `origin` stands for the default branch of your repo.. Then after making changes use the usual:

```sh
git add .
git commit -m "First commit"
git push -u origin master
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

<br />

<p>_ _ _ _ _ _ _ _ _ _ _ _ _ _ _</p>

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
