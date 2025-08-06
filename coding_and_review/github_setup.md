# GitHub Project, Repositories, and Rules Setup

- Other general and additional information can be found in [GitHub Best Practices](./github_best_practices.md)

## Starting a GitHub project

There are three possible ways to start your project:

1) Create a draft Issue in [BiCU Projects Overview](https://github.com/orgs/BiCU-CCRI/projects/2/), create a Repository, convert the draft Issue into an Issue `Convert to issue`, and assign it to the Repository.
2) Create a [Project](https://github.com/orgs/BiCU-CCRI/projects) first, then create a Repository, and link the Project there.
3) Create a [Repository](https://github.com/orgs/BiCU-CCRI/repositories) first, then create a Project in the Repository Projects tab.

We recommend using option 1. This is the most efficient way to record the incoming request/task, gather all the information, distribute the work, and start working on the request.

### Project Tracking

In BiCU, we use [BiCU Projects Overview](https://github.com/orgs/BiCU-CCRI/projects/2/) for general project tracking. This Project is used to *track* individual projects, requests, analyses, or tasks. It is not meant for the code development itself. Code development is tracked in individual Repository Projects.

Unfortunately, GitHub Projects works best with an existing project repository. Either create the project repository first, or, if you must, make a temporary dummy/draft repository to use the full features and temporarily use that.

When you start working on a new project/request, please follow these instructions:

1) Make a [project Repository](#setting-up-a-github-repository). For example, `POP drug screening`. Note: You can always rename it later, but try to use some reasonable and explicit name from the get-go.
2) Make a [new Project](#github-project) in the Repository
3) Go to the [BiCU Projects Overview](https://github.com/orgs/BiCU-CCRI/projects/2)
4) Under `Backlog`, start typing to create the tracking task and `Create a draft`. This could have, but doesn't have to, the same name as the project repository (e.g., `POP drug screening`)
5) Open the `Draft` and click `Convert to issue`, and assign it to the project repository.
6) Under `Projects`, assign it to the `BICU Projects Overview` if it's not assigned already. You can also assign it to the Repository Project if you want to track it there as well, but it's not necessary since it will already be there as an `Issue`.

**Steps 7-8 are only for large, continuous, long-term projects with expected subanalyses (for example, continuous patient diagnostics analyses). For *one-time* projects, don't create the `Epic` ticket but select `Task` for the main ticket directly = ~skip steps 7-9 and continue from step 10**

7) Under `Type`, select `Epic`. This will make it obvious that this is the general tracking task. This creates one common tracking task for the whole `POP drug screening` project, which stays around as long as the main project is active
8) Edit the description field and add:

```bash
[ ] POP drug screening - AML sample 1
[ ] POP drug screening - MDS sample 1
```

9) Click on the three small dots next to the created `- [ ]` lines and `Covert to sub-issue`
10) Open the issues one by one and assign them to the `BiCU Projects Overview`. Tag them with `Task`. This creates tracking issues for individual analyses. Again, you can, but don't have to, assign it to the Repository Project as well (it should be there as an Issue already).
11) Fill out the dates, the sizes, priorities, assign it to a group, etc.
12) Update the [status](#github-project-ticket-status) as you go.

Summary: Projects go to `BiCU Projects Overview` and repository Projects - `Epic` issue for the whole project (long-term projects with additional analyses), `Task` for individual analyses that are sub-issues of the `Epic`. One-time projects don't have `Epic` but are directly tagged with `Task`. Individual code development is done only at the project repository level with `Feature`, `Subtask`, or `Bug` types.

### Setting up a GitHub repository

To set up a repository:

1) Go to [BiCU GitHub page](https://github.com/orgs/BiCU-CCRI/repositories)
2) Click `New repository`
3) Give the repository a **reasonable name** (try to be as explicit as possible). Note: You can also use a specific prefix to help you with tracking your projects. F, `jo001`, `ab16`, ... If you have multiple open projects, it might be easier to remember the simple prefix than the full name.
4) Choose visibility: `Private`
5) Start with a template: `No template`. TODO: Create BiCU repository template
6) Add README: `On`
7) Add .gitignore: `No .gitignore`
8) Add license: `MIT License`. Note: MIT License is recommended but you can choose your own.
9) Click `Create repository`

It is strongly recommended to follow GitHub repository rules described in [GitHub branches, commits, and push rules](#github-branches-commits-and-push-rules).

#### GitHub branches, commits, and push rules

In order to make the development more efficient and safe, we have to establish certain GitHub rules. These will make sure our code is safe and properly reviewed and that we follow the agreed CR practices.

We follow these rules and settings when creating a new GitHub repository:

1) **Protect the `main` branch**\
Changes to the `main` branch must be handled only through a **reviewed** PR merge. This prevents random, non-unreviewed code in the `main` branch and helps to keep the commit history clean.
2) **PR to the `main` branch has to be reviewed** (and approved) by **another person** before merging\
The PR merge needs to undergo the full CR process and, ultimately, be approved by at least one more person. Only then can it be merged into the `main` (or parent) branch
3) **All threads need to be resolved** by the reviewer before the merge\
The reviewer needs to resolve all the CR comments and suggestions before the merge is allowed. The developer **must not resolve** the comments themselves. If the original reviewer is not available anymore, the developer must request an additional reviewer. Note: GitHub suggestions are resolved automatically if accepted as suggested by the reviewer.
4) **Not implemented** ~~**Branch names and commit messages** need to follow **specific structure**~~\
Branch names and commit messages must have a specific structure. This makes it easier to standardize and read the Git history.
5) **Squashing commits before the merge** is strongly encouraged\
Branch commits should be squashed before the merge. This keeps the `main` (or the parent) branch history nice and tidy (=one commit per merge) while keeping the full history in the original branch. Note: This assumes we do not delete the *original merged* branch.
6) **The final merge has to be done by the author**\
Once the whole CR process is over, the author has to do the final PR merge.
7) **Rebase your local branches when necessary** to the latest changes\
In case multiple people contribute to the same code, make sure you rebase your local branches to the latest PR changes if the other person merges their code first. Talk to each other and decide who merges first and who rebases, or if the other person should wait before starting a new branch.

Recommendation: Create a Pull request as soon as possible, even if the development is not complete. You can use
 `Still in progress? Convert to draft` option in GitHub Pull request and/or prefix the *draft* PR title with `Draft:`
 to keep track of your open PRs. You can view the open PRs by clicking the Pull request icon on the top right (next to your profile icon).

Recommendation: You can put a checklist in the PR message body to track your TODO list. This also makes it easier to summarize the *implementations* included in the PR before the merge.

##### Branch rulesets

Branch rulesets allow us to enforce specific *rules* for branch names, commit message structures, and the type of commits
 themselves and, for example, protect the code from accidental non-unreviewed changes.

Branch rulesets are applicable to all branches; however, the most important are the
 `main` branch rules, which should be as strict as possible to protect the final code.

More information about individual [rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets), and [GitHub branch protection rules](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule) or [settings](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#about-branch-protection-settings).

##### `main` branch protection rules

We use the following rules to protect the `main` branch:
    - Deleting the branch is disallowed (from git)
    - All the commits must be done through a Pull request (=no direct `git push`)
    - `git push -f` is not allowed
    - Merges are allowed only after an approved and reviewed PR
    - The PR has to be approved by at least one reviewer
        - If the requested reviewer isn't available, it has to be approved by somebody else, but not any of the PR contributors (except when contributing through GitHub PR suggestions)
    - Require review by at least 1 person other than the author
    - The reviewer cannot be a person who contributed code to the PR (except when contributing through GitHub PR suggestions)
    - All reviewers' comments must be resolved before the merge
    - The branch commits are squashed before the merge (squashing *merges* all commits in the branch to one commit to `main`, making the history linear)

Why not push directly to the `main` branch?
    - Prevents non-reviewed, potentially breaking changes​
    - The `main` branch is functional until the changes are merged
    - Makes the `main` commit history clean​
        - Fewer commits from (squashed) PR branches while keeping the original commit history in the source PR branch (assuming you do not delete the *source* branch)​
    - Easier backtracking of where the changes happened​
    - Easier backtracking of the previous code​
    - Easier backtracking for task description (GitHub Project tickets)
    - Two (or more) people can work on the same code at the same time​ and submit PRs

We protect the `main` branch to ensure we follow the agreed best coding practices and CR.

###### `main` branch rules setup

To set the rules to protect the `main` branch:

1) Go to GitHub Repository
2) Click on `Settings` on the top panel (below the Repository name)
3) Click on `Branches` on the left (under `Code and automation`)
4) Click on `Add classic branch protection rule`
5) Branch name pattern: `main` or `main*` (or `master` if you haven't switched yet to the ["new" naming](https://github.com/github/renaming))
6) `Require a pull request before merging`: **check**

**Only for shared reviewed repositories. For other repositories continue from step 12):**

7) `Require approvals`: **check**
8) `Required number of approvals before merging`: `1`
9) `Dismiss stale pull request approvals when new commits are pushed`: **check**
10) `Require approval of the most recent reviewable push`: **check**
11) Require conversation resolution before merging: **check**

**For all the repositories:**

12) `Require linear history`: **check** (requires either `squash before merging` or `rebase before merging` but the requirement of `squash before merging` cannot be directly enforced)
13) `Do not allow bypassing the above settings`: **check**
14) (**optional**) `Restrict who can push to matching branches`: **check** and specify the people allowed to push and merge to the repository
15) Click `Create`

##### General branch protection rules

The full branch protection ruleset settings allowing more fine-tuned restrictions can be accessed by:

`Repository -> Settings -> Rules -> Rulesets -> New ruleset -> New branch ruleset`

- `Ruleset Name`: `Branch protection`
- `Enforcement status`: `Active`
- `Bypass list`: keep `Bypass list is empty`
- `Target branches -> Add target`: `Include all branches` (or you can select specific branches you want to protect, including `main`/default branch)
- Rules:
    - (**optional**) `Restrict deletions`: **check** (recommended to prevent accidental branch deletions directly from `git`)
    - `Require linear history`: **check**
    - `Require a pull request before merging`: **check**
        - **Only for shared reviewed repositories:**
            - `Required approvals`: `1`
            - `Dismiss stale pull request approvals when new commits are pushed`: **check**
            - `Require approval of the most recent reviewable push`: **check**
            - `Require conversation resolution before merging`: **check**
        - (optional; not tested) `Automatically request Copilot code review`: **check**
        - (optional but recommended) `Allowed merge methods` - `Squash`
    - (not implemented; applicable if [GitHub Actions](#github-actions) are set up) `Require status checks to pass`: **check**
    - **Only for main/default branch:**
        - `Block force pushes`: **check**
    - **Only with Enterprise license:**
        - `Restrictions`:
            - `Restrict commit metadata`: **check**
                - Must match a given regex pattern and paste commit message regex from [GitHub Best Practices - Commit Message Structure](./github_best_practices.md#commit-message-structure) `^#\d+ [A-Z][a-zA-Z0-9\s]*$` (as of 05.03.2025)
            - `Restrict branch names`: **check**
                - Must match a given regex pattern and paste commit message regex from [GitHub Best Practices - Branch Name Structure](./github_best_practices.md#branch-name-structure) `^#\d+ [A-Z][a-zA-Z0-9\s]*$` (as of 05.03.2025)
    - `Create`

If we had an **Enterprise license**, we could set additional restrictions to enforce, for example, branch naming, ~~PR title~~ (not supported by GitHub as of Q1 2025), commit message structure to follow regex patterns, ...:
    - GitHub would then reject commits/branch names that don't follow the pattern
    - For example, if you don't follow the predefined commit message structure, the `git commit` gets rejected. You we can correct the message with `git commit --amend -m '...'` and push again with `git push --force`
    - Setting the rules helps with consistency across the developers and simplifies project and code sharing

### GitHub Project Ticket status

We use the following columns in GitHub Project:
    - **Backlog**: The task was created but isn't complete or the work hasn't started yet
    - **In Progress**: The task is being actively worked on
    - **On Hold**: The task cannot be worked on atm or had to be paused.
    - **In Review**: The task/code is being reviewed (either by another developer or the person who requested the task)
    - **Done**: The task is finished

Please, move the tickets from one column to another as you progress even if it just a formality. Each change is recorded and it is generally a good practice to follow the status *flow*. In code development, it is common to predefine mandatory *status change diagram* which limits the possible ticket status changes and getting this habit will help you in environments where this is implemented.

### GitHub Project

#### New project

These are the steps to start a new Project:

1) Collect information about the project. Temporarily, you can keep the notes at your personal notes organizer (OneNote, Obsidian, personal GitHub, Word, ...)
2) Open the project tab in your Repository or go to BiCU GitHub project page [https://github.com/orgs/BiCU-CCRI/projects](https://github.com/orgs/BiCU-CCRI/projects)
3) Click on `New project`
4) Select `BiCU Project Template` at the bottom
5) Give the Project a name. It is recommended to use the same project name as the name of the Repository.
6) Give your project a reasonable name (if possible, keep it the same as the GitHub repository if it already exists)
7) Click on Add status update on top right and add a brief Project description.
8) You can add links to the locally stored data and other important locally stored information to the README part. Don't go too crazy.
9) Add the tickets/tasks
10) Make a GitHub repository. Try to keep the GitHub repository name in lowercase. If it's a common pipeline/workflow, use `_pipeline` suffix. Copy GitHub project link to the Description. **TODO**: Make a template for GitHub repositories:
11) common code/pipelines (more strict, reviews, etc)
12) personal projects (less strict but structured)
13) On top of the repository, click on Projects and on the right click on Link a project->Select the project you created in 3) and click Submit

