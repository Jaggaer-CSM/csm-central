---
title: CSM AI Plan - Cloud Ops Handoff
created: 2026-05-06
source_folder: /home/yshvadro/CSM Central
tags:
  - csm-ai-plan
  - cloud-ops
  - handoff
---

# CSM AI Plan - Cloud Ops Handoff

## Purpose

This folder is a Cloud Ops handoff packet for the current `CSM Central` workspace. It is based only on files present in `/home/yshvadro/CSM Central` on 2026-05-06.

The current workspace is a static HTML tool collection, not a complete production application. Several tools are fully client-side prototypes. One tool, `Mockup_Release_Assistant.html`, expects a backend and a missing local static index file. `Elevator.html` references supporting local files that are not present in this folder.

## Documents In This Packet

- `Full Tech Stack Map.md` - confirmed frontend, browser APIs, third-party dependencies, missing assets, and backend references.
- `Full AI Roadmap Map.md` - full roadmap from `AI_Roadmap.html`, including planned/prototype/ideation items not currently surfaced in Central.
- `CSM Central Architecture Map.md` - architecture of `CSM_Central.html` as the site launcher.
- `Data Requirements.md` - data needed by each tool and by the future AI/Cloud Ops build.
- `Data Exposure.md` - where data is visible, exported, stored, sent, linked, or exposed to third parties.
- `Data Security.md` - security risks and controls Cloud Ops should plan before production.
- `Backend Integration Contract - Release Assistant.md` - observed API calls and backend behavior required by the Release Assistant prototype.
- `Open Questions and Decisions.md` - items that are not answerable from the current files and should be decided with Cloud Ops.
- `Source Inventory.md` - complete inventory of files read and what each file appears to do.

## Immediate Cloud Ops Takeaways

1. Treat `AI_Roadmap.html` as the broader source of roadmap truth: it contains 24 formal roadmap items, while `CSM_Central.html` currently surfaces only 8 child pages.
2. Host `CSM_Central.html` and its child tools as a private authenticated internal app if any embedded customer/account data stays in the files.
3. Decide whether confidential demo/customer data should remain embedded in static HTML. If the answer is no, move it behind authenticated APIs.
4. Do not deploy `Success_Plan.html` as-is to a broad audience without reviewing the Google Tag Manager, Embedly, EverAfter redirect/cookie code, and embedded Kohler success-plan content.
5. Do not treat `Mockup_Release_Assistant.html` as complete. It needs backend endpoints, a static release index at `data/release_26_1_index.js`, authentication, generated-file controls, and retention rules.
6. Do not treat `Elevator.html` as runnable from this folder alone. It references `styles.css`, `tamu-kb.js`, `app.js`, and `flow-chart.html`, which are not present here.
7. Add a deployment decision for external dependencies: Google Fonts, jsDelivr `xlsx`, Google Tag Manager, Embedly, JAGGAER Library PDFs, Salesforce report link, SharePoint links, and one local `file://` link in the roadmap.

## Known Sensitive Content In Current Files

- `Elevator.html` labels the demo as `POC - Confidential Data` and mentions SFDC, FinancialForce, Teams meeting summaries, scanned email volume, PROD data, CSM notes, and JAGGAER Engage.
- `Support_Case_Analysis.html` embeds support case numbers, customer/account names, case-owner names, case subjects, severity, Jira ticket status, and summary counts.
- `Success_Plan.html` embeds a Kohler success plan with business goals, supplier-risk notes, SAP/MuleSoft references, dates, KPIs, recommendations, and notes.
- `Full-suite-savings-tool.html` embeds UT System example institution names, operating budgets, transaction baselines, and commercial assumptions.
- `AI_Roadmap.html` embeds internal roadmap records and SharePoint documentation links.

## Extraction Note

The bundled extraction script for mixed document folders did not extract this workspace because the files are HTML plus Windows `Zone.Identifier` metadata. I read and analyzed the source files directly.
