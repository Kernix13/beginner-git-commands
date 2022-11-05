# Advanced Git Commands

This markdown file is a work-in-process...there is not a lot here now. I will be adding to this file as I learn more.

<a id="back-to-top"></a>

1. [Handling merge conflicts](#handling-merge-conflicts)
1. [Mistakes](#mistakes)
   1. [Undo Staging](#undo-staging)
   1. [Undo a Commit](#undo-a-commit)
   1. [Remove Git](#remove-git)
   1. [Remove remote origin](#remove-remote-origin)

## Handling merge conflicts

I'm a little fuzzy on this process. There are a few of ways to handle merge conflicts: 1) on Github, 2) in your terminal, or 3) directly in your code. However, try not to make any mistakes so you don't have to deal with conflicts.

Read more here: [Conflicts on a pull request](https://github.com/freeCodeCamp/freeCodeCamp/blob/main/docs/how-to-setup-freecodecamp-locally.md#making-changes-locally 'Making changes locally').

A merge conflict is when 2 or more people change the same code/content but with different values. However, I don't think a beginner contributor would actually run `git merge branch_name`.

But if you did and there was a conflict, in VS Code you will see something like:

```sh
<<<<<<< HEAD (Current Change)
<p>some change here</p>
=======
<p>different change here</p>
>>>>>>> Branch-Name (Incoming Change)
```

Where `HEAD` is your current branch, usually main/master. Once again, this would only be done by the owner of the repo, but what you would do is:

1. Decide which change you want to keep,
1. Delete EVERYTHING else -> the change you don't want and the equal (`=`), less than (`<`), and greater than (`>`) signs along with the text like `HEAD` and `Current Change`. Everything other than the actual change that you want.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Mistakes

You will undoubtedly make mistakes when working with Git. Here are common mistakes that I have made and how to fix/undo them.

### Undo Staging

If you accidentally added a file with `git add .`, to remove it from the staging area, use:

```sh
# without arguments
git reset
# with filename and optional path
git reset path/filename.ext
```

### Undo a Commit

Use `git reset` again but include `HEAD` which means the last commit. But to undo the last coomit add `~1` to go back 1 commit past the last commit which will undo the last commit:

```sh
git reset HEAD~1
```

But what if you want to go back a number of commits or to a specific commit. First use `git log` which gives you a list of your commits in reverse chronological order. You can scroll down the log with <kbd>SPACEBAR</kbd>.

You will see the commit hash and the commit message along with other information. To go back to a specific commit and undo it, use the hash for it:

```sh
# use git reset HASH:
git reset e220bfb1e34b8c6b6fce1deb7884244239284716
```

That will unstage any changes made to the file(s) AFTER that commit. The changes will be in your files but they will not be saved into git anymore. But how do you get rid of all the changes after a certain point? USe the same command but add the flag `--hard`:

```sh
git reset --hard e220bfb1e34b8c6b6fce1deb7884244239284716
```

You can also remove a specific file from staging by using `git rm –cached filename.ext` where `rm` is short for remove.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Remove Git

To remove git tracking from a folder use the following command in `git bash`, the command prompt or in VS Code:

```sh
rm -rf .git
```

### Remove remote origin

I once pasted in my repo link ending in `.gi` instead of `.git` because I missed copying the `t`. Use the following to remove the origin and try again:

```sh
git remote remove origin
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>
