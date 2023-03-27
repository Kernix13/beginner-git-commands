# Summary of the most important Git Commands

| Command                           | Purpose                                 |
| :-------------------------------- | :-------------------------------------- |
| **BASIC**:                        | -                                       |
| `git init`                        | Create local repo                       |
| `git add .`                       | Stage all changed files                 |
| `git commit -m`                   | Commit staged files with a msg          |
| `git status`                      | List new/changed files                  |
| `git remote add origin https_url` | git remote add origin https_url         |
| `git push -u origin master`       | Push changes to and sets remote master  |
| `git remote -v`                   | Checks where your local copy points to  |
| `git push`                        | Push changes after upstream is set      |
| **INTERMEDIATE**:                 | -                                       |
| `git branch -a`                   | List all branches                       |
| `git checkout -b <branch>`        | Create & Switch to `<branch>`           |
| `git checkout <branch>`           | Switch to `<branch>`                    |
| `git branch -d <branch>`          | Delete `<branch>`                       |
| `git push -u origin <branch>`     | Push changes to and sets remote branch  |
| _Stayin up to date_:              | -                                       |
| `git checkout master`             | Switch to the master branch             |
| `git fetch upstream`              | fetch all objects/changes from upstream |
| `git merge upstream/master`       | Merch fetch files in to local           |
| **MISCELLANEOUS**:                | -                                       |
| `git diff`                        | Show unstaged changes                   |
| `git log`                         | Show full change history                |
