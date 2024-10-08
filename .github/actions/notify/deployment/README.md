# Notify Deployment
Action: [deployment](./action.yml)

Send a notification when a deployment has finished.

## Inputs
| Name                      | Description                                              | Required | Default |
|---------------------------|----------------------------------------------------------|----------|---------|
| `environment`             | The name of the environment the changes were deployed to | true     |         |
| `google-chat-webhook-url` | The Webhook URL for the chat to send the message to      | true     |         |
| `subtitle`                | The subtitle of the message                              | true     |         |

## Example
```yaml
name: Notify PR

jobs:
  deployment:
    name: Pull Request
    runs-on: ubuntu-latest
    steps:
      - name: Notify
        uses: cupel-co/actions/.github/actions/notify/deployment@vX.X.X
        with:
          environment: "Production"
          google-chat-webhook-url: "${{ secrets.GOOGLE_CHAT_WEBHOOK_URL }}"
          subtitle: "Workspace: github-team-support"
```
