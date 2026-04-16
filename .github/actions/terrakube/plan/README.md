# Terrakube CLI Plan
Action: [plan](./action.yml)

Runs an OpenTofu plan using Terrakube as the cloud backend. This action installs OpenTofu, configures Terrakube credentials, initializes the infrastructure, and generates a plan.

## Inputs
| Name                 | Description                                                              | Required | Default Value                  |
|----------------------|--------------------------------------------------------------------------|----------|--------------------------------|
| `init-args`          | Additional arguments for the `init` command.                             | false    |                                |
| `plan-args`          | Additional arguments for the `plan` command.                             | false    |                                |
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
  plan:
    name: Plan Infrastructure
    runs-on: ubuntu-latest
    concurrency:
      cancel-in-progress: false
      group: terrakube-plan
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          fetch-tags: true

      - name: Plan
        uses: cupel-co/actions/.github/actions/terrakube/plan@vx.x.x
        with:
          init-args: '-var-file="variables/platform.tfvars"'
          plan-args: '-var-file="variables/platform.tfvars"'
          terrakube-token: ${{ secrets.TERRAKUBE_TOKEN }}
```

## Notes

- **Cost estimation and linting**: Configure these in your Terrakube workspace template. When the CLI triggers a plan, Terrakube executes the full template workflow server-side.
- **Authentication**: The action uses `setup-opentofu`'s built-in credential handling via `cli_config_credentials_hostname` and `cli_config_credentials_token`.


