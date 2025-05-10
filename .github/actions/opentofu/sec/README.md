# OpenTofu Static Analysis
Action: [tfsec](./action.yml)

This GitHub Action runs a security scan on OpenTofu files using tfsec, a static analysis tool for detecting security vulnerabilities in OpenTofu code. It scans the specified directory and posts comments directly to the pull request with the findings.

## Inputs
| Name                | Description                               | Required | Default Value        |
|---------------------|-------------------------------------------|----------|----------------------|
| `working-directory` | Directory that contains the OpenTofu code | true     | `'./infrastructure'` |

## Secrets
| Name           | Description                                                                | Required |
|----------------|----------------------------------------------------------------------------|----------|
| `github.token` | GitHube token. Needs `pull-requests: write` or `content: write` permission | true     |

## Example
```yaml
jobs:
  analyse:
    name: Analyse
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: write
    concurrency:
      cancel-in-progress: false
      group: opentofu-sec-${{ github.ref_name }}
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          fetch-tags: true
      - name: Infrastructure
        uses: cupel-co/actions/.github/actions/opentofu/sec@vx.x.x
```
