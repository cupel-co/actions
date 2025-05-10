# Release
Action: [release](action.yml)

Create a GitHub release from a tag

## Inputs
| Name    | Description                                                                   | Required | Default |
|---------|-------------------------------------------------------------------------------|----------|---------|
| `files` | Files to include in GitHub Release                                            | false    |         |
| `tag`   | Tag value                                                                     | true     |         |
| `token` | Token for GHA. This must be a PAT or the release events will not be triggered | true     |         |

## Outputs
| Name      | Description                 |
|-----------|-----------------------------|
| `changes` | The changes for the release |

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
          token: ${{ secrets.GHA_PAT }}
```