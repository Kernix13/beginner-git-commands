# Useful files for repository projects

This file should not be in here but I will leave it anyway. They are files added in a repo I was contributing to. Check out my repo [github-actions-dotfiles](https://github.com/Kernix13/github-actions-dotfiles) for more dotfiles and a more in-depth explanation of each.

<a id="back-to-top"></a>

## Table of contents

1. [github folder](#github-folder)
1. [husky folder](#husky-folder)
1. [editorconfig file](#editorconfig-file)
1. [prettierignore file](#prettierignore-file)
1. [prettierrc file](#prettierrc-file)
   1. [How to configure Prettier and VSCode](#how-to-configure-prettier-and-vscode)
1. [Code of Contact file](#code-of-contact-file)
1. [Workflow Rules](#workflow-rules)

## github folder

This has one file in a repo I am contributing on: `pull_request_template.md`

```
# Description

<!-- Please include a detailed summary of the changes made. Also please link the issue that this PR is fixing. -->

Fixes # (issue)

<!-- Please place an x in the [ ] to check off the type of change for this PR -->

## Type of change

- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Chore items (this includes basic clean up of files, or updates to packages)
- [ ] Updates to documentation

<!-- Please make sure to go through the entire checklist before requesting a review. Place an x in the [ ] to check off all of the items completed -->

## Checklist

- [ ] I have a descriptive title for my PR
- [ ] I have linked this PR to the corresponding issue. [See how to do that here.](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue)
- [ ] I have run the project locally and reviewed the code changes
- [ ] My changes generate no new warnings
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## husky folder

Has the following files:

1. `_` folder
   1. `.gitignore` file - makes no sense to have this because the `.gitignore` in the husky folder has this folder in it - this only has `*` in it
   1. `husky.sh` file: see below
1. `.gitignore` file only has `_`
1. `pre-commit` file: see below

husky.sh file:

```sh
#!/usr/bin/env sh
if [ -z "$husky_skip_init" ]; then
  debug () {
    if [ "$HUSKY_DEBUG" = "1" ]; then
      echo "husky (debug) - $1"
    fi
  }

  readonly hook_name="$(basename -- "$0")"
  debug "starting $hook_name..."

  if [ "$HUSKY" = "0" ]; then
    debug "HUSKY env variable is set to 0, skipping hook"
    exit 0
  fi

  if [ -f ~/.huskyrc ]; then
    debug "sourcing ~/.huskyrc"
    . ~/.huskyrc
  fi

  readonly husky_skip_init=1
  export husky_skip_init
  sh -e "$0" "$@"
  exitCode="$?"

  if [ $exitCode != 0 ]; then
    echo "husky - $hook_name hook exited with code $exitCode (error)"
  fi

  if [ $exitCode = 127 ]; then
    echo "husky - command not found in PATH=$PATH"
  fi

  exit $exitCode
fi
```

pre-commit file

```sh
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npx lint-staged
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## editorconfig file

From EditorConfig.org:

> EditorConfig helps maintain consistent coding styles for multiple developers working on the same project across various editors and IDEs. The EditorConfig project consists of a file format for defining coding styles and a collection of text editor plugins that enable editors to read the file format and adhere to defined styles. EditorConfig files are easily readable and they work nicely with version control systems.

I assume this along with the prettier files means you do not need the Prettier extension.

editorconfig file:

```md
# EditorConfig is awesome: https://EditorConfig.org

# top-most EditorConfig file

root = true

# Unix-style newlines with a newline ending every file

[*]
end_of_line = lf
insert_final_newline = true

# Matches multiple files with brace expansion notation

# Set default charset

[*.{js,html}]
charset = utf-8

# 2 space indentation

[*.{js,html,css}]
indent_style = space
indent_size = 2

# Tab indentation (no size specified)

[Makefile]
indent_style = tab

# Indentation override for all JS under lib directory

[lib/**.js]
indent_style = space
indent_size = 2

# Matches the exact files either package.json or .travis.yml

[{package.json,.travis.yml}]
indent_style = space
indent_size = 2
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## prettierignore file

```sh
# Ignore artifacts:
build
coverage
```

## prettierrc file

```json
{
  "trailingComma": "es5",
  "tabWidth": 2,
  "semi": true,
  "singleQuote": false
}
```

### How to configure Prettier and VSCode

- https://glebbahmutov.com/blog/configure-prettier-in-vscode/
- https://github.com/yi-Xu-0100/Application-Lists/blob/main/.prettierrc.js
- https://github.com/cccttt10/css-analytics-frontend/blob/master/.prettierrc.json

```json
{
  "arrowParens": "avoid",
  "bracketSpacing": true,
  "endOfLine": "auto",
  "printWidth": 85,
  "quoteProps": "preserve",
  "semi": true,
  "singleQuote": true,
  "tabWidth": 4,
  "useTabs": false
}
```

```json
{
  "arrowParens": "always",
  "bracketSpacing": true,
  "singleQuote": true,
  "jsxBracketSameLine": true,
  "parser": "babylon",
  "printWidth": 180
}
```

- https://github.com/SchemaStore/schemastore/blob/master/src/schemas/json/prettierrc.json

My settings.json file (prettier only):

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "prettier.printWidth": 9999,
  "prettier.arrowParens": "avoid",
  "prettier.trailingComma": "none"
}
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Code of Contact file

```md
# Contributor Code of Conduct

All members and contributors should strive to create a harassment-free experience for everyone, regardless of age, body size, visible or invisible disability, ethnicity, sex characteristics, gender identity and expression, level of experience, education, socio-economic status, nationality, personal appearance, race, religion, or sexual identity and orientation.

We are here to encourage a welcoming, diverse, inclusive, and healthy community.

## Examples of positive community involvement

- Practicing empathy and kindness toward other people
- Being respectful of differing opinions
- Be open to providing and receiving constructive feedback

## Examples of negative community involvement

- The use of sexualized language or imagery, and sexual attention or advances of any kind
- Trolling, insulting or derogatory comments, and personal or political attacks
- Public or private harassment
- Publishing others' private information, such as a physical or email address, without their explicit permission
- Other conduct which could reasonably be considered inappropriate in a professional setting

If you wish to participate in our open source project, please adhere to this code of conduct.
```

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>

## Workflow Rules

Notes from the Discord server for the repo contrast-ratio-repo that I did a few contributions to.

1. All discussions for new features will be in the discussions tab on github. Check that periodically and leave your comments.
1. Once we have decided on features, then it will be broken into issues for people to pick up and work on.
   1. Make sure to break the work down into tickets for everyone to work on.
1. Once you pick up an issue, make sure to
   1. Create a new branch and make your changes there.
   1. Then you will need to push your changes to GitHub and create a new PR.
   1. Then request a review so we can review changes and approve it and merge it into main.
   1. Also make sure to link the issue you are working on to that PR.
1. Once your PR is merged, you are free to delete the branch from both the remote and local repos. Then make sure to update your main branch locally by using git pull.
1. Then update your main branch using git fetch && git rebase if you feel comfortable with that option.
1. While you are waiting for a review on your PR, feel free to pick up any new issue that hasn't been assigned yet.
1. Please make sure to link the issue you are working on to the PR you created. That will automatically close the issue when the PR is merged so we don't have to remember to do that ourselves and have old issues on the board that has been completed.
1. When you create a PR, you can request a review from someone on the team and they will be alerted through email to leave a review

<div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div>
