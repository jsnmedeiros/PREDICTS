# Windows installation

## Requirements

- Python 3.11 or newer
- Ollama
- Tesseract OCR
- Chrome or Firefox

## Setup

Check that Python is installed:

```powershell
py --version
```

Create and activate a virtual environment:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

Install the Python dependencies:

```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Install Ollama from:

https://ollama.com/

Download the required models:

```powershell
ollama pull gemma3:4b
ollama pull moondream
```

Install Tesseract OCR separately and add it to your Windows `PATH`.

If necessary, configure its location in Python:

```python
import pytesseract

pytesseract.pytesseract.tesseract_cmd = (
    r"C:\Program Files\Tesseract-OCR\tesseract.exe"
)
```
