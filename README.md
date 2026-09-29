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

For more information, please visit:

https://jsnmedeiros.github.io/PREDICTS/

## Requirements

**Python:** 3.11 or newer  
Developed using Python 3.11.6.

## Installation

### Linux and macOS

Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Upgrade `pip`:

```bash
python -m pip install --upgrade pip
```

Install the Python dependencies:

```bash
python -m pip install -r requirements.txt
```

### Windows

First, install Python 3.11 or newer.

Check that Python is installed:

```powershell
py --version
```

or:

```powershell
python --version
```

From the project directory, create a virtual environment:

```powershell
py -3.11 -m venv .venv
```

Activate the virtual environment:

```powershell
.\.venv\Scripts\Activate.ps1
```

If PowerShell prevents the virtual environment from being activated, run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

Then activate the environment again:

```powershell
.\.venv\Scripts\Activate.ps1
```

Upgrade `pip`:

```powershell
python -m pip install --upgrade pip
```

Install the Python dependencies:

```powershell
python -m pip install -r requirements.txt
```

The complete Windows setup is therefore:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## Python dependencies

The required Python packages are listed in `requirements.txt`:

```text
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
```

You can install them manually with:

```bash
python -m pip install pandas pdfplumber pypdf openpyxl requests pymupdf docling pillow pytesseract selenium
```

On Windows, use:

```powershell
python -m pip install pandas pdfplumber pypdf openpyxl requests pymupdf docling pillow pytesseract selenium
```

## External dependencies

The following dependencies are not installed through `pip`.

### Ollama

Ollama is required for:

- the LLM metadata fallback using `--model`;
- vision-based image, map, and plot analysis using `--vision-model`.

#### Linux and macOS

Install Ollama separately, then start the Ollama server:

```bash
ollama serve
```

In another terminal, download the required models:

```bash
ollama pull gemma3:4b
ollama pull moondream
```

#### Windows

Install Ollama using the Windows installer from:

https://ollama.com/

Ollama normally runs as a background service on Windows, so `ollama serve` is usually not required.

Download the required models:

```powershell
ollama pull gemma3:4b
ollama pull moondream
```

Check that Ollama and the models are available:

```powershell
ollama list
```

The project may use different models if they are specified through the `--model` or `--vision-model` options.

### Tesseract OCR

Tesseract OCR is required only for the OCR step, such as `ocr_useful_images`.

The Python package `pytesseract` is only a Python interface. The Tesseract application must also be installed separately.

If Tesseract is not available, the script should skip OCR instead of crashing.

#### Linux

Install Tesseract using your system package manager. For example:

```bash
sudo apt install tesseract-ocr
```

#### macOS

Install Tesseract using Homebrew:

```bash
brew install tesseract
```

#### Windows

Install the Windows version of Tesseract OCR. Then either:

1. Add the Tesseract installation directory to your Windows `PATH`; or
2. Set the executable path in Python:

```python
import pytesseract

pytesseract.pytesseract.tesseract_cmd = (
    r"C:\Program Files\Tesseract-OCR\tesseract.exe"
)
```

### Firefox or Chrome

Firefox or Chrome is used only as a Selenium fallback for supplementary-data downloads that require a real browser, such as Dryad share links.

Install either Google Chrome or Mozilla Firefox normally. Selenium 4.6 or newer includes Selenium Manager, which usually handles the matching browser driver automatically.

## Windows notes

- The Python packages install through `pip` in the same way as on Linux and macOS.
- The project uses `pathlib.Path`, so Windows path separators should be handled automatically.
- No Linux-specific build steps are required for the Python package installation.
- If `python` is not recognized, try using `py` instead.
- If PowerShell blocks environment activation, use:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

- If OCR does not work, check that Tesseract is installed and available in `PATH`.
- If Ollama-related features do not work, check the installed models:

```powershell
ollama list
```

## Quick Ollama check

To verify that the required Ollama models are installed:

```bash
ollama list
```

The list should include:

```text
gemma3:4b
moondream
```