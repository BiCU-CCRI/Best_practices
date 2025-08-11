# GitHub Project, Repositories, and Rules Setup

This document summarizes BiCU tasks and projects tracking setup. Following these guidelines will simplify tracking of our tasks and allow to easily report our achievements.

In BiCU, we use [`BiCU Projects Overview`](https://github.com/orgs/BiCU-CCRI/projects/2/) for general project tracking. This Project *tracks* individual projects, requests, analyses, and tasks. It is not meant to track the code development itself. Code development is tracked in individual Repository Projects.

Using GitHub projects allows for a simple export of all the work and described [here](https://docs.github.com/en/issues/planning-and-tracking-with-projects/managing-your-project/exporting-your-projects-data).

**Note:** Other general and additional information can be found in [GitHub Best Practices](./github_best_practices.md).

## Starting a GitHub project

There are three possible ways to start your project:

1. Create a draft Issue (=Project *tracking* Issue) in [`BiCU Projects Overview`](https://github.com/orgs/BiCU-CCRI/projects/2/), create a Repository, convert the draft Issue into an Issue `Convert to issue`, and assign it to the Repository. Then create a Project in the Repository Project tab.
2. Create a [Repository](https://github.com/orgs/BiCU-CCRI/repositories) first, then a *tracking* Issue and link it to the [`BiCU Projects Overview`], and create a Project in the Repository Projects tab.
3. Create a [Project](https://github.com/orgs/BiCU-CCRI/projects) first, then create a Repository, and link the Project there. Then create the *tracking* issue in the Repository Issues tab and link it to the `BiCU Projects Overview`.

We recommend using option 1. This is the most efficient way to record the incoming request/task, gather all the information, distribute the work, and start working on the request.

## Project Tracking

Unfortunately, GitHub Projects works best with an existing project repository. If you must, make a temporary dummy/draft repository to use the full features and temporarily use that.

We introduce a *tracking* Issue types (this is differnt from the code development [Issue Types](./github_best_practices.md#issue-types)):

- `Epic`: A high-level tracking issue for a broader initiative or project. It typically encompasses multiple `Tasks` and serves as an organizational *container* rather than a unit of work. We do not work directly on `Epics`; instead, they help us group related efforts and track overall progress. `Epics` are long-lived and may span multiple reporting cycles.
- `Task`: A concrete, actionable unit of work—such as an analysis, implementation, or request. Each `Task` should be estimable in terms of priority, effort, and duration, and ideally completable within a reasonable timeframe. `Tasks` are the basis for planning, execution, and reporting to management. They should be clearly scoped and outcome-oriented.

When you start working on a new project/request, please follow these instructions:

**Note**: Steps 8-10 are only for large, continuous, long-term projects with expected subanalyses (for example, continuous patient diagnostics analyses). For *one-time* projects, don't tag the Issue in step 7 as `Epic` ticket but select `Task` for the main ticket directly = ~skip these steps and continue from the next one.

1. Go to the [`BiCU Projects Overview`](https://github.com/orgs/BiCU-CCRI/projects/2)
2. Under `Backlog`, start typing to create the tracking task and `Create a draft`. This could have, but doesn't have to, the same name as the project repository (e.g., `POP drug screening`)
3. Make a [project Repository](#setting-up-a-github-repository). For example, `POP drug screening`. **Note:** You can always rename it later, but try to use some reasonable and explicit name from the get-go.
4. Go back to `BiCU Projects Overview`
5. Open the `Draft` made in step 2, click `Convert to issue`, and assign it to the Repository made in step 3.
6. Under `Projects`, check if it's assigned to the `BICU Projects Overview`. **Note:** You can also assign it to the Repository Project if you want to track it there, but it's unnecessary since it will already be there as an `Issue`.
7. Under `Type`, select `Epic`. This will make it obvious that this is the general tracking task. This creates one common tracking task for the whole `POP drug screening` project, which stays around as long as the main project is active.
8. Edit the description field and add:

```shell
- [ ] POP drug screening - AML sample 1
- [ ] POP drug screening - MDS sample 1
```

9. Click on the three small dots next to the created `- [ ]` lines and `Covert to sub-issue`
10. Open the issues one by one and assign them to the `BiCU Projects Overview`. Tag them with `Task`. This creates tracking issues for individual analyses. Check that they are assigned as Issues to the Repository. **Note:** You can also assign it to the Repository Project if you want to track it there, but it's unnecessary since it will already be there as an `Issue`.
11. Fill out the dates, the sizes, priorities, assign it to a group, etc.
12. Update the [status](#github-project-ticket-status) as you go.

**Summary:** Project/task tracking goes to `BiCU Projects Overview` and Repository Issues. `Epic` issue for the whole project (long-term projects with additional analyses), `Task` for individual analyses that are sub-issues of the `Epic`. One-time projects don't have `Epic` but are directly tagged with `Task`. Individual code development is done only at the project repository level with `Feature`, `Subtask`, and others (more info at [GitHub Best Practices/Issue Types](./github_best_practices.md#issue-types).

**Note:** You can also create the *tracking* Issue from the Repository `Issues` tab directly - create an issue in the Repository, tag it as `Epic`, and assign it to the `BiCU Projects Overview` project.

**Note:** You can also do steps 8-10 from the repository `Issues` tab directly - create an Issue in the repository, tag it as `Task`, in `Relationships` (on the right) select the parent `Epic`, and assign the Issue to the `BiCU Projects Overview` project.

## Setting up a GitHub repository

To set up a repository:

**Note:** Steps 6-8 will dissapear if you use one of the repository templates from step 5

1. Go to [BiCU GitHub page](https://github.com/orgs/BiCU-CCRI/repositories)
2. Click `New repository`
3. Give the repository a **reasonable name** (try to be as explicit as possible). **Note:** You can also use a specific prefix to help you track your projects. For example, `jo001`, `ab16`, ... If you have multiple open projects, it might be easier to remember the simple prefix than the full name.
4. `Choose visibility`: `Private`
5. `Start with a template`: For personal repositories, you can use [BiCU_personal_repository_template](https://github.com/BiCU-CCRI/BiCU_personal_repository_template). For shared/common repositories, you can use [BiCU_shared_repository_template](https://github.com/BiCU-CCRI/BiCU_shared_repository_template). These can be selected in `Create a new repository` under `Start with a template: Templates pre-configure your repository with files.`. **Note:** You can always edit the repository settings if must be (or if they don't fit your preferences).
6. `Add README`: `On`
7. `Add .gitignore`: `No .gitignore`
8. `Add license`: `MIT License`. **Note:** MIT License is recommended but you can choose your own.
9. Click `Create repository`

It is strongly recommended to follow GitHub repository rules described in [GitHub Branches, Commits, and Push Rules](#github-branches-commits-and-push-rules).

### GitHub Branches, Commits, and Push Rules

To make the development more efficient and safe, we have to establish certain GitHub rules. These will ensure our code is safe and properly reviewed, and we follow the agreed CR practices.

We follow these general rules and settings when creating a new GitHub repository:

1. **Protect the `main` branch:** Changes to the `main` branch must be handled only through a **reviewed** PR merge. This prevents random, non-unreviewed code in the `main` branch and helps to keep the commit history clean.
2. **PR to the `main` branch has to be reviewed:** (and approved) by **another person** before mergingThe PR merge needs to undergo the full CR process and, ultimately, be approved by at least one more person. Only then can it be merged into the `main` (or parent) branch
3. **All threads need to be resolved:** The reviewer needs to resolve all the CR comments and suggestions before the merge is allowed. The developer **must not resolve:** the comments themselves. If the original reviewer is not available anymore, the developer must request an additional reviewer. **Note:** GitHub suggestions are resolved automatically if accepted as suggested by the reviewer.
4. **Not implemented** ~~**Branch names and commit messages** need to follow **specific structure**~~Branch names and commit messages must have a specific structure. This makes it easier to standardize and read the Git history.
5. **Squashing commits before the merge:** It is strongly encouraged that branch commits should be squashed before the merge. This keeps the `main` (or the parent) branch history nice and tidy (=one commit per merge) while keeping the full history in the original branch. **Note:** This assumes we do not delete the *original merged* branch. [https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests)
6. **The final merge has to be done by the author** Once the whole CR process is over, the author has to do the final PR merge.
7. **Agree merge and rebase order:** If multiple people contribute to the same code, rebase your local branches to the latest merged PR changes if the other person merges their code first. **Talk to each other** and **decide** who merges first and who rebases, or if the other person should wait before starting a new branch.

#### Branch rulesets

Branch rulesets allow us to enforce specific *rules* for branch names, commit message structures, and the type of commits themselves and, for example, protect the code from accidental non-unreviewed changes.

Branch rulesets are applicable to all branches; however, the most important are the `main` branch rules, which should be as strict as possible to protect the final code.

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

###### `main` branch rules setup

To set the rules to protect the `main` branch:

**Note:** Steps 7-11 are only for shared reviewed repositories. For other repository types continue from step 12.

1. Go to the GitHub Repository
2. Click on `Settings` on the top panel (below the Repository name)
3. Click on `Branches` on the left (under `Code and automation`)
4. Click on `Add classic branch protection rule`
5. Branch name pattern: `main` or `main*` (or `master` if you haven't switched yet to the [&#34;new&#34; naming](https://github.com/github/renaming))
6. `Require a pull request before merging`: **check**
7. `Require approvals`: **check**
8. `Required number of approvals before merging`: `1`
9. `Dismiss stale pull request approvals when new commits are pushed`: **check**
10. `Require approval of the most recent reviewable push`: **check**
11. Require conversation resolution before merging: **check**
12. `Require linear history`: **check** (requires either `squash before merging` or `rebase before merging, but the requirement of`squash before merging` cannot be directly enforced)
13. `Do not allow bypassing the above settings`: **check**
14. (**optional**) `Restrict who can push to matching branches`: **check** and specify the people allowed to push and merge to the repository
15. Click `Create`

#### General branch protection rules

The full branch protection ruleset settings, allowing more fine-tuned restrictions, can be accessed by:

`Repository -> Settings -> Rules -> Rulesets -> New ruleset -> New branch ruleset`

- `Ruleset Name`: `Branch protection`
- `Enforcement status`: `Active`
- `Bypass list`: keep `Bypass list is empty`
- `Target branches -> Add target`: `Include all branches` (or you can select specific branches you want to protect, including the `main`/default branch)
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
    - **Only for the main/default branch:**
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
    - For example, if you don't follow the predefined commit message structure, the `git commit` gets rejected. You can correct the message with `git commit --amend -m '...'` and push again with `git push --force`
    - Setting the rules helps with consistency across the developers and simplifies project and code sharing

## GitHub Project Ticket status

We use the following columns in GitHub Project:
    - **Backlog**: The task was created but isn't complete, or the work hasn't started yet
    - **In Progress**: The task is being actively worked on
    - **On Hold**: The task cannot be worked on atm or has to be paused.
    - **In Review**: The task/code is being reviewed (either by another developer or the person who requested the task)
    - **Done**: The task is finished

Please, move the tickets from one column to another as you progress, even if it's just a formality. Each change is recorded, and following the status flow is generally a good practice. In code development, it is common to predefine a mandatory status change diagram that limits the possible ticket status changes, and getting this habit will help you in environments where this is implemented.

**Note:** Predefined ticket status change comes into play when we apply for ISO certification or have code audits. Code development-related ISOs and audits require a clear track of code development, including predefined status changes (~ticket development workflow).

## Adding Issues and Sub-issues from the Project tab

For general Issues and Sub-issues (subtasks) setup, please see [GitHub Best Practices](./github_best_practices.md).

To add Issues and Sub-issues (subtasks) to the Repository from the Projects tab:

1. Go to the Repository Project page and select `+ Add item` at the bottom of the Backlog column.
2. Use `#reponame` and and `(+) Create new issue`
   - This creates a new Project Item and a Repository Issue
3. After you complete the task description, check `Create more` to make more Issues
