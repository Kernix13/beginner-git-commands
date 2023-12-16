# Issues, Labels, and Branch Strategies

Anchor Links: [Issues](#issues) | [Branch Strategies](#branch-strategies) |

- A `Git strategy` might be around cloning, branching, and merging
- A `GitHub strategy` would be around Issues, Actions, and PRs (and how they relate to clones, branches, and merges)

## Labels

1. [GitHub Labels article](https://seantrane.com/posts/logical-colorful-github-labels-18230/):

- GitHub Labels are used for both Issues and Pull Requests
- the default state should be label-less
- should only provide important context; priority, effort and the state of solution and/or decision-making
- Labels and their associated colors should have a logical connection that is intuitive at-a-glance
- Labels should be lowercase
- Prefixes: `priority`, `state` (approved, blocked, inactive, pending), `type` (bug, chore, discussion, docs, feature, fix, security, testing)
- labels without prefixes: breaking, good first issue, greenkeeper, help and semantic-release

2. [Stackoverflow label post](https://stackoverflow.com/questions/26944762/when-to-use-chore-as-type-of-commit-message):

- `feat`: Short for "feature," used when introducing a new feature or functionality to the codebase, e.g.: `feat: Add user authentication feature`
- `chore`: used for commits related to maintenance tasks, build processes, or other non-user-facing changes. It typically includes tasks that don't directly impact the functionality but are necessary for the project's development and maintenance, e.g.: `chore: Refactor build script`
- `docs`: Used when making changes to documentation, including comments in the code, README files, or any other documentation associated with the project, e.g.: `docs: Update API documentation`
- `style`: This prefix is used for code style changes, such as formatting, indentation, and whitespace adjustments. It's important to separate style changes from functional changes for better clarity
- **`refactor`**: Used when making changes to the codebase that do not introduce new features or fix issues but involve restructuring or optimizing existing code, e.g.: `refactor: Reorganize folder structure`
- `test`: Used when adding or modifying tests for the codebase, including unit tests, integration tests, and other forms of testing
- `perf`: Short for "performance," this prefix is used when making changes aimed at improving the performance of the codebase, e.g.: `perf: Optimize database queries for faster response times`

2. [FCC Labels](https://github.com/freeCodeCamp/freeCodeCamp/labels):

- 2 pages, I like: scope: a11y, scope: docs, scope: ui, status: discussing, status: merge conflict, status: PR in works, status: waiting review, status: waiting update, type: bug, type: feature request

## Issues

1. [GitHub Issues Best Practices](https://rewind.com/blog/best-practices-for-using-github-issues/), Really good:

- 1st screenshot is good, In most cases, GitHub Issues is used for reporting bugs and requesting features, also - hosts discussions, helps process support requests, or even submit documentation feedback - consider following basic issue tracker maintenance practices
- `Best Practice 1`: If You’re Just Starting, Go With the Defaults - This could be a good idea in the early stages of your project when you’re still getting a feel for your users and the problems they face
- `Best Practice 2`: Encourage Search to Avoid Duplication - ...before submitting new issues, use contributing guidelines for that - Simply create a document called CONTRIBUTING.md in the root of your repository, use it to describe your preferred issue reporting workflow, and make sure to emphasize the importance of searching for existing issues before submitting anything new. Feel free to draw inspiration from guidelines in existing repositories ( See below 1 )
- `Best Practice 3`: Add Structure to Issue Reporting and Encourage Reporters to Be Specific - There’s one way to submit a feature request. There’s a different way to submit a bug. Discussions and support requests may or may not be welcome in your issue tracker
- As your repository receives more issue reports, you need to define exactly what kind of issues you’re ready to accept and what kind of information you want them to contain. To help you with this, GitHub Issues provides issue templates
- To start off, use GitHub’s [template builder](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository) to set up standard templates for bug and feature reporting
- After configuring the basic templates, try clicking New Issue. Instead of a regular issue form, you’ll land at the template chooser—a view that requires you to choose a specific type of issue
- You can now customize GitHub’s default issue templates and add more templates to match your team’s preferences. To do this, use the template builder described above or edit template files manually. Issue template files are YAML files that are stored in your repository in the .github/ISSUE_TEMPLATE folder
- For inspiration, check out issue templates used in popular repositories, such as tensorflow, angular, or freeCodeCamp.
- `Best Practice 4`: Route Vulnerability Reports Elsewhere - the common practice is to provide a separate reporting path for responsible disclosure, where the vulnerability is reported privately to the vendor and is not disclosed publicly until the vendor has prepared a patch
- `Best Practice 5`: Use (But Don’t Overuse) Labels - Labels are a great way to categorize issues and slice your team’s work into manageable pieces. Since you can apply multiple labels to any given issue, labels are a highly flexible tool that can solve various problems
  - Break the project down by areas of responsibility. Depending on the architecture of your application, you may want to use labels for individual components or subsystems
  - Mark non-triaged issues: ???
  - Isolate issues that await additional information from the reporter. If an issue lacks details necessary to make it actionable, you can request the details from the reporter and set a special label, such as needs more info
  - Create a pool of issues that are open for external contributions. Labels like good first issue and help wanted are normally used for this purpose
- GitHub default labels: you can make changes like use prefixes to reflect the kind of property that a label expresses like `type: bug`. Use consistent colors across all labels of a particular kind
- `Best Practice 6`: Mention the Appropriate People - Mention other people if you want to use their expertise, have them provide an estimate, or just be aware of an issue. When you add mentions, consider the following:
  - Since every mention results in an email notification to the person you’re mentioning, try to mention sparingly
  - When mentioning a user who was previously not involved in an issue, try to make it clear if there’s an action you want them to take or if you’re just making them aware of what’s going on
- `Best Practice 7`: Choose a Workflow to Assign Issues to Developers - Assigning issues to specific developers is a great practice
- `Best Practice 8`: Don’t Forget to Close Issues - there’s a special syntax, `Closes #issue_number`, to auto-close issues from pull request descriptions and commit messages. When you use this syntax, once the commit is pushed (or PR is merged) into the main branch, GitHub automatically closes the referenced issue(s) - I think `resolves` does the same as `closes`
- `Best Practice 9`: Backing up GitHub Issues - back up the code and the Issues & other metadata - there are some free simple like `BackHub (now part of Rewind)`

## Branch Strategies

### 1. [AB Tasty: Git Branching Strategies](https://www.abtasty.com/blog/git-branching-strategies/)

- Branches are primarily used as a means for teams to develop features giving them a separate workspace for their code. These branches are usually merged back to a master branch upon completion of work
- A `branching strategy` is the strategy that software development teams adopt when writing, merging and deploying code when using a version control system
- It is essentially a set of rules that developers can follow to stipulate how they interact with a shared codebase
- adhering to a branching strategy...so that developers can work together without stepping on each other’s toes
- it enables teams to work in parallel to achieve faster releases and fewer conflicts by creating a clear process when making changes to source control
- When we talk about branches, we are referring to independent lines of code that branch off the master branch, allowing developers to work independently before merging their changes back to the code base
- branching strategies that teams use in order to organize their workflow... pros and cons...
- having a branching strategy is necessary to avoid conflicts when merging and to allow for the easier integration of changes into the master trunk

#### Strategy #1 GitFlow

- Considered to be a bit complicated and advanced for many of today’s projects - SKIP

#### Strategy #2: GitHub Flow

- this model doesn’t have release branches. You start off with the main branch then developers create branches, feature branches that stem directly from the master, to isolate their work which are then merged back into main. The feature branch is then deleted.
- The main idea behind this model is keeping the master code in a constant deployable state and hence can support continuous integration and continuous delivery processes.
- Github Flow focuses on Agile principles and so it is a fast and streamlined branching strategy with short production cycles and frequent releases
- allows for fast feedback loops so that teams can quickly identify issues and resolve them
- Since there is no `development` branch as you are testing and automating changes to one branch which allows for quick and continuous deployment
- This strategy is particularly suited for small teams and web applications and it is ideal when you need to maintain a single production version
- Thus, this strategy is not suitable for handling multiple versions of the code
- the lack of development branches makes this strategy more susceptible to bugs and so can lead to an unstable production code if branches are not properly tested before merging with the master
- The master branch, as a result, can become cluttered more easily as it serves as both a production and development branch

#### Strategy #3 GitLab Flow

- a simpler alternative to GitFlow that combines feature-driven development and feature branching with issue tracking
- developers create a develop branch and make that the default while GitLab Flow works with the main branch right away
- is great when you want to maintain multiple environments and when you prefer to have a staging environment separate from the production environment
- whenever the main branch is ready to be deployed, you can merge back into the production branch and release it
- this strategy offers propers isolation between environments allowing developers to maintain several versions of software in different environments
- this method is suited for situations where you don’t control the timing of the release, such as an iOS app that needs to go through the App store validation first or when you have specific deployment windows

#### Strategy #4 Trunk-based development

- a branching strategy that in fact requires no branches but instead, developers integrate their changes into a shared trunk at least once a day. This shared trunk should be ready for release anytime
- ... make smaller changes more frequently... developers commit directly into the trunk without the use of branches
- trunk-based development is a key enabler of continuous integration (CI) and continuous delivery (CD) since changes are done more frequently to the trunk
- This strategy is often combined with feature flags. As the trunk is always kept ready for release, feature flags help decouple deployment from release so any changes that are not ready can be wrapped in a feature flag and kept hidden while features that are complete can be released to end-users without delay

> I want to use _GitHub Flow_ - When first starting out, it’s best to keep things simple and so initially `GitHub Flow` or `Trunk-based development`

### 2. [Tilburg Science Hub: Git Branching Strategies](https://tilburgsciencehub.com/building-blocks/collaborate-and-share-your-work/use-github/git-branching-strategies/)

- A Git branching strategy allows developers to collaborate on a project while also tracking changes and maintaining multiple versions of the codebase
- This article lists the same strategies as above with the exception of GitLab Flow

#### Strategy 1: Trunk-Based Development

- A branching strategy in which all developers make changes directly on the main branch, commonly referred to as the trunk, which holds the project’s deployable code
- Developers are encouraged to commit frequently and use feature toggles`*` and other techniques to manage changes that are not yet ready for release
- Testing is typically automated, with a focus on continuous integration (CI) and continuous delivery (CD) to ensure that code changes are thoroughly tested before they are deployed
- **Feature toggles**, also known as _feature flags_, can be used in software development to manage features that are not yet ready for release or that need to be shown only to specific users or groups

#### Strategy 2: Feature Branching

- a commonly used workflow that involves creating a new branch for a specific feature or change in the codebase
- This allows developers to work on the feature independently without affecting the `main` branch. When the feature is complete, it can be merged back into the `main` branch through a pull request

Feature Branching Workflow:

1. Create a new branch for each feature or task you’re working on
2. start implementing the new feature by making as many commits as necessary. The branch should only contain changes relating to that particular feature
3. When you’re finished working on the feature branch, you create a pull request to merge the changes into the main branch
4. Other developers review the changes in the pull request and approve them if they are satisfied with the changes. Code review can help catch issues or mistakes before they are merged into the `main` branch
5. Once you’re done working on the feature, you can merge the feature branch back into the `main` branch
6. After merging, you can delete the feature branch, as it is no longer needed

> This strategy can lead to conflicts due to branch dependencies - is this an alternate name for _GitHub Flow_?

#### Strategy 3: Git Flow

- Git Flow is a branching strategy that uses two main long-lived branches - `main` and `develop`
- several short-lived branches (feature, release, hotfix) are created as needed to manage the development process and deleted once they have fulfilled their purpose
- The `main` branch is the stable production-ready code and the `develop` branch is where all development takes place.
  - `feature` branches are used to develop new features or changes,
  - `release` branches are used to prepare for a new release, and
  - `hotfix` branches are used to quickly address critical issues in the production code
