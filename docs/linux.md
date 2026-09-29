# Linux installation

## Requirements

- Python 3.11 or newer
- Ollama
- Tesseract OCR
- Chrome or Firefox

## Setup

Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the Python dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Install and start Ollama:

```bash
ollama serve
```

In another terminal, install the required models:

```bash
ollama pull gemma3:4b
ollama pull moondream
```

Install Tesseract using your Linux distribution's package manager.

For Ubuntu:

```bash
sudo apt install tesseract-ocr
```
