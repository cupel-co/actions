# OpenTofu Plan
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
  generate-version:
    name: Generate Version
    runs-on: ubuntu-latest
    steps:
      - name: Publish ${{ inputs.artifact-name }}
        if: ${{ inputs.artifact-name != '' }}
        uses: cupel-co/actions/artifact/upload@v0.5.0
        with:
          name: ${{ inputs.artifact-name }}
          overwrite: true
          path: ${{ inputs.working-directory }}
          retention-days: 1
```
