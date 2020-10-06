setup-manala
============

This action download and install the Manala binary and make it available in your
workflows.

Usage
-----

```yaml

steps:

  - uses: actions/checkout@v2
  - uses: manala/setup-manala-action@master

  - name: Run Manala update
    run: manala update
```
