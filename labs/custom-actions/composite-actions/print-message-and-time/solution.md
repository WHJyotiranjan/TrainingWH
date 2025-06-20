## Solution: Create and Run a Custom Composite Action to Print a Message and the Current Time

```yaml
name: Custom Action - Composite - Print Message and Time

on:
  push:
    paths:
      - '.github/actions/print-message-and-time-composite-action/**'
      - '.github/workflows/custom-action-composite-print-message-and-time.yml'
  workflow_dispatch:

jobs:
  test-composite-action:
    runs-on: ubuntu-latest
    steps:
      # Checkout the repository
      - name: Checkout code
        uses: actions/checkout@v4.1.7

      - name: List the files in print-message-and-time-composite-action directory
        run: ls -R .github/actions/print-message-and-time-composite-action

      # Use the composite action
      - name: Run the custom composite action
        id: composite-action
        uses: ./.github/actions/print-message-and-time-composite-action
        with:
          message: 'Hello from Composite Action!'

      # Access the output of the composite action
      - name: Print the timestamp
        run: |
          echo "The timestamp is: ${{ steps.composite-action.outputs.timestamp }}"
```
