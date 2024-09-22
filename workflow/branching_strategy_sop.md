# Standard Operating Procedure (SOP) for Branching Strategy

## 1. Purpose
This SOP defines the standardized branching strategy for version control to ensure consistent and efficient development workflows. A well-defined branching strategy facilitates collaboration, simplifies integration, and maintains codebase stability throughout the development lifecycle.

## 2. Scope
This procedure applies to all developers and team members involved in writing, reviewing, and deploying code within the organization’s projects. It covers the creation, management, and merging of branches in the version control system (e.g., Git).

## 3. Definitions
- **Main Branch**: The primary branch where the source code of HEAD always reflects a production-ready state. Commonly named `main` or `master`.
- **Develop Branch**: A branch from which feature branches are created and into which feature branches are merged. It reflects the latest delivered development changes for the next release.
- **Feature Branch**: A short-lived branch created from the develop branch to develop a specific feature or fix a bug.
- **Release Branch**: A branch created from the develop branch when the develop branch has acquired enough features for a release. It allows for final testing and bug fixing before the release.
- **Hotfix Branch**: A branch created from the main branch to quickly address critical issues in the production codebase.
- **Pull Request (PR)**: A request to merge code changes from one branch into another, typically reviewed by peers before integration.

## 4. Responsibilities
- **Developers**:
  - Follow the branching strategy for all code changes.
  - Create feature branches for new features or bug fixes.
  - Ensure timely merging of branches following code reviews.
- **Project Leads**:
  - Oversee the implementation of the branching strategy.
  - Ensure that branches are managed correctly and merged appropriately.
- **Reviewers**:
  - Review pull requests to ensure compliance with the branching strategy.
  - Approve or request changes for pull requests as necessary.

## 5. Procedure

### 5.1. Branch Types and Naming Conventions
1. **Main Branch (`main` or `master`)**:
   - Reflects the production-ready state.
   - Direct commits to this branch are restricted and require pull requests.

2. **Develop Branch (`develop`)**:
   - Integration branch for features.
   - Regularly updated with feature branches.

3. **Feature Branches (`feature/<feature-name>`)**:
   - Created from the develop branch.
   - Naming convention: `feature/<descriptive-name>`
   - Example: `feature/user-authentication`

4. **Release Branches (`release/<version-number>`)**:
   - Created from the develop branch when preparing for a new release.
   - Naming convention: `release/<version-number>`
   - Example: `release/1.2.0`

5. **Hotfix Branches (`hotfix/<issue-number>`)**:
   - Created from the main branch to address critical bugs.
   - Naming convention: `hotfix/<issue-number>`
   - Example: `hotfix/urgent-payment-bug`

### 5.2. Creating a Feature Branch
1. **From Develop**: Ensure you are on the develop branch.
   ```bash
   git checkout develop
   git pull origin develop
   ```
2. **Create Branch**:
   ```bash
   git checkout -b feature/<feature-name>
   ```
3. **Develop Feature**: Implement the feature and commit changes.
4. **Push Branch**:
   ```bash
   git push origin feature/<feature-name>
   ```
5. **Create Pull Request**: Submit a pull request to merge the feature branch into develop.

### 5.3. Merging Feature Branches
1. **Code Review**: Ensure the pull request is reviewed and approved by at least one team member.
2. **Resolve Conflicts**: Address any merge conflicts before merging.
3. **Merge**: Merge the feature branch into develop.
4. **Delete Branch**: After successful merge, delete the feature branch from the remote repository.
   ```bash
   git push origin --delete feature/<feature-name>
   ```

### 5.4. Creating a Release Branch
1. **From Develop**: Ensure you are on the develop branch with all features merged.
   ```bash
   git checkout develop
   git pull origin develop
   ```
2. **Create Release Branch**:
   ```bash
   git checkout -b release/<version-number>
   ```
3. **Prepare Release**:
   - Update version numbers.
   - Perform final testing and bug fixes.
4. **Push Branch**:
   ```bash
   git push origin release/<version-number>
   ```
5. **Create Pull Request**: Submit a pull request to merge the release branch into both main and develop.

### 5.5. Merging Release Branches
1. **Code Review**: Ensure the pull request is reviewed and approved by team members.
2. **Merge into Main**: Merge the release branch into the main branch.
3. **Tag Release**:
   ```bash
   git checkout main
   git pull origin main
   git tag -a v<version-number> -m "Release version <version-number>"
   git push origin v<version-number>
   ```
4. **Merge into Develop**: Merge any changes from the release branch back into develop.
5. **Delete Branch**: After successful merge, delete the release branch from the remote repository.

### 5.6. Creating a Hotfix Branch
1. **From Main**: Ensure you are on the main branch.
   ```bash
   git checkout main
   git pull origin main
   ```
2. **Create Hotfix Branch**:
   ```bash
   git checkout -b hotfix/<issue-number>
   ```
3. **Implement Fix**: Address the critical issue and commit changes.
4. **Push Branch**:
   ```bash
   git push origin hotfix/<issue-number>
   ```
5. **Create Pull Request**: Submit a pull request to merge the hotfix branch into both main and develop.

### 5.7. Merging Hotfix Branches
1. **Code Review**: Ensure the pull request is reviewed and approved promptly.
2. **Merge into Main**: Merge the hotfix branch into the main branch.
3. **Tag Hotfix**:
   ```bash
   git checkout main
   git pull origin main
   git tag -a v<new-version-number> -m "Hotfix version <new-version-number>"
   git push origin v<new-version-number>
   ```
4. **Merge into Develop**: Merge the hotfix branch into develop to ensure the fix is included in future releases.
5. **Delete Branch**: After successful merge, delete the hotfix branch from the remote repository.

## 6. Best Practices
- **Descriptive Naming**: Use clear and descriptive names for branches to convey purpose.
- **Small Commits**: Make frequent, small commits with meaningful messages.
- **Regular Syncing**: Regularly pull changes from the parent branch to minimize merge conflicts.
- **Code Reviews**: Always have code reviewed before merging to maintain code quality.
- **Automated Testing**: Implement automated tests to validate changes before merging.

## 7. References
- [Codebase Generation SOP](workflow/codebase_generation_sop.md)
- [Code Review SOP](workflow/SOP_code_review.md)
- [Release Management SOP](workflow/release_management_sop.md)
- [Testing SOP](workflow/testing_sop.md)
- [ChatGPT Codegen Workflow](workflow/chatgpt_codegen_workflow.md)
- [Use Case Checklist](checklists/usecasechecklist.md)
- [Standardized Code Checklist](checklists/standardized_code_checklist.md)

## 8. Revision History

| Version | Date       | Author      | Description              |
|---------|------------|-------------|--------------------------|
| 1.0     | 2024-04-27 | P. Tolbert  | Initial creation of SOP  |
| 1.1     | YYYY-MM-DD | Your Name   | [Description of changes] |
