# v0.1.5 — FileMerge PDF for TOS 7

Release date: 2026-11-17

## Release type

UI and error-handling fix release of the FileMerge PDF TOS 7 application.

## Fixes

- Fixed the export error path that could surface `Cannot read properties of undefined (reading 'id')`. The API client now rejects 401, non-2xx, non-JSON and `ok:false` responses instead of resolving with an `Error` object.
- Exports containing Word/Excel files are now blocked with a clear “无法开始导出 / Export cannot start” dialog listing the files that need LibreOffice, instead of an internal error.
- Added regression tests for API error classification.

## UI

- Replaced every native browser `<select>` popup with a custom trigger and floating menu: selected check mark, hover/focus/disabled states, light and dark themes, keyboard navigation, typeahead, outside-click close, scroll tracking, viewport flipping and narrow-screen clamping.
- Updated the application icon to the blue multi-format document icon with the orange plus. The same artwork is used by the App Center icon, favicon and in-app brand mark.

## Verification

- 71 backend tests passed on Windows and on Linux x86_64 Python 3.10 with packaged dependencies; 14 frontend tests passed.
- Local Playwright E2E passed, including PDF export and download.
- Real TOS 7.1 x86_64: App Center 0.1.4 → 0.1.5 upgrade completed at 100%; new icon renders in App Center and in the iframe.
- Custom dropdowns and the LibreOffice-missing export dialog were verified in the real TOS iframe. The dialog listed the two Excel files and did not show the previous `id` error.
- Existing workspaces, assets, assemblies, assembly items and export history were preserved after the upgrade.
- Health endpoint reports `version=0.1.5`; systemd service active; Unix socket healthy.
- x86_64 and aarch64 packages structure, ELF architecture and SHA-256 verified.

## Assets

| File | Size | SHA-256 |
| --- | ---: | --- |
| `filemerge-pdf_0.1.5_x86_64.deb` | 8,661,356 B | `6233f93b2e534bf3232a6b84c27653b227ff98c04e7ba928dd90b334366f117e` |
| `filemerge-pdf_0.1.5_aarch64.deb` | 6,875,784 B | `07d0a5a5f62cfe11ea8a62681e0e02eb74c72688472142ed14ae4aed69d38722` |

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
