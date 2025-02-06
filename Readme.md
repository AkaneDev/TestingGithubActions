# Testing GitHub Actions with Discord Webhook

This repository is a test for using GitHub Actions to run a Discord webhook every day at 12 PM AEST or manually when pushed to the `manual` branch.

## Setup

1. Clone the repository.
2. Create a `.github/workflows` directory if it doesn't exist.
3. Add a workflow file (e.g., `discord-webhook.yml`) in the `.github/workflows` directory.

## Workflow File Example

```yaml
name: Send to Discord Webhook

on:
  schedule:
    # Trigger at 12pm every day in AEST (UTC+10)
    - cron: '0 2 * * *'  # 12:00 PM AEST is 2:00 AM UTC
  push:
    branches:
      - manual  # Trigger on push to 'manual' branch

jobs:
  send-discord:
    runs-on: ubuntu-latest
    steps:
      - name: Send message to Discord Webhook
        env:
          DISCORD_WEBHOOK_URL: ${{ secrets.DISCORD_WEBHOOK_URL }}
        run: |
          curl -X POST -H "Content-Type: application/json" \
            -d '{"content": "Hello from GitHub Actions!"}' \
            $DISCORD_WEBHOOK_URL
```

## Secrets

Make sure to add your Discord webhook URL as a secret in your GitHub repository settings:

1. Go to the repository on GitHub.
2. Click on `Settings`.
3. Navigate to `Secrets` > `Actions`.
4. Click `New repository secret`.
5. Name the secret `DISCORD_WEBHOOK_URL` and paste your webhook URL.

## License

This project is licensed under the MIT License.