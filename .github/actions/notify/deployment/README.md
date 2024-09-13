# Notify Deployment
Action: [deployment](./action.yml)

Send a notification when a deployment has finished.

## Inputs
| Name                      | Description                                         | Required | Default |
|---------------------------|-----------------------------------------------------|----------|---------|
| `google-chat-webhook-url` | The Webhook URL for the chat to send the message to | true     |         |

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
          google-chat-webhook-url: "${{ secrets.GOOGLE_CHAT_WEBHOOK_URL }}"
```
