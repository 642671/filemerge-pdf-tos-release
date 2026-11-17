# v0.1.6 — FileMerge PDF for TOS 7

Release date: 2026-11-17

## Release type

LibreOffice sandbox compatibility fix release.

## Fixes

- Fixed Word/Excel export failing with `ERROR: no valid pipe path found.` or `converter_failed` even after LibreOffice was installed on the NAS.
  - TOS uses `ProtectSystem=strict`; `/tmp` and `/var/tmp` were read-only inside the service and LibreOffice's `oosplash` needs a writable temporary directory.
  - `soffice.bin` also needs a writable current directory for `.execooo*` and a writable HOME for dconf. The service's working directory and HOME point at the read-only application root.
  - The service now grants write access to `/tmp` and `/var/tmp` without enabling `PrivateTmp` (which would hide the TOS `/var/api` proxy socket).
  - Each conversion now gets an isolated short-lived runtime tree with writable `cwd`, `HOME`, `TMPDIR`, XDG directories and LibreOffice profile. The tree is cleaned up after the conversion.
- LibreOffice remains an optional system dependency and is not bundled in the Deb. If it is missing, exports containing Office files still fail with the clear `converter_missing` dialog instead of producing a partial PDF.

## LibreOffice installation

On the NAS, install the Writer and Calc components:

```sh
sudo apt-get update
sudo apt-get install -y --no-install-recommends libreoffice-writer libreoffice-calc
```

Then reopen the app or click “重新检测” on the workspace settings page. The 0.1.6 sandbox changes do not require a NAS reboot.

## Verification

- 71 backend tests passed on Windows and on Linux x86_64 Python 3.10 with packaged dependencies; 14 frontend tests passed.
- Local Playwright E2E passed, including PDF export and download.
- Real TOS 7.1 x86_64:
  - App Center 0.1.5 → 0.1.6 upgrade completed at 100%.
  - LibreOffice 7.3.7 detected at `/usr/bin/soffice`.
  - Excel + image assembly exported successfully: 71 pages, 3.17 MB.
  - After adding a Word document, export succeeded: 72 pages, 3.18 MB.
  - Existing workspaces, assets, assemblies, assembly items and export history were preserved.
  - Health endpoint reports `version=0.1.6`.
- x86_64 and aarch64 packages structure, ELF architecture and SHA-256 verified.

## Assets

| File | Size | SHA-256 |
| --- | ---: | --- |
| `filemerge-pdf_0.1.6_x86_64.deb` | 8,661,630 B | `f7f27c58e95856ba672c382b0828a73f6a42acfdb215ccd38ace65c2461a2eff` |
| `filemerge-pdf_0.1.6_aarch64.deb` | 6,876,188 B | `ffd6474a88072088f8fd90f96aac7967ef6423728e8075f951c62e082fbfdd46` |

Each package has a matching `.sha256` file in this Release.

## Requirements

- TerraMaster TOS 7.0+
- x86_64/amd64 or aarch64/arm64
- Python 3.10 runtime provided by TOS
- LibreOffice Writer and Calc for Word/Excel export

## Known limitations

- No SMB/NFS-visible application shared folder yet.
- Single-user administrator MVP; no per-TOS-user workspace isolation.
- Encrypted PDFs are rejected.
- Page-level PDF editing is planned for P1.
- Word/Excel layout may differ from Microsoft Office; output follows LibreOffice and the source file's print settings.
- aarch64 runtime, App Center disable/uninstall data retention are not yet verified.
