# OpenTofu Lint
Action: [tflint](./action.yml)

The Lint TF files GitHub Action installs TFLint, initializes its configuration, and runs a linting process on OpenTofu files in the specified directory.

## Inputs
| Name                | Description                               | Required | Default Value      |
|---------------------|-------------------------------------------|----------|--------------------|
| `working-directory` | Directory that contains the OpenTofu code | true     | `./infrastructure` |

## Secrets
| Name           | Description                                            | Required |
|----------------|--------------------------------------------------------|----------|
| `github.token` | GitHube token. Needs `pull-requests: write` permission | true     |

## Example
```yaml
jobs:
  lint:
    name: Lint
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
    concurrency:
      cancel-in-progress: false
      group: tflint-${{ github.ref_name }}
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          fetch-tags: true
      - name: Infrastructure
        uses: cupel-co/actions/.github/actions/opentofu/lint@vx.x.x
```
