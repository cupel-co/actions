# OpenTofu Apply
Action: [apply](./action.yml)

The OpenTofu Apply GitHub Action installs a specified version of OpenTofu, and applies the plan using the apply command with optional custom arguments.

## Inputs
| Name            | Description                                   | Required | Default Value |
|-----------------|-----------------------------------------------|----------|---------------|
| `apply-args`    | Additional arguments for the `apply` command. | false    | N/A           |
| `version`       | The version of OpenTofu to install.           | true     | `1.8.1`       |

## Example
```yaml
jobs:
  apply:
    name: Apply opentofu-aws-backend
    runs-on: ubuntu-latest
    environment: Production
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
      - name: Apply
        uses: cupel-co/platform-opentofu-aws-backend/.github/actions/opentofu/apply@vx.x.x
        with:
          artifact-name: 'opentofu-aws-backend'
```
