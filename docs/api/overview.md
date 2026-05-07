# API Overview

## Base URL
- Production: `https://api.facturation-saas.com/v1`
- Sandbox: `https://sandbox-api.facturation-saas.com/v1`
- Local: `http://localhost:3000/v1`

## Versioning
Versioning is handled via the URL prefix (`/v1/`). Breaking changes will result in a new version (e.g., `/v2/`).

## Response Format
All responses are returned in JSON format.
Success responses use standard HTTP 2xx codes.

## Error Handling
Errors follow a consistent structure:
```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable message",
    "details": {}
  }
}
```

## Rate Limiting
- Free Tier: 100 requests / minute
- Pro Tier: 1000 requests / minute
- Enterprise: Custom
