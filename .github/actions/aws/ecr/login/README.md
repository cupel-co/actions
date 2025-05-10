# AWS ECR Login
Action: [apply](./action.yml)

This action logs into an AWS ECR registry.

## Inputs
| Name                         | Description                                 | Required | Default Value |
|------------------------------|---------------------------------------------|----------|---------------|
| `github-role-to-assume`      | The role to assume for GitHub               | true     | N/A           |
| `integration-role-to-assume` | The role to assume for integration          | true     | N/A           |
| `region`                     | The AWS region                              | true     | N/A           |

## Example
```yaml
jobs:
  apply:
    name: Build dockerfile
    runs-on: ubuntu-latest
    steps:
      - name: Login to AWS ECR
        uses: cupel-co/actions/.github/actions/aws/ecr/login@vx.x.x
        with:
          github-role-to-assume: 'arn:aws:iam::123456789012:role/GitHubRole'
          integration-role-to-assume: 'arn:aws:iam::123456789012:role/IntegrationRole'
          region: 'ap-southeast-2'
```
