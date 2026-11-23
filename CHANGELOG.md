# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.3] - 2026-11-23

### Added
- Added MkDocs Material documentation (`mkdocs.yml`, `docs/`) with `mkdocstrings` API reference and GitHub Pages deployment workflow (`.github/workflows/docs.yml`).
- Added `.github/CODEOWNERS`, `.pre-commit-config.yaml`, `LICENSE`, `.python-version` (`3.14`), and `uv.lock`.

### Changed
- Hardened and refactored compliance, ELF/PE inspection, SBOM/SPDX generation, workspace scanning, and CLI modules alongside expanded test coverage.
- Aligned `pyproject.toml` metadata/URLs/classifiers, CI matrix across Python `3.11`–`3.14` and `ubuntu`/`windows`/`macos`, and PyPI Trusted Publishing release workflow (`.github/workflows/release.yml`).
- Upgraded locked dependencies in `uv.lock` (`backrefs`, `certifi`, `charset-normalizer`, `coverage`, `filelock`, `pymdown-extensions`, `pyyaml`, `virtualenv`, `watchdog`).

## [0.1.2] - 2026-10-30

### Fixed
- Classified `libz.so` as a standard Linux system ABI library and added unversioned library fallback handling during ELF linkage verification.

## [0.1.1] - 2026-10-30

### Fixed
- Classified `libuuid` under LGPL compliance rules and normalized SONAME ABI versions to `unknown` when no real package version is embedded.

## [0.1.0] - 2026-10-29

### Added
- Pre-commit hook definitions in `.pre-commit-hooks.yaml` (`rhada` and `rhada-audit`).
- Vulnerability ignore support via `--ignore-vulnerability` and `[tool.rhada.ignore-vulnerabilities]`.
- Verbatim licence text overrides via `--license-file`, `[tool.rhada.license-files]`, and `[tool.rhada.license-texts]`.
- `rhada diff` subcommand for comparing baseline and target SBOM or audit report JSON files (`--fail-on-downgrade`, `--fail-on-new-vuln`, `--fail-on-changes`).
- Markdown output support for `THIRD_PARTY_NOTICES` (`--notices-format markdown`).

## [0.0.9] - 2026-10-29

### Changed
- Trimmed excess `--allow-extra-licence` CLI option aliases for cleaner CLI help output.

## [0.0.8] - 2026-10-29

### Added
- Supplemental licence allowlist via `--allow-extra-licence` / `--allow-extra-license` and `[tool.rhada] extra-allowed-licenses`.

## [0.0.7] - 2026-10-29

### Added
- CLI reference table in `README.md`.

### Fixed
- Improved Nuitka Linux compilation report discovery across distribution paths.

## [0.0.6] - 2026-10-28

### Added
- Accounting for bare Linux standard library `.so` files and explicit `unknown` version rendering.

## [0.0.5] - 2026-10-28

### Added
- Declarative `[tool.rhada]` configuration support in `pyproject.toml`.

## [0.0.4] - 2026-10-28

### Added
- Distribution file accounting and inventory classification (`--verbose` / `--full` and `file_inventory` in JSON reports).

## [0.0.3] - 2026-10-27

### Changed
- Hardened SPDX compliance evaluation and CycloneDX/SPDX SBOM generation engines.

## [0.0.2] - 2026-10-27

### Added
- Enhanced compliance engine and legacy `setup.py` / `setup.cfg` / `requirements.txt` workspace inspection.

## [0.0.1] - 2026-10-25

### Added
- Initial release of `rhada`: legal compliance, CycloneDX 1.5 / SPDX 2.3 SBOM generation, ELF/PE binary linkage verification, and OSV.dev/`pip-audit` vulnerability auditing.
- Windows UTF-8 stream handling and Python 3.11+ compatibility.
