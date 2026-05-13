# GitHub only related topics

1. Creating a GitHub gist (cut from INTERMEDIATE_GIT.md)
2. GitHub pages (cut from INTERMEDIATE_GIT.md)
3. Repo Management (NEW)
4. Pull Request Reviews (NEW)

## My repos needing branch rules

Repos with no issues with npm or branches or other:

- skills-communicate-using-markdown | skills-getting-started-with-github-copilot | vision-grid-express | learn-git | task-tracker | github-finder | music-store-mern-ecommerce | house-marketplace | _github-actions-dotfiles_ | CY_project | feedback-app | typescript-virtual-keyboard | WriterAssist | chordy-svg | content | tarp-configurations | webpack-starter | freeCodeCamp

Repos with no issues, vanilla repo:

- personal-portfolio | guitar-chord-names | CY-portfolio-template | DataAnalysisModule3 | skills-introduction-to-github | bash-shell-scripts | windows-cmd-prompt | to-do-app | codeCompare | fetch-apis | dev-tools | music-player | rural-homestead | htaccess | M1W6Deliverable | M1W4Deliverable | M1W3Deliverable | in-class-assignment-m1-w1 | print-student-grades | markdown-cheatsheet | csharp-oop-interface-inheritance | csharp-oop-class-syntax | csharp-exception-object-demo | what-chord-is-this | cy-pathway-readmes | Kernix13 | skills-review-pull-requests | csharp-JsonSerializer-example | csharp-boilerplate-code-snippets | beginner-git-commands | csharp-system-io-classes | mobile-menus | rebuild | learnWP | freelance | kernix13.github.io | basic-fetch-practice | summer-chores | media-queries-practice | responsive-contact-card | correct-the-html-responsive | grid-wireframe-practice | flexbox-wireframe-practice | personal-swot | code-you-resume | Text_File_Creator | website-marketing | word-count-read-time | WP-Docs | custom-admin-footer | kwd-word-filter | tower | lynbrooke | express-pets | pet-adoption | dns-records | node-npm-basics | form-submit | pre-code-formatter | springfield-leaf-pickup | word-count-plugin | online-communication | tmdb-flixx-app | video_player | javascript-cheat-sheet | basic-mysql-statements | markdown-preview | web-dev-job | weather-api-app | web-development-notes | search-and-shortcuts |

Repos needing protection

| repo name                                    | Protect? | Yes ID |
| :------------------------------------------- | :------: | :----: |
| github-readme-seo-analysis                   | **Yes**  |   1    |
| skills-introduction-to-repository-management |   _No_   |   2    |
| tarp-configs                                 |  MAYBE   |   3    |
| tailwind-example                             | **Yes**  |   4    |
| vs-code-tips                                 | **Yes**  |   5    |
| netlify-pets                                 | **Yes**  |   6    |
| the-quote-card-express                       |  MAYBE   |   7    |
| kwd-react-plugin                             | **Yes**  |   8    |
| sass-library                                 | **Yes**  |   9    |
| php-laravel-postnchat                        | **Yes**  |   10   |
| puppeteer-web-scraper                        | **Yes**  |   11   |
| support-desk                                 | **Yes**  |   12   |
| yelp-retreat                                 | **Yes**  |   13   |
| astro-website                                | **Yes**  |   14   |
| web-accessibility-tester                     | **Yes**  |   15   |
| posts-and-chat-app                           | **Yes**  |   16   |
| astro-blog                                   | **Yes**  |   17   |
| astro-blog                                   | **Yes**  |   18   |
| postcss-demo                                 | **Yes**  |   19   |
| webpack-demo                                 | **Yes**  |   20   |
| parcel-sass-setup                            | **Yes**  |   21   |

Yes ID:

