---
title: Source Inventory
created: 2026-05-06
source_folder: /home/yshvadro/CSM Central
tags:
  - csm-ai-plan
  - source-inventory
---

# Source Inventory

## Inventory Summary

Files found in `/home/yshvadro/CSM Central` before creating this packet:

- 9 HTML files.
- 7 Windows `Zone.Identifier` metadata files.
- 13,330 total lines across all files.

The `CSM AI Plan` folder was created after this inventory.

## Source Files

| File | Lines | Type | Notes |
|---|---:|---|---|
| `AI_Roadmap.html` | 3,415 | HTML, UTF-8 | Static roadmap dashboard with inline CSS/JS, roadmap data, manager tools, accelerator drops, ROI view, SharePoint and local links. |
| `CSM_Central.html` | 1,453 | HTML, ASCII | Main launcher site. Static inline CSS/JS, hard-coded child tool list, search/filter/quick actions, favorites/recent localStorage. |
| `Elevator.html` | 109 | HTML, UTF-8 | Incomplete account-view demo shell. References missing `styles.css`, `tamu-kb.js`, `app.js`, and `flow-chart.html`. Labels itself `POC - Confidential Data`. |
| `Full-suite-savings-tool.html` | 2,109 | HTML, ASCII | Browser-only savings calculator. Generates XLSX and PPTX using custom ZIP/OpenXML logic. Embeds UT System example data. |
| `Mockup_Release_Assistant.html` | 1,070 | HTML, UTF-8 | Release assistant prototype. Uses Google Fonts, missing local release index, and same-origin backend APIs. |
| `New_Value_Calculator.html` | 2,071 | HTML, ASCII | Browser-only ROI/value calculator. Can download/upload customer Excel or CSV/TSV, print/PDF, and copy summary. |
| `Success_Plan.html` | 139 | HTML, ASCII | Compact exported/static success-plan app. References EverAfter-style assets, Google Tag Manager, Embedly, Google Material Icons, and embeds Kohler success-plan data. |
| `Support_Case_Analysis.html` | 1,069 | HTML, ASCII | Support case dashboard. Uses Google Fonts and jsDelivr XLSX parser; embeds default support case dataset and can refresh from uploaded report. |
| `workflow_analyzer.html` | 1,888 | HTML, ASCII | Browser-only JAGGAER workflow XML analyzer and text report exporter. |

## Zone.Identifier Metadata Files

Each metadata file contains:

```text
[ZoneTransfer]
ZoneId=3
```

Files:

- `CSM_Support_Case_Analysis_Tool.html:Zone.Identifier`
- `New_Value_Calculator.html:Zone.Identifier`
- `csm-roadmap-flow.html:Zone.Identifier`
- `end_result_mockup.html:Zone.Identifier`
- `index.html:Zone.Identifier`
- `success_plan_mock.html:Zone.Identifier`
- `ut-full-suite-savings-tool.html:Zone.Identifier`

Note: these metadata filenames reference some HTML names that are not present as actual HTML files in this folder.

## Missing Referenced Files

Referenced but not found in the current folder:

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

## Read/Analysis Method

- File inventory via `rg --files -uu` with `.git`, build, cache, and dependency folders excluded.
- Line counts via `wc -l`.
- File type checks via `file`.
- Direct source inspection with pattern searches and targeted line reads.
- HTML extraction script was attempted but returned zero extracted files because this workspace is HTML-centric and the script targets document/text formats, not HTML.
