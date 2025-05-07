# GitHub Best Practices Guidelines

## General guidelines

- We and do not push code directly to `main`
    - Branches can be easily merged, reverted, commented on (Pull Request), removed without affecting the `main` branch
    - More info [here](https://stackoverflow.com/questions/46146491/prevent-pushing-to-master-on-github)
- `main` branch should only contain clean, tested, and functional code
- Keep the commit/PR/branches title structure consistent
- Keep the message styles consistent
- Keep the analysis-specific/experiment-specific code separately from the main code
    - Only keep *general* code in the `main` branch
- Keep locally the same directory structure as on GitHub
    - For example, keep the GitHub repo `https://github.com/BiCU-CCRI/scripts-Public` in `~/BiCU-CCRI/scripts-Public` (or `~/projects/BiCU-CCRI/scripts-Public)
    - This makes it easier to organize your code if you have multiple projects or collaborations
    - Also makes it easier to follow the paths when you share the code if everybody uses the same structure

## GitHub Projects

- GitHub Projects are extremely helpful in tracking the overall project status and in collaborations
- They allow us to write Items (Issues; Tickets) with detailed descriptions, track the development progress (Item status), assign tasks to individual developers, etc.
- They serve as the primary project documentation for code development together with README
    - For example, we can link individual branches and commits to the GitHub Project Item using the Item # id and get all the information used to make decisions during the development

### GitHub Project Items

- The individual GitHub Project *tickets* are called **Items**
    - Items, if assigned to a GitHub repository, can be further structured as **Issues** (**Features**) or **Sub-Issues** (**Subtasks**)
    - Note: In code development, GitHub Items would be called **Tickets**
- Item without assigned repository is a **Draft** ticket
    - We can also create draft tickets on purpose - a quick idea with a simple description that is not ready to be started to work on, but we want to remember
    - We can prefix it with `Draft:` to make it obvious it is not a complete ticket
    - This helps, for example, to distinguish Items with unassigned repository by accident from those that really are drafts
- Assigning a repository to the Item *copies* the Item to the tagged repository and crates an **Issue**
    - Repository-assigned Items (->Issues) should have **a complete description** (see below) or be tagged as `Draft:`
- If, for some reason, you make a mistake and the Item is not ready, remove the tagged repository from the Item and move the Item back to Backlog (should happen automatically)
- Before creating a new Item, look into the Project columns (or use the Table view) and look for potentially similar Items to avoid duplication
    - If duplication still happens, comment on the Item with a link to the *other* duplicated Item and close it (`Close issue` at the bottom)

#### Issue Types

- Item/Issue name should be a brief description of the actual task that it solves
- We also add a task prefix `<prefix-><Item name>` to further highlight the ticket type and for faster orientation in the commit history:
    - **`feature`** (or Item on GitHub) - main tickets introducing new functionality. This is what we aim to implement and include in the *main* part of the code. The Feature description includes the overall goal, relevant literature, examples, etc. The Feature can be divided into **Subtasks** (Sub-issues; see the next point). In [Code Review](./code_review.md), we review both Feature and Subtask PRs. If we use the `subtask(s)`->`feature`->`main` development style, most development should be done on the Subtask level. The complete Subtasks should be merged into the Feature branch. If there are no changes on the Feature level, the reviewer can (but doesn't have to) approve the Feature merge directly. However, another person might have reviewed the Subtasks, so it's worth going through them again (or at least taking a *quick* peek). If necessary, we can also add changes on the Feature level, but then the Feature needs to be adequately re-reviewed. The complete Feature is then merged into the `main` branch.
    - **`subtask`** (or Sub-issue on GitHub) - These are detailed *chunks* of work that together *define* a Feature. Most development is usually done here. Individual Subtasks are merged into the Feature. Ticket description of Subtasks further develops the general description of the Feature Item. As mentioned above, we do Code Review on `subtask`->`feature` PR. We can skip `subtask` if the `feature` is relatively well-defined and short. We can also merge `subtask->main` if we need to merge some code quickly (for example, breaking changes).
    - **`experiment`** - tickets that **do not change the code** but include experiment-/analysis-specific files that we want to keep track of. For example, config files for the latest diagnostic run. Experiment-specific files/commits should **not be included in the `main` code**. They will stay in their `experiment` branch. `experiment` branches are not deleted because they contain code relevant to an analysis/publication/experiment.
    - **`spike`** - tickets that are meant to collect information or gain knowledge. They do not have to have code associated with them. For example, collect and summarize information about new variant callers. You can create a branch if the spike requires some sort of comparison. The **code will not be included** in the **`main` branch**.
    - **`test`** - tickets primarily for testing and trial purposes. For example, trying new settings or tools, experimental combinations, etc. The code **will not be included** in the `main`, and the branch **might be deleted**. These branches might include additional test results required for the CR.
    - **`janitor`** - smaller code improvements, README updates, and other smaller fixes that are not crucial for the code execution but improve or complete the code. These changes can be cumulative over, for example, a month based on continuous observations or a collaborator's input.
    - **`bugfix`** - correction of a *bug* found during the development or testing phases. Bugfixes are typically planned and integrated into regular updates, addressing less urgent problems than hotfixes.
    - **`hotfix`** - tickets with crucial bug fixes that must be implemented ASAP. They can bypass the regular development process. These should be used only if absolutely necessary. Use **`janitor`** or **`bugfix`** for regular code updates, minor improvements, or fixes.
    - **`release`** - ATM, we don't have code releases

##### Merging order

- You can decide on what level you want to work and how to structure the *merging* order:

 1. `subtask`->`feature`->`main`
 2. `feature`->`main`
 3. `subtask`->`main`

- The decision should be based on the Issue *size* and urgency:

 1) For bigger tasks, it is recommended to go `subtask`->`feature`->`main`
 2) For smaller tasks that add new functionality, you can do `feature`->`main`
 3) The third option is usually used if we collaborate on a project with another person. and the finished Subtask makes it easier for the other person to continue the development.

#### Items (Tickets/Issues) Description

- Ticket description should include **enough information** so **another person** can start working on the task without any (~much) additional information if necessary
    - What might be clear to you doesn't have to be transparent to others - if in doubt, add more description rather than less
- As we do not do many collaboration projects ATM, writing a detailed ticket description might sound like too much overhead, but it is still recommended for keeping track of what has been done, what needs to be done, why, and how, even for yourself
- Some Tickets types might not need full description if they are *simple* enough so the commit/PR message can describe them well enough
    - For example, `janitor` or `hotfix` tickets

#### Sub-Issues (Subtasks)

- GitHub now offers creating Subtasks (Sub-Issues) automatically
    - When writing the Feature description, you can use check-box markdown notation `- [ ]`  in the description *body* and then click on *Create Sub-issue* on the right
- You can also assign an existing Item as a Sub-Issue (*Add existing issue*) or create a Sub-Issue with *Create sub-issue*
- This links the Items together, and you see which ones are related

#### Ticket status in GitHub Project

- GitHub Project offers *status columns*
    - These are useful when we want to fully track the development process (for example, essential for many IT-related ISO certification) when multiple people collaborate on the same project, or when we want to keep track of where we left off if we have to switch between projects
- As we do not follow any ISO (we might have to follow IVDR regulations in the future), and we don't have many collaboration projects, following GitHub Project status might be too much overhead, but it is still recommended
    - It helps to track the project progress and, for example, to enable better project handover
- GitHub allows automatic Status change - See [GitHub Best Practices Guidelines/Pull Request Commit Message](./github_best_practices.md#pull-request-commit-message)
- See [GitHub Setup - GitHub Project Ticket status](coding_and_review/TODO_github_setup.md#github-project-ticket-status) for more details

## Branches

- We do **all the development** in branches
- Branches can be reviewed, merged, deleted, reverted
- Committing everything into the parent (~`main`) branch directly:
    - Makes the `git` history difficult to read
    - Very difficult to revert if necessary
    - Doesn't allow version releases properly
    - Is generally a bad practice
- Name your current development branch the same as the Project Item, including the ticket number
    - This way, it's easy to find the full task description and track the origin of the code

### Branch Name Structure

- The branch **name structure**: `<issue_number>-<issue_prefix>-<rest-of the-issue-name>`
- Regex: `^\d+-(feature|subtask|experiment|test|janitor|bugfix|hotfix|release)-([a-zA-Z0-9]+(-[a-zA-Z0-9]+)*)$`
    - We can enforce the `git branch` regex for every commit to keep the structure standardized
    - Note: The name structure follows GitHub *automatic*
- For example: `4-subtask-assemble-chromosomes`

### Creating Branches

- The easiest is to use the default GitHub functionality to create the branch directly from the Issues options
    - GitHub then names the branch according to the Issue name
- **Don't forget** to change the *parent* branch to the Feature branch when using this GitHub functionality!
    - It avoids unnecessary `git rebase` commands and conflict resolution
- Don't forget to include the Issue number, the prefix, and the name as described above if you create the branch yourself

## Commits

- Commits have to have a meaningful message so it's clear what has been done
    - It makes it easier for Code Review, follow the code changes, and revert the code if necessary
- Commit **messages** are written in [**imperative**](https://cbea.ms/git-commit/#imperative) verb form
    - For example: **Write** "*Fix missing variable*" and **do not** write "*Fixed missing variable*" or "*Fixes missing variable*"
    - Note: An easy way to remember is to say to yourself: "*If applied, my commit will (INSERT COMMIT MESSAGE TEXT)*"
- Use the ticket number, including the hash symbol `#` as the first character of the commit message
    - This allows easier traceability (you can directly click the ticket number in the commit to see the ticket description)
    - Note: You might have to change your `git` settings to turn off ignoring commit messages starting with `#<issue_number>` (unfortunate GitHub Issues labeling)
    - `git config --global commit.cleanup whitespace`
- The next word of the commit message starts with a **capital letter**
    - This makes it clear the commit message is complete and as intended
- More on how to write a good commit message [here](https://cbea.ms/git-commit/) and [here](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/)

### Commit Message Structure

- The commit message structure: `#<issue_number> <Commit message starting with a capital letter>`
- Regex:  `^#\d+ [A-Z][a-zA-Z0-9\s]*$`
- For example: `#14 Filter unwanted reads`

### Commit Message Verbs

- One action can be described using different verbs with the same meaning
    - Using different verbs for the same action might be confusing when the commit history gets longer - try to stick to the same set of verbs
- This improves clarity and consistency
- This is a **non-exhaustive** list:

#### General Verbs for Commit Messages

- **Initialize** - For the initial setup of a repository or a new
    - Example: `Initialize repository`
- **Add** - For adding new files, features, or functionality.
    - Example: `Add login feature`
- **Update** - For making non-breaking changes or enhancements.
    - Example: `Update documentation`
- **Modify** - For making changes to existing code or resources.
    - Example: `Modify user validation logic`
- **Improve** - For optimization or quality improvements.
    - Example: `Improve performance of sorting algorithm`
- **Fix** - For bug fixes or addressing issues.
    - Example: `Fix crash on app startup`
- **Refactor** - For code restructuring without changing functionality.
    - Example: `Refactor authentication module`
- **Rename** - For renaming files, variables, or components.
    - Example: `Rename User class to Account`
- **Reorganize** - For changing the project *higher* structure.
    - Example: `Reorganize project directory`
- **Remove** - For deleting files, features, or functionality.
    - Example: `Remove deprecated API endpoint`
- **Deprecate** - For marking features as outdated.
    - Example: `Deprecate legacy logging system`

#### Verbs for Reversals or Cleanup

- **Revert** - For undoing previous commits.
    - Example: `Revert changes to login feature`
- **Clean** - For cleaning up code or resources.
    - Example: `Clean unused imports`

#### Specialized Verbs

- **Document** - For updating or adding documentation.
    - Example: `Document API usage`
- **Optimize** - For performance improvements.
    - Example: `Optimize image loading`
- **Configure** - For changes to configuration files or settings.
    - Example: `Configure database connections`
- **Enhance** - For minor upgrades to functionality.
    - Example: `Enhance error message display`
- **Test** - For adding or modifying test cases.
    - Example: `Test edge cases for login`
- **Build** - For changes related to build or deployment systems.
    - Example: `Build production release`

## Pull Request

- PR is the last step in code development before merging the code into the parent branch
- The PR contains all the commits, has a title, and a final commit message
- The PR title should match the Issue name, including the Issue prefix and the `#` at the beginning of the Issue
- An exception to this rule is when the main implemented feature(s) significantly differs from the original ticket name and content
    - You can also consider changing the Issue title, but be cautious not to break any links and collaborator's local repository

### Pull Request Title Structure

- The RP title structure: `<#issue number> <issue type>-<Rest of the issue name>`
- Regex: `^#\d+ (feature|subtask|experiment|test|janitor|bugfix|hotfix|release)-[A-Z][a-zA-Z0-9]*$`
- For example: `#1 feature-Implement performance testing`
- Note: Unfortunately, GitHub doesn't allow setting rulesets separately for PR merge and *regular* commit message (PR merge is technically just another commit). We cannot include the `(feature|subtask|experiment|test|janitor|bugfix|hotfix|release)` in the rulesets

### Pull Request Commit Message

- The PR commit message should be written **in the third person** and **summarize what has been implemented or what it does** or what is being added by the PR to the main code
- Do not confuse the **PR commit message** with **PR comment** (=PR comment is **not** included in the `git` history)
    - Unfortunately, GitHub puts PR comment on the top, making it slightly less obvious what is what
    - You can use the PR comment section to make notes and keep track of the development and then copy the text (or part of it) to the PR commit message
    - Note: You can use the `- [ ]` markdown check-box option to keep track of your own development progress on both Subtask and Feature levels
- For a Subtask merge, the PR commit message can be a sentence or bullet points summarizing the commits
- For a Feature merge, the PR commit message can be a list of included Subtasks + the description of the additional commit(s) at the Feature level:

```git
- Removes unused dependencies # Commit added at the Feature level

- Includes: # Commits added by merging Subtasks into the Feature
  - [x] subtask-Reference datasets #2
  - [x] subtask-Performance testing framework #3

closes #14
```

- You can use the following [GitHub keywords](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword) in the **PR commit message** (they won't do anything in the PR comment)
    - The keywords can trigger other GitHub actions
    - For example, to automatically close the repository Issue and the Project Item when merging the PR, use `closes #<ticket_number>`
    - The `closes` therefore closes the PR itself, the Issue, and the Item
        - You can also close the Issues manually by clicking on `Close issue` in the Issues tab and by moving the GitHub Project Item to "*Done*"
- More on how to write a good PR commit message [here](https://medium.com/@koklitheen/writing-a-good-merge-request-3916cfce0518) - you can be as verbose as necessary
- Note: Once the PR is merged with the parent branch and you or your collaborator have other branches from the same parent branch, it can happen that the *other* merges won't be possible without rebasing
    - `git rebase` basically means "*Take my changes (commits) and put them on top of the other changes (commits)*"
    - You might have to do this manually in your code editor by `git checkout` to your branch and then clicking on the parent branch and *Rebase my current branch onto the parent branch*
    - VS Code offers a nice visual rebasing guide to get you through the changes
    - The rebase has to be done for each of the new commits (that's why Squashing the commits is useful - see below)

### Pull Request Merge Types

- There are several [types of merges](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges)( and [here](https://docs.gitlab.com/user/project/merge_requests/methods/))
    - Merge - add the entire history to the parent branch (including all the commits)
    - **Squash and merge** - *summarizes* all the merge code to a single commit and adds this to the parent branch
    - Rebase and merge - rewrites the commit history by integrating each of the changes to the parent branch
- [Squash and merge](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests) is strongly encouraged
    - This keeps the history of the parent branch clean and [**linear**](https://stackoverflow.com/questions/20348629/what-are-the-advantages-of-keeping-linear-history-in-git)
- You can decide whether you want to **keep** or **delete** the **development** branch after the merge:
    - *Advantage of keeping*: It keeps a detailed history of changes and makes it easier to track the feature development - what was implemented, when, how, and why.
    - *Disadvantage of keeping*: potential clutter and increased complexity in branch management - it is difficult to *remember* if the branch still has some relevant code or if everything was already merged
    - For example, we don't have to keep branches with simple single tasks

### Pull Request Review as a Developer

- PR is initiated by the developer by:

 1. Clink on *Pull requests*  in your repository
 2. *New pull request*
 3. Choose the right parent branch to merge to and the branch to be merged on the top left
 4. *Create pull request*
 5. Assign yourself as the *Assignee* (to get notifications about changes/comments)

- Note: I like to create a PR right after the first commit to the new branch and assign myself
    - Because the PR is not ready for review, I mark it as *Draft* (on the top right *Still in progress? Convert to draft*). Once done, you can open the PR and click *Ready for review* to enable the review process
    - This helps me to keep track of all my open PRs

### Pull Request Review as a Reviewer

- Once you are nominated as a PR Reviewer, don't forget to check if you are *officially* assigned in the *Reviewers* tab in the PR (top left)
    - This way, you get notified about any changes to the PR

- To start a review as a reviewer:

1) Go to *Pull requests* tab
2) Find the Pull request you were asked to review
3) Go to *Files changed* tab
4) Look for the changes
5) Go to the line you want to comment on/make a suggestion
6) Click on the small blue `+` sign (you can select multiple lines by dragging the `+` sign down)
7) Add a comment or a suggestion (`+/-` sign)
8) Click on *Start a review* (if it's the first comment/suggestion, otherwise click on *Add review comment/suggestion*)*
9) Repeat until happy ...
10) Once done, go to the top and click *Finish your review*
11) You add an overall comment if you like
12) Select the required follow-up - *Comment/Approve/Request changes*. *Request changes* will probably be the most common option, especially at the beginning of the PR

- - Submitting comments/suggestions this way, all your comments/suggestions will be marked as *Pending* and submitted only once at the very end of this PR round.
        - Clicking on *Add single comment* instead of *Add review comment/suggestion* would send a separate notification for each comment to everyone following the repository.

- You can also comment on the PR request as a whole on the main PR request page
    - For example, ask the author for more PR descriptions, links to test results, etc.
- You can click on *Viewed* if you went over the file and you want to hide it temporarily
- A simple video example [here](https://www.youtube.com/watch?v=lSnbOtw4izI&ab_channel=CoderDave)

#### PR in VS Code plugin

- VS Code has a plugin for [GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github) (still under development)
- You can do **everything** you can do in GitHub without leaving the VS Code
- Check out this [video](https://www.youtube.com/watch?v=DSl-L6B_Qb4&ab_channel=DevLeonardo) for a nice summary

## GitHub Rules

- GitHub offers a lot of [rules/rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets) to help us enforce the agreed *rules* for commit names, branch names, PR rules, branch protection rules, etc.
- We primarily use these rules:

 1. Commit message structure
 2. Branch name structure
 3. PR title structure
 4. `main` branch protection (no direct commit - only through PR)
 5. Code Review rules (resolving threads, required approval)
 6. (Not implemented yet) Successful PR tests*

- See more information in [GitHub Setup](coding_and_review/TODO_github_setup.md)
    - In the future, we will include [GitHub Actions](https://docs.github.com/en/actions/about-github-actions/understanding-github-actions) to include tests in the PR approval rulesets

## Notes

### Commit/Branch/Pull Request title structure

- We have two (+1) different ways how to name commits, branches, and PR merges
    - This comes from the unfortunate GitHub styling of `#<issue number>`
- Some *sections* are ok with having `#` as the title/message character (commit message `git`/PR title), while some struggle (switching branches names in the command line)
- The current title/message structure comes from the *least necessary* changes
- In optimal case, the Issue IDs would start with a custom ID that can be used in all three names (=starting with anything but `#`)

### Code Publishing

- Be aware that code on GitHub is not stored permanently - the repository or the branch can be modified or completely deleted
- To permanently publish and share your code, you can use one of the following:
    - [Zenodo](https://zenodo.org/)
    - [FigShare](https://figshare.com/)
- Both provide **DOI to your code** - *freeze* the software code, version and allow citations
    - They also offer direct code import from GitHub (how-to video [Zenodo](https://www.youtube.com/watch?v=HZ6m8oxwvig&ab_channel=LukeDataManager); how-to [FigShare](https://help.figshare.com/article/how-to-connect-figshare-with-your-github-account))
- Simple Zenodo example:

1) Create tag on GitHub. For example, `v1.0`. You could use also use something like `v1.0_prepub`
2) Login to Zenodo.com with your GitHub account. You can also use orcid or just create a user account. I find GitHub the easiest since I only upload code. 
3) Upload the tagged GitHub code to Zenodo. 
4) Add description if not included by default. For example, **Is supplement to** and add the link your GitHub repo.
5) Finish
- If you get any revision requests or you want to update something, you can update your _Zenodo_ repo with the latest code
- Zenodo then creates two DOIs - one for the _repo_ and one for each uploaded _version_. You can then decide if you want to use the _repo_ DOI or the specific version in your paper. You can upload multiple GitHub tags (versions) and each of the _versions_ will get their own DOI. The main _repo_ DOI stays the same regardless on the version of the code
- You can also limit the visibility of the code and, for example, restrict it only to certain users (like reviewers or the editor)
- Once uploaded you cannot edit the code (unless you make a new DOI version) but you can edit the metadata anytime