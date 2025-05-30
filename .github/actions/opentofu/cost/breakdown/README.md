# OpenTofu Cost Breakdown
Action: [breakdown](./action.yml)

Generate a cost breakdown for the specified infrastructure

## Inputs
| Name                | Description                                  | Required | Default            |
|---------------------|----------------------------------------------|----------|--------------------|
| `api-key`           | Infracost API Key                            | true     |                    |
| `currency`          | The currency to show estimates in            | false    | `AUD`              |
| `output-path`       | The file path for the JSON file              | false    | `./infracost.json` |
| `template`          | The infracost template                       | false    |                    |
| `usage`             | The usage file contents                      | false    |                    |
| `version`           | The version of Infracost to install          | false    | `0.10.x`           |
| `working-directory` | The directory containing the OpenTofu code.  | true     | `./infrastructure` |
| `workspace-prefix`  | The prefix for the workspace name            | false    |                    |

## Example
```yaml
jobs:
  generate:
    name: Generate
    runs-on: ubuntu-latest
    steps:
      - name: Breakdown
        uses: cupel-co/actions/.github/actions/opentofu/cost/breakdown@vX.X.X
        with:
          api-key: "${{ secrets.INFRACOST_API_KEY }}"
          currency: AUD
          output-path: /tmp/infracost.json
          template: |
            version: 0.1
            projects:
            {{- range `$project := matchPaths "variables/:env.tfvars" }}
            - path: "./"
              name: "github-{{ `$project.env }}"
              terraform_workspace: "github-{{ `$project.env }}"
              terraform_var_files:
                - "{{ relPath "./" `$project._path }}"
              dependency_paths:
                - "**"
                - "{{ relPath "./" `$project._path }}"
            {{- end }}
          version: 0.10.x
```
