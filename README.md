# Beginner Git commands

**Note**: On your first push ever to GitHub, you may need to provide a user name and email address, I assume the ones used when you created your GitHub account. I think the commands are something like this:

```
git config --global user.name “your-name”

git config --global user.email “something@something.com”
```

Sorry, I can't remember exactly what you have to do.

## Pushing your local files to an existing empty repo

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

### Commands after you do the above commands

after making some changes do:

```
git add .
git status
git commit -m "Reason for commit"
git push -u origin master
```

**Note**: You need to use `git push -u origin master` for the next commit only after the initial push (don't ask me why). After that just use `git push`, although I believe you could do `git push origin master` and it won't have a negative effect. Also, I'm adding `git status' as a habit to check the status of the files. That command is not necessary.

## Clone your own repo

Why would you do this?

## Clone an existing repo (cloning a repo that is not yours)

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

## Create a repo from the command line and initialize the repo

I don't think anyone does this. Everyone seems to just create an empty repo. But you can try using this link:
[Adding an existing project to GitHub using the command line](https://docs.github.com/en/github/importing-your-projects-to-github/importing-source-code-to-github/adding-an-existing-project-to-github-using-the-command-line).

```
git init -b main
git add . && git commit -m "initial commit"
gh repo create project-name
```

I get an error for the use of `&&` and `gh` so just create an empty repo.

## Branches and merging

Here are common commands:

```
git branch
git checkout branch_name
git checkout -b new_branch
git merge branch_name
git diff branch_name
```

The 1st command above just lists all the branch names in your repo. The next two switches to the branch and creates then switches to that branch, respectively. The merge command merges the branch into whatever branch you are currently in, most likely master.

More commonly you will push the changes to github then make a PR (push request).. For a new branch, git push wont work because git doesn’t know what branch you are pushing to – so do:

```
git push --set-upstream origin branch-name
```

To pull changes from GitHub to your machine use `git pull origin master`

To delete a branch use `git branch -d branch_name`

## Miscellaneous commands to know

I need to look into somee of these:

```
git commit -am
git reset filename.ext
git reset HEAD
git revert id
git log
git add -A
git add *.html
git --version
git config -l
git rm –cached filename
git remote -v
git push --set-upstream origin branch-name
git merge --abort
git config --global core.editor "code –wait"
git config --global core.autocrlf true
```
