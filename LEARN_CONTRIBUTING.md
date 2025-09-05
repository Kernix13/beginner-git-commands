# Learn the basic of the contributing process

> **Issue to Pull Request process**

Learn the steps you will need to contribute to an open-source project.

## Detailed Steps

> ### REMEMBER, REMEMBER, REMEMBER TO CREATE YOUR BRANCH _BEFORE_ DOING ANY WORK!!!

1. Create a branch on local machine for the issue
2. Create an issue with label(s) on GitHub
   1. Issue title
   2. Issue description
   3. Issue label
   4. Issue assignee
3. Make changes, commit and push the changed file(s)
4. Merging the resulting pull request
   1. Click the "Compare and pull request" button
   2. Rewrite PR title (original commit mesage) to more clearly descibe your work
   3. Add a description of the actions you took to fix the issue
   4. Add "Fixes #number" in the title to close the issue (or in the description field? Which is best: title or description?) You can also add it in the final merge description field
   5. Click the "Create pull request" button below textarea field
   6. Click the "Merge pull request" button. Other options are "Squash and merge" or "Rebase and merge"
   7. Click the "Confirm merge" button: "_Pull request successfully merged and closed_"
5. Pull main/merged changes from remote to local
6. Delete the local branch and the remote branch
7. Run `git fetch --prune`

## Overview

Looking at freeCodeCamp and React repos for their use of prefixes in issue and PR titles, and commit messages:

Issues

- freeCodeCamp: just title + 2-3 labels
- React: `prefix:` or `[prefix]:` or nothing + 1 to 3 labels (mostly 1)

Commits

- freeCodeCamp: `prefix:` or `prefix(scope):`
- React: `[prefix]` sometimes

PRs

- freeCodeCamp: `prefix:` or `prefix(scope):`
- React: `[prefix]` sometimes

