# Changelog

All notable changes to Metadata Cleaner & Editor are documented here.

---

## [v0_3] — 2026-06-28

### Changed
- **Bundled both libraries locally** — JSZip and pdf-lib are now served from `vendor/` instead of external CDNs. The app now works fully offline from the first visit with no internet connection required at any point.
- Added `vendor/LICENSES.md` preserving the MIT copyright notices for both bundled libraries (JSZip © Stuart Knightley et al.; pdf-lib © Andrew Duncanu).
- Added inline attribution comments in `index.html` next to each `<script>` tag.
- Version label updated to v0_3 throughout.

### Why
CDN-hosted scripts require an internet connection on first load. Bundling eliminates that dependency while remaining fully MIT-compatible — both libraries are MIT licensed, matching this project.

---

## [v0_2] — 2026-06-28

### Added
- **Full PDF read/write support** via [pdf-lib](https://pdf-lib.js.org/) — PDFs now save with edited metadata. Previously, the app could only extract PDF properties and would re-download the original file unchanged on save.
- **Subject** field — exposed in both Office (`dc:subject` in `core.xml`) and PDF (`/Subject`).
- **Description / Comments** field — reads and writes `dc:description` in Office files; maps to `/Subject` in PDFs (closest equivalent in the PDF spec).
- **Last Modified By** field — reads and writes `cp:lastModifiedBy` in Office files. This field tracks the username of whoever last saved the document and is a common privacy leak when sharing files externally.
- **Producer / App** field — reads and writes the `Application` entry in `docProps/app.xml` for Office files and `/Producer` for PDFs. This field fingerprints the software used to create or last save the document (e.g. "Microsoft Word 16.0", "Adobe Acrobat Pro").

### Changed
- Renamed project from **Copilot Agent: Metadata Cleaner & Editor** to **Metadata Cleaner & Editor**.
- Replaced the fragile regex-based PDF header scan with a proper pdf-lib parse, which correctly handles hex-encoded strings and modern PDF structures.
- Reorganized the metadata form into labeled sections — **Core Identity**, **Organization**, **Classification**, **Dates & Tracking**, **Software Fingerprint**, and **Description** — for easier scanning.
- Description field uses a full-width textarea instead of a single-line input.

---

## [v0_1] — 2026-06-28

### Initial Release

First public alpha of Metadata Cleaner & Editor — a 100% client-side web app for viewing, cleaning, and editing the hidden metadata embedded in Office documents and PDFs. No installation, no build step, no backend. All processing happens in the browser; no file content or metadata is ever sent to a server.

### Features
- **Drag-and-drop upload** for `.docx`, `.pptx`, `.xlsx`, and `.pdf` files.
- **OOXML metadata extraction and write-back** — reads `docProps/core.xml` and `docProps/app.xml` from Office Open XML archives using [JSZip](https://stuk.github.io/jszip/); patches only metadata nodes on save, leaving document content untouched.
- **Basic PDF metadata extraction** — scans the PDF file header for standard Info dictionary entries.
- **10 editable metadata fields**: Title, Author, Company, Manager, Keywords, Created Date, Category, Revision Number, Status, Copyright.
- **Template system** — two renameable template slots for applying a pre-configured set of field values in one click; ideal for enforcing consistent metadata standards across a team.
- **Split save button** — download using the original filename or export with a new name.
- Works fully offline once the JSZip CDN script is cached.
- MIT License.
