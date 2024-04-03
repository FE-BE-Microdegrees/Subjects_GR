# Git and Github Best Practices

In this topic, we'll learn about best practices for using Git and GitHub. We'll explore the best practices for both Git and GitHub, and learn how to apply them in a software development project.

- [Git and Github Best Practices](#git-and-github-best-practices)
  - [Learning Outcomes](#learning-outcomes)
  - [Git Best Practices:](#git-best-practices)
  - [GitHub Best Practices:](#github-best-practices)
  - [Excercises](#excercises)

## Learning Outcomes

After completing this topic, you'll be able to:

- describe best practices for using Git and GitHub;
- apply Git and GitHub best practices in a software development project.

Using *Git* and *GitHub* effectively involves more than just knowing the commands and tools. Following best practices ensures that the development process is smooth, the project history remains clean, and collaboration among team members is efficient.

Here's an overview of best practices for both Git and GitHub:

## Git Best Practices:

1. **Commit Often, Push Less:** 
   - Make frequent, smaller commits that capture a single logical change (e.g., fixing a bug or adding a feature). This makes it easier to understand the history and isolate problems.
2. **Write Meaningful Commit Messages:** 
   - Start with a short, descriptive title. If more detail is needed, provide a comprehensive description after a blank line.
3. **Use Branches:**
   - Never work directly on the `main` or `master` branch. Use feature branches for each new feature or bugfix.
   - Delete branches after merging them to keep the repo clean.
4. **Avoid Modifying Published History:** 
   - Once commits are pushed to a shared branch, avoid using commands that rewrite history (e.g., `rebase` or `force push`), unless you're certain of what you're doing.
5. **Sync Regularly:** 
   - Frequently `pull` from the main repository to integrate changes and resolve conflicts early.
6. **Resolve Conflicts Promptly:** 
   - Address and resolve merge conflicts as soon as they arise.
7. **Use `.gitignore`:**
   - Add files that shouldn't be in the repository (e.g., build artifacts, cache, log files) to a `.gitignore` file.
8. **Backup:**
   - While Git is a version control system, it’s still a good practice to have backups of your repository, especially if you're hosting it locally.

## GitHub Best Practices:

1. **Use Descriptive Repository Names:** 
   - Names should give a hint about the project’s purpose or content.
2. **Add a `README.md`:**
   - Always include a `README.md` in your repositories. It should explain the project, how to set it up, its dependencies, how to contribute, and other pertinent information.
3. **Utilize Issue Templates and Pull Request Templates:**
   - Templates guide contributors to provide the necessary information when creating issues or PRs.
4. **Protect Your Main Branch:** 
   - Use branch protection rules to ensure that the `main` or `master` branch can't be directly pushed to, and require pull request reviews before merging.
5. **Use Labels and Milestones:** 
   - Organize issues and PRs with labels (e.g., `bug`, `enhancement`). Use milestones to group issues and PRs by feature, version, or timeframe.
6. **Code Reviews:**
   - Always review pull requests before merging. This ensures code quality, consistency, and that multiple eyes have checked the changes.
7. **Engage with the Community:**
   - Respond to issues and PRs in a timely manner. Thank and encourage contributors, even if their contribution isn't accepted.
8. **Use GitHub Actions:**
   - Automate testing, building, and deployment processes using GitHub Actions.
9. **Keep Personal Data Out:**
   - Never store sensitive information like passwords, API keys, or secrets in your repositories. Use GitHub's Secrets feature or external tools like environment variables for this purpose.
10. **Regularly Review Permissions and Access:** 
   - Ensure that only the necessary collaborators have access to your repository, and regularly review and adjust permissions.

By adhering to these best practices, you'll ensure that your Git and GitHub usage is efficient, your project history remains meaningful and organized, and collaboration is smooth and productive.

## Excercises

To practice what you've learned in this topic, do the following:

- Create a new repository on course Github organization.
- Name the repository as `Firstname-Lastname`.
- Add a `README.md` file to the repository.
- Add some description about yourself in the `README.md` file.
- Create a branch named `feature-gitignore`.
- Add a `.gitignore` file to the repository with the following content:

```
# Node
node_modules/
```
- Commit and push your changes to the `feature-gitignore` branch.
- Create a pull request to merge `feature-gitignore` branch to `main` branch.
- Assign your instructor as a reviewer to the pull request.
- Merge the pull request after your instructor approves it.
