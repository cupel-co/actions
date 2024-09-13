# Notify Release
Action: [release](./action.yml)

Send a notification when a release has been created.

## Secrets
| Name                              | Description                                         | Required |
|-----------------------------------|-----------------------------------------------------|----------|
| `secrets.GOOGLE_CHAT_WEBHOOK_URL` | The Webhook URL for the chat to send the message to | true     |

## Example
```yaml
jobs:
  release:
    name: Release
    runs-on: ubuntu-latest
    steps:
      - name: Notify
        uses: cupel-co/actions/.github/actions/notify/release@vX.X.X
```
