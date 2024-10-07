# Update PR Description
Action: [update](./action.yml)

Replace template variables in the Pull Request description and then update the description

## Supported Values
| Name                  | Description                                                       |
|-----------------------|-------------------------------------------------------------------|
| `BRANCH_NAME`         | The name of the branch                                            |
| `ENVIRONMENT`         | The environment                                                   |
| `ISSUE_NUMBER`        | The number of the issue                                           |
| `ISSUE_TITLE`         | The title of the issue                                            |
| `PULL_REQUEST_NUMBER` | The number of the pull request                                    |
| `PULL_REQUEST_TITLE`  | The pull request title                                            |
| `REPOSITORY`          | The name of the repository. This includes the the owner name too. | 

## Inputs
| Name          | Description          | Required | Default Value |
|---------------|----------------------|----------|---------------|
| `environment` | The environment name | true     |               |

## Secrets
| Name           | Description                                            | Required |
|----------------|--------------------------------------------------------|----------|
| `github.token` | GitHube token. Needs `pull-requests: write` permission | true     |

## Outputs
| Name          | Description                                       |
|---------------|---------------------------------------------------|
| `description` | The pull request description with replaced values |

## Example
```yaml
jobs:
  update:
    name: Update
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
    concurrency:
      cancel-in-progress: false
      group: pr-update-${{ github.ref_name }}
    steps:
      - name: Update
        uses: cupel-co/actions/.github/actions/pull-request/update@vx.x.x
```