Note: You can also do it the other way around - make GitHub repository first and then click on Projects-> +New project

#### Add issues

- Go to the project page and select `+ Add item` at the bottom at the Backlog column.

- Use #reponame and and `(+) Create new issue`

- This create new project task and repository issue
- After you complete the task description, check `Create more` to make more issues
- Tasks in the project automatically open Issues in the repository
- Closing issue in the repository closes the task in the project

#### Add subtasks

- **Update:** GitHub can now create [issues and sub-issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/adding-sub-issues) automatically
- GitHub can automatically create a subtask if you use `- [ ]` list in the Issue description.
- When you are done with the description, you can click on the three dots next to the `- [ ]` list, and select `Convert to issue`.
    - This creates a new issue and replaces the current *text* with the new issue hashtag
- Other option is to specify which issue a) is a `feature` (prefix issue name with `feature-`) and list the associated subtasks as `- [ ]` list and b) which one is a `subtask` (prefix issue name with `subtask-`) and put `subtask of #parent-feature-issue-name` at the end of the description
- For technical tickets without a *feature*, use `janitor-`
- For technical tickets that need immediate fix, we use the `bugfix-` prefix
- For experiments and run analysis that are not supposed to go into the `main` branch, please use `experiment-`

##### TODO

- [ ] Check Settings -> General -> (go down) Pull Requests -> see if we can disallow "Allow merge commits" and "Allow rebase merging"
    - The goal is to "enforce" `squash before merging`
    - <https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests>

## GitHub Actions

[GitHub Actions](https://github.com/features/actions) allow us to automatically run a specific set of commands after each GitHub event (often at `push`). These commands run on the GitHub side and are paid.

We can, for example, run tests, code formatting, code linting, and even automatic PR suggestions (for example, [CODEX CLI](https://github.com/openai/codex?tab=readme-ov-file#non-interactive--ci-mode), a similar product from [GitHub Copilot Code Review](https://docs.github.com/en/copilot/how-tos/agents/copilot-code-review/configuring-automatic-code-review-by-copilot), and a custom GitHub Actions [here](https://gist.github.com/bradenkeith/e25914ba3150d7bb575f7ccc7eb24767) for catching errors, typos, and getting automatic recommendations).

Example of GitHub Actions:

- Python: <https://github.com/actions/setup-python>
- Shell: <https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/add-scripts>
- R: <https://github.com/r-lib/actions/>

A nice summary is available [here](https://codex.so/github-actions-intro-en), for example.
