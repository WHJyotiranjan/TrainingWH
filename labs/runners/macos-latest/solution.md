## Solution: Runner - MacOS Latest

```yaml
name: Runner - MacOS Latest

on: workflow_dispatch

jobs:
  run:
    runs-on: macos-latest
    steps:
      - run: echo "This is a message from MacOS latest runner"
      - name: Display OS Information
        run: |
          system_profiler SPSoftwareDataType
```
