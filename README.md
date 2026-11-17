# FileMerge PDF — TOS 7 Releases

Public release assets for **FileMerge PDF**, a persistent workspace and PDF assembly application for TerraMaster TOS 7.

The full development source repository is private. Only installable release assets, checksums, and release notes are published here for TOS Developer Platform / App Center distribution.

## Latest release

**v0.1.3** — 2026-11-17

| Asset | SHA-256 |
| --- | --- |
| `filemerge-pdf_0.1.3_x86_64.deb` | `6e8cf1f3bc81b801f7094afb1ebb1bc02f9f26f64d7276882bb00a25f358727f` |
| `filemerge-pdf_0.1.3_aarch64.deb` | `6ebf6a0170055b28b025e0328a9756e0da006c2d1ece95e1c28feade07e1ee8a` |

Download the matching `.sha256` file from the same Release.

## Requirements

- TerraMaster TOS 7.0+ (TOS 7.1 tested on x86_64)
- Architecture: `x86_64` / Debian `amd64` or `aarch64` / Debian `arm64`
- Python 3.10 runtime is provided by TOS; the application bundles pypdf, Pillow and typing_extensions
- LibreOffice is optional: Word/Excel export requires a system-installed LibreOffice. Without it, such exports are blocked with a clear error instead of producing incomplete PDFs.

## Install

Download the package for your NAS architecture, then install from App Center's manual installation or:

```sh
sudo dpkg -i filemerge-pdf_0.1.3_x86_64.deb
```

The package starts `filemergepdf-system.service` and creates `/var/api/filemerge-pdf.sock`. Installation diagnostics are written to `/usr/local/filemerge-pdf/logs/postinst-diagnostic.txt` when startup fails.

## Features

- Persistent workspaces with SQLite and managed file copies.
- Asset library for images, PDF, Word and Excel, with search, filters, previews and hashes.
- Multiple ordered assemblies with drag/up-down sorting, undo/redo, auto-save and version conflict handling.
- PDF export with paper size, orientation, fit, quality and margins; exact assembly order.
- Export history with immutable snapshots, failure details, download and re-export.
- TOS iframe WebUI with TOS session/CSRF handling and Unix-socket backend.

## Known limitations

- Business data lives in the application data directory, not yet an SMB/NFS-visible `ter_share_add` shared folder.
- The 0.1.x line is an administrator single-user MVP; per-TOS-user workspace isolation is not implemented.
- Encrypted PDF input is rejected in this version.
- Page-level PDF editing is planned for P1; current sorting is file-level.
- App Center disable/uninstall data-retention paths and aarch64 runtime testing are not yet verified.
- Windows PySide6 desktop version is not part of this release.

## License

MIT. Third-party notices are included in the installed package (`THIRD_PARTY_NOTICES.md`).
