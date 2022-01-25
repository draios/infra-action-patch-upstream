# action-patch-upstream

Checkout the ref (or latest) upstream version and apply one or more patch files

## Inputs

### Required

- `upstream_repo`: The upstream repo we want to checkout and patch
- `local_patch_dir`: Directory of the patch files, must end with .patch

### Optional

- `upstream_ref`: The upstream ref, can be: branch, tag, sha, if not provided last semver tag will be grabbed automatically
- `upstream_tag_regex`: Regex to use while checking the last upstream versions

## Caveats

- The action will always checkout the upstream repo under `upstream` directory.

## Example workflow

Perform all checks on pull requests

```yaml
name: Checkout and Patch

on:
  pull_request:
    types: [opened, edited, synchronize, reopened]
    paths:
      - 'containers/**'
jobs:
  build:
    runs-on: self-hosted
    steps:
    - uses: draios/infra-action-patch-upstream@v1
      with:
        upstream_repo: sysdiglabs/charts
        local_patch_dir: tests/sysdiglabs/charts
        upstream_ref: master
```
