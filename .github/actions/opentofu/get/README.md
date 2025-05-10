# OpenTofu Get
Action: [get](./action.yml)

The OpenTofu Get action gets OpenTofu modules from the OpenTofu registry.

## Inputs
| Name                  | Description                                                             | Required | Default            |
|-----------------------|-------------------------------------------------------------------------|----------|--------------------|
| `version`             | The version of OpenTofu to install.                                     | true     | `1.8.1`            |
| `working-directory`   | The directory containing the OpenTofu code.                             | true     | `./infrastructure` |

## Example
```yaml
jobs:
  get:
    name: Get OpenTofu modules
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
      - name: Get
        uses: cupel-co/actions/.github/actions/opentofu/get@vx.x.x
        with:
          version: 1.8.1
          working-directory: './infrastructure'
```
