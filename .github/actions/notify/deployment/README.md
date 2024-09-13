# Notify Deployment
Action: [deployment](./action.yml)

Send a notification when a deployment has finished.

## Secrets
| Name                              | Description                                         | Required |
|-----------------------------------|-----------------------------------------------------|----------|
| `secrets.GOOGLE_CHAT_WEBHOOK_URL` | The Webhook URL for the chat to send the message to | true     |

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
```
