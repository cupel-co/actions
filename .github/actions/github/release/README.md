# Release
Action: [release](./action.yml)

Create a GitHub release from a tag

## Inputs
| Name    | Description                            | Required | Default |
|---------|----------------------------------------|----------|---------|
| `files` | Files to include in GitHub Release     | false    |         |
| `tag`   | Tag value                              | true     |         |
| `token` | GitHub Token to use. This can be a PAT | true     |         |

## Example
```yaml
jobs:
  release:
    name: Release
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Create
        uses: cupel-co/actions/.github/actions/github/release@vX.X.X
        with:
          tag: v1.0.0
          token: ${{ github.token }}
```
