## setup brane action

GitHub action to setup brane.

#### Usage

**Note**: Make sure the runner or container image you use the action with has at least `wget`/`curl`, `unzip` and a java jdk installed.

```yaml
# .github/workflows/ci.yml
name: CI
on: ['push']

jobs:
  build:
    runs-on: 'ubuntu-latest'
    steps:
    - uses: actions/checkout@v2

    - name: 'setup brane'
      uses: 'romnn/setup-brane-action@master'
      id: brane_setup
      # optionally:
      with:
        start_instance: true
        start_ide: true

    - name: 'use the brane CLI'
      run: |
        brane --help

    - name: 'query the jupyterlab IDE access token'
      run: |
        brane --help
```
