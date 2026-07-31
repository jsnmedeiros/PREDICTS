# PREDICTS Metadata Extraction

This project automatically extracts metadata from ecological papers for the PREDICTS database.

## Pipeline

1. Extract PDF text
2. Extract tables with Docling
3. OCR maps and figures
4. Analyse figures using Ollama Vision
5. Download repository data
6. Extract metadata
7. Fill the PREDICTS form

## Website 
For more information please go to https://jsnmedeiros.github.io/PREDICTS/

## Requirements

**Python:** 3.11+ (developed on 3.11.6)

### Python packages

pip install pandas pdfplumber pypdf openpyxl requests pymupdf docling pillow pytesseract selenium

Or as `requirements.txt`:

pandas
pdfplumber
pypdf
openpyxl
requests
pymupdf
docling
pillow
pytesseract
selenium

### External (non-pip) dependencies - LiNuX

- **Ollama** — required for the LLM metadata fallback (`--model`) and vision-based
  image/map/plot analysis (`--vision-model`). Not on PyPI; install separately and
  keep the server running:

  ollama serve
  ollama pull gemma3:4b   # or whichever model you pass to --model / --vision-model

- **Tesseract OCR** — required only for the OCR step (`ocr_useful_images`); the
  script degrades gracefully (skips OCR, no crash) if `pytesseract` can't find a
  Tesseract binary. Install the Tesseract binary separately from the `pytesseract`
  pip package.

- **Firefox or Chrome** — used only as a Selenium fallback for supplementary-data
  downloads that need a real browser (e.g. Dryad share links). Selenium ≥4.6
  auto-manages the matching driver, so just having the browser installed is enough.

### External (non-pip) dependencies - Windows 

- **Ollama**: native Windows installer available from ollama.com — installs as a
  background service, so no separate `ollama serve` step; just `ollama pull <model>`.
- **Tesseract**: no system package manager equivalent to `apt`/`brew` — install via
  the Windows build, then either add its install folder to `PATH` or
  set it explicitly in code:
  `pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"`
- **Selenium/browsers**: Chrome or Firefox installed normally; Selenium Manager
  handles the driver the same as on Linux.
- **Everything else** (pandas, pdfplumber, pymupdf, docling, etc.) installs
  identically via `pip` on Windows — no Linux-specific build steps in this stack.
- **Path separators**: the script uses `pathlib.Path` throughout, so no changes
  needed there.
