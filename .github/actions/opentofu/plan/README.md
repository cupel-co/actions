# OpenTofu Plan
Action: [plan](./action.yml)

The OpenTofu Plan GitHub Action installs a specific version of OpenTofu, initializes the infrastructure with custom arguments, selects or creates a workspace, and generates a plan file. If specified, it can upload the plan file as an artifact. The action supports flexible inputs such as additional arguments for init and plan commands, custom working directories, and backend settings.

## Inputs
| Name                  | Description                                                                                         | Required | Default Value         |
|-----------------------|-----------------------------------------------------------------------------------------------------|----------|-----------------------|
| `artifact-name`       | The name of the artifact to publish, including the plan file. No artifact uploaded if not provided. | false    | N/A                   |
| `init-args`           | Additional arguments for the `init` command.                                                        | false    | N/A                   |
| `plan-args`           | Additional arguments for the `plan` command.                                                        | false    | N/A                   |
| `use-primary-backend` | Flag to indicate if the primary backend should be used.                                             | true     | `'true'`              |
| `version`             | The version of OpenTofu to install.                                                                 | true     | `'1.8.1'`             |
| `working-directory`   | Directory containing the OpenTofu code.                                                             | true     | `'./infrastructure'`  |
| `workspace`           | The name of the workspace. If it doesn't exist, it will be created.                                 | true     | N/A                   |

## Example
```yaml
jobs:
  plan:
    name: Plan opentofu-aws-backend
    runs-on: ubuntu-latest
    concurrency:
      cancel-in-progress: false
      group: opentofu-aws-backend
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          fetch-tags: true
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v3
        with:
          role-to-assume: ${{ vars.OIDC_ROLE_ARN }}
          aws-region: ap-southeast-2
      - name: Plan
        uses: cupel-co/platform-opentofu-aws-backend/.github/actions/opentofu/plan@vx.x.x
        with:
          artifact-name: 'opentofu-aws-backend'
          init-args: '-var-file="variables/platform.tfvars"'
          plan-args: '-var-file="variables/platform.tfvars"'
          use-primary-backend: ${{ vars.OPENTOFU_USE_PRIMARY_BACKEND }}
          workspace: cicd-platform
```
