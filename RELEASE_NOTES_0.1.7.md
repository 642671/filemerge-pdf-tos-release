# v0.1.7 — FileMerge PDF for TOS 7

Release date: 2026-11-18

## Release type

Export dialog, export history, home navigation and Chinese font fix release.

## Fixes and improvements

- All dialogs can now be dragged by their title bar, including export progress, success and failure details. The dialog is clamped to the viewport and has a visible drag handle.
- Clicking “导出记录” inside a result dialog now closes the dialog before navigating, so the history page is no longer hidden behind the old modal.
- Successful history entries now have a “详情” action, and the “更多” menu shows an enabled “查看详情”. The old disabled “查看错误详情” behavior is gone.
- Redesigned export details:
  - Success, failure and cancellation states have distinct status panels.
  - Shows assembly, output file, export time, duration, pages/size, output path and source-file list.
  - Failure details use a readable, wrapped, selectable error block with a copy button.
  - Stored internal file-name prefixes are stripped from error messages.
- The failed-export progress dialog uses the same structured layout.
- Home stat cards are now buttons:
  - “工作区” scrolls to the workspace list.
  - “资料总数”, “编排方案” and “导出记录” open the corresponding page in the most recently used workspace.

## Chinese PDF fix

The NAS had no CJK fonts (`fc-list :lang=zh` returned 0), so LibreOffice rendered Chinese as tofu boxes. Version 0.1.7 documents and verifies:

```sh
sudo apt-get install -y --no-install-recommends libreoffice-writer libreoffice-calc fonts-noto-cjk
```

The conversion cache key now includes the app version, LibreOffice version/path and a `fc-list :lang=zh` font fingerprint. Re-exporting after installing fonts forces a fresh conversion instead of reusing an old tofu PDF.

On the real NAS, the previously cached tofu PDF was regenerated: 72 pages, 1.31 MB, Chinese text renders correctly in the PDF viewer.

> Note: LibreOffice's CJK font subsetting can make the PDF text layer incomplete for copy/search, even though visual rendering is correct.

## Verification

- 71 backend tests passed on Windows and on Linux x86_64 Python 3.10 with packaged dependencies; 14 frontend tests passed.
- Local Playwright UI regression passed: stat-card navigation, draggable dialogs, history-link close, success details, success menu and detail download.
- Real TOS 7.1 x86_64:
  - App Center 0.1.6 → 0.1.7 upgrade completed at 100%.
  - Progress dialog dragged while an Office export was running.
  - Success and failure detail dialogs are draggable and structured.
  - History navigation closes the old dialog.
  - Chinese Excel + Word export succeeded: 72 pages, 1.31 MB, Chinese visible.
  - Existing workspaces, assets, assemblies, assembly items and export history were preserved.
  - Health endpoint reports `version=0.1.7`.
- x86_64 and aarch64 packages structure, ELF architecture and SHA-256 verified.

## Assets

| File | Size | SHA-256 |
| --- | ---: | --- |
| `filemerge-pdf_0.1.7_x86_64.deb` | 8,664,278 B | `e7d22ab9928e60aa8666561632898adcd6c5e7f038838332b967f63e65ce2225` |
| `filemerge-pdf_0.1.7_aarch64.deb` | 6,878,526 B | `4312d75dfbc764d1123086d1d948244deac589afffd4121215abeb277a4cda09` |

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
- Word/Excel layout may differ from Microsoft Office; output follows LibreOffice and the source file's print settings.
- PDF text copy/search with CJK fonts may be incomplete even when visual rendering is correct.
- aarch64 runtime and App Center disable/uninstall data retention are not yet verified.
