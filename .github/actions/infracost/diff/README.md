# Diff
Action: [diff](./action.yml)

Generate a cost difference between the old and new change

## Inputs
| Name                  | Description                                       | Required | Default  |
|-----------------------|---------------------------------------------------|----------|----------|
| `api-key`             | Infracost API Key                                 | true     |          |
| `base-breakdown-path` | The path to the breakdown file for the base state | true     |          |
| `currency`            | The currency to show estimates in                 | false    | `AUD`    |
| `head-breakdown-path` | The path to the breakdown file for the head state | true     |          |
| `output-path`         | The file path for the JSON file                   | false    |          |
| `version`             | The version of Infracost to install               | false    | `0.10.x` |

## Example
```yaml
jobs:
  diff:
    name: Diff
    runs-on: ubuntu-latest
    steps:
      - name: Diff
        uses: cupel-co/actions/.github/actions/infracost/diff@vX.X.X
        with:
          api-key: "${{ secrets.INFRACOST_API_KEY }}"
          base-breakdown-path: /tmp/main.json
          currency: AUD
          head-breakdown-path: /tmp/feature.json
          output-path: /tmp/diff.json
          version: 0.10.x
```
