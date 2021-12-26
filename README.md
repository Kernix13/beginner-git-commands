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

**Note**: You need to use `git push -u origin master` for the next commit only after the initial push (don't ask me why). After that just use `git push`, although I believe you could do `git push origin master` and it won't have a negative effect.

## Clone your own repo

Why would you do this?

## Clone an existing repo (cloning a repo that is not yours)

something here

## Create a repo from the command line and initialize the repo

I don't think anyone does this. Everyone seems to just create an empty repo. But you can try using this link:
[Adding an existing project to GitHub using the command line](https://docs.github.com/en/github/importing-your-projects-to-github/importing-source-code-to-github/adding-an-existing-project-to-github-using-the-command-line).

```
git init -b main
git add . && git commit -m "initial commit"
gh repo create project-name
```

I get an error for the use of `&&` and `gh` so just create an empty repo.
