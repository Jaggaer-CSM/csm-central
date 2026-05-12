---
title: Full Tech Stack Map
created: 2026-05-06
source_folder: /home/yshvadro/CSM Central
tags:
  - csm-ai-plan
  - tech-stack
  - cloud-ops
---

# Full Tech Stack Map

## Confirmed Stack

The current project is a static HTML/CSS/JavaScript workspace.

There is no package manifest, build configuration, framework config, server file, Dockerfile, CI file, or environment file in the current folder. The runnable files are standalone `.html` files with inline CSS and inline JavaScript, except where noted below.

## Frontend

| Area | Confirmed implementation | Source evidence |
|---|---|---|
| App shell | `CSM_Central.html` is a static launcher page with inline CSS and JavaScript. | `CSM_Central.html:1`, `CSM_Central.html:7`, `CSM_Central.html:988` |
| UI runtime | Vanilla browser DOM APIs. No React/Vue/Angular imports in the current launcher. | `CSM_Central.html:1122`, `CSM_Central.html:1194`, `CSM_Central.html:1240` |
| Styling | Inline CSS using CSS variables and responsive media queries. | `CSM_Central.html:7`, `CSM_Central.html:8`, `CSM_Central.html:803` |
| Icons | Inline SVG `<symbol>` sprite inside the HTML. | `CSM_Central.html:925` |
| Navigation | Links open child tools in new tabs with `target="_blank"` and `rel="noopener"`. | `CSM_Central.html:891`, `CSM_Central.html:1307` |
| State | `localStorage` for favorites and recently used tools only. | `CSM_Central.html:1061`, `CSM_Central.html:1402`, `CSM_Central.html:1410` |
| Clipboard | Clipboard write for copy-link behavior, with textarea fallback. | `CSM_Central.html:1381` |

## Tool Pages

| File | Type | Stack / dependencies | Data handling |
|---|---|---|---|
| `CSM_Central.html` | Static launcher | Inline CSS/JS, inline SVG icons, browser localStorage, clipboard API. | Uses hard-coded list of child HTML files. Stores favorites/recent tool ids in localStorage. |
| `AI_Roadmap.html` | Static roadmap dashboard | Inline CSS/JS, inline SVG icons. No network `fetch` calls found. | Embeds roadmap metadata, SharePoint documentation links, accelerator data, and ROI assumptions. |
| `Elevator.html` | Incomplete local demo shell | References `./styles.css`, `./tamu-kb.js`, `./app.js`, and `./flow-chart.html`; these files are not present in the current folder. | HTML labels the demo as confidential and references SFDC, FinancialForce, Teams, Email, PROD Data, CSM Notes, and JAGGAER Engage. Actual logic/data likely lives in missing files. |
| `Full-suite-savings-tool.html` | Static calculator/exporter | Inline CSS/JS. Uses custom JavaScript ZIP/OpenXML generation for XLSX/PPTX. Uses `Blob` and `URL.createObjectURL`. | In-browser model inputs and example UT System rows. Exports XLSX/PPTX locally from browser. |
| `Mockup_Release_Assistant.html` | Hybrid static/backend prototype | Inline CSS/JS; Google Fonts; external JAGGAER Library links; local `data/release_26_1_index.js`; backend API calls through `fetch`. | Uses local release index in file/demo mode, otherwise sends questions and selected feature IDs to backend endpoints. |
| `New_Value_Calculator.html` | Static value calculator/exporter | Inline CSS/JS. Uses browser `Blob`, `URL.createObjectURL`, `DecompressionStream`, `DOMParser`, `navigator.clipboard`, and `window.print`. | In-browser ROI inputs. Can generate and parse customer Excel/CSV/TSV/HTML-table data locally. |
| `Success_Plan.html` | Static success-plan view inside exported app shell | Inline CSS/JS plus references to `/static/js/main.b7ebef3f.js`, `/static/css/main.987b114f.css`, Google Material Icons, Google Tag Manager, Embedly, `/manifest.json`, and `/favicon.ico`. | Embeds Kohler success-plan data and in-memory user selections/notes. Has `?export=1` print/export mode. |
| `Support_Case_Analysis.html` | Static dashboard with upload refresh | Inline CSS/JS, Google Fonts, jsDelivr `xlsx@0.18.5`. | Embeds a default support case analysis dataset and can parse uploaded XLSX/XLS/CSV in browser using FileReader/XLSX. |
| `workflow_analyzer.html` | Static XML analyzer | Inline CSS/JS. Uses `DOMParser`, `Blob`, and `URL.createObjectURL`. | Parses uploaded JAGGAER workflow XML locally in browser and exports a text report. |

## External Runtime Dependencies

| Dependency | Where found | Use | Cloud Ops note |
|---|---|---|---|
| Google Fonts / Material Icons | `Support_Case_Analysis.html`, `Mockup_Release_Assistant.html`, `Success_Plan.html` | Fonts/icons. | Decide whether external font loading is allowed for confidential internal tools. |
| jsDelivr `xlsx@0.18.5` | `Support_Case_Analysis.html:593` | Parse uploaded support report spreadsheets. | Pin/SRI or vendor internally if production requires supply-chain control. |
| Google Tag Manager | `Success_Plan.html:33-35` | Tracking script loader. | Remove or explicitly approve before handling customer-confidential content. |
| Embedly | `Success_Plan.html:37-38` | Widget/platform script. | Remove or explicitly approve before production. |
| JAGGAER Library URLs | `Mockup_Release_Assistant.html`, `Success_Plan.html` | Release documentation references. | Confirm access model and whether external links are intended. |
| Salesforce report URL | `Support_Case_Analysis.html:495` | Manual source-report link. | Confirm link visibility and whether users have permission. |
| SharePoint folder links | `AI_Roadmap.html:2036`, `AI_Roadmap.html:2063` | Full documentation links. | Confirm links are permissioned and not anonymous. |
| `file://wsl.localhost/...` local link | `AI_Roadmap.html:2693` | Local prototype reference. | Replace before any shared deployment. |

## Backend References

Only `Mockup_Release_Assistant.html` contains active `fetch()` calls. It calls:

- `POST /api/chat`
- `GET /api/backend/filters`
- `GET /api/backend/features?limit=3000`
- `GET /api/backend/metrics`
- `GET /api/backend/export.xlsx?...`
- `POST /api/create-document`
- `POST /api/create-video-tutorial`
- `POST /api/create-feature-slides`

`API_BASE` and `BACKEND_BASE` are both empty strings in the file, so the backend is expected to be same-origin unless Cloud Ops changes those values.

## Missing Assets / Not Present In Folder

These are referenced by HTML but not present in the folder inventory:

- `styles.css`
- `tamu-kb.js`
- `app.js`
- `flow-chart.html`
- `data/release_26_1_index.js`
- `/static/js/main.b7ebef3f.js`
- `/static/css/main.987b114f.css`
- `/manifest.json`
- `/favicon.ico`
- `AI roadmap copied to wsl2.xlsx`

Some may exist elsewhere, but they are not in `/home/yshvadro/CSM Central`.

## What Is Not Confirmed

- No production hosting platform is defined in the files.
- No database is defined in the files.
- No authentication or authorization layer is defined in the files.
- No backend implementation is present in this folder.
- No AI model provider or LLM runtime is directly configured in the current files.
- No centralized logging, monitoring, telemetry, or error reporting is defined in the current files, except third-party tracking code embedded in `Success_Plan.html`.

