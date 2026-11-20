# rhada

Legal compliance, SBOM generation, binary linkage verification, and security vulnerability auditor for Python source workspaces and compiled Nuitka/PyInstaller distributions.

---

## Key Capabilities

* **Dual-Mode Operation:** Audits Python source workspaces (`pyproject.toml`, `uv.lock`, `setup.py` via safe AST parsing, `setup.cfg`, `requirements.txt`) as well as compiled Nuitka and PyInstaller distributions (`--dist`).
* **Legal & Licence Compliance:** Normalises PEP 639 expressions, Trove classifiers, and verbatim licence texts into canonical SPDX identifiers using `license-expression`, flags copyleft/LGPL obligations, and generates `THIRD_PARTY_NOTICES` in plain text or Markdown.
* **ELF & PE Binary Inspection:** Parses ELF and PE executables and shared libraries (`.so`, `.dll`, `.pyd`, `.exe`), verifies `DT_NEEDED` dynamic linkage, flags insecure `RPATH`/`RUNPATH` tokens, and accounts for 100% of files in a distribution.
* **Security Vulnerability Auditing:** Integrates `pip-audit` (`OsvService`) and the OSV.dev batch API with CVSS v3/v4 scoring via `cvss`.
* **Standards-Compliant SBOMs & Diffs:** Exports **CycloneDX 1.5 JSON** and **SPDX 2.3 JSON** SBOMs and compares snapshots via `rhada diff`.

---

## Quick Example

```bash
# Audit a Python / uv source workspace
uv run rhada --project . --sbom sbom.cdx.json --notices THIRD_PARTY_NOTICES

# Audit a compiled Nuitka or PyInstaller distribution
uv run rhada --project . --dist ./build/app.dist \
  --sbom dist-sbom.json \
  --notices dist/THIRD_PARTY_NOTICES \
  --fail-on-linkage
```

!!! warning "Legal Disclaimer"
    `rhada` is an automated static and metadata analysis tool and does not provide legal advice or guarantee legal compliance. Software distributors remain solely responsible for verifying legal obligations with qualified counsel.
