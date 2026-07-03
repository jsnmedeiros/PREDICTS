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
