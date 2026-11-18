# FileMerge PDF — TOS 7 Releases

Public release assets for **FileMerge PDF**, a persistent workspace and PDF assembly application for TerraMaster TOS 7.

The full development source repository is private. Only installable release assets, checksums, and release notes are published here for TOS Developer Platform / App Center distribution.

## Latest release

**v0.1.7** — 2026-11-18

| Asset | SHA-256 |
| --- | --- |
| `filemerge-pdf_0.1.7_x86_64.deb` | `e7d22ab9928e60aa8666561632898adcd6c5e7f038838332b967f63e65ce2225` |
| `filemerge-pdf_0.1.7_aarch64.deb` | `4312d75dfbc764d1123086d1d948244deac589afffd4121215abeb277a4cda09` |

Download the matching `.sha256` file from the same Release. Previous releases remain available under [Releases](https://github.com/642671/filemerge-pdf-tos-release/releases).

## Requirements

- TerraMaster TOS 7.0+ (TOS 7.1 tested on x86_64)
- Architecture: `x86_64` / Debian `amd64` or `aarch64` / Debian `arm64`
- Python 3.10 runtime is provided by TOS; the application bundles pypdf, Pillow and typing_extensions
- LibreOffice is optional: Word/Excel export requires a system-installed LibreOffice. Without it, such exports are blocked with a clear error instead of producing incomplete PDFs
- For Word/Excel on TOS, install LibreOffice Writer and Calc:

```sh
sudo apt-get update
sudo apt-get install -y --no-install-recommends libreoffice-writer libreoffice-calc fonts-noto-cjk
```

## Install

Download the package for your NAS architecture, then install from App Center's manual installation or:

```sh
sudo dpkg -i filemerge-pdf_0.1.7_x86_64.deb
```

The package starts `filemergepdf-system.service` and creates `/var/api/filemerge-pdf.sock`. Installation diagnostics are written to `/usr/local/filemerge-pdf/logs/postinst-diagnostic.txt` when startup fails.

## Features

- Persistent workspaces with SQLite and managed file copies.
- Asset library for images, PDF, Word and Excel, with search, filters, previews and hashes.
- Multiple ordered assemblies with drag/up-down sorting, undo/redo, auto-save and version conflict handling.
- PDF export with paper size, orientation, fit, quality and margins; exact assembly order.
- Export history with immutable snapshots, failure details, download and re-export.
- TOS iframe WebUI with TOS session/CSRF handling and Unix-socket backend.
- Custom-styled dropdowns with keyboard navigation, dark theme and viewport-aware menus.
- Clear blocked-export dialog when Word/Excel files need LibreOffice, including the affected file list.
- LibreOffice works under the TOS systemd `ProtectSystem=strict` sandbox by using isolated writable runtime directories.
- Draggable export dialogs, structured success/failure details, clickable home stat cards, and Chinese font cache invalidation.

## Known limitations

- Business data lives in the application data directory, not yet an SMB/NFS-visible `ter_share_add` shared folder.
- The 0.1.x line is an administrator single-user MVP; per-TOS-user workspace isolation is not implemented.
- Encrypted PDF input is rejected in this version.
- Page-level PDF editing is planned for P1; current sorting is file-level.
- App Center disable/uninstall data-retention paths and aarch64 runtime testing are not yet verified.
- Windows PySide6 desktop version is not part of this release.

## License

MIT. Third-party notices are included in the installed package (`THIRD_PARTY_NOTICES.md`).
