# Metadata Cleaner & Editor (v0_1)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![No Backend](https://img.shields.io/badge/backend-none-brightgreen)

> A lightweight, **100% client-side** web app for viewing, cleaning, and editing the hidden metadata embedded in Office documents and PDFs — no server, no uploads, no data leaves your machine.

---

## What It Does

Every `.docx`, `.pptx`, `.xlsx`, and `.pdf` file carries invisible metadata: author names, company identifiers, revision history, internal keywords, and more. This information often travels with a document long after it should — to clients, regulators, or the public.

**Metadata Cleaner & Editor** lets you:

- **Drag and drop** a file to instantly extract all its embedded properties
- **Review and edit** every metadata field in a clean form
- **Apply a template** to normalize fields in one click (useful for consistent company-wide standards)
- **Save the cleaned file** — either overwriting the original filename or exporting a new copy
- Do all of this **entirely in your browser**, with no data ever sent to a server

---

## Screenshot

![App UI](MetadataCleanerandEditorUI.jpg)

---

## Supported File Types

| Format | Extension | Metadata Source |
|--------|-----------|-----------------|
| Word   | `.docx`   | `docProps/core.xml` + `docProps/app.xml` |
| PowerPoint | `.pptx` | `docProps/core.xml` + `docProps/app.xml` |
| Excel  | `.xlsx`   | `docProps/core.xml` + `docProps/app.xml` |
| PDF    | `.pdf`    | File header scan (`/Author`, `/Title`, `/Keywords`) |

---

## Metadata Fields

The app surfaces and lets you edit all ten standard document properties:

| Field | Description |
|-------|-------------|
| **Title** | Document title |
| **Author** | Original author name |
| **Company** | Organization that created the document |
| **Manager** | Manager associated with the author |
| **Keywords** | Searchable tags embedded in the file |
| **Created Date** | Original creation timestamp |
| **Category** | Document classification (Business, Internal, Confidential, etc.) |
| **Revision Number** | How many times the file has been saved |
| **Status** | Workflow state (Draft, In Review, Final, Approved, Archived) |
| **Copyright** | Rights statement embedded in the file |

---

## Templates

The template system lets you apply a pre-configured set of field values in a single click — ideal for enforcing consistent metadata standards across a team or project.

Two template slots ship by default (**Template 1** and **Template 2**). Each template can be **renamed** in the UI via the ✏ button, so you can label them whatever makes sense for your workflow (e.g. "Client Deliverable", "Internal Draft", "Confidential").

---

## How It Works

Office Open XML files (`.docx`, `.pptx`, `.xlsx`) are ZIP archives. The metadata lives in two small XML files inside:

```
document.docx
├── docProps/
│   ├── core.xml     ← title, author, keywords, dates, category, revision, rights
│   └── app.xml      ← company, manager, application name
└── word/
    └── document.xml ← actual content (untouched)
```

This app uses [JSZip](https://stuk.github.io/jszip/) to unpack and repack the archive entirely in memory. When you save, it patches only the metadata XML nodes and regenerates the ZIP — the document content is never modified.

PDF metadata is extracted by scanning the file header for standard PDF info dictionary entries (`/Title`, `/Author`, `/Keywords`, `/Creator`, `/Company`).

---

## Usage

No installation. No build step. No dependencies to install.

1. Clone or download this repo
2. Open `index.html` in any modern browser
3. Drop a file onto the upload zone
4. Edit fields or apply a template
5. Click **Save Changes** to download the cleaned file

```bash
git clone https://github.com/toddholloway/O365Metadata.git
cd O365Metadata
open index.html   # macOS
# or just double-click index.html on Windows/Linux
```

---

## Privacy

All processing happens in your browser using the [File API](https://developer.mozilla.org/en-US/docs/Web/API/File) and [JSZip](https://stuk.github.io/jszip/). No file content, metadata, or any other data is ever transmitted to a remote server. The app works fully offline once the JSZip library is cached.

---

## Browser Compatibility

Works in all modern browsers (Chrome, Firefox, Edge, Safari). Requires JavaScript enabled.

---

## License

MIT License — Copyright © 2026 Todd Holloway. See [LICENSE](LICENSE) for full text.

You are free to use, modify, and distribute this software for any purpose.
