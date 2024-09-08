# Upload Tar Artifact
Action: [upload](./action.yml)

The Upload Tar Artifact action compresses specified files or directories into a .tar archive and uploads the artifact, ensuring that file permissions are preserved. This is useful when file privileges need to remain intact across different environments or workflows. The action also allows specifying the artifact name, overwrite settings, and retention days.

## Outputs
| Name             | Description                                                                                                     | Required | Default |
|------------------|-----------------------------------------------------------------------------------------------------------------|----------|---------|
| `name`           | The name of the artifact.                                                                                       | true     |         |
| `overwrite`      | Whether to overwrite an existing artifact with the same name.                                                   | false    | true    |
| `path`           | A file, directory, or wildcard pattern describing what to upload. The file structure will be preserved via tar. | true     |         |
| `retention-days` | The number of days after which the artifact will expire. 0 uses the default retention. Min: 1, Max: 90 days.    | false    |         |

## Example
```yaml
jobs:
  upload-artifact:
    name: Upload Artifact 
    runs-on: ubuntu-latest
    steps:
      - name: Publish artifact
        uses: cupel-co/actions/.github/actions/artifact/upload@vX.X.X
        with:
          name: artifact
          overwrite: true
          path: ./
          retention-days: 1
```
