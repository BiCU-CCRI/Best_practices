# Best Coding Practices and Code Review

## Introduction

This documentation aims to standardize coding practices, improve code quality, and streamline collaboration within the Bioinformatics Core Unit (BiCU) at St. Anna CCRI and with its collaborators.

It serves as a practical guideline for existing and new BiCU members. It is focused on but not limited to best coding practices in bioinformatics.

The documentation describes:

- [Best Coding Practices](./best_coding_practices.md): outlines the standards and guidelines for writing clean, efficient, and maintainable code.
- [Repository Structure](./repository_structure.md): describes the repository's organization of files and directories within the repository to ensure consistency between projects and developers.
- [Code Reproducibility](./code_reproducibility.md): provides guidelines on code reproducibility in different environments.
- [Code Review](./code_review.md): explains the process and best practices for Code Review.
- [Code Testing](./code_testing.md): covers the methods and tools for code testing.
- [GitHub Best Practices](./github_best_practices.md): offers guidelines for using GitHub effectively and efficiently. It primarily focuses on structuring tasks, commits, and pull requests. Contains some guidelines for `git` best practices.
- [GitHub setup](github_setup.md): provides instructions on setting up GitHub for your projects and repositories, including initial configuration and settings.

## Glossary

- There are some differences between naming things in *regular* code development environment and on GitHub
    - **Note: **[GitLab](https://about.gitlab.com/) is more consistent with the standard development jargon
- The following terms are interchangeable:
    - **Ticket** – GitHub Project Item; turns into GitHub Issue when assigned to a Repository; A general description for a task (Feature, Subtaks, ...).
    - **Issue** - GitHub Issue; a general *task* that can be worked on or *instructions* on how to achieve something. GitHub uses Issues and Sub-issues.
    - **Merge Request** - GitHub Pull Request; PR; request to merge a development branch code into a parent branch
    - **Code Review** - CR; a process of reviewing the code by your peers
    - **`main` branch** - sometimes called `default` or `production` branch; somethimes called `master` in the past
