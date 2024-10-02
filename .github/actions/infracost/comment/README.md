# Comment
Action: [breakdown](./action.yml)

Add a comment to a GitHub PR

## Inputs
| Name        | Description                         | Required | Default  |
|-------------|-------------------------------------|----------|----------|
| `api-key`   | Infracost API Key                   | true     |          |
| `behaviour` | The behaviour for the comment       | true     | `update` |
| `currency`  | The currency to show estimates in   | false    | `AUD`    |
| `path`      | The path to the JSON report file    | true     |          |
| `version`   | The version of Infracost to install | false    | `0.10.x` |

## Example
```yaml
jobs:
  comment:
    name: Comment
    runs-on: ubuntu-latest
    steps:
      - name: Comment
        uses: cupel-co/actions/.github/actions/infracost/comment@vX.X.X
        with:
          api-key: "${{ secrets.INFRACOST_API_KEY }}"
          base-breakdown-path: /tmp/main.json
          currency: AUD
          head-breakdown-path: /tmp/feature.json
          output-path: /tmp/diff.json
          version: 0.10.x
```
