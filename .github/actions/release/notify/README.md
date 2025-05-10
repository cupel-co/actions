# Notify Release
Action: [release](./action.yml)

Send a notification when a release has been created.

## Inputs
| Name                      | Description                                         | Required | Default |
|---------------------------|-----------------------------------------------------|----------|---------|
| `google-chat-webhook-url` | The Webhook URL for the chat to send the message to | true     |         |

## Example
```yaml
jobs:
  release:
    name: Release
    runs-on: ubuntu-latest
    steps:
      - name: Notify
        uses: cupel-co/actions/.github/actions/notify/release@vX.X.X
        with:
          google-chat-webhook-url: "${{ secrets.GOOGLE_CHAT_WEBHOOK_URL }}"
```
