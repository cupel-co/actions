# Create Tag
Action: [tag](./action.yml)

Create a tag

## Inputs
| Name           | Description                  | Required | Default |
|----------------|------------------------------|----------|---------|
| `gpg-key`      | The GPG key.                 | true     |         |
| `gpg-password` | The password for the GPG key | true     |         |
| `tag`          | Tag value                    | true     |         |

## Secrets
| Name            | Description                                       | Required |
|-----------------|---------------------------------------------------|----------|
| `github.token`  | GitHube token. Needs `contents: write` permission | true     |

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
          gpg-key: "${{ secrets.GH_GPG_KEY }}"
          gpg-password: "${{ secrets.GH_GPG_KEY_PASSWORD }}"
          tag: v1.0.0
```