1. requirements.txt, dependabot branches, .env, Security & quality vulnerabilities ✅
2. exercise - was setup already I think
3. MAYBE: Security & quality vulnerabilities, Dependabot alerts but no message on main page, 3 personal branches
4. branches, dependabot, Security & quality vulnerabilities
5. package.json, Security & quality vulnerabilities
6. package.json, Security & quality vulnerabilities
7. MAYBE: package.json, .env, Security & quality vulnerabilities
8. package.json, dependabot branches
9. package.json, dependabot branches
10. package.json, dependabot branches
11. package.json, dependabot branches
12. package.json, dependabot branches
13. package.json, dependabot branches
14. package.json, dependabot branches
15. package.json, dependabot branches
16. package.json, dependabot branches
17. package.json, dependabot branches
18. package.json, dependabot branches
19. package.json, dependabot branches
20. package.json, dependabot branches
21. package.json, dependabot branches ✅

### Dependabot PRs are "Active" Pushes

GitHub’s branch protection warning is often "event-driven." When Dependabot identifies a vulnerability in your requirements.txt or package.json, it automatically creates a branch and opens a Pull Request (PR).

1. Grouped Security Updates

Instead of getting 10 separate PRs for 10 different minor vulnerabilities, you can now toggle Grouped Security Updates. This consolidates multiple alerts into a single "batch" PR.

Where to find it: Settings > Code security and analysis > Grouped security updates (Look for the "Grouped" toggle).

Once you turn on branch protection, Dependabot might suddenly seem "broken" because it can't merge its own fixes anymore. When you see a blocked Dependabot PR:

1. Check for "Auto-merge": In the PR itself, look for the "Enable auto-merge" button. If you click that, GitHub will automatically merge it the moment your requirements (like passing a status check) are met.

**Recommended Ruleset Setup**:

For your specific "one-person team" workflow, here is a balanced ruleset configuration to aim for:

- Restrict Deletions: ON (Stops accidental git push origin :main).
- Block Force Pushes: ON (Ensures your history stays linear).
- Require a Pull Request: ON (This is what clears the banner).
- Require Approvals: OFF (Since you are one person, requiring an approval will just lock you out of your own repo unless you have a second account).

> See "_Repo Management_" below for notes from the GitHub exercise

## Creating a GitHub gist

These are not git commands, rather they are a way to have code on GitHub that is not a stand-alone repository. People ceate them because they are chunks of code that other people can use.

To search for a gist on GitHub: `https://gist.github.com/username/` or just `https://gist.github.com/`

**<ins>What is a Gist?</ins>**

They are basically code snippets to save/store and share. Gists do not have Issues, PR's, Projects or Actions. If you have a simple JavaScript function that is not part of a project, then that would be something you could add to its own gist. From Github:

> Every gist is a Git repository, which means that it can be forked and cloned...and you will see it in your list of gists when you navigate to your gist home page. They're also searchable, so you can use them if you would like other people to find and see your work.

Besides being able to fork and clone gists, you can also:

- Leave comments
- Star them
- Download them
- Share them
- Embed them
- Have collaborators
- See revisions and diffs (history)

1. Navigate to your [gist home page](https://gist.github.com/) and click the `+` button - OR -
1. Click the down arrow next to your profile image thumbnail > click _New Gist_
1. Type a description and file name with extension for your gist (you want the extension for code highlighting).
1. Optionally, you can change the Indent Mode, Indent Size, and if you want it to Wrap or not.
1. Type or copy the code/text of your gist into the gist text box
1. When done Click either `Create secret gist` or `Create public gist`

**NOTE**: For the gist filename just make something up. For example, if you have a JavaScript function that takes a blog post title and converts it to a URL string, then give it a name like `BlogTitleUrl.js`.

Then you can get the Share link for the gist to share with people or to add to an online article. When you choose `Embed` and add the link to an HTML page it will output as a formatted code block (not for all sites though).

You can add code blocks or other files for your gist by clicking _Add file_.

**Public gists** can be found on the Discover page. Just click _All gists_ from the menu bar and they are listed in reverse chronologial order of creation date. You can also search for gists by keywords, add comments on gists you found, and have comments on your gists.

**NOTE**: You can create a gist if you are not signed into GitHub but it will be an anonymous gist which you will not be able to edit or delete. I don't know why you would want to do that but you can if you want to.

<!-- <div align="right"><a href="#back-to-top" title="Table of Contents">Back to Top</a></div> -->

### Clone or fork a gist

Your options from the dropdown list after creating your gist are to _Embed_, _Share_ or _Clone_ the gist. If you want to clone the gist then in your terminal do:

```shell
git clone gist_url
```

If you choose to _fork_ someone else's gist then it will show on your gist home page similar to how forked repos will show in your repositories.

### Editing a gist

Just click the Edit button while in your gist and edit the code as you see fit. There is also a delete button next to edit if you want to delete your gist.

When done editing click the _Update public gist_ button. Click the _Revisions_ link to see your changes. Remember that your gists are also repositories. You can go pulls and pushes.

## GitHub pages

Use [GitHub Pages](https://pages.github.com/) to host your portfolio or a live version of your app(s). Other options would be to use Netlify or Vercel. Portfolios, personal websites, projects, documentation all are good reasons to use these

Links:

- **NOTE**: https://pages.github.com/ redirects to [GitHub Pages documentation](https://docs.github.com/en/pages)
- [Quickstart for GitHub Pages](https://docs.github.com/en/pages/quickstart)
- [Creating a GitHub Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)

There are 2 types:

1. User sites, and
2. Project sites

> Because https://pages.github.com/ redirects to a new page, I'm not sure if ths is true anymore, or the page describing both is unavailable at this time?!?

- Project sites: for every repo you can have a corresponding website
  - URL pattern: `username.github.io/repo-name` – one per project
- User site: `username.github.io` – you can only have 1 per GitHub account
- You can have a website or just markdown files like docs
- To setup a website go into one of your repos > select a branch (`main`/`master` but it could be any branch)
  - It would be good to have a branch solely for the GitHub page and the main branch is for your code and docs
- You need to tell GitHub that the branch contains a website, specificall an `index.html` file
- Then go to the Repo _Settings_ tab > in the left sidebar look for _Pages_ under _Code and automation_ > go the the _Branch_ subheading where it says:

> "GitHub Pages is currently disabled. Select a source below to enable GitHub Pages for this repository"

- Then select the branch you want
- The old convention was to name the branch `gh-pages` so use that and keep main for your `project/portfolio` – but you can name the branch anything
- Make sure your `index.html` file is either in the root or a `/docs` folder – tell GitHub where it is
- Any time you update the `gh-pages` branch (or whatever page you chose) your website will update

> Open a browser and go to https://username.github.io

## Repo Management

> [!NOTE]
> The [skills-introduction-to-repository-management](https://github.com/Kernix13/skills-introduction-to-repository-management) lesson from GitHub is excellent to learn how to protect your repo and other tips!

Notes:

1. **Rulesets**: Settings tab: Rules > Rulesets > Click the New ruleset dropdown and select New branch ruleset

- Set the Ruleset Name as Protect main and change the Enforcement status to Active
- Find the Targets section and use the Add target dropdown to add 2 entries
  - Add the _Include default branch_ option to ensure protections aren't bypassed by switching the default branch
  - Use the _include by pattern_ option and enter the pattern main
- Find the Rules section and ensure the following items are checked
  - Restrict deletions
  - Require a pull request before merging -> Required approvals: 0 & Require review from Code Owners
  - Block force pushes
- Scroll to the bottom and click the Create button to save the ruleset

2. CONTRIBUTING.md and CODEOWNERS files
3. Add your first collaborator: requires another person with a GitHub account to participate

- Settings tab > select Collaborators > Manage access > click the Add people button
- Enter a friend/colleague's GitHub username or email then press the Add to repository button
- NOTE: Personal repositories only have one collaboration role type. A "collaborator" receives write permissions but NOT admin permissions. If you need finer permissions, consider starting a free organization and assigning repository roles.

4. Code of Conduct - This document sets expectations for how community members should interact. Think of it like the Student Handbook at Mergington High - it outlines respectful behavior, how to report non-technical problems, and consequences for violations.

- The [Contributor Covenant](https://www.contributor-covenant.org/) is a popular code of conduct used by many projects
- Settings tab > verify Issues is enabled > Set up templates button to enter the issue templates editor > Click the Add template dropdown and select Bug report > Click the Preview and edit button to show the current template. Click the Edit icon (pencil) to make the fields editable

5. Issue Templates - These provide structure when someone reports a problem or suggests a new feature. They can help the community effectively communicate their needs for new features and provide enough information to solve bugs. You might consider trying the public preview for [issue forms](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms), which provide a friendlier user experience when creating issues

> working in parallel on 2 branches now: That's exactly what working with multiple collaborators is like

6. **Dependabot** - Track and create alerts for vulnerabilities found in upstream dependencies used in your project. Automatically create pull requests to upgrade dependencies to safe versions.

- check out the [Secure Repository Supply Chain](https://github.com/skills/secure-repository-supply-chain) Skills exercise
- Settings tab > Advanced Security > Dependabot section > Verify or change the settings to match the following
  - Dependabot alerts: enabled
  - Dependabot security updates: enabled
  - Grouped security updates: enabled
- Find Dependabot version updates and click the Enable button - This will open an editor to create a configuration file
  - In the left files list, at the top, click the Expand file tree button to show the list of files
  - Set the package-ecosytem to pip or npm or whatever you need to so Dependabot will automatically monitor your requirements/packages

7. Code Scanning - Analyze your repository's code to find security vulnerabilities and coding errors. Use GitHub Copilot Autofix to automatically suggest fixes for these alerts.

- Check out the [Introduction to CodeQL Skills](https://github.com/skills/introduction-to-codeql) exercise
- select the Settings tab > Advanced Security > Code scanning section > Click the Set up button and select the Default option to open a configuration panel > Click the Enable CodeQL button to accept the default configuration > Below the Tools section. Verify Copilot Autofix is set to On

8. Security Policy and Private vulnerability reporting - Provide a guide and simple form for security researchers and end users to responsibly report vulnerabilities directly to the repository maintainer. This prevents sensitive issues from being publicly disclosed before they're fixed.

- Settings tab > Advanced Security > Private vulnerability reporting setting and verify it is enabled
- At the top navigation, click the Security tab > In the left navigation, click the Policy option > Click the Start setup button. An editor will be started to create the file SECURITY.md > click the Expand file tree button to show the list of files > change the branch to prepare-to-collaborate
- Tip If you switch to a branch that does not contain the same file, the editor will become empty. Press the Restore button to retrieve the previous editor's content

Here are some useful references from the GitHub Docs:

- [Template gitignore files](https://github.com/github/gitignore)
- [Creating rulesets for a repository](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/creating-rulesets-for-a-repository#using-fnmatch-syntax)
- [Managing a branch protection rule](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/managing-a-branch-protection-rule)
- [About code owners](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)
- [Setting guidelines for contributors](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/setting-guidelines-for-repository-contributors)
- [Add a code of conduct](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/adding-a-code-of-conduct-to-your-project)
- [Configuring default setup for code scanning](https://docs.github.com/en/code-security/code-scanning/enabling-code-scanning/configuring-default-setup-for-code-scanning)
- [Adding a security policy](https://docs.github.com/en/code-security/getting-started/adding-a-security-policy-to-your-repository)

## Pull Request Reviews

> [!NOTE]
> The [review-pull-requests](https://github.com/skills/review-pull-requests) lesson from GitHub is interesting. If you complete, check the Issues tab and click on the one closed issues for some really good notes about reviewing PRs.

```
The "24-Hour Rule" for npm

If you want that same safeguard on your current npm projects, you can actually add it to your .npmrc file right now. As of npm CLI 11.10.0 (released in February 2026), you can set a "cooldown" just like pnpm.

- How to do it: Add min-release-age=1 to your .npmrc.
- What it does: It tells npm: "If a package version was published less than 24 hours ago, do not install it."
```
