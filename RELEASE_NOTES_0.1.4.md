# v0.1.4 — FileMerge PDF for TOS 7

Release date: 2026-11-17

## Release type

Maintenance/stable release of the FileMerge PDF TOS 7 application.

## Changes

- Version bump to 0.1.4.
- Added public release/help links to `config.ini`.
- Cleared the `beta` flag so App Center no longer shows the beta warning when opening the app.
- Includes all 0.1.3 real-device fixes:
  - TOS proxy CSRF handling for thumbnails, PDF.js previews and downloads (authenticated fetch + Blob URLs, PDF.js `httpHeaders`).
  - Exports under platform-mapped symlinked data roots no longer fail with HTTP 500.
  - Upload progress panels no longer cover export dialog controls.
  - Removed the duplicate in-app titlebar inside the TOS App Center iframe while keeping the 56px host-titlebar safe area.

## Verification

- 71 backend tests passed on Linux x86_64 Python 3.10 with the packaged dependencies; 9 frontend tests passed.
- Real TOS 7.1 x86_64: App Center 0.1.3 → 0.1.4 upgrade completed at 100%; app opens without the Beta warning.
- Workspaces, assets, assemblies and export history were preserved across 0.1.0 → 0.1.1 → 0.1.2 → 0.1.3 → 0.1.4 upgrades.
- Health endpoint reports `version=0.1.4`; systemd service active; Unix socket healthy.
- x86_64 and aarch64 packages structure, ELF architecture, dynamic links and SHA-256 verified.

## Assets

| File | Size | SHA-256 |
| --- | ---: | --- |
| `filemerge-pdf_0.1.4_x86_64.deb` | 8,620,560 B | `2b6f577493aac430f3c8fbcf3f721b2f1b0607378fbff23d825c606918507fb1` |
| `filemerge-pdf_0.1.4_aarch64.deb` | 6,835,950 B | `b619a733fa4530c4f8dad6ef53ebcbb82cde0235e1582336248c246a98eca0fc` |

Each package has a matching `.sha256` file in this Release.

## Requirements

- TerraMaster TOS 7.0+
- x86_64/amd64 or aarch64/arm64
- Python 3.10 runtime provided by TOS
- LibreOffice is optional and required only for Word/Excel export

## Known limitations

- No SMB/NFS-visible application shared folder yet.
- Single-user administrator MVP; no per-TOS-user workspace isolation.
- Encrypted PDFs are rejected.
- Page-level PDF editing is planned for P1.
- aarch64 runtime, App Center disable/uninstall data retention and LibreOffice conversion are not yet verified.
