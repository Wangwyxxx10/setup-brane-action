## setup brane action

GitHub action to setup [brane](https://github.com/epi-project/brane). (Fork others' action and make some changes. Origin: https://github.com/romnn/setup-brane-action/tree/c6af2d863079aef95b15af9919e2a0122f0a884f)

#### Usage

**Note**: Make sure the runner or container image you use the action with has at least `docker`, `git` and `make` installed.

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
        # check that the brane services are running
        docker ps

    - name: 'query the jupyterlab IDE access token'
      run: |
        echo "${{ steps.brane_setup.outputs.jupyterlab_token }}"
```
