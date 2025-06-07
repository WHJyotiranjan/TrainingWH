## Solution : Deployment Protection Rules

```yaml
name: Env - Deployment Protection Rule

on:
  push:
    branches:
      - main

jobs:
  deploy-to-dev:
    runs-on: ubuntu-latest
    environment: dev
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Deploy to Dev
        run: echo "Deploying to the dev environment."

  deploy-to-prod:
    needs: deploy-to-dev
    runs-on: ubuntu-latest
    environment: prod
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Deploy to Prod
        run: echo "Deploying to the prod environment."
```
