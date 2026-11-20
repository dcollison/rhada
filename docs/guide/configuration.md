# Configuration & Policy

All operational defaults and legal/security policies can be configured via CLI flags or centrally under `[tool.rhada]` in `pyproject.toml`. CLI flags supplement and take precedence over `pyproject.toml` settings.

## Declarative `pyproject.toml` Configuration

```toml
[tool.rhada]
# Whitelist internal corporate packages (supports exact names and wildcards)
internal-packages = [
    "mycorp-*",
    "internal-security-sdk",
]

# Completely ignore specific dependencies
ignore-packages = [
    "legacy-stub",
]

# Strict exclusive allowlist (optional; replaces default permissive baseline)
# allowed-licenses = ["MIT", "Apache-2.0", "BSD-3-Clause", "0BSD"]

# Supplemental approved licenses (preserves standard permissive defaults)
extra-allowed-licenses = [
    "Proprietary",
    "LicenseRef-Corporate",
]

fail-on-severity = "high"
fail-on-license = "high"
allow-unknown-license = false
verbose = false
offline = false

[tool.rhada.ignore-vulnerabilities]
"CVE-2024-99999" = "Non-exploitable in CLI context"
"GHSA-34jh-p97f-mpxf" = { reason = "Awaiting upstream patch", expires = "2026-12-31" }

[tool.rhada.license-files]
"some-legacy-package" = "licenses/legacy-license.txt"

[tool.rhada.license-texts]
"proprietary-sdk" = "Copyright (c) 2026 Acme Corp. All rights reserved."
```

---

## Internal & Ignored Packages

* **`--internal-package` / `--allow-package`:** Treats matching packages as first-party code. Exempts them from third-party licence checks, suppresses OSV.dev queries (preventing private package name leakage), and omits them from `THIRD_PARTY_NOTICES`.
* **`--ignore-package`:** Completely omits matching packages from compliance evaluation and vulnerability scanning.

## Licence Allowlists & Denylists

* **`--allow-licence` / `--allow-license`:** Closed-world strict allowlist. Any licence not listed triggers `LIC-POLICY-NOT-ALLOWED`.
* **`--allow-extra-licence` / `--allow-extra-license`:** Supplements the default permissive baseline without rejecting standard permissive licences (`MIT`, `Apache-2.0`, `BSD-3-Clause`, etc.).
* **`--deny-license`:** Explicitly forbids specific SPDX licence identifiers (`HIGH` severity).
