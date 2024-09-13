# Create Tag
Action: [tag](./action.yml)

Create a tag

## Inputs
| Name  | Description | Required | Default |
|-------|-------------|----------|---------|
| `tag` | Tag value   | true     |         |

## Secrets
| Name                                  | Description                                       | Required |
|---------------------------------------|---------------------------------------------------|----------|
| `github.token`                        | GitHube token. Needs `contents: write` permission | true     |
| `secrets.GH_GPG_PRIVATE_KEY`          | GPG key for signing requests                      | true     |
| `secrets.GH_GPG_PRIVATE_KEY_PASSWORD` | Password for GPG key                              | true     |

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
        uses: cupel-co/actions/.github/actions/github/tag@vX.X.X
        with:
          tag: v1.0.0
```
