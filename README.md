
# AI-Agent PDF Extractor

This repository contains a Python-based automation script that processes PDF files by extracting their text content and performing natural language processing tasks, such as summarization or email extraction. The AI processing is powered by the [Ollama](https://ollama.com/) language model, with an option to integrate Azure OpenAI for more advanced or scalable NLP tasks.

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Examples](#examples)
- [Limitations](#limitations)
- [Contributing](#contributing)
- [License](#license)

## Project Overview

The **AI-Agent PDF Extractor** allows you to automate the extraction and processing of PDF documents using AI. It is designed to support various operations, such as:
- Summarizing the content of PDFs.
- Extracting email addresses from PDFs.

The project integrates with the Ollama language model, and it also provides an option to switch to Azure OpenAI for cases where large models, such as Phi-3, may be too large for your system.

## Features

- **PDF Text Extraction**: Uses `pdfplumber` to extract text from each page of the PDF.
- **Summarization**: Summarizes the extracted text using the Ollama model or Azure OpenAI.
- **Email Extraction**: Extracts email addresses from the text content.
- **Customizable Processing**: Choose between summarization or email extraction with an easy-to-configure setting.

## Requirements

- Python 3.7 or higher
- `pdfplumber` for PDF processing
- `requests` for making HTTP requests to the Ollama API

### External Services

- [Ollama](https://ollama.com/) for language model API
- Optional: [Azure OpenAI API](https://azure.microsoft.com/en-us/services/cognitive-services/openai-service/) for large-scale AI processing

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/Morteningemann86/AI-Agent-PDF-Extractor.git
   cd AI-Agent-PDF-Extractor
   ```

2. Create a virtual environment and activate it:

   ```bash
   python -m venv venv
   source venv/bin/activate   # On Windows use: venv\Scriptsctivate
   ```

3. Install the required Python dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Install the Ollama language model (optional):

   ```bash
   ollama run llama3.2:1b
   ```

5. If you're using Azure OpenAI, follow their [setup guide](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/quickstart).

## Configuration

All configurations are defined inside the script. You need to set the following variables:

- `PDF_DIR`: Path to the folder where your PDF files are located (e.g., `pdf_input`).
- `OUTPUT_DIR`: Path to the folder where the output files (summaries or extracted emails) will be saved (e.g., `pdf_output`).
- `OLLAMA_MODEL`: The model you want to use (default is `"phi3:latest"`).
- `OLLAMA_ENDPOINT`: The URL for the Ollama API (default: `http://localhost:11434/api/generate`).
- `PROCESSING_TYPE`: Choose between `"summarize"` or `"extract_emails"` to set the desired processing type.

Example:
```python
PDF_DIR = "pdf_input"              # Directory for input PDF files
OUTPUT_DIR = "pdf_output"          # Directory for processed output
OLLAMA_MODEL = "phi3:latest"       # Ollama model version
OLLAMA_ENDPOINT = "http://localhost:11434/api/generate"
PROCESSING_TYPE = "summarize"      # Choose 'summarize' or 'extract_emails'
```

## Usage

### Running the Script

1. Place your PDF files inside the folder specified by the `PDF_DIR` configuration.

2. Run the script with Robocorp:

   ```bash
   rcc run
   ```

The script will iterate through all the PDF files, extract the text, and either summarize it or extract email addresses, depending on the `PROCESSING_TYPE` setting.

### Customizing the Script

To modify the processing behavior, update the following configurations directly in the script:

- To **summarize** the text, set:
  ```python
  PROCESSING_TYPE = "summarize"
  ```

- To **extract email addresses**, set:
  ```python
  PROCESSING_TYPE = "extract_emails"
  ```

### Example Output

For summarization, the output will be saved as a text file with the suffix `_summary.txt`. For email extraction, the output will be saved with the suffix `_emails.txt`.

## Examples

### Summarization

If you choose to summarize a PDF, the extracted text from each page will be processed through the Ollama model, and a concise summary will be generated.

Example summary output (`_summary.txt`):

```
--- Page 1 ---
This document provides an overview of the project...

--- Page 2 ---
In conclusion, the key points discussed include...
```

### Email Extraction

If you opt to extract emails, the script will detect and list all email addresses found in the document.

Example email output (`_emails.txt`):

```
email1@example.com
contact@domain.com
```

## Limitations

- **Model Size**: Large models, such as `phi3`, may require a machine with higher specs. Consider using a smaller Ollama model like `llama3.2:1b` for testing or switch to Azure OpenAI.
- **PDF Content**: The script works best with text-based PDFs. Scanned or image-based PDFs will not yield useful results without OCR preprocessing.

## Contributing

Contributions are welcome! Please follow these steps to contribute:

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Submit a pull request with a detailed explanation of your changes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
