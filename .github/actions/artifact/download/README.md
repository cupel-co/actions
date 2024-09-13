# Download Tar Artifact
Action: [download](./action.yml)

The Download Tar Artifact action retrieves an artifact previously uploaded via the Upload Tar Artifact action, extracts the contents from the .tar archive, and restores the original file structure and permissions. It is useful for workflows where artifacts need to be transferred between jobs or workflows with file privileges intact.

## Inputs
| Name   | Description                                           | Required | Default |
|--------|-------------------------------------------------------|----------|---------|
| `name` | The name of the artifact to download.                 | true     |         |
| `path` | The destination directory where the artifact is saved | true     |         |

## Example
```yaml
jobs:
  download-artifact:
    name: Download Artifact
    runs-on: ubuntu-latest
    steps:
      - name: Publish artifact
        uses: cupel-co/actions/.github/actions/artifact/download@vX.X.X
        with:
          name: artifact
          path: ./
```
