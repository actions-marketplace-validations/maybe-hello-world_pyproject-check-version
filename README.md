# pyproject-check-version
This action checks if the version in the `pyproject.toml` file is newer than in published package on PyPI.
You can use it to trigger a new release or to skip the release if the version is already published.

Usage example:
```yaml
name: CI
on:
  push:
    branches: [ "main" ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Check pypi versions
        uses: maybe-hello-world/pyproject-check-version@v2
        id: versioncheck
        with:
          pyproject-path: "./pyproject.toml"    # default value
      
      - name: check output
        run: |
            echo "Output: ${{ steps.versioncheck.outputs.local_version_is_higher }}"  # 'true' or 'false
            echo "Local version: ${{ steps.versioncheck.outputs.local_version }}"     # e.g., 0.1.1
            echo "Public version: ${{ steps.versioncheck.outputs.public_version }}"   # e.g., 0.1.0
```
