# Tag
Action: [tag](action.yml)

Create a tag

## Inputs
| Name              | Description                                            | Required | Default |
|-------------------|--------------------------------------------------------|----------|---------|
| `ssh-private-key` | The private SSH key                                    | true     |         |
| `ssh-public-key`  | The public SSH key                                     | true     |         |
| `tag`             | Tag value                                              | true     |         |
| `user-email `     | Email of the user the SSH signing key is registered to | true     |         |
| `user-name`       | Name of the user the SSH signing key is registered to  | true     |         |

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
          ssh-public-key: "${{ secrets.SSH_PUBLIC_KEY }}"
          tag: v1.0.0
          user-email: "${{ secrets.GH_SIGNING_SSH_USER_EMAIL }}"
          user-name: "${{ secrets.GH_SIGNING_SSH_USER_EMAIL }}"
```