# Terrakube CLI Apply
Action: [apply](./action.yml)

Applies OpenTofu changes using Terrakube as the cloud backend. This action installs OpenTofu, configures Terrakube credentials, initializes the infrastructure, and runs apply.

## Inputs
| Name                 | Description                                                              | Required | Default Value                 |
|----------------------|--------------------------------------------------------------------------|----------|-------------------------------|
| `init-args`          | Additional arguments for the `init` command.                             | false    |                               |
| `apply-args`         | Additional arguments for the `apply` command.                            | false    |                               |
| `version`            | The version of OpenTofu to install.                                      | true     | `1.11.6`                      |
| `working-directory`  | Directory containing the OpenTofu code.                                  | true     | `./infrastructure`            |
| `terrakube-hostname` | The hostname of your Terrakube instance.                                 | true     | `terrakube-api.cicd.cupel.co` |
| `terrakube-token`    | The API token for authenticating with Terrakube.                         | true     |                               |

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
  apply:
    name: Apply Infrastructure
    runs-on: ubuntu-latest
    environment: Production
    concurrency:
      cancel-in-progress: false
      group: terrakube-apply
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          fetch-tags: true

      - name: Apply
        uses: cupel-co/actions/.github/actions/terrakube/apply@vx.x.x
        with:
          init-args: '-var-file="variables/platform.tfvars"'
          apply-args: '-var-file="variables/platform.tfvars"'
          terrakube-token: ${{ secrets.TERRAKUBE_TOKEN }}
```

## Notes

- **Approval workflow**: The action does not use `-auto-approve`. Terrakube controls the approval flow based on your workspace settings (auto-apply or manual approval via Terrakube UI).
- **Authentication**: The action uses `setup-opentofu`'s built-in credential handling via `cli_config_credentials_hostname` and `cli_config_credentials_token`.
- **Cost estimation and security scanning**: Configure these in your Terrakube workspace template. They run server-side as part of the Terrakube workflow.
