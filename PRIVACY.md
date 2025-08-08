## Privacy Policy for Upstage Document Parser Plugin

Last Updated: 2025-08-08

This privacy policy explains how the Upstage Document Parser Plugin (the "Plugin") processes data when used within the Dify platform. This policy is designed to comply with Dify’s Plugin Privacy Protection Guidelines. See the guideline reference: [Dify Plugin Privacy Protection Guidelines](https://docs.dify.ai/en/plugins/publish-plugins/publish-to-dify-marketplace/plugin-privacy-protection-guidelines).

### 1. Overview

The Plugin enables document parsing by sending user-provided documents to the Upstage Document Digitization API for conversion into structured outputs (Markdown, HTML, Text). The Plugin operates as a processing tool and does not attempt to identify individuals beyond what is necessary to provide the service.

### 2. Types of Data Collected/Processed

The Plugin processes only the data you provide through your Dify application flow and generated outputs. Depending on the content you upload, documents may contain personal or sensitive information. Examples below follow the guideline categories:

- Direct identifiers (Type A): names, email addresses, phone numbers, physical addresses, government-issued identifiers (if present in the document content)
- Indirect identifiers (Type B): device identifiers, IP address (handled by hosting/network layers, not stored by the Plugin); location or online identifiers if included in the document content; financial, health, or biometric information if present in the document
- Potentially identifiable attributes (Type C): age, gender, occupation, interests when included in the document content

The Plugin itself does not prompt for or collect user profile data. Any such data appears only insofar as it is contained within the uploaded documents.

### 3. Data Sources

- User-provided files: PDF, DOCX, and image formats supplied by the user/application.
- Derived outputs: Structured results produced by the Upstage API (Markdown, HTML, Text) and optionally intermediate batch data during processing.

### 4. Purpose of Processing

- To convert documents into machine-readable formats (Markdown/HTML/Text)
- To optionally extract chart/table/figure content
- To facilitate downstream use in your Dify workflows or applications

### 5. Data Sharing with Third Parties

The Plugin transmits your documents to the Upstage Document Digitization API for processing:

- Service: Upstage Document Digitization API (document parsing/inference)
- Endpoint: https://api.upstage.ai/v1/document-digitization (default, configurable)
- Data shared: the uploaded document and parsing options; the service returns parsed content and batch metadata

Please review and comply with Upstage’s applicable terms and privacy policy for details on their data handling and retention. If your use requires a DPA or regional data residency, configure and contract with Upstage accordingly.

### 6. Credentials and Authentication

- The Plugin uses an `upstage_api_key` to authenticate with Upstage. This credential is configured in Dify and provided to the Plugin at runtime.
- The Plugin does not write the API key to exported files. Logs are limited and do not contain the API key.

### 7. Local Storage and Caching

- Exported files: Parsed outputs are written to the local filesystem directory configured by `output_dir` (default: `upstage_export/`). These files remain until deleted by the operator.
- In-memory cache: The Plugin maintains an in-memory cache of recently processed files (content-hash keyed) for up to 1 hour to avoid reprocessing. This cache stores only file paths, request identifiers, and timestamps in memory; it is not persisted across restarts.
- Temporary files: When debug mode is enabled, temporary JSON files may be written to a temporary directory and retained for troubleshooting. When debug mode is disabled (default), temporary files are deleted after use.

### 8. Retention

- The Plugin does not persist personal data beyond exported results and optional debug artifacts. Exported files remain on disk until you or your infrastructure lifecycle policies remove them. The in-memory cache expires automatically (default TTL: 1 hour) and is not persisted.

### 9. Security

- Transport security: Communication with Upstage uses HTTPS with Bearer token authentication.
- Access controls: Access to files and logs is controlled by your hosting environment. Ensure proper filesystem permissions and secret management for `upstage_api_key`.
- Logging: Operational logs avoid sensitive payloads but may include filenames, request identifiers, and status information. Configure logging levels according to your risk posture.

### 10. User and Operator Controls

- Consent and lawful basis: You are responsible for ensuring that you have the legal right to upload and process any documents (including those containing personal data).
- Deletion: Remove exported files under the configured `output_dir` and any `temp/` or debug directories in your environment to delete locally stored outputs. If you need deletion on Upstage’s side, follow Upstage’s procedures for data removal.
- Configuration: You can adjust OCR mode, chart recognition, coordinate extraction, and output formats in the Plugin settings to minimize data processing as needed.

### 11. Children’s Data

The Plugin is not intended for processing children’s personal data. Do not upload documents containing children’s personal information unless you have a lawful basis and necessary safeguards.

### 12. International Transfers

Documents are transmitted to Upstage’s API endpoint. Depending on your configuration and Upstage’s infrastructure, processing may occur in different regions. Consult Upstage’s documentation and agreements for data residency guarantees if required.

### 13. Changes to This Policy

We may update this policy to reflect functional or regulatory changes. Material changes will be versioned and dated at the top of this document.

### 14. Contact

For questions, requests, or to report an issue, please open an issue in the project repository: https://github.com/grayashh/dify-upstage-document-parser-plugin

---

Alignment with Dify Guidelines: This policy enumerates data categories, declares third-party processing, explains usage and retention, and points to a manifest reference (`privacy: PRIVACY.md`) in `manifest.yaml`. For the source guideline, see [Dify Plugin Privacy Protection Guidelines](https://docs.dify.ai/en/plugins/publish-plugins/publish-to-dify-marketplace/plugin-privacy-protection-guidelines).
