# OpenTofu Plan
Action: [tflint](./action.yml)

The Lint OpenTofu files GitHub Action installs TFLint, initializes its configuration, and runs a linting process on OpenTofu files in the specified directory. This action ensures that the OpenTofu code is linted for best practices and potential issues.

## Inputs
| Name                | Description                               | Required | Default Value        |
|---------------------|-------------------------------------------|----------|----------------------|
| `working-directory` | Directory that contains the OpenTofu code | true     | `'./infrastructure'` |

## Example
```yaml
jobs:
  lint:
    name: Lint
    runs-on: ubuntu-latest
    permissions:
      contents: read
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
        uses: ./.github/actions/tflint
```
