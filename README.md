## Upstage Document Parsing Plugin for Dify

A powerful document parsing plugin for the [Dify](https://dify.ai) platform that leverages the Upstage Document Parse API to convert various document formats into structured Markdown, HTML, or plain text.

### Features

- **Broad format support**: Handles PDF, DOCX, and various image formats
- **Intelligent document understanding**: Extracts text, tables, charts, and figures while preserving original structure
- **Multiple output formats**: Converts documents to Markdown, HTML, or plain text
- **Efficient caching**: Content-based caching prevents reprocessing of identical files
- **OCR capability**: Extracts text from scanned documents and images
- **Chart recognition**: Identifies and extracts charts from documents
- **Batch processing**: Efficiently processes multi-page documents
- **Coordinate extraction**: Obtains bounding box coordinates for document elements

### Installation

This plugin is under active development.

```bash
pip install -r requirements.txt
```

Configure the plugin in the Dify platform.

### Configuration

#### Required credentials

The plugin requires the following credentials:

- `upstage_api_key`: Upstage API key (obtain it from the [Upstage Console](https://console.upstage.ai))
- `base_url`: Base URL for your Dify instance (default: "https://cloud.dify.ai")

#### Parameter options

You can configure the following parameters when using the tool:

- `result_type`: Output format (options: "md", "html", "text")
- `as_file`: Whether to return the result as a file or text (options: "file", "text")

### Usage

#### In a Dify application

1. Add the Upstage Document Parse tool to your application.
2. Configure the required credentials.
3. Use the tool within your application flow to process documents.

#### Direct usage in Python

You can also use the client directly in Python:

```python
from tools.upstage_client import UpstageDocumentParseClient

# Initialize the client
client = UpstageDocumentParseClient(
    api_key="your_upstage_api_key",
    output_dir="exported_documents"
)

# Convert a document to Markdown
markdown_content = client.convert_to_markdown("path/to/your/document.pdf")

# Convert a document to HTML
html_content = client.convert_to_html("path/to/your/document.docx")

# Convert a document to plain text
text_content = client.convert_to_text("path/to/your/image.jpg")
```

### API Parameters

The plugin uses the following parameters when calling the Upstage Document Parse API:

| Parameter           | Type         | Description                                                                                           | Default                      |
| ------------------- | ------------ | ----------------------------------------------------------------------------------------------------- | ---------------------------- |
| `document`          | File         | The document file to process                                                                          | Required                     |
| `ocr`               | String       | Control OCR behavior: "auto" (applies only to images) or "force" (convert everything to images first) | "auto"                       |
| `coordinates`       | Boolean      | Whether to return bounding box coordinates                                                            | false                        |
| `chart_recognition` | Boolean      | Whether to use chart recognition                                                                      | true                         |
| `output_formats`    | List[String] | Formats for layout elements: "text", "html", "markdown"                                               | ["html", "markdown", "text"] |
| `model`             | String       | Model used for inference                                                                              | "document-parse-250305"      |
| `base64_encoding`   | List[String] | Layout categories to provide as base64-encoded strings                                                | ["table", "figure", "chart"] |

### Caching Mechanism

The plugin implements an efficient caching system:

1. File content hashing to identify duplicate documents
2. Result caching based on content hash and output format
3. TTL-based cache expiration (default: 1 hour)

### Examples

#### Convert a PDF to Markdown

```python
client = UpstageDocumentParseClient(api_key="your_api_key")
markdown = client.convert_to_markdown("sample.pdf")
print(markdown)
```

#### Handling large documents

```python
client = UpstageDocumentParseClient(api_key="your_api_key")
exported_files = client.process_document(
    "large_document.pdf",
    wait=True,
    poll_interval=2,
    max_wait=600
)
print(f"Exported files: {exported_files}")
```

### Development

#### Project structure

- `upstage-documentparse.py`: Main Dify plugin integration
- `upstage_client.py`: Core client that interacts with the Upstage API
- `requirements.txt`: Python dependencies
