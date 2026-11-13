# Confluence RAG Exporter

Windows desktop application for exporting selected Confluence pages and their child-page hierarchy to a local RAG knowledge base.

## Features

- Confluence Server / Data Center via REST API and Netscape-format browser cookies
- Page-tree selection with checkboxes (all selected by default)
- Support for `/pages/viewpage.action?pageId=...` and `/display/SPACE/Page+Title` URLs
- Hierarchical export with natural sorting and configurable export depth
- Combined Markdown and HTML, plus PDF generated with Chromium / Playwright
- Local download of embedded images to an `assets/` directory
- Source links back to individual Confluence pages
- Export manifest with warnings, missing pages and failed assets
- Configurable local RAG and temporary export folders
- REST request timeouts, retries and fallback to alternative body representations

## Requirements

- Windows 11
- Python 3.12+
- Chromium installed by Playwright
- Access to a Confluence instance and an authenticated Netscape-format `cookies.txt`

## Installation

```powershell
git clone https://github.com/nikolay-kochubashev/confluence-RAG-exporter.git
cd confluence-RAG-exporter
python -m pip install -r requirements.txt
python -m playwright install chromium
python .\confluence_rag_exporter.py
```

Alternatively, start the app with `run.bat` after installing its dependencies.

## Usage

1. Log in to your Confluence site and export its cookies in **Netscape** format.
2. Select the exported cookies file in the application.
3. Paste a Confluence page URL and click **Загрузить дерево**.
4. Review and adjust the checked pages and export depth.
5. Choose the destination (local RAG or temporary directory) and export name.
6. Export the selected content and check the resulting `manifest.json` for warnings.

Exports contain a combined Markdown file, an HTML file, a PDF, downloaded images and a manifest. The PDF filename matches the chosen export folder name.

## Limitations

- Some Confluence macros and embedded assets may not export exactly as rendered in the browser.
- Some on-prem Confluence instances do not support the `descendant/page` endpoint. The application falls back to `child/page`.
- A page that remains unavailable after retries is marked as incomplete; verify the manifest before importing the PDF into a ChatGPT Project.
- Uploading files to ChatGPT Projects is not automated.

## Security

**Do not commit cookies, downloaded internal Confluence documents, exported PDFs or local settings.** Cookies can grant access to your corporate Confluence session. Only upload material you are authorized to publish.

## Development

The application is built with Python, PySide6, Requests, Beautiful Soup and Playwright. Development is ongoing; see the app log for detailed diagnostics.
