# Getting Started

## Installation

Install using `uv` (recommended):

```bash
uv add rhada
```

Or using `pip`:

```bash
pip install rhada
```

---

## Quick Walkthrough

### 1. Audit a Source Workspace

Run `rhada` in the root of a Python project (defaults to the `audit` subcommand):

```bash
uv run rhada --project . \
  --sbom sbom.cdx.json \
  --notices THIRD_PARTY_NOTICES
```

### 2. Audit a Compiled Distribution

Point `--dist` at a Nuitka `.dist` folder, PyInstaller bundle directory, or single-file binary:

```bash
uv run rhada --project . --dist ./dist/app.dist \
  --sbom dist-sbom.spdx.json \
  --sbom-format spdx \
  --notices dist/THIRD_PARTY_NOTICES \
  --fail-on-linkage
```

### 3. Pre-Commit Hook Integration

Use `rhada` in downstream repositories via `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/dcollison/rhada
    rev: v0.1.3
    hooks:
      - id: rhada
```

### 4. GitHub Actions CI Gate

```yaml
jobs:
  compliance-gate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: astral-sh/setup-uv@v5
      - name: Run Rhada Audit
        run: |
          uv run rhada audit \
            --project . \
            --dist ./dist/my-service.dist \
            --sbom ./dist/sbom.cdx.json \
            --notices ./dist/THIRD_PARTY_NOTICES \
            --report-json ./dist/rhada-report.json \
            --fail-on-severity high \
            --fail-on-licence high \
            --fail-on-linkage
```
