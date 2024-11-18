# confluenceScraper 

## Overview

ConfluenceScraper is a Python script designed to search and extract information from Confluence pages and attachments. It supports searching for keywords in page content, binary attachments (like PDFs, DOCX, XLSX, TXT files), and images using Optical Character Recognition (OCR). The script allows you to specify search terms, control the number of threads, limit results, and more.

## Disclaimer

- Use at your own risk
- You may need to alter code for optimal usage

## Features

- Search for keywords in Confluence page content.
- Extract information from binary attachments (PDF, DOCX, XLSX, TXT).
- Perform OCR on image attachments to extract text (PNG, JPG, JPEG, TIFF, BMP, GIF).
- Limit the number of images processed.
- Multithreaded for faster processing.
- Save extracted information to a file.

## Requirements

- **Python 3.7+**
- **Confluence API Access Token** with appropriate permissions.

### Python Packages

All required Python packages are listed in `requirements.txt`.

### External Dependencies

- **Tesseract OCR Engine** (for OCR functionality)

  - **macOS**: Install via Homebrew
    ```bash
    brew install tesseract
    ```
  - **Ubuntu/Debian**:
    ```bash
    sudo apt-get install tesseract-ocr
    ```
  - **Windows**:
    - Download and install from [Tesseract OCR GitHub](https://github.com/UB-Mannheim/tesseract/wiki).

## Installation

### Required Arguments

- `-c, --url <TARGET_URL>`: **Mandatory**. The base URL of the Confluence instance (e.g., `https://confluence.company.com`).

### Optional Arguments

- `-p, --accesstoken <API_ACCESS_TOKEN>`: API access token for authentication, if needed.
- `-w, --wordlist <WORDLIST_FILE_PATH>`: Path to a file containing keywords to search for. One keyword per line.
- `-k, --keyword <SINGLE_KEYWORD>`: Specify a single keyword for the search.
- `-s, --search-content`: If set, the script will extract and save content around the found keyword on each page.
- `-n, --num-chars <NUM_CHARS>`: Number of characters to extract after the found keyword. Default is 10 characters.
- `-t, --threads <THREADS>`: Number of threads to use. Default is 10.
- `-l, --limit <LIMIT>`: Limit the number of search results to process. By default, all results are processed.

And more! 

### Some Example Commands

1. **Search using a wordlist**:
    ```bash
    python3 ConfluenceScraper.py -c https://confluence.company.com -p myApiToken123 -w keywords.txt -t 10 -s -n 200
    ```

2. **Search using a single keyword**:
    ```bash
    python3 ConfluenceScraper.py -c https://confluence.company.com -p myApiToken123 -k "search-term" -s
    ```

3. **Limit the number of search results**:
    ```bash
    python3 ConfluenceScraper.py -c https://confluence.company.com -p myApiToken123 -w keywords.txt -l 50
    ```

4. **Run with default settings but extract surrounding content**:
    ```bash
    python3 ConfluenceScraper.py -c https://confluence.company.com -p myApiToken123 -k "search-term" -s -n 150
    ```
5. **Run with OCR in images and max image search number**:
    ```bash
    python3 ConfluenceScraper.py -c https://confluence.company.com -p myApiToken123 -k "search-term" -s -i -m 5
    ```


## Output

- Results will be saved in the `./loot` directory.
  - If `-s` is used, the script will save both the URLs and extracted content surrounding the found keyword.
  - If `-s` is not used, only the page URLs and titles will be saved.

