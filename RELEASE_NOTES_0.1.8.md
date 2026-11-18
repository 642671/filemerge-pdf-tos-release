# v0.1.8 — FileMerge PDF for TOS 7

Release date: 2026-11-18

## Release type

Light-theme and sidebar polish release.

## Fixes

- Removed the `>` chevron from the sidebar “所有工作区 / All workspaces” link. The entry is now plain text and aligned with the workspace title.
- Set native control `color-scheme` from the application theme:
  - Light theme uses `color-scheme: light`.
  - Dark theme uses `color-scheme: dark`.
  - This fixes native checkboxes and other form controls rendering with the OS dark palette—and black selection boxes—while the application is in light mode.
- Includes all 0.1.7 improvements: draggable export dialogs, structured success/failure details, history-link dialog close, clickable home stat cards, and Chinese font cache invalidation.

## Verification

- 71 backend tests passed on Windows and on Linux x86_64 Python 3.10 with packaged dependencies; 14 frontend tests passed.
- Local UI check with browser `colorScheme: dark` and the app forced to light:
  - `data-theme=light`
  - checkbox `color-scheme=light`
  - checkbox accent color `rgb(37, 99, 235)`
  - sidebar back link contains no SVG chevron.
- Real TOS 7.1 x86_64:
  - App Center 0.1.7 → 0.1.8 upgrade completed at 100%.
  - Sidebar “所有工作区” displays without `>`.
  - Light-mode checkbox selection is blue, not black.
  - Existing workspaces, assets, assemblies, assembly items and export history were preserved.
  - Health endpoint reports `version=0.1.8`.
- x86_64 and aarch64 packages structure, ELF architecture and SHA-256 verified.

## Assets

| File | Size | SHA-256 |
| --- | ---: | --- |
| `filemerge-pdf_0.1.8_x86_64.deb` | 8,664,126 B | `193a1af6ab4a88c04d7999b3cdc068bd9f9940c7b267c32804164d3859b85176` |
| `filemerge-pdf_0.1.8_aarch64.deb` | 6,878,466 B | `ef62920d4da8c89101b060337b421276f31cd0535f695198b930dcda7e700fa4` |

Each package has a matching `.sha256` file in this Release.

## Requirements

- TerraMaster TOS 7.0+
- x86_64/amd64 or aarch64/arm64
- Python 3.10 runtime provided by TOS
- LibreOffice Writer and Calc for Word/Excel export
- `fonts-noto-cjk` for Chinese Word/Excel PDF output

## Known limitations

- No SMB/NFS-visible application shared folder yet.
- Single-user administrator MVP; no per-TOS-user workspace isolation.
- Encrypted PDFs are rejected.
- Page-level PDF editing is planned for P1.
- Word/Excel layout may differ from Microsoft Office.
- PDF text copy/search with CJK fonts may be incomplete even when visual rendering is correct.
- aarch64 runtime and App Center disable/uninstall data retention are not yet verified.