Mine: (Copy freeCodeCamp's approach)

1. Issue titles: just title + 1-3 labels
2. Branch name: type/task - refactor/button-css, bug/hamburger-menu
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

Basic Steps:

1. Create a branch
2. Create an issue
3. Do the work
4. Add, commit, push changes -> Pull Request
5. Merge PR
6. Pull changes
7. Delete the branch

## 1. Issues

- Issue title
- Issue description
- Issue label

**Issue title**:

Best practice for solo or small repos: Let labels do the categorization, and keep issue titles clean and descriptive.

. . . . . . . . . . . . . . . . . . .

**Issue description**:

- What the current state is (anonymous function)
- What needs to change (refactor to named function)
- Where it should go (/utils folder)

1. Current state – What’s happening now?
2. Desired change – What should be different?
3. Location/context – Where in the codebase or app does this apply?

OPTIONAL:

- Steps to reproduce (for bugs)
- Expected vs. actual behavior (for bugs again)
- Screenshots or code snippets
- Checklist (for multi-step tasks)
- Related issues or context

. . . . . . . . . . . . . . . . . . .

**Issue label**:

```
bug: Something isn't working
documentation: Improvements or additions to documentation
enhancement: New feature or request
feature: a new addition, big or small (or enhancement?)

refactor: architectural/code restructuring
chore: minor maintenance, like updating deps, renaming, cleaning files

in progress: currently being worked on
todo: queued for work

good first issue: Good for newcomers
help wanted: Extra attention is needed
question: Further information is requested

high priority
low priority

duplicate: This issue or pull request already exists
invalid: This doesn't seem right
wontfix: This will not be worked on
```

### More on Issues

Create an Issue

1. Click "Issues" > New Issue
2. Write:
   1. A clear title
   2. A brief, structured description (what it is, where it is, how to fix it)
3. Apply a label (e.g. bug, refactor, etc.)
4. Assign someone to the issue (optional)
5. Submit

## 2. Branch name

**Branch name**:

- type/task
  - fix/navbar-spacing
  - chore/update-deps
  - refactor/pricing-card-css
  - feat/contact-form

## 3. Commits

A good commit message should:

- Explain what changed
- 50 chars to 70 chars max

Commit Hygiene (What it Really Means):

- Write clear, concise, and useful commit messages
- Prefer atomic commits — each commit does one thing
  - Group related changes into single commits
- Avoid meaningless messages like "update" or "fix stuff"

Be consistent:

- lowercase types,
- no period at end,
- concise phrasing

Commit Messages

- Commits are small, atomic units of change.
- Many repos follow Conventional Commits style:

```sh
type(optionalscope): description
# Examples
refactor(api): simplify error handling
fix(auth): handle expired tokens correctly
refactor(keyboard): extract tab key handler
fix(navbar): resolve mobile overlap
```

- Consider: api, build, ci, chore, config, docs, env, feat, fix, perf, refactor, sec (Security), style, test, deps, design, revert, merge

> Use the `type: description` format

- Commits: `prefix: desc` or `prefix(scope): desc`
- Prefixes are most useful if they align with your issue labels!
  - See Conventional Commits

## 4. Pull Requests

**Pull Request Titles**:

- By default, GitHub sets the PR title to the commit message of the first commit in the branch. So yes — it "defaults" to a commit message, but you should edit the PR title to be more human-readable.
- A PR is the package of changes you’re proposing, so its title should summarize the whole branch, not just the first commit.

. . . . . . . . . . . . . . . . . . . . . .

**Pull Request Description**:

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

### Open a Pull Request (PR)

> "Compare & pull request" - is a short cut to open a PR from that branch into the base branch

1. Click Pull Requests > New Pull Request
2. Add:
   1. PR title (e.g. Fix: broken tab key shortcut)
   2. PR description (what you changed and why)
3. Click Create Pull Request

- Wait for Feedback or Merge

After Merge: Clean Up

```sh
git switch main
git pull
# Then delete your branch
git branch -d fix/tab-key-shortcut
git push origin -d fix/tab-key-shortcut
# Optional cleanup
git fetch --prune

warning: deleting branch 'docs/learn-contributing' that has been merged to
'refs/remotes/origin/docs/learn-contributing', but not yet merged to HEAD.
Deleted branch docs/learn-contributing (was b737c7e).
```

## Git Commnads

```sh
# Create new_branch and switch to it (I don't use checkout):
git switch -c new_branch

# Add and commit:
git add .
git commit -m "your message"

# push changes to GitHub:
git push --set-upstream origin new_branch
# or shorthand:
git push -u origin new_branch

# future pushes:
git push

# switch back to main
git switch main
git status

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
# Pull the latest from main (make sure you are on main):

# Optional but Recommended
# Removes stale tracking references like origin/new_branch that no longer exist remotely
git fetch --prune
```

## Clone vs fork and contributing

### Cloning

Cloning: gets a repo that is not on your machine based on a URL, but you can't push your changes to someone's repo

Typical use cases for cloning:

- You own the repo
- You’re a collaborator or team member
- Your teammate added you with push access

### Forking

FORKS: a personal copy of someone else's repos in your account – the copy is called a "fork". If you want to make changes and push them up to GitHub, then fork the repo and push to your forked version. Then you can clone your fork and the remote will be set to push to your copy of the repo.

THAT IS THE POINT OF FORKING - TO CONTRIBUTE TO AN OPEN-SOURCE PROJECT!

Reasons to fork:

- Creates a personal copy of a repo on GitHub, under your own account
- Used when you don’t have write access to the original repo
- You work on your own copy and then open a pull request to contribute back

Steps:

1. Click "Fork" on GitHub to create your own copy
2. Clone your forked repo
3. Make changes, push to your fork
4. Open a pull request to the original repo

When to Use Each

- Clone - You’re working on your own project - You already own the repo
- Clone - Your class/teammate adds you as a collaborator - You now have write access
- Fork - You want to contribute to a repo - You can’t push directly, so you fork and PR
- Fork - You’re contributing to a public open-source project - You won’t have push access

## Issue Labels and Commit/PR Prefixes

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
