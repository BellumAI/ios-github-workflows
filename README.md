# iOS Shared GitHub Workflows
Repository for shared iOS Github Workflows

## Deployment Notes

The starter files reference a tag on this repository. If you need to modify the shared workflow but continue using it in other projects, replace the `v1` tag with one pointing at the latest commit.

## Usage in Swift Package Repositories

1. Create a new branch to add the shared workflows
2. Copy the contents of `spm-starters` directory to `.github/workspaces/` in the git repository.
3. Edit `pr-checks.yml` in the repository:
    1. Replace `ProjectNameHere` with the `Package` `name` from the package's Package.swift.
    2. If desired, uncomment and edit the default values from `code-coverage-required` and `code-coverage-exclude`.
4. Edit `push.yml` in the repository and replace `ProjectNameHere` with the `Package` `name` from the package's Package.swift.
    1. Replace `ProjectNameHere` with the `Package` `name` from the package's Package.swift.
    2. If you changed `code-coverage-required` and/or `code-coverage-exclude` in `pr-checks.yml` make the same changes in `push.yml`.
    3. If desired, uncomment and edit the default values from `code-coverage-warning`.
5. If you're using SonarQube make sure a `sonar-project.properties` file is created with an appropriate `projectKey` and checked-in to the repo. If you're not using SonarQube, delete the `sonarqube-check.yml` file.
5. Commit and Push your changes to the remote. 
6. Open a PR for your changes - This will trigger the `SonarQube Check` and `Swift Package PR Checks` workflows to run. Let them finish, they may or may not be successful.
7. Request review(s) for the PR. 
8. Upon approval, merge it, ignoring the results of any failed checks at this time. (You may need an admin override to merge.) This will trigger the `push.yml` workflow.
9. When the `Swift Package Push to Main Publish Coverage` workflow completes successfully the `gh-pages` should now exist, and it should contain the `coverage.json` file that makes the `pr-checks.yml` workflow work.
10. Configure GitHub Pages:
    1. Go to the repository settings.
    2. Select "Pages" from the left nav.
    3. Leave "Source" set to "Deploy from branch"
    4. Set the "Branch" to the `gh-pages` branch and root, and hit Save.
    5. Verify that the report has been published by visiting `https://bellumai.github.io/{repo-name}/coverage-table.txt`.
11. Edit the project's README.md and add the following line immediately after the title:

``` markdown
[![Test Coverage](https://github.com/BellumAI/{repo-name}/blob/gh-pages/coverage-badge.svg?raw=true)](https://bellumai.github.io/{repo-name}/coverage-table.txt)
```
    
Where `{repo-name}` is the github name of the repo. E.g. `ios-core`.
