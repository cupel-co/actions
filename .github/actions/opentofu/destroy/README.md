# OpenTofu Destroy
Action: [destroy](./action.yml)

The OpenTofu Destroy action automates the process of tearing down infrastructure defined in OpenTofu code. It initializes the OpenTofu environment, selects or creates the necessary workspace, destroys the resources, and optionally deletes the workspace.

## Inputs
| Name                  | Description                                                             | Required | Default            |
|-----------------------|-------------------------------------------------------------------------|----------|--------------------|
| `destroy-args`        | Additional arguments for the `destroy` command.                         | false    |                    |
| `init-args`           | Additional arguments for the `init` command.                            | false    |                    |
| `use-primary-backend` | A flag to indicate whether the primary backend should be used.          | true     | `true`             |
| `version`             | The version of OpenTofu to install.                                     | true     | `1.8.1`            |
| `working-directory`   | The directory containing the OpenTofu code.                             | true     | `./infrastructure` |
| `workspace`           | The workspace name. If the workspace doesn't exist, it will be created. | true     |                    |

## Example
```yaml
jobs:
  destroy:
    name: Destroy opentofu-aws-backend
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
        uses: cupel-co/platform-opentofu-aws-backend/.github/actions/opentofu/destroy@vx.x.x
        with:
          destroy-args: '-var-file="variables/platform.tfvars"'
          init-args: '-var-file="variables/platform.tfvars"'
          use-primary-backend: ${{ vars.OPENTOFU_USE_PRIMARY_BACKEND }}
          workspace: cicd-platform
```
