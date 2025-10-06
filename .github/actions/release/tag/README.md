# Tag
Action: [tag](action.yml)

Create a tag

## Inputs
| Name                       | Description                          | Required | Default |
|----------------------------|--------------------------------------|----------|---------|
| `ssh-private-key`          | The private SSH key                  | true     |         |
| `ssh-private-key-password` | The password for the private SSH key | true     |         |
| `tag`                      | Tag value                            | true     |         |

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
          ssh-private-key: "${{ secrets.SSH_PRIVATE_KEY }}"
          ssh-private-key-password: "${{ secrets.SSH_PRIVATE_KEY_PASSWORD }}"
          tag: v1.0.0
```