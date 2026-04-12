# Terrakube Plan
Action: [plan](./action.yml)

The Terrakube Plan GitHub Action logs in to Terrakube, resolves a workspace by name, creates a plan job, and polls until the job completes or fails.

## Inputs
| Name                        | Description                                                                      | Required | Default Value            |
|-----------------------------|----------------------------------------------------------------------------------|----------|--------------------------|
| `terrakube_token`           | Terrakube Personal Access Token or Team API Token.                               | true     |                          |
| `terrakube_endpoint`        | Base URL of the Terrakube API (for example `https://terrakube-api.example.com`). | true     |                          |
| `terrakube_organization_id` | UUID of the Terrakube organisation.                                              | true     |                          |
| `terrakube_workspace_name`  | Name of the Terrakube workspace to plan.                                         | true     |                          |
| `terrakube_template`        | Name of the plan template to use.                                                | false    | `Plan`                   |
| `branch`                    | Branch to run the plan against.                                                  | false    | `${{ github.head_ref }}` |
| `show_output`               | Whether to stream job output to the GitHub Actions log.                          | false    | `true`                   |

## Outputs
| Name         | Description                                                          |
|--------------|----------------------------------------------------------------------|
| `job_id`     | The Terrakube job UUID.                                              |
| `job_status` | Final job status (`completed`, `failed`, `cancelled`, or `timeout`). |
| `job_url`    | URL to the Terrakube job in the Terrakube UI.                        |

## Example
```yaml
jobs:
  terrakube-plan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Run Terrakube plan
        id: terrakube-plan
        uses: cupel-co/actions/.github/actions/terrakube/plan@main
        with:
          terrakube_token: ${{ secrets.TERRAKUBE_TOKEN }}
          terrakube_endpoint: ${{ vars.TERRAKUBE_ENDPOINT }}
          terrakube_organization_id: ${{ vars.TERRAKUBE_ORGANIZATION_ID }}
          terrakube_workspace_name: my-workspace
          terrakube_template: Plan
          show_output: 'true'

      - name: Print job details
        run: |
          echo "Job ID: ${{ steps.terrakube-plan.outputs.job_id }}"
          echo "Job URL: ${{ steps.terrakube-plan.outputs.job_url }}"
          echo "Job status: ${{ steps.terrakube-plan.outputs.job_status }}"
```

## Behavior
- Installs the Terrakube CLI and ensures `jq` is available.
- Logs in with the supplied token and API endpoint.
- Resolves workspace ID from `terrakube_workspace_name`.
- Creates a Terrakube job using `terrakube_template`.
- Polls every 10 seconds for up to 10 minutes (`timeout=600`).
- Fails the action if final job status is `failed`, `cancelled`, or `timeout`.

## Troubleshooting
- `Workspace '<name>' not found`: confirm workspace exists in the provided organisation ID.
- Authentication/login errors: verify `terrakube_token` and `terrakube_endpoint`.
- `Failed to create job`: check template name and workspace permissions.
- Timeout after 10 minutes: inspect Terrakube job logs in `job_url`; the run may still be queued or waiting on dependencies.
- Missing streamed output: set `show_output: 'true'` and verify Terrakube step output exists for the job.
