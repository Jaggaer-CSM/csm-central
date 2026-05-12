---
title: Data Security
created: 2026-05-06
source_folder: /home/yshvadro/CSM Central
tags:
  - csm-ai-plan
  - data-security
  - cloud-ops
---

# Data Security

## Security Posture In Current Files

The current project is prototype-level from a security standpoint. Most tools are client-side static HTML. The files do not define authentication, authorization, server-side access control, encrypted storage, backend logging, rate limiting, or deployment headers.

Some tool code does escape user-rendered text before injecting into HTML, but several pages also use `innerHTML` heavily. This is manageable for trusted static data, but Cloud Ops should review it carefully before connecting untrusted backend data or uploaded customer content.

## Current Positive Signals

- `CSM_Central.html` escapes generated tool names, descriptions, and attributes before injecting markup.
- Most uploaded files are processed locally in the browser instead of sent to a server.
- Tool links generally use `rel="noopener"` when opened in a new tab.
- `Success_Plan.html` includes `meta name="robots" content="noindex, nofollow"`.
- `workflow_analyzer.html` escapes parsed XML content before rendering table values.
- `Support_Case_Analysis.html` escapes rendered dashboard values from parsed support data.

## Current Risks

| Risk | Why it matters | Where observed |
|---|---|---|
| Embedded confidential data in static HTML | Any user with file access can read source data. | `Success_Plan.html`, `Support_Case_Analysis.html`, `Full-suite-savings-tool.html`, `AI_Roadmap.html`, `Elevator.html` |
| No authentication in files | No access control is implemented at app level. | Entire folder |
| External scripts on confidential pages | Third-party scripts can expand data/privacy surface. | `Success_Plan.html`, `Support_Case_Analysis.html` |
| Missing backend security contract | Release Assistant needs APIs and generated files, but auth/retention is not defined. | `Mockup_Release_Assistant.html` |
| Generated-file exposure | File URLs returned by backend may be shareable or long-lived unless Cloud Ops controls them. | `Mockup_Release_Assistant.html` |
| Local/missing asset references | Broken references can produce incomplete behavior or accidental path leakage. | `Elevator.html`, `AI_Roadmap.html`, `Success_Plan.html` |
| Supply-chain dependency | Spreadsheet parsing loads from jsDelivr. | `Support_Case_Analysis.html` |
| CSP not defined | No browser-level allowlist is present in the files. | Entire folder |
| Large upload parsing in browser | Could freeze the browser or expose parsing bugs. | `Support_Case_Analysis.html`, `New_Value_Calculator.html`, `workflow_analyzer.html` |

## Minimum Production Controls

### Hosting And Access

- Host behind company SSO.
- Restrict access by role and audience: CSM, manager, Cloud Ops/admin, product, or account-owner roles.
- Use HTTPS only.
- Do not rely on `noindex` for confidentiality.
- Separate demo/prototype tools from production tools if they contain sample customer data.

### Data Handling

- Classify every data source before ingestion: public, internal, confidential customer, support case, commercial/financial, employee/manager, or highly restricted.
- Do not embed confidential datasets directly into static HTML for production.
- If uploads remain browser-only, document that the data does not leave the browser.
- If uploads move server-side, define:
  - maximum file size,
  - allowed file types,
  - malware scanning,
  - tenant/customer/account scoping,
  - encryption at rest,
  - deletion window,
  - audit log events,
  - redaction of sensitive fields from logs.

### Backend / API

- Require authentication for every API.
- Enforce authorization on every customer/account/resource id.
- Validate all request bodies and query parameters.
- Rate limit chat and document-generation endpoints.
- Log request metadata without storing full prompts, customer data, uploaded file content, or generated documents unless explicitly required.
- Return generated files through authenticated, short-lived URLs.
- Add retention cleanup for generated XLSX, PPTX, HTML tutorials, and scripts.

### Frontend

- Add a strict Content Security Policy.
- Prefer vendored or approved internal versions of dependencies used on confidential pages.
- Remove Google Tag Manager and Embedly from customer-confidential pages unless approved.
- Add `rel="noopener noreferrer"` to external links.
- Replace local `file://` links with authenticated internal URLs or remove them.
- Avoid rendering backend-controlled HTML directly. Use textContent or sanitized templates.

### Headers To Plan

Recommended starting point for an authenticated internal deployment:

```text
Content-Security-Policy: default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data:; font-src 'self'; connect-src 'self'; frame-ancestors 'none'; base-uri 'self'; form-action 'self'
Referrer-Policy: no-referrer
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Permissions-Policy: clipboard-write=(self)
Strict-Transport-Security: max-age=31536000; includeSubDomains
```

This CSP will need adjustment if Cloud Ops allows Google Fonts, jsDelivr, GTM, Embedly, JAGGAER Library, SharePoint, or Salesforce links/scripts.

## Security Review By Tool

| Tool | Security recommendation |
|---|---|
| `CSM_Central.html` | Safe as a private launcher if child tool permissions are controlled. Consider server-provided manifest with role filtering. |
| `AI_Roadmap.html` | Treat as internal confidential roadmap. Remove local `file://` link and confirm SharePoint links are permissioned. |
| `Elevator.html` | Do not deploy until missing assets and actual data handling are reviewed. The page self-labels as confidential. |
| `Full-suite-savings-tool.html` | Fine as browser-only calculator for authorized users. If saving outputs centrally, apply commercial-data retention and access controls. |
| `Mockup_Release_Assistant.html` | Needs full API security design before production. Main risk is backend prompts, generated files, and source-document access. |
| `New_Value_Calculator.html` | Treat uploaded/customer-entered data as commercial confidential. Browser-only mode reduces server exposure. |
| `Success_Plan.html` | Remove third-party tracking/widgets or get explicit approval. Move customer-specific data behind auth/account permissions. |
| `Support_Case_Analysis.html` | Treat data as confidential support/customer data. Consider vendoring `xlsx` or replacing with backend-controlled parser if required. |
| `workflow_analyzer.html` | Treat workflow XML as sensitive configuration. Browser-only parsing is good, but file outputs should be handled carefully. |

## Questions Cloud Ops Must Answer

- Is this intended as an internal authenticated app only, or will customers ever access it?
- Which tools are production candidates now versus prototypes?
- Should customer data be embedded in static files for demos, or always loaded from authenticated APIs?
- Are third-party scripts allowed on pages containing customer-specific data?
- What retention policy applies to uploaded support reports, workflow XML files, generated PPTX/XLSX, and LLM prompts/responses?
- Which source systems are approved for automated data pulls?

