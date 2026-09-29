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

For more information, visit:

https://jsnmedeiros.github.io/PREDICTS/

## Installation

Choose the instructions for your operating system:

- [Linux installation](docs/linux.md)
- [Windows installation](docs/windows.md)

## Python dependencies

Install the required packages with:

```bash
python -m pip install -r requirements.txt
```

## External dependencies

The project also requires:

- [Ollama](https://ollama.com/) for LLM and vision analysis
- Tesseract OCR for OCR functionality
- Chrome or Firefox for Selenium-based downloads