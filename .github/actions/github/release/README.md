# Release
Action: [release](./action.yml)

Create a GitHub release from a tag

## Inputs
| Name  | Description | Required | Default |
|-------|-------------|----------|---------|
| `tag` | Tag value   | true     |         |

## Secrets
| Name           | Description                                      | Required |
|----------------|--------------------------------------------------|----------|
| `github.token` | GitHube token. Needs `contents: read` permission | true     |

## Example
```yaml
jobs:
  release:
    name: Release
    runs-on: ubuntu-latest
    steps:
      - name: Create
        uses: cupel-co/actions/.github/actions/github/release@vX.X.X
        with:
          tag: v1.0.0
```
