## Solution: Python Flask App Deploy to Azure

```yaml
name: Python Flask App Deploy to Azure
on:
  workflow_dispatch:
  push:
    paths:
      - '.github/workflows/python-flask-app-deploy-to-azure.yml'
      - 'src/python/flask-app/**'

env:
  AZURE_WEBAPP_NAME: app-flask-webapp-on-linux
  AZURE_WEBAPP_PACKAGE_PATH: .
  PYTHON_VERSION: '3.11'
  WORKING_DIRECTORY: 'src/python/flask-app'

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: ${{ env.PYTHON_VERSION }}

      - name: Upgrade pip
        run: python -m pip install --upgrade pip

      - name: Install dependencies
        run: |
          pip install -r requirements.txt
        working-directory: ${{ env.WORKING_DIRECTORY }}

      - name: Azure Login
        uses: azure/login@v2
        with:
          creds: ${{ secrets.AZURE_SERVICE_PRINCIPAL }}

      - name: Deploy to Azure Web App
        uses: azure/webapps-deploy@v2
        with:
          app-name: ${{ env.AZURE_WEBAPP_NAME }}
          package: ${{ env.WORKING_DIRECTORY }}
```
