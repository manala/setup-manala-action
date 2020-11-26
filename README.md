# Setup Manala Action

This action downloads and installs the Manala binary and makes it available in
your workflows.

## Usage

```yaml

steps:
  - uses: actions/checkout@v2
  - uses: manala/setup-manala-action@master

  - name: Run Manala update
    run: manala update
```

## Checks

Additionally, the action provides some common `checks` you can opt-in using JSON format.

### `update` check

Use this check in your workflow, to ensure any `.manala.yaml` changes are 
properly reflected in your PRs, or get a failure otherwise:

```yaml
  - uses: manala/setup-manala-action@master
    with:
      checks: '["update"]'
```

Here is a suggested `.github/workflows/.manala-update.yaml` workflow:

```yaml 
name: Manala update

on:
  push:
    branches: [master]
    paths: ['.manala.yaml']
  pull_request:
    types: [opened, synchronize, ready_for_review]
    paths: ['.manala.yaml']

jobs:
  manala-update:
    runs-on: ubuntu-latest
    timeout-minutes: 2
    steps:

      - name: 'Checkout head'
        uses: actions/checkout@v2

      - name: 'Check .manala changes are up-to-date'
        uses: manala/setup-manala-action@master
        with:
          checks: '["update"]'
```
