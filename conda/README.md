# conda-forge recipe

This directory contains the conda recipe used to publish `wildberries-sdk` to
[conda-forge](https://conda-forge.org/). It is **not** consumed by the build
pipelines in this repo — once accepted, conda-forge maintains a separate
"feedstock" repository (`conda-forge/wildberries-sdk-feedstock`) and a bot
auto-updates that feedstock from PyPI on every new release.

## Submitting the recipe (one-time)

1. Fork [`conda-forge/staged-recipes`](https://github.com/conda-forge/staged-recipes).
2. Copy `conda/recipe/meta.yaml` from this repo into
   `recipes/wildberries-sdk/meta.yaml` in your fork.
3. Open a PR titled `Add wildberries-sdk` against `conda-forge/staged-recipes:main`.
4. Wait for CI: the PR runs `linter`, `recipe-lint`, and builds on Linux/macOS/Windows.
5. After review (usually a few maintainer comments), the PR is merged and a
   feedstock repository is created automatically. From then on, the
   conda-forge "regro" bot opens PRs against that feedstock whenever a new
   PyPI release is detected — you only have to merge them.

## Updating this file when the package changes

After every PyPI release we should refresh `version` and `sha256` here so the
recipe in this repo stays a faithful template. Typical refresh:

```bash
VERSION=$(curl -sS https://pypi.org/pypi/wildberries-sdk/json \
  | python3 -c 'import json,sys; print(json.load(sys.stdin)["info"]["version"])')
SHA256=$(curl -sS "https://pypi.org/pypi/wildberries-sdk/json" \
  | python3 -c "
import json,sys
d=json.load(sys.stdin); v=d['info']['version']
for f in d['releases'][v]:
    if f['packagetype']=='sdist':
        print(f['digests']['sha256'])
")
echo "version=$VERSION sha256=$SHA256"
# update those two lines at the top of conda/recipe/meta.yaml
```

For the live package on conda-forge this is automatic — the bot scrapes PyPI.
The copy here is purely for visibility and bootstrapping.

## After acceptance

Add a badge to the main README:

```markdown
[![conda-forge](https://img.shields.io/conda/vn/conda-forge/wildberries-sdk.svg)](https://anaconda.org/conda-forge/wildberries-sdk)
```

And users will install with:

```bash
conda install -c conda-forge wildberries-sdk
# or
mamba install -c conda-forge wildberries-sdk
# or
pixi add wildberries-sdk
```
