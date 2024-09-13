# Notify Pull Request
Action: [pull-request](./action.yml)

Send a notification when a PR has been raised.

## Secrets
| Name                              | Description                                         | Required |
|-----------------------------------|-----------------------------------------------------|----------|
| `secrets.GOOGLE_CHAT_WEBHOOK_URL` | The Webhook URL for the chat to send the message to | true     |

## Example
```yaml
name: Notify PR

on:
  pull_request:
    types:
      - opened
      - reopened

jobs:
  pull-request:
    name: Pull Request
    runs-on: ubuntu-latest
    steps:
      - name: Notify
        uses: cupel-co/actions/.github/actions/notify/pull-request@vX.X.X
```
