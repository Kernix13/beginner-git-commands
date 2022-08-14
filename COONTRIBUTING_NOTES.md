# NOTES

Notes for the [contrast-ratio-repo](https://github.com/DBenMoshe/contrast-ratio-repo) that I am a part of

## Notes from Discord

Summary of most important points:

**<ins>General and Workflow</ins>**:

1. New features will be added on the discussions tab
1. Then it will be broken into issues for people to pick up and work on
1. Assign yourself to open issues
1. Reviews: you should see a dropdown list of everyone
1. Request a reviewer(s) so changes can be requested, followed by approval to merge with main/master.
1. Add a `label` to the issue to give more information about the issue
1. Once you pick up an issue, make sure to create a new branch
1. Then you will need to push your changes to github and create a new PR.
1. Make sure to link the issue you are working on to that PR
1. Once you PR is merged, you are free to delete the branch from both the remote and local repos.
1. Resolve conversation button (?)

Git specific:

- `--set-upstream` adds the local branch you were working on to the remote repo. Setting that up will allow git to track those changes and allow you to push commits to that branch
- You only need to use that command the first time you create a new branch and push it up to github. After that, you can just use `git push`
- Then make sure to update your main branch locally by using `git pull`.
- You can also update your main branch using `git fetch` or `git rebase`.

Branching, PR's and Issues

- Branch conventions example: `[type of change]/issue number: branch name`
- Make your branch names descriptive
- Merge conflicts (later)
- Link your pull requests to an issue to show that a fix is in progress and to automatically close the issue when the pull request is merged
- [Linking a pull request to an issue](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue)
- Use a short descriptive name (for PR title or branch?).
- As for leaving a comment, you can just assign yourself to it and that will let everyone know you are working on it
- When you create a PR, you can request a review from someone on the team and they will be alerted through email to leave a review
- Please make sure to link the issue you are working on to the PR you created. That will automatically close the issue when the PR is merged
- You should only merge a PR when it has been approved. Squash and merge button
- If you want to request changes, make sure to select that option and submit review. Then your comments will show up in the PR
- Difference between `merge pull request` and `squash and merge` buttons -> `Merge pull request` will add all of the commits from that PR, all of those will be added when it is merged. But the `squash and merge` option will squash all of those commits into one commit. It keeps the git history a little bit cleaner.
- PR Titles: [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
- open draft PR...
- Typically it is not best practice to push changes to someone else's PR. It is best to leave a review comment on their PR of suggested changes
- `labels` are there to give basic info
- Once you have made some changes, push up your changes to the new branch and select the "Create draft" option. You can also place the WIP label on it. This will let people know that it is a work in progress. People can still leave early feedback, but they will know that it is not finished yet.
- create tickets(issues) to address the work that needs to be done
- check the issues tab to see who is assigned to what issue. When you are interested in working on an issue assign yourself so others know it is taken

### Collaboration (General)

- 8/5 - Notes from page [Permission levels for a personal account repository](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-personal-account-settings/permission-levels-for-a-personal-account-repository#collaborator-access-for-a-repository-owned-by-a-personal-account)
- Collaborators on a personal repository can pull (read) the contents of the repository and push (write) changes to the repository. Collaborators can also perform the following actions:
- Fork the repository | Rename a branch other than the default branch | Create, edit, and delete comments on commits, pull requests, and issues in the repository | Create, assign, close, and re-open issues in the repository | Manage labels for issues and pull requests in the repository | Manage milestones for issues and pull requests in the repository | Mark an issue or pull request in the repository as a duplicate | ...and...
- Create, merge, and close pull requests in the repository | Enable and disable auto-merge for a pull request | Apply suggested changes to pull requests in the repository | Create a pull request from a fork of the repository | Submit a review on a pull request that affects the mergeability of the pull request | Create and edit a wiki for the repository | Create and edit releases for the repository | Act as a code owner for the repository | Publish, view, or install packages | Remove themselves as collaborators on the repository
- Once you assign yourself, then you will clone the repo in your command line. Then you will create a branch
- 8/6 - The last step would be to update your local main branch with the latest changes. You run `git pull` on the local main branch to pull down those changes. Since you are done with this issue branch you can remove it on github and remove it locally if want...As for reviews, you should see a dropdown list of everyone who has accepted the invite for this repo to be a collaborator
- code comments: They can be really helpful. "The purpose of comments is to explain code that cannot explain itself." As long as your code has good variable and function names, then your comments can provide additional information for other developers
- resolve conversation button: Is that a button for me to click on? or is it there for you too, you can also click on it ? I don't know for sure actually. I guess it's clicked by reviewer when requested changes discussed or done
- 8/9 - An SSH key is another way to identify yourself to Github instead of using a username and password. If you are receiving those errors messages, there might be an issue with your SSH keys. You can just use the HTTPS
- what is `--set-upstream` ? basically it just adds the local branch you were working on to the remote repo. The remote repo is github in this case. Setting that up will allow git to track those changes and allow you to push commits to that branch - You only need to use that command the first time you create a new branch and push it up to github. After that, you can just use `git push`
- 8/10 - Hopefully this project will encourage people to take a chance and try something even if it is incorrect. Getting in the habit of trying new things and learning from mistakes is the best way to learn and grow. Plus it is great preparation for the actual job where you will frequently thrown into new situations and technologies you have never worked with
- The local server is your computer serving you up the website using your local network. When you run `npm start` it will start up a local server on port `3000`. This allows you to see your website and make changes especially since we haven't deployed it anywhere yet for it to be made publicly available.

### Collaboration Basic Workflow

- 8/7 - Here is the basic workflow process that we will all follow that mimic what you would do on professional dev teams.
- All discussions for new features will be in the discussions tab on github. Check that periodically and leave your comments.
- Once we have decided on features, then it will be broken into issues for people to pick up and work on.
- Once you pick up an issue, make sure to create a new branch and make your changes there. Then you will need to push your changes to github and create a new PR. Then request a review so we can requests changes and approve it so it can be merged into main. Also make sure to link the issue you are working on to that PR. Check the pinned messages here on how to do that.
- Once you PR is merged, you are free to delete the branch from both the remote and local repos. Then make sure to update your main branch locally by using `git pull`. You can also update your main branch using `git fetch` && `git rebase` if you feel comfortable with that option.
- While you are waiting for a review on your PR, feel free to pick up any new issue that hasn't been assigned yet.

### Branching

- 8/5 - There are different branch conventions that teams will use. One pattern is `[type of change]/issue number: branch name`, e.g. `chore/2,setting-up-basic-files`
- 8/9 - A merge conflict happens when two or more developers make changes to the exact same lines of code. GIt does not know which changes to keep just like the picture shows.
- To resolve a merge conflict, you have to go back into the code on the branch you were working on and resolve the conflict. In most cases, you will keep both sets of changes. If you need to remove the other person's changes, it is always best to consult with them first.

```powershell
remove these comments  that git added
<<<<<<< feature-readme
=======
>>>>>>> main
```

- and push up a new change to the branch
- 8/10 - all branch names will start with the conventional commits model we have been using.
- make your branch names descriptive: `fix/23,fixing-cypress-tests`
- 8/11 - The best way to resolve merge conflicts is to use VS code, it will show you a nice interface so you can see what changes you have to make. The way to resolve them is to manually look at the differences between your changes and the other developers and decide on which ones to keep.

### Pull Requests

- 8/5 - [Linking a pull request to an issue](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue)
- You can link a pull request to an issue to show that a fix is in progress and to automatically close the issue when the pull request is merged
- If you want to include the issue number. As long as everyone uses a short descriptive name. As for leaving a comment, you can just assign yourself to it and that will let everyone know you are working on it...you can go back to your local setup, add those changes, push up another commit to that branch and request a rereview...edit your post to link the PR to the issue. That will automatically close the issue when the PR is merged
- 8/7 - When you create a PR, you can request a review from someone on the team and they will be alerted through email to leave a review. Since you just created your first PR, please request a review from...?
- Please make sure to link the issue you are working on to the PR you created. That will automatically close the issue when the PR is merged so we don't have to remember to do that ourselves and have old issues on the board that have been completed
- You should only merge a PR when it has been approved. Squash and merge button
- If you want to request changes, make sure to select that option and submit review. Then your comments will show up in the PR
- you can edit your comment a little bit, and issue will be automatically closed when merge will happen
- You can add at the end of comment specific keyword and number of the issue
- what's the difference between `merge pull request` and `squash and merge` buttons -> `Merge pull request` will add all of the commits from that PR. So if someone has 50 commits, all of those will be added when it is merged. But the `squash and merge` option will squash all of those commits into one commit. It keeps the git history a little bit cleaner. Since this is a smaller repo, either option is fine. But in a lot of cases, especially for larger projects, the squash and merge is used
- 8/8 - since you assigned to this issue, you can add label WIP to it
- I brought up a discussion in the github discussions tab about following conventional commits. The consensus was that people wanted to follow that. For all PR titles, we will follow that convention.
- This makes our PR title more semantic instead of saying "fixing files" or something like that. I have already edited some of the PR titles for our repo. You can read more about it here: [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
- open draft PR to adding a formatter to the project to clean up our code format and ensure that the codebase if properly formatted at all times
- If you pull down a branch, make changes to it, and push those changes it will show up in that existing PR. It will not create a new one. The only way you would create a new PR is if you first created a new branch off of his and then made changes.
- But typically it is not best practice to push changes to someone else's PR. It is best to leave a review comment on their PR of suggested changes.
- The only time I pushed up to someone's PR in this project was your old one for the readme because there was a merge conflict and I used that as an example to show the team how to resolve merge conflicts. But other than that, you shouldn't push to other people's PRs without their permission first
- `labels` are there to give basic info
- feel free to review the codebase and create issues if you feel like they are needed
- you can simply change title of your PR to something else
- 8/10 - Since you are pushing to the same branch, it will add to that same PR. Not create a new one.
- [WIP]: `This is just a demo - DO NOT MERGE #28`
- Once you have made some changes, push up your changes to the new branch and select the "Create draft" option. You can also place the WIP label on it. This will let people know that it is a work in progress. People can still leave early feedback, but they will know that it is not finished yet.

### Issues

- 8/11 - team members to start creating tickets(issues) to address the work that needs to be done.
- 8/11 - You can always check the issues tab to see who is assigned to what issue. When you are interested in working on an issue assign yourself so others know it is taken.
- We typically don't assign issues to each other

### Notes from Repo

DISCUSSION TAB

The Prettier issue...

- The dependencies that will be added are `prettier`, `husky`, `lint-staged` and `browser-sync`.
- Every time you work on a new issue and push changes to GitHub, the prettier precommit hook will fire and automatically check to make sure that your code is formatted. If not, it will automatically format it for you.
- Husky added the "prepare": "husky install" script
- I added a `"start": "browser-sync start --server --files .",` and found that in the documentation.
- When you run `npm start`, it will start the local server and use hot reloading when new changes are made.
- **Now people won't be dependent on installing local server extensions like Live Server on their IDE's and code editor**
- They can just run that command it will start the local server.
- You can still use the Live server extension, but now it will just be optional.
- > Can you recommend any resources on how to write those scripts based on the packages being used? Some of the packages will automatically add a script.
- But for writing script commands, always check with documentation first.
- You can also study large open source codebases.
- If you inspect their codebases, you can study their package.json files and see what kinds of scripts they wrote.

MISC

- https://github.com/thisdot/starter.dev
- https://github.com/thisdot/starter.dev/pull/269
- README: Prettier formatting script - The `npm run format` command will format all of the files for the project.

### Job or Team notes

Convention for the branch naming

- Whenever you join a new team, you should first look to the onboarding docs if they exist. Some teams will be very particular about what branch names and PR titles they want to use and it will be documented in the onboarding docs for that project. Other teams are not that picky and will default to some common patterns
- Learning how to break up the work and create tickets is an important skill to learn because you will be doing it on the job.
- On the job, most of the time you will pick up tickets(issues) on the board that are free to work on. Sometimes your manager will assign you an issue if they want you to work on that specific task right then.
- On any team environment, you should always wait for approval.
- for larger projects, the squash and merge is used
- It is common to ask questions on PR's
- When you are working on larger issues, it is important to commit your work along the way because you never know if something will happen to your computer and all of your information is lost. Plus it will help you get into the habit when working on large codebases, and you are working on a big feature. It is best to commit your code along the way in that case.

A realistic experience that you would find on a professional dev team.

- Typically what happens, is when a new project is greenlit, the senior architects, team leads and project managers will get together and make all of the decisions for the features, technologies, the architecture and will create all of the basic setup. Then they will create a whole bunch of tickets dividing up the work and the rest of the team will pick them up and work on them.
- It is always best to start off with a basic starter code and then work on fine details. Once the basic prototype is finished, we will do some manual testing of the app and find bugs and create issues for them. We will also add some basic unit tests using Jest. Then we will deploy it
- Also this process, will hopefully show people that there is a lot of discussion that happens when building out software. Most people think that workdays are filled with 8 hours of coding. But that is very far from the truth. Your days will be filled with meetings with clients, pair programming sessions with teammates, and team discussions on how to implement new features.
- The most programming you will ever do is as an entry level developer. The higher up you go, the more responsibility you will be given and the more meetings and decisions you will have to make. You will have less time to code
- As a junior you will start off working on small bug fixes. It will also take a while to get onboarded with the project and company. So you won't be contributing a lot because you are still getting use to the codebase. Then they will start to hand you small features to complete with the assistance of the team.
- Mid level will start to be trusted with more responsibilities and implementing features on their own with very little assistance. Seniors will start to make more of the architectural decisions on what technologies, libraries, tooling, etc to use. They are still coding, just not as much.
- Staff, architects and Principals will be leading teams. They make the final decisions and will have the technical knowledge and experience to jump on any project and assist where needed. These engineers usually have 10+ years of experience
- When you are first starting out, you will probably be coding 5-6 hours. You won't have to many meetings. Then it bumps down to about 4-5 hours. Then it goes from there.
- It also depends on where you are at in the project. For example, the team may be testing the app and, doing code reviews and making small bug fixes... testing the edge cases and making sure the product is good to go for the launch.
- Also, don't worry about error handling right now. We can decide on how we best want to show the user they have an invalid input in a later ticket
