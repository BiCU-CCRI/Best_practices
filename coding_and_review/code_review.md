# Code Review Guidelines

- Every *production-level* code **should be reviewed**
- We **should not share, publish, or recommend code** that hasn't been looked at by **at least one more person**
- **Second Set of Eyes​** approach (sometimes called the Four Eyes principle) for coding - Anybody can write the (produce) code themselves, but at least one more person has to look at it before the code is published
- This can be achieved through setting up a **Code Review** process.

## What is Code Review

- It is a **set of agreed-upon rules** that the code has to pass before publishing or sharing of code written by an individual or a group of individuals
- A **common practice** in any organization engaged in code development
- It is **a must in collaborative coding** and very useful for general coding and coding *as a service* (sort of our case, quite often)​
- It works hand in hand with the [Best Coding Practices](./best_coding_practices.md), [Code Testing](./code_testing.md), [Code Reproducibility](./code_reproducibility.md), and [GitHub Best Practices](./github_best_practices.md)
    - It can be supported by a set [GitHub Setup and Rules](github_setup.md)
- Results in **comprehensive, readable, functional, and tested code** written according to the agreed-upon best practices
- Code Review benefits are nicely summarized [here](https://www.devart.com/review-assistant/learnmore/benefits.html) and [here](https://www.browserstack.com/guide/code-review-benefits)
- In practice, a **Developer** writes code, and when they finish a particular *feature*, they request a second person (**Reviewer**) to check the code, see if it works as intended, and follow the agreed-upon best practices. Therefore, both the Developer and the Reviewer are responsible for the final code quality.

## Why is Code Review useful

- **Overall code quality** improvements, better performance, fewer bugs, fewer future problems​
- **Enhanced collaboration** and ideas exchange results in more efficient code​
- **Improved learning** in coding for both the Developer and the Reviewer​
- **Greater code readability**, which makes it easier for other Developers to understand and work with the code​
- **Better code maintainability**, so it is easier to implement changes and introduce new features​
- **Higher code awareness** within the team​

### Pros and Cons of Code Review

#### Pros of Code Review

- **Decreases errors**: By having multiple sets of eyes on the code, potential mistakes and bugs are more likely to be caught and corrected before the code is merged.
- **Increases productivity**: When errors are caught early, less time is spent debugging and fixing issues later, allowing the team to focus on new features and improvements.
- **Improves clarity**: CR encourages Developers to write clear and understandable code, making it easier for others to read and maintain.
- **Increases code quality**: Regular reviews ensure that the code adheres to best practices and standards, leading to higher overall quality.
- **Increases code maintainability**: Well-reviewed code is more consistent and easier to maintain, as it follows agreed-upon conventions and is less likely to contain hidden issues.
- **Increases credibility**: Code reviewed and approved by peers is more trustworthy and reliable, enhancing the team's reputation.
- **Increases learning**: CR provides an opportunity for team members to learn from each other, share knowledge, and improve their skills.
- **Creates good coding practices and habits**: Regular reviews reinforce good coding habits, helping Developers to adopt best practices and apply them consistently.
- **Increases code awareness within the team**: Reviewing each other's code lets team members stay informed about different parts of the codebase, fostering better collaboration and understanding.

#### Cons of Code Review

- Proper CR takes time and is more work​
    - You have to follow the process completely to fully leverage the CR benefits
    - We have to plan extra time for CRs when planning for other projects and analyses
- You have to ask a second person (Reviewer) for the Review, but the Reviewers might be busy
    - Their work, other projects, vacations, etc.
    - **Note:** We should target making CR our priority because it blocks the other person from progressing their Project or from handing over the code to their collaborator
- Personal preferences and miscommunication happen
    - Different coding preferences and styles might lead to conflicts​ (see [Code styling](./best_coding_practices.md#code-styling) for easy ways to mitigate this)
    - Sometimes, it is better to accept a suggestion than to argue if it doesn't break the functionality and still follows the best practices
    - Ask a third person in case of disagreement to prevent unnecessary clashes and decreased morale​
- Takes some time to get used to it​
    - It gets easier with time, but it needs a lot of discipline at the beginning​
    - After a few CRs, it becomes a habit, and then it doesn't feel like extra work anymore

#### Unreviewed Code

- **Increases the number of errors and bugs**: Without the CR, mistakes are more likely to go unnoticed, leading to more bugs in the code.
- **Decreases productivity**: More time will be spent fixing issues that could have been caught earlier, slowing down the development process.
- **Decreases code clarity**: Unreviewed code may be harder to understand and follow, making it difficult for others to work with.
- **Decreases code sharing**: Without Reviews, code may not adhere to team standards, making it harder for others to use or build upon.
- **Decreases the credibility**: Code that hasn't been reviewed may be seen as less reliable and trustworthy, potentially harming the team's reputation.

### Other benefits of Core Review

- **Easier Project handover​**
- **Easier new members onboarding​**
- **Builds useful habits for the future​** and for your career in general
- **Necessary for [ISO](https://www.institutedata.com/us/blog/iso-standards-for-software-engineering/) certification​s** including [IVDR](https://eur-lex.europa.eu/eli/reg/2017/746/oj)
    - **Note:** `nextflow` has a nice summary of pipeline [certification requirements](https://nf-co.re/docs/guidelines/regulatory/overview)

## When to do Code Review

- CR is **a must** for collaborative projects and shared code​ (for example, shared pipelines, scripts to run jobs on the cluster, etc.)
    - It's recommended for all the other code as well ​, whenever possible
- It works best with well-defined tasks (*features*) or functionality, but can be adapted to other types of tasks as well
- There are many types of projects with code development in research:
    - Research-heavy​
    - Pipelines and workflows
    - Shared public code (run interactive RStudio, gists, best practices, etc.)​
    - Multi-group collaboration projects
    - General code development
- CR might not be suitable for all of them​
    - Research-heavy code might be too dynamic​ or too specific for full-scale CR

## Code Development with Code Review in Mind

### Outline

- Most of our Code Reviews are based on GitHub Projects, GitHub Repositories, and the **GitHub Pull Request** feature
    - GitHub contains quite nice [documentation](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/getting-started/about-collaborative-development-models) about PR-based code development and collaboration
    - **Note:** Pull Requests are also commonly referred to as Merge Requests

- TL;DR: Code development with Code Review goes as follows:

> *Create repository->Create Project->Add ticket->Describe the tasks->Make a branch->Write code->Make documentation and tests->Push code->Make Pull/Merge Request->Ask for Review->(Reviewer asks questions, makes comments or gives suggestions)->Work on suggestions/Reply to comments->Resubmit Review->...repeat as many times necessary...->Merge​ the code->Close ticket->...repeat as many times necessary...->Close the Project*

### Details of Each Step

**Note:** This is only a general description. Detailed steps are described in [GitHub Setup](./github_setup.md).

#### 1. Create a GitHub Project and assign it an empty repository

- Create an empty repository where you will store the code, documentation, and issues related to the Project
- When making a new repository, make the initial commit with, for example, a README, titled, for example, `Initial commit`, `First commit`, or `Initialize repo`, and push the code. This is the only time you make a push directly to the `main` branch
    - **Note:** You can also let GitHub create an empty README/LICENSE when creating the repository
        - This way, you can track your open PR and enable Code Review based on PRs
- **Avoid pushing any other code** to the `main` branch directly without a reviewed PR

#### 2. Create a GitHub Project and assign it an empty repository

- This sets up a dedicated space for your Project, ensuring all related work is organized and accessible
- GitHub project is used to track the overall development, store additional issue info, track dependencies between Issues, and can be used to export a summary of your development

#### 3. Define, describe, and create Project Items (Issues and Sub-Issues)

- Outline the Project's objectives by breaking them down into manageable tasks (*Issues*) that altogether complete the Project
    - It helps you stay focused and aligned
    - It helps you to work more incrementally and better define the task at hand
    - It also makes it easier to collaborate on the Project
- Try to keep the Items reasonably sized to make CR efficient - this translates to reasonably sized PRs
- **Issues** (also called **Features**) are a bigger *chunk* of code, a functionality, a collection of Sub-issues/Subtasks, or a complete functional **Feature** that can be added to the main code
- **Sub-Issue** (also called **Subtask**) is an individual step/implementation used to complete the feature
    - Feature doesn't always have to have subtasks
- You can add new Items later if the Project develops while working on it
- **Note:** Technically, you create an **Item** in the GitHub Project, and it becomes an **Issue only** once you assign a repository to it (otherwise it stays as a `Draft`)
- Give your Item names a proper prefix as described in [GitHub Best Practices - Ticket types](./github_best_practices.md#ticket-types)

#### 4. Make a new branch from the `main` or the parent branch

- Creating a separate branch for your work ensures that the `main` (~parent) branch remains stable and free from incomplete or experimental code until the development is done
- First, make a Feature branch and then make a Subtask branch from the Feature branch as its parent
- Give your Branch a proper name as described in [GitHub Best Practices - Branch Naming](./github_best_practices.md#branch-naming)
- When creating a completely new branch and after pushing a first commit, create a `Draft` PR right away - see [7. Create and submit a GitHub Pull Request](#7-create-and-submit-a-github-pull-request)
    - This way, you can easily track your open development tasks
    - **Note:** You change the PR to *ready for review* when you are finished with the development

#### 5. Work on the code based on the Tickets described in the GitHub Project

- Following the predefined tasks ensures that all aspects of the Project are addressed systematically
- Well-organized code is easier to review and maintain - see [Best Coding Practices](./best_coding_practices.md) and [Code Reproducibility](code_reproducibility.md)
- Don't forget to organize your code properly as described in [Repository Structure](./repository_structure.md)
- Don't forget to use the right commit message structure as described in [GitHub Best Practices - Commits](./github_best_practices.md#commits)

#### 6. Document and test the code

- Code documentation and testing are important for verifying functionality and providing clear guidance for future Developers or collaborators
- Document the main parts of the Project in README with clear instructions on why, what, and how
- If applicable, write tests (end-to-end tests, unit tests) or at least provide instructions on how to test the code and what the output should be - see [Code Testing](./code_testing.md) for more information

#### 7. Create and submit a GitHub Pull Request

<a name="7-create-and-submit-a-github-pull-request"></a>

- PRs can be drafted, reviewed, commented on, deleted, merged, and shared
- Keep the PR small
    - It's easier to review 100 lines of code than 1000 lines of code
    - The more lines of code, the more difficult it is for the Reviewer to understand and review the code
    - Large PRs slow down the CR, increase the number of overlooked errors, and decrease morale
- You can also make a `Draft` PR request right at the time when you start working on a feature/subtask
    - It helps with keeping track of your open PRs (don't forget to assign yourself to the PR) if you have to switch between different projects
    - If that's the case, don't forget to mark the PR as *Draft* and use the `Draft:` prefix in the PR title
- Don't forget to assign yourself to the PR so you are notified about the CR comments.
- Give your PR the right title and commit message as described in [GitHub Best Practices - Pull Request](./github_best_practices.md#pull-request)

#### 8. Ask for a Code Review (either a randomly selected person or a specific person)

- Requesting a Code Review from a colleague ensures that your code is checked for potential improvements and errors
- Avoid asking "*Can anyone look at my PR, please*?" - be specific
- **At least one person** has to be assigned as a **Reviewer**
- You can assign everyone as a Reviewer, but still choose one as the primary
    - Everyone is notified about the comments, changes, etc., and can react to them if they know the answer/solution
    - Anyone can unsubscribe at any time
- Avoid adding changes to the PR once you request the Code Review - it is difficult for the Reviewer to review code that keeps changing
    - If you must change the code, inform the Reviewer that you will add more changes
- Some more info on GitHub Pull Requests and how to request a CR [here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/requesting-a-pull-request-review)
- More details about the CR can be found in [GitHub Best Practices/Pull Request Review as a Developer](./github_best_practices.md#pull-request-review-as-a-developer)

#### 9. The Reviewer asks questions about the code or makes suggestions

- This step involves a detailed examination of the code, with the Reviewer providing constructive feedback
    - Reviewer reads the Project description, tests the code, adds comments or suggestions
- **Prefer Suggestions over Comments** whenever possible (see [GitHub Comments vs. Suggestions](#github-comments-vs-suggestions) below)
- Comments and Suggestions should be on point and constructive
- The Reviewer can ask questions if they don't understand the code implementation or the *flow*
    - Code following the best practices with tests makes this much easier for the Reviewer
- Once done with the Review, the Reviewer informs the Developer so it's clear that this step of the Review is done
- Align with the Reviewer if you want to start implementing suggestions while the Review is still in progress for the same reasons as in point no. 7
- More details about the CR can be found in [GitHub Best Practices/Pull Request Review as a Reviewer](./github_best_practices.md#pull-request-review-as-a-reviewer)

##### How to Comment on the PR

1. **On GitHub as part of the PR** - visible for everyone, traceable, and least personal

- **Pros**:
    - Other people can see the comments and react
    - Easy to track the changes and resolve once implemented
    - The history is recorded, and we can always go back
    - Everybody can learn from the comments
    - You can use Suggestions that can be automatically applied to the code and committed directly from GitHub
- **Cons**:
    - People might be shy and might not feel comfortable with everyone seeing comments on their code
    - Might sometimes sound harsher than intended (no language *tone* feeling from the text) - be respectful

2. **On Teams (DM)** – only one person can see it​; somehow personal

- **Pros**:
    - Personal and confidential​
    - Might feel less stressful and more private
- **Cons**:
    - Nobody can see what the CR process was, what the changes were, and why
    - Other people cannot contribute
    - The history is very limited
    - All the changes have to be manual (no Suggestions)
    - It can lead to fragmented communication if multiple reviewers are involved

3. **Personal discussion** – only one person can hear it​; very personal

- **Pros**:
    - Very personal
    - One-on-one discussion might bring clarity faster
- **Cons**:
    - No history at all
    - Might be more time-consuming
    - More difficult to schedule
    - It can lead to fragmented communication if multiple reviewers are involved
- **Note:** Document key decisions in the PR comments for both On Teams (DM) and Personal discussion for future references

##### GitHub Comments vs Suggestions

- **Comments** are general questions or queries on the code, structure, formatting, etc.
- **Suggestions** are direct *proposals* on how to change the code and what to implement
- It is best to put even general comments as *code comments* because this is the only way one can react to the comments, track them, and resolve them
- Some more info [here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/commenting-on-a-pull-request), [here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/reviewing-proposed-changes-in-a-pull-request) and [here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/approving-a-pull-request-with-required-reviews).

##### General Comments on PR vs Comments on Code

Commenting on the PR in different tabs triggers different actions. Comments in the `Conversation` tab are considered general comments and do not require the Reviewer's resolution. It is not possible to add an answer to these comments directly (only as another general comment). Comments to the `Files changed` tab must be resolved before the PR merge. These comments allow the Developer (or anybody else) to add a direct reply. Comments in the `Review changes` (as part of the submitted Review) are considered in the same way as in the `Conversation` tab and don't require resolving.

To summarize:

- `Conversation` tab: General PR comments (no action required)
- `Files changed` tab: Comments and suggestions to code that always trigger or require an action
- `Files changed` tab -> `Review changes` -> `Comment` is similar to a general PR comment
- `Files changed` tab -> `Review changes` -> `Approve` is similar to a general PR comment

#### 10. Implement suggestions/discuss the PR comments

- Same as in point no. 8 - reacting to comments and/or suggestions can be either done on GitHub, Teams, or in person, and the same rules apply here as well
    - For GitHub discussions - addressing the feedback collaboratively helps improve the code and ensures that all team members are on the same page
- Code Suggestions from the Reviewer can be implemented at once instead of doing it one-by-one by adding them to a batch - *Add suggestion to batch*
    - This also adds the Reviewer as the author of the changes for future references
- More info about how to incorporate suggestions in the PR [here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/incorporating-feedback-in-your-pull-request)
- Inform the Reviewer once you implement all the changes
    - The Reviewer resolves the threads or adds more comments if not satisfied
    - **The threads should be only resolved by the Reviewer** (~creator) of the thread
- Don't forget to `git pull` locally once you apply the suggestions on GitHub or use GitHub's *edit/commit functionality*!

#### 11. Re-request the Review, inform the Reviewer, and repeat until done

- Iterative Reviews ensure that all feedback is addressed and the code meets the required standards
- Repeat as many times as necessary, following the same steps as described above

#### 12. Reviewer approves the PR

- Once the Reviewer is happy with the changes, they can approve the PR, indicating that the code is ready to be merged
- All the open threads/comments/suggestions should be closed
- Technically, anyone can approve the PR, **but** the author(s) of the code
    - This ensures we used the **Second Set of Eyes** principle

#### 13. Publish the code by merging it into the target branch

- Merging the approved code into the target branch makes it part of the main codebase, ready for deployment or further development
- **The merge should only be done by the author of the PR**
- Don't forget to `git checkout <target_branch>` and `git pull` locally once you merge the PR!

#### 14. Close the ticket and repeat until the Project is finished, and close the Project

- Happy Code Review!

### How to do a Good Code Review

#### As a Reviewer

- **Foster a positive feedback culture**: Encourage constructive criticism and appreciate good practices to create a supportive environment
- **Comment on the code, not the person**: Focus on the code's quality and functionality, avoiding personal remarks
- **Give objective reasons for the comments**: Provide clear, logical explanations for your feedback to help the Developer understand your perspective
- **Make suggestions or point out useful resources**: Offer practical advice or direct the Developer to helpful documentation or examples
- **Remember, there are always multiple solutions to the same problem**: Be open to different approaches and consider the Developer's reasoning
- **Discuss with an open mind - support open discussion**: Engage in a dialogue to explore various viewpoints and reach the best solution

#### As a Developer

- **Don't take the comments personally**: Understand that feedback aims to improve the code, not criticize you
- **The main goal of CR is to improve the code for everyone**: Keep the focus on enhancing the Project and learning from the feedback
- **Discuss, agree, implement, test**: Collaborate with the Reviewer to address comments, make necessary changes, and ensure the code works as intended. Even Reviewers might make mistakes

#### As Both

- **The discussion goes both ways**: Encourage a two-way conversation where both parties can share insights and learn from each other
- **Use the Review to learn new things and improve**: Treat the Review process as an opportunity for growth and skill development
- **Get a third-person opinion if you cannot devise a compromise**: Involve another team member to mediate and provide a fresh perspective if disagreements arise
- **Make the Review your priority**: Prioritize the Review process to keep the Project moving forward efficiently
