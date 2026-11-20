# Compliance, SBOMs & Notices

## SPDX Normalisation & Risk Evaluation

`rhada` parses PEP 639 `License-Expression` metadata, `METADATA` licence headers, Trove classifiers, and verbatim licence files into canonical SPDX identifiers and compound expressions using `license-expression`.

Licences are classified into risk tiers (`permissive`, `public-domain`, `weak-copyleft`, `strong-copyleft`, `proprietary`, `unknown`):

* Strong copyleft (`GPL-*`, `AGPL-*`, `SSPL-1.0`) obligations are flagged via `LIC-COP-STRONG` and `LIC-COP-NETWORK`.
* LGPL dynamic vs. monolithic relinking obligations are evaluated via `LIC-LGPL-DYNAMIC` and `LIC-LGPL-MONOLITHIC`.
* Missing verbatim licence files trigger `LIC-MISSING-TEXT`, which can be remediated via `--license-file` or `[tool.rhada.license-files]`.

## LGPL Source Code Offers

For LGPL-2.0, LGPL-2.1, and LGPL-3.0 dependencies, `rhada` resolves upstream repository and release source URLs from package `Project-URL` metadata, PyPI metadata, or native library registries, embedding them in SBOMs and generating a dedicated **LGPL Compliance & Source Code Offer** section in `THIRD_PARTY_NOTICES`.

## SBOM Generation & Diffing

```bash
# Generate CycloneDX 1.5 or SPDX 2.3 JSON SBOM
uv run rhada sbom --project . --format spdx --output sbom.spdx.json

# Generate plain text or Markdown attribution notices
uv run rhada notices --project . --format markdown --output THIRD_PARTY_NOTICES.md

# Compare two SBOMs or audit report JSON files
uv run rhada diff base-report.json new-report.json --fail-on-new-vuln --fail-on-downgrade
```
