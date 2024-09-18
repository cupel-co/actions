# Generate Semantic Version
Action: [generate](./action.yml)

The Generate Semantic Version GitHub Action uses GitVersion to generate semantic versioning information for a project. It calculates and outputs detailed versioning components such as major, minor, patch, pre-release tags, build metadata, and commit information. The action ensures that versioning is automatically derived based on Git history, which can then be used for various purposes like tagging releases or setting version numbers in a project.

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
