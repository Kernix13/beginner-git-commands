# Learn the basic of the contributing process

> **Issue to Pull Request process**: Learn the steps you will need to contribute to an open-source project.

There is a lot you need to be good at before contributing like creating branches, pushing branches, and deleting branches. You also need how to write good commit messages, Pull Request Titles and Descriptions, creating issues and labels, plus all t he correct git commands.

This document is meant to do all of the steps on your repos first, so that when you start contributing, you will understand the entire process.

<a id="back-to-top"></a>

## Table of contents

1. [Detailed Steps](#detailed-steps)
1. [Overview](#overview)
   1. [Issue titles](#issue-titles)
   1. [Commit messages](#commit-messages)
   1. [Pull Request titles](#pull-equest-titles)
   1. [My approach](#my-approach)
   1. [Basic Steps](#basic-steps)
1. [1. Branch name](#1-branch-name)
   1. [Strict Rules](#strict-rules)
   1. [Best Practices for branch names](#best-practices-for-branch-names)
1. [2. Issues](#2-issues)
   1. [A. Issue title](#a-issue-title)
   1. [B. Issue description](#b-issue-description)
   1. [C. Issue label](#c-issue-label)
   1. [More on Issues](#more-on-issues)
1. [3. Commits](#3-commits)
   1. [Commit Messages](#commit-messages)
1. [4. Pull Requests](#4-pull-requests)
   1. [A. Pull Request Titles](#a-pull-request-titles)
   1. [B. Pull Request Description](#B-pull-request-description)
   1. [Open a Pull Request](#open-a-pull-request)
1. [Git Commands](#git-commands)
1. [Important notes on commits and PRs](#important-notes-on-commits-and-prs)
1. [Issue Labels and Commit and PR Prefixes](#issue-labels-and-commit-and-pr-prefixes)
1. [Clone vs fork and contributing](#clone-vs-fork-and-contributing)
   1. [Cloning](#cloning)
   1. [Forking](#forking)
1. [Detailed steps with code blocks](#detailed-steps-with-code-blocks)

## Detailed Steps

> ### REMEMBER, REMEMBER, REMEMBER TO CREATE YOUR BRANCH <ins><em>BEFORE</em></ins> DOING ANY WORK!!!

1. Create a branch on local machine for the issue
2. Create an issue with a label(s) on GitHub
   1. Issue title
   2. Issue description
   3. Issue label
   4. Issue assignee (optional)
3. Make changes, commit and push the changed file(s)
4. Merging the resulting pull request
   1. Click the "Compare and pull request" button
   2. Rewrite PR title (edit original commit message) to more clearly descibe your work
   3. Add a description of the actions you took to fix the issue
   4. Add "closes #123" in the PR description field
   5. Click the "Create pull request" button below textarea field
   6. Click the "Merge pull request" button. Other options are "Squash and merge" or "Rebase and merge"
   7. Click the "Confirm merge" button: "_Pull request successfully merged and closed_"
5. Pull main/merged changes from remote to local
6. Delete the local branch and the remote branch
7. Run `git fetch --prune`

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Overview

Looking at freeCodeCamp and React repos for their use of prefixes in issue and PR titles, and commit messages:

### Issue titles

- freeCodeCamp: just title + 2-3 labels
- React: `prefix:` or `[prefix]:` or just title + 1 to 3 labels (mostly 1)

### Commit messages

- freeCodeCamp: `prefix:` or `prefix(scope):`
- React: `[prefix]` sometimes

### Pull Request titles

- freeCodeCamp: `prefix:` or `prefix(scope):`
- React: `[prefix]` sometimes

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### My approach

1. Branch name: type/task (e.g., refactor/button-css, bug/hamburger-menu)
2. Issue titles: just title + 1-3 labels
3. Commit titles: `prefix: desc` or `prefix(scope): desc`
4. Pull Request titles: `prefix: desc` or `prefix(scope): desc`

Example:

- Issue: "Refactor data fetching logic"
- Commit: refactor(api): simplify error handling
- PR: "refactor: API data fetching for clarity and maintainability"

Prefix example:

- Issue label -> `docs`
- Issue title beginning -> `docs:` (NOT FOR ME)
- Commit message beginning -> `docs:`
- PR title beginning -> `docs:`

### Basic Steps

1. Create a branch
2. Create an issue
3. Do the work
4. Add, commit, push changes -> Pull Request
5. Merge PR
6. Pull changes
7. Delete local and remote branches

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## 1. Branch name

Choose a branch name that is descriptive of the task. Also, remember to switch to main - don't create a branch on the tip on another branch!

### Strict Rules

- Cannot start with a hyphen (`-`)
- Cannot end with a dot (`.`)
- Cannot be the single character `@`
- Cannot contain:
  - multiple consecutive forward slashes (`//`)
  - the sequence `@{.`
  - control characters (like newline, tab - `\n`, `\t`, `\r`)
  - special characters that have meaning in the shell, unless escaped or quoted (e.g., `$` for variables)
  - characters like `~`, `^`, `:`, `?`, `*`, `[`, `\`, or spaces without proper escaping/quoting, as these can conflict with shell or Git's internal parsing.

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Best Practices for branch names

- **Lowercase and Hyphen-separated**: Use lowercase letters and separate words with hyphens
- **Descriptive and Concise**: The name should clearly indicate the purpose of the branch
- **Prefixing for Categories**: Use prefixes to categorize the branch's purpose (e.g., `feature/`, `bugfix/`, `hotfix/`, `release/`). This helps in organizing and identifying branches
- **Avoid Long Names**: Keep branch names reasonably short for better readability and ease of use in commands
- **Consistency**: Maintain a consistent naming convention across the project or team
- **Include Issue/Ticket ID** (Optional but Recommended): If working with an issue tracker, include the issue ID for easy reference (e.g., feature/JIRA-123-new-dashboard)

**Examples of a good branch name**: type/task

- feature/user-profile-enhancements
- bugfix/login-authentication-error
- hotfix/critical-production-issue
- fix/navbar-active-item
- chore/update-deps
- refactor/pricing-card-css
- feat/add-contact-form

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## 2. Issues

- Issue title
- Issue description
- Issue label

### A. Issue title

Best practice for solo or small repos: Let labels do the categorization, and keep issue titles clean and descriptive.

. . . . . . . . . . . . . . . . . . .

### B. Issue description

- Current state – What's happening now?
  - What the current state is (_anonymous function_)
- Desired change – What should be different?
  - What needs to change (_refactor to named function_)
- Location/context – Where in the codebase or app does this apply?
  - Where it should go (_/utils folder_)

OPTIONAL:

- Steps to reproduce (for bugs)
- Expected vs. actual behavior (for bugs again)
- Screenshots or code snippets
- Checklist (for multi-step tasks)
- Related issues or context

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### C. Issue label

Here are some common issue labels:

- docs or documentation: Improvements or additions to documentation
- enhancement: New feature or request (or feature)
- bug: Something isn't working
- refactor: architectural/code restructuring
- chore: minor maintenance, like updating deps, renaming, cleaning files
- in progress: currently being worked on
- todo: queued for work
- good first issue: Good for newcomers
- help wanted: Extra attention is needed
- question: Further information is requested
- high priority
- low priority
- duplicate: This issue or pull request already exists
- invalid: This doesn't seem right
- wontfix: This will not be worked on

To create a label:

1. Click the Issues tab
2. Click Labels button
3. Click New label button
4. Give it a name, description, and color
5. Click Create label

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### More on Issues

Create an Issue

1. Click "Issues" > New Issue
2. Write:
   1. A clear title
   2. A brief, structured description (what it is, where it is, how to fix it)
3. Apply a label (e.g. bug, refactor, etc.)
4. Assign someone to the issue (optional)
5. Submit

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## 3. Commits

A good commit message should:

- Explain what changed
- 50 characters to 70 characters max

Commit Hygiene (What it Really Means):

- Write clear, concise, and useful commit messages
- Prefer atomic commits — each commit does one thing
  - Group related changes into single commits
- Avoid meaningless messages like "update" or "fix stuff"

Be consistent:

- lowercase types
- no period at end
- concise phrasing

### Commit Messages

- Commits are small, atomic units of change
- Many repos follow Conventional Commits style:

```sh
type(optionalscope): description

# Examples
refactor(api): simplify error handling
fix(auth): handle expired tokens correctly
refactor: extract tab key handler
fix(navbar): resolve mobile overlap
docs: edit README file
```

- Consider these prefixes: api, build, ci, chore, config, docs, env, feat, fix, perf, refactor, sec (security), style, test, deps, design, revert, merge

> Use the `type: description` format

- Commits: `prefix: desc` or `prefix(scope): desc`
- Prefixes are most useful if they align with your issue labels!
  - See Conventional Commits

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## 4. Pull Requests

### A. Pull Request Titles

- By default, GitHub sets the PR title to the commit message of the commit for the branch, but you should edit the PR title to be more human-readable.
- _A PR is the package of changes you're proposing, so its title should summarize the whole branch, not just the first commit_.

. . . . . . . . . . . . . . . . . . . . . .

### B. Pull Request Description

Write a helpful PR description

- Brief summary of what was done and why
- Optionally mention:
  - What files or modules were affected
  - Any side effects or follow-ups
  - Links to related issues (e.g., Closes #14)

Choose a merge strategy - GitHub lets you:

- Squash and merge — good if you want one tidy commit per PR
- Merge commit — preserves full commit history
- Rebase and merge — linear history, but more advanced

Example:

- Issue: "Refactor data fetching logic"
- Commit: refactor(api): simplify error handling
- PR: "Refactor API data fetching for clarity and maintainability"

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Open a Pull Request

> "Compare & pull request" - is a short cut to open a PR from that branch into the base branch

1. Click Pull Requests > New Pull Request
2. Add:
   1. PR title (e.g. Fix: broken tab key shortcut)
   2. PR description (what you changed and why)
3. Click Create Pull Request

- Wait for Feedback or Merge

After Merge: Clean Up

```sh
# Switch to main branch
git switch main

# Pull down changes from the merge on GitHub
git pull

# Then delete your local and remote branches
git branch -d fix/tab-key-shortcut
git push origin -d fix/tab-key-shortcut

# Optional cleanup
git fetch --prune

# I saw this warning:
warning: deleting branch 'docs/learn-contributing' that has been merged to
'refs/remotes/origin/docs/learn-contributing', but not yet merged to HEAD.
Deleted branch docs/learn-contributing (was b737c7e).
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Git Commands

Here are the commands needed from start to finish

```sh
# Remember to run git status as often as you need
# Create new_branch and switch to it (I don't use checkout -b):
git switch -c new_branch

# Make changes then add and commit:
git add .
git commit -m "your message"

# Push changes to GitHub:
git push --set-upstream origin new_branch
# or shorthand:
git push -u origin new_branch

# Future pushes:
git push

# switch back to main
git switch main

# Ensures your local main branch reflects any changes from the merged PR
git pull

# check branches
git branch

# delete a local branch that has been fully merged
git branch -d branch-to-delete

# check branches
git branch

# delete a remote branch
git push origin -d branch-to-delete

# Optional but Recommended
# Removes stale tracking references like origin/new_branch that no longer exist remotely
git fetch --prune
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Important notes on commits and PRs

The green "Compare & pull request" button is GitHub saying: "Hey, you pushed a new branch. Do you want to open a PR right away?"

But you don't have to. Two options: you can open the PR right away, or wait until you're done

1. Option 1: Open PR immediately

- You click the button right after your first push.
- A PR is created, even if the work isn't finished yet.
- You keep pushing commits → they show up automatically in that PR.
- This is handy if you want early feedback or to track progress.

2. Option 2: Wait until you're ready

- Ignore the button at first.
- Keep committing and pushing to your branch until the issue is solved.
- Only when you're satisfied, open the PR.
- Cleaner if you're working solo and don't need anyone watching your progress.

So the process for option 1 is:

- Click the "Compare and pull request" button
  - You do not need to finish all your work before creating the PR
  - Once the PR is open, you can continue committing and pushing to the same branch
  - Every push updates the open PR automatically
- Rewrite PR title (original commit mesage) to more clearly descibe your work
- Add a description of the actions you took to fix the issue
- Add "`closes #123`" in the PR description field
  - NOTE: You can always edit the PR description before merging at which point you can add "`closes #123`"
- Click the "Create pull request" button below textarea field
- Click the "Merge pull request" button when done your work. Other options are "Squash and merge" or "Rebase and merge"
- Click the "Confirm merge" button, you will see this message: "Pull request successfully merged and closed"

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Issue Labels and Commit and PR Prefixes

| Issue Label   | Commit/PR Prefix | Example Commit Message               |
| :------------ | :--------------- | :----------------------------------- |
| bug           | fix:             | fix: resolve crash when saving form  |
| feature       | feat:            | feat: add user profile page          |
| enhancement   | refactor:        | refactor: simplify API call handling |
| documentation | docs:            | docs: update README with setup steps |
| chore         | chore:           | chore: update dependencies           |
| in progress   | (no prefix)      | N/A                                  |
| blocked       | (no prefix)      | N/A                                  |
| todo          | (no prefix)      | N/A                                  |
| high priority | (no prefix)      | N/A                                  |

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Clone vs fork and contributing

### Cloning

Cloning: gets a repo that is not on your machine based on a URL, but you can't push your changes to someone's repo

Typical use cases for cloning:

- You own the repo
- You're a collaborator or team member
- Your teammate added you with push access

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

### Forking

FORKS: a personal copy of someone else's repos in your account – the copy is called a "fork". If you want to make changes and push them up to GitHub, then fork the repo, clone your fork and the remote will be set to push to your copy of the repo. Now you can push to your forked version

THAT IS THE POINT OF FORKING - TO CONTRIBUTE TO AN OPEN-SOURCE PROJECT!

Reasons to fork:

- Creates a personal copy of a repo on GitHub, under your own account
- Used when you don't have write access to the original repo
- You work on your own copy and then open a pull request to contribute back

Steps:

1. Click "Fork" on GitHub to create your own copy
2. Clone your forked repo
3. Make changes, push to your fork
4. Open a pull request to the original repo

When to Use Each

- Clone - You're working on your own project - You already own the repo
- Clone - Your class/teammate adds you as a collaborator - You now have write access
- Fork - You want to contribute to a repo - You can't push directly, so you fork and PR
- Fork - You're contributing to a public open-source project - You won't have push access (this sounds wrong)

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Detailed steps with code blocks

These are the steps from above but with git code blocks and my method of writing titles and messages. The commands will include practical examples instead of `branch_name`.

1. Create a branch on local machine for the issue.

```sh
# Make sure you have committed and pushed all changes from/for main
git status

# Check what branch you are on and to see the other branch names
git branch

# Create a branch and switch to it
git switch -c utils/local-storage
```

2. Create an issue with a label(s) on GitHub.
   1. Issue title: **_Create functions to set and get localStorage_**.
   2. Issue description.
   3. Issue label: `utils`.
   4. Issue assignee (optional).
3. Make changes, commit and push the changed file(s).

```sh
git status
git add .
git commit -m "utils: create FXs to set/get localStorage for form elements"

# Push changes to GitHub:
git push --set-upstream origin utils/local-storage
# or shorthand:
git push -u origin utils/local-storage
```

4. Merging the resulting pull request.
   1. Click the "_Compare and pull request_" button.
   2. Rewrite PR title if necessary (edit original commit message) to more clearly descibe your work.
   3. Add a description of the actions you took to fix the issue - be as descriptive as necessary.
   4. Add `Closes #123` in the PR description field.
   5. Click the "_Create pull request_" button below textarea field.
   6. Click the "_Merge pull request_" button.
   7. Click the "_Confirm merge_" button: "_Pull request successfully merged and closed_".
5. Pull main/merged changes from remote to local.

```sh
# switch back to main
git switch main

# Bring changes from the merged PR down to yout local machine
git pull
```

6. Delete the local branch & the remote branch,

```sh
# check branches
git branch

# delete a local branch that has been fully merged
git branch -d utils/local-storage

# check branches
git branch

# delete a remote branch
git push origin -d utils/local-storage

# Optional but Recommended
# Removes stale tracking references like origin/utils/local-storage that no longer exist remotely
git fetch --prune
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>
