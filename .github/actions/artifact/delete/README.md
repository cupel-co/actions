# Delete Artifact
Action: [delete](./action.yml)

Delete the specified artifact.

## Inputs
| Name   | Description               | Required | Default |
|--------|---------------------------|----------|---------|
| `name` | The name of the artifact. | true     |         |

## Example
```yaml
jobs:
  delete-artifact:
    name: Delete Artifact 
    runs-on: ubuntu-latest
    steps:
      - name: Delete
        uses: cupel-co/actions/.github/actions/artifact/delete@vX.X.X
```
