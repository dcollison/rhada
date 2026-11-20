# Binary & Linkage Auditing

When `--dist` is supplied, `rhada` inspects compiled Nuitka and PyInstaller distributions (both standalone folders and monolithic single-file binaries).

## ELF & PE Inspection

* Parses 32-bit and 64-bit ELF executables and `.so` libraries via `pyelftools` with a `struct` fallback, plus Windows PE binaries (`.dll`, `.pyd`, `.exe`).
* Extracts `DT_NEEDED`, `DT_SONAME`, `DT_RPATH`, `DT_RUNPATH`, `PT_INTERP`, exported symbols (`PyInit_*`, `modulecode_*`), and embedded library version strings (`OpenSSL`, `zlib`, `SQLite`, `libffi`, `gmp`, `readline`, etc.).
* Verifies that every `DT_NEEDED` dependency is bundled in the distribution or provided by the standard Linux/glibc ABI, and flags insecure `RPATH`/`RUNPATH` entries when `--fail-on-linkage` is enabled.

Inspect a binary or distribution directory directly:

```bash
uv run rhada inspect-elf ./build/app.dist
```

## Distribution File Accounting

Pass `--verbose` (or `-v`, `--full`) to inspect the complete file-by-file inventory (`file_inventory` in JSON reports), classifying every distributed file into:

* `application-binary`
* `python-runtime`
* `compiler-abi`
* `native-library`
* `python-package`
* `data-metadata`
* `unaccounted`
