---
title: Backend Integration Contract - Release Assistant
created: 2026-05-06
source_folder: /home/yshvadro/CSM Central
tags:
  - csm-ai-plan
  - backend
  - release-assistant
---

# Backend Integration Contract - Release Assistant

## Scope

This document captures the backend behavior implied by `Mockup_Release_Assistant.html`. It is not a final API spec. It is the observed contract from the current frontend code.

## Current Frontend Assumptions

- `API_BASE = ''`
- `BACKEND_BASE = ''`
- Therefore all API paths are same-origin unless Cloud Ops edits the file.
- If the page is opened with `file://`, the `api()` function throws and tells the user to open `http://127.0.0.1:8000/mockup`.
- The page tries backend mode first, then falls back to local/offline release index data in some flows.
- Local/offline mode expects `window.RELEASE_26_1_INDEX` from `data/release_26_1_index.js`, which is not present in the folder.

## Observed Endpoints

### `POST /api/chat`

Used by search/ask flow.

Request body:

```json
{
  "question": "user question text",
  "show_sources": true,
  "top_k": 8
}
```

Expected response fields:

```json
{
  "answer": "string",
  "results": [
    {
      "title": "string",
      "url": "string",
      "product": "string",
      "feature_name": "string",
      "release": "string",
      "enabled": "string",
      "value_analysis": "string",
      "answer": "string",
      "description": "string",
      "location": {
        "page": 1
      },
      "files": []
    }
  ]
}
```

The frontend mostly renders `results`; the raw `answer` is read but not directly displayed as the main answer in the current code.

### `GET /api/backend/filters`

Used to populate planner filters.

Expected response:

```json
{
  "releases": ["26.1"],
  "products": ["eProcurement"]
}
```

### `GET /api/backend/features?limit=3000`

Used to load planner feature rows.

Expected response:

```json
{
  "rows": [
    {
      "id": "string",
      "name": "string",
      "feature_name": "string",
      "release": "26.1",
      "product": "string",
      "core": "string",
      "enablement_type": "string",
      "source_url": "string",
      "url": "string"
    }
  ]
}
```

Also called with query parameters:

```text
/api/backend/features?releases=26.1&products=eProcurement&limit=3000
```

### `GET /api/backend/metrics`

Used to show feature counts and enablement mix.

Expected response:

```json
{
  "total_features": 0,
  "requires_testing": 0,
  "by_enablement": [
    {
      "name": "Configuration required",
      "count": 0
    }
  ]
}
```

Also called with the same `releases`, `products`, and `limit` query parameters as the features endpoint.

### `GET /api/backend/export.xlsx?...`

Used by the `Generate Excel Test Plan` button when backend mode is enabled.

Expected behavior:

- Return an XLSX file download or browser-openable response.
- Query parameters may include `releases` and `products`.
- The frontend opens this URL in a new tab/window.

### `POST /api/create-document`

Used for:

- local/non-backend `Generate Excel Test Plan`,
- `Create File` for testing CSV export, PowerPoint deck, or training tool.

Observed request bodies:

```json
{
  "pdf_ids": ["selected source ids or source URLs"],
  "title": "Test and Training Plan"
}
```

or:

```json
{
  "pdf_ids": ["selected source ids or source URLs"],
  "title": "PowerPoint Deck - Release Materials"
}
```

Expected response:

```json
{
  "file_url": "https://authenticated-or-signed-file-url"
}
```

### `POST /api/create-video-tutorial`

Used by Feature Video Studio.

Request body:

```json
{
  "pdf_ids": ["selected source ids or source URLs"],
  "impact_context": "user supplied audience/context text"
}
```

Expected response:

```json
{
  "tutorial": "generated tutorial text",
  "html_url": "generated walkthrough URL",
  "file_url": "generated script URL"
}
```

### `POST /api/create-feature-slides`

Used by Feature Slide Studio.

Request body:

```json
{
  "pdf_ids": ["selected source ids or source URLs"]
}
```

Expected response:

```json
{
  "file_url": "generated PPTX URL",
  "template_used": "template name",
  "slides_created": 0
}
```

## Backend Data Model Implied By Frontend

Minimum backend objects:

- Release document/source:
  - id/source URL
  - title
  - URL
  - product
  - core
  - release
  - page/location
  - text chunks or semantic summaries
- Feature row:
  - id
  - feature_name/name
  - release
  - product
  - core
  - enablement_type
  - source_url/url
- Metrics:
  - total features
  - requires testing count
  - enablement distribution
- Generated file:
  - id
  - file type
  - owner/user
  - created time
  - expires time
  - storage URI
  - download URL

## Security Requirements For This Backend

- Same SSO/auth as the CSM Central app.
- Authorization on every selected `pdf_id` or source URL.
- Validate all selected source IDs against allowed release-document records.
- Do not let arbitrary URLs become backend fetch targets.
- Return generated file links that are authenticated or short-lived signed links.
- Enforce retention and cleanup for generated files.
- Avoid logging raw user questions, prompt context, selected confidential documents, or generated content unless required and approved.
- Rate limit chat/document/video/slide generation.
- Add malware/content checks if users can upload source docs in future.

## Open Implementation Questions

- What backend runtime is intended: Python/FastAPI, Node/Express, serverless, or existing internal platform?
- What AI/LLM provider is intended, if any?
- Where will source PDFs/release notes be indexed?
- Should `pdf_ids` be stable database ids instead of source URLs?
- Where will generated files be stored, and for how long?
- Should generated outputs be watermarked or tagged as AI-generated/internal?
- Should release source data be refreshed manually, scheduled, or via CI?

