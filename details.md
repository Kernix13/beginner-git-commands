# Detailed descriptions on the commands

This is meant to be details and descriptions of the main files. I wanted to keep the main files as brief as possible, with explanations and insights on the commands placed here.

<a id="back-to-top"></a>

## Table of contents

1. [Beginner file notes](#beginner-file-notes)
1. [Intermediate file notes](#intermediate-file-notes)

## Beginner file notes

The `git config` command is used initially to configure the `user.name` and `user.email` fields. This specifies what email and username will be used from a local repository.

The `--global` flag tells Git that you're going to use the email above for all repos on your computer. Replace that with `--local` to use different emails for your projects/repos, although that is not recommended if you are new to Git.

Table of commands:

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

The command `git branch -M main` is optional and I think the flag `-M` means changing the default branch name from master to the name **main**. I tried searching for it and I found that Git has changed the default branch name from `master` to `main` though GitHub still uses `master` by default. It's your choice. To see the branch you are on, look to the far left of the bottom bar in VS Code or run `git branch`.

The command `git remote add origin https_url` connects the local repository to a remote server (GitHub repo). `https_url` is the URL that is on the page when you create a new repo. It is also shown when you click the `Code` button in your GitHub repo.

Also, the flag `-u` is not needed if you are pushing to the default branch. The flag `-u` is short for `--set-upstream` which is what you would use when you are pushing a branch you created locally for the first time. By using that flag you set that as the default when you push to GitHub

The `git push` command is used to send local commits to the _master_ (or _main_) branch of the remote repository. But to use `git push` in the future you have to set something called an _upstream_, meaning where you want to push it to by default. That is why you use `-u`. The whole command `git push -u origin master` pushes your commits and sets the branch `master` as the origin for the location of `git push` in the future.

The keyword `origin` means the branch you want to push to. Replace `master` with the branch where you want to push your changes when you're _not_ intending to push to the master branch (See the Branch section in INTERMEDIATE_GIT.md).

Here is a comparison of my commands vs. the commands you see on GitHub when you create an empty repo (there is only 1 difference). I am also tacking on the standard `add`, `commit`, and `push` commands and I removed the keyword `git` to dsave space in the table:

| Command Description           |             My Git commands | GitHub commands             |
| :---------------------------- | --------------------------: | :-------------------------- |
| Initiate tracking             |                        init | init                        |
| Make changes                  |                           - | -                           |
| Add changes to staging        |                       add . | add README.md               |
| Save changes to local         |    commit -m "First commit" | commit -m "First commit"    |
| Change default branch to main |                           - | branch -M main              |
| Add url as remote repo        | remote add origin https_url | remote add origin https_url |
| Verify repo url               |                   remote -v | remote -v                   |
| Push changes to remote        |       push -u origin master | push -u origin main         |
| Make additional changes       |                           - | -                           |
| Add new changes to staging    |                       add . | add .                       |
| Saves changes to local        |     commit -m "Next commit" | commit -m "Next commit"     |
| Recurring pushes              |                        push | push                        |

Other commands you may find useful are:

1. `git log`: this shows your commit history for the day with the hash you would use to undo a commit with some of the advanced git commands. Type `q` to exit the screen.
1. `git log --oneline`: show your commit hashes and messages on one line.
1. `git diff`: this shows you the file(s) that changed and the actual changes by showing the before and after pictures of your files. Type `q` to exit the screen.
1. `clear`: to clear the console/terminal. That is a terminal command, not a Git command.

**Clone notes**:

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
