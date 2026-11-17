# v0.1.3 — FileMerge PDF for TOS 7

Release date: 2026-11-17

## Highlights

- Persistent workspaces, asset library, ordered assemblies, PDF export and export history.
- TOS 7 iframe WebUI with TOS session/CSRF and HTTP-over-Unix-Socket backend.
- Bundled pypdf, Pillow and typing_extensions; local PDF.js preview.
- Dual-architecture Debian packages for x86_64/amd64 and aarch64/arm64.

## Fixes in this release

- TOS proxy binary requests (thumbnails, PDF.js previews and downloads) now send `X-Csrf-Token` through authenticated fetch/Blob handling.
- Exports under platform-mapped symlinked data roots no longer fail with HTTP 500.
- Upload progress panels no longer cover export dialog controls.
- Removed the duplicate in-app titlebar inside the TOS App Center iframe.
- Kept the 56px host-titlebar safe area so the app topbar is not covered by TOS window controls.

## Verification

- 71 backend tests passed on Linux x86_64 Python 3.10 with the packaged dependencies.
- 9 frontend unit tests passed.
- Real TOS 7.1 x86_64: App Center install/enable, iframe open, TOS proxy/session/CSRF, upload, assembly, PDF export, history, download and PDF preview passed.
- App Center upgrades 0.1.0 → 0.1.1 → 0.1.2 → 0.1.3 preserved workspaces, assets, assemblies and export history.
- systemd stop/start and crash self-healing passed.
- x86_64 and aarch64 package structure, ELF architecture, dynamic links and SHA-256 verified.

## Assets

| File | SHA-256 |
| --- | --- |
| `filemerge-pdf_0.1.3_x86_64.deb` | `6e8cf1f3bc81b801f7094afb1ebb1bc02f9f26f64d7276882bb00a25f358727f` |
| `filemerge-pdf_0.1.3_aarch64.deb` | `6ebf6a0170055b28b025e0328a9756e0da006c2d1ece95e1c28feade07e1ee8a` |

Each package has a matching `.sha256` file in this Release.

## Known limitations

- No SMB/NFS-visible application shared folder yet; business data is retained across App Center upgrades in the application data directory.
- Single-user administrator MVP; no per-TOS-user workspace isolation.
- Encrypted PDFs are rejected.
- LibreOffice is not bundled; Word/Excel export requires a system installation.
- aarch64 runtime, App Center disable/uninstall data retention and page-level editing are not yet verified/implemented.
