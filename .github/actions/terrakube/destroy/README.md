# Terrakube CLI Destroy
Action: [destroy](./action.yml)

Destroys OpenTofu-managed infrastructure using Terrakube as the cloud backend. This action installs OpenTofu, configures Terrakube credentials, initializes the infrastructure, and runs destroy.

## Inputs
| Name                 | Description                                                              | Required | Default Value                  |
|----------------------|--------------------------------------------------------------------------|----------|--------------------------------|
| `init-args`          | Additional arguments for the `init` command.                             | false    |                                |
| `destroy-args`       | Additional arguments for the `destroy` command.                          | false    |                                |
| `version`            | The version of OpenTofu to install.                                      | true     | `1.11.6`                       |
| `working-directory`  | Directory containing the OpenTofu code.                                  | true     | `./infrastructure`             |
| `terrakube-hostname` | The hostname of your Terrakube instance.                                 | true     | `terrakube-api.cicd.cupel.co`  |
| `terrakube-token`    | The API token for authenticating with Terrakube.                         | true     |                                |

## Requirements

Your OpenTofu configuration must include a `cloud` block pointing to Terrakube:

```hcl
terraform {
  cloud {
    hostname     = var.terrakube_hostname
    organization = "your-org"

    workspaces {
      name = "your-workspace"
    }
  }
}

variable "terrakube_hostname" {
  type = string
}
```

The action automatically sets `TF_VAR_terrakube_hostname` so the cloud block can reference it.

## Example
```yaml
jobs:
  destroy:
    name: Destroy Infrastructure
    runs-on: ubuntu-latest
    environment: Production
    concurrency:
      cancel-in-progress: false
      group: terrakube-destroy
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          fetch-tags: true

      - name: Destroy
        uses: cupel-co/actions/.github/actions/terrakube/destroy@vx.x.x
        with:
          init-args: '-var-file="variables/platform.tfvars"'
          destroy-args: '-var-file="variables/platform.tfvars"'
          terrakube-token: ${{ secrets.TERRAKUBE_TOKEN }}
```

## Notes

- **Approval workflow**: Terrakube controls the approval flow based on your workspace settings. Destroy operations may require manual approval in the Terrakube UI.
- **Authentication**: The action uses `setup-opentofu`'s built-in credential handling via `cli_config_credentials_hostname` and `cli_config_credentials_token`.
- **Use with caution**: This action destroys infrastructure. Ensure you have appropriate environment protection rules configured in GitHub.

