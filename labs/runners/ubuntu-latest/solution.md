## Solution: Runner - Ubuntu Latest

```yaml
name: Runner - Ubuntu Latest

on: workflow_dispatch

jobs:
  run:
    runs-on: ubuntu-latest
    steps:
      - run: echo "This is a message from ubuntu latest runner"
      - name: Display OS Information
        run: |
          uname -a
          lsb_release -a
```
