# OpenTofu Plan
Action: [plan](./action.yml)

The Run tfsec GitHub Action runs a security scan on OpenTofu files using tfsec, a static analysis tool for detecting security vulnerabilities in Terraform code. It scans the specified directory and posts comments directly to the pull request with the findings.

## Inputs
| Name                | Description                               | Required | Default Value        |
|---------------------|-------------------------------------------|----------|----------------------|
| `working-directory` | Directory that contains the OpenTofu code | true     | `'./infrastructure'` |

## Example
```yaml
jobs:
  analyse:
    name: Analyse
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: write
    concurrency:
      cancel-in-progress: false
      group: tfsec-${{ github.ref_name }}
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          fetch-tags: true
      - name: Infrastructure
        uses: ./.github/actions/tfsec
```
