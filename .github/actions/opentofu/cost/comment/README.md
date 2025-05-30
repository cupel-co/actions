# OpenTofu Cost Comment
Action: [breakdown](./action.yml)

Add a comment to a GitHub PR

## Inputs
| Name                  | Description                                                         | Required | Default            |
|-----------------------|---------------------------------------------------------------------|----------|--------------------|
| `api-key`             | Infracost API Key                                                   | true     |                    |
| `behaviour`           | The behaviour for the comment                                       | false    | `update`           |
| `comment-identifier`  | A unique identifier to for the comment added by this implementation | false    | `comment`          |
| `currency`            | The currency to show estimates in                                   | false    | `AUD`              |
| `path`                | The path to the JSON report file                                    | true     |                    |
| `pull-request-number` | The PR number                                                       | true     |                    |
| `repository`          | The repository name                                                 | true     |                    |
| `token`               | The GitHub token                                                    | true     |                    |
| `version`             | The version of Infracost to install                                 | false    | `0.10.x`           |
| `working-directory`   | The directory containing the OpenTofu code.                         | true     | `./infrastructure` |

## Example
```yaml
jobs:
  comment:
    name: Comment
    runs-on: ubuntu-latest
    steps:
      - name: Comment
        uses: cupel-co/actions/.github/actions/opentofu/cost/comment@vX.X.X
        with:
          api-key: "${{ secrets.INFRACOST_API_KEY }}"
          behaviour: update
          comment-identifier: comment-production
          currency: AUD
          path: /tmp/diff.json
          pull-request-number: ${{ github.event.number }}
          repository: ${{ github.repository }}
          token: ${{ github.token }}
          version: 0.10.x
```
