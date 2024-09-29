# Generate Semantic Version
Action: [generate](./action.yml)

The Generate Semantic Version GitHub Action uses GitVersion to generate semantic versioning information for a project. It calculates and outputs detailed versioning components such as major, minor, patch, pre-release tags, build metadata, and commit information. The action ensures that versioning is automatically derived based on Git history, which can then be used for various purposes like tagging releases or setting version numbers in a project.

## Commit Messages
Commit messages need to follow [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/#specification). The commits are used to generate the semantic version. Breaking changes MUST be indicated in the footer AND by appending a ! after the type/scop.

| Type     | Category                 | Explanation                                                                                                 | Major              | Minor              | Patch              |
|----------|--------------------------|-------------------------------------------------------------------------------------------------------------|--------------------|--------------------|--------------------|
| build    | Builds                   | Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)         | :x:                | :x:                | :white_check_mark: |
| chore    | Chores                   | Other changes that don't modify src or test files                                                           | :x:                | :x:                | :white_check_mark: |
| ci       | Continuous Integrations  | Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs) | :x:                | :x:                | :white_check_mark: |
| docs     | Documentation            | Documentation only changes                                                                                  | :x:                | :x:                | :white_check_mark: |
| feat     | Features                 | A new feature                                                                                               | :white_check_mark: | :white_check_mark: | :x:                |
| fix      | Bug Fixes                | A bug fix                                                                                                   | :white_check_mark: | :x:                | :white_check_mark: |
| perf     | Performance Improvements | A code change that improves performance                                                                     | :white_check_mark: | :x:                | :white_check_mark: |
| refactor | Code Refactoring         | A code change that neither fixes a bug nor adds a feature                                                   | :white_check_mark: | :x:                | :white_check_mark: |
| revert   | Reverts                  | Reverts a previous commit                                                                                   | :white_check_mark: | :white_check_mark: | :x:                |
| style    | Styles                   | Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)      | :x:                | :x:                | :white_check_mark: |
| test     | Tests                    | Adding missing tests or correcting existing tests                                                           | :x:                | :x:                | :white_check_mark: |

The commit message must follow the format noted below:
```
<type>[(optional <scope>)][optional !]: <description>

[optional <body>]

[optional <footer(s)>]
```
> [!CAUTION]  
> Commits that do not follow the format above cannot be pushed to GitHub.

## Inputs
| Name        | Description                        | Required | Default Value |
|-------------|------------------------------------|----------|---------------|
| `flow-type` | The flow type to use (GITHUB_FLOW) | true     | `GITHUB_FLOW` | 

## Outputs
| Name                           | Description                              |
|--------------------------------|------------------------------------------|
| `major`                        | The Major value                          |
| `minor`                        | The Minor value                          |
| `patch`                        | The Patch value                          |
| `pre-release-tag`              | The prerelease tag value                 |
| `pre-release-tag-with-dash`    | The prerelease tag with dash value       |
| `pre-release-label`            | The prerelease label value               |
| `pre-release-number`           | The prerelease number value              |
| `weighted-pre-release-number`  | The weighted prerelease number value     |
| `build-meta-data`              | The build metadata value                 |
| `full-build-meta-data`         | The full build metadata value            |
| `major-minor-patch`            | The major-minor-patch value              |
| `sem-ver`                      | The semantic version value               |
| `assembly-sem-ver`             | The assembly semantic version value      |
| `assembly-sem-file-ver`        | The assembly file semantic version value |
| `full-sem-ver`                 | The full semantic version value          |
| `informational-version`        | The informational version value          |
| `branch-name`                  | The branch name value                    |
| `escaped-branch-name`          | The escaped branch name value            |
| `sha`                          | The sha value                            |
| `short-sha`                    | The short sha value                      |
| `version-source-sha`           | The version source sha value             |
| `commits-since-version-source` | The commits since version source value   |
| `uncommitted-changes`          | The uncommitted changes value            |
| `commit-date`                  | The commit date value                    |

## Example
```yaml
jobs:
  generate-version:
    name: Generate Version
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          fetch-tags: true
      - name: Generate version
        id: generate
        uses: cupel-co/actions/.github/actions/version/generate@vX.X.X
        with:
          
```
