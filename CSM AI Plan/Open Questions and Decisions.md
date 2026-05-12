---
title: Open Questions and Decisions
created: 2026-05-06
source_folder: /home/yshvadro/CSM Central
tags:
  - csm-ai-plan
  - questions
  - cloud-ops
---

# Open Questions And Decisions

## Questions I Cannot Answer From The Current Files

1. What is the intended production hosting target?
   - Static hosting only?
   - Internal app platform?
   - Existing JAGGAER/EverAfter environment?
   - New cloud service?

2. Who is the audience?
   - Internal CSMs only?
   - CSM managers?
   - Product/Support?
   - Customers?

3. What authentication is required?
   - SSO?
   - Group-based RBAC?
   - Account/team ownership checks?

4. Should customer data remain embedded in static HTML?
   - Current files embed Kohler, UT System, support case, roadmap, and other sensitive/internal details.
   - Production may need API-backed customer/account scoping instead.

5. What is the source of truth for roadmap data?
   - Current `AI_Roadmap.html` points to an Excel file that is not in the folder.
   - Is the source Excel, SharePoint, a database, or static JSON?

6. Where are the missing Elevator files?
   - `styles.css`
   - `tamu-kb.js`
   - `app.js`
   - `flow-chart.html`

7. Where is the missing Release Assistant index?
   - `data/release_26_1_index.js`

8. Does Cloud Ops want to support browser-only processing for sensitive uploads?
   - Support case exports, customer value spreadsheets, and workflow XML currently stay local in the browser.

9. Does Cloud Ops want backend storage/history for generated outputs?
   - New Value Calculator and Full-Suite Savings Tool generate outputs locally.
   - Release Assistant expects backend-generated files.

10. Are Google Tag Manager and Embedly approved for pages containing customer-specific data?

11. Should external CDN dependencies be allowed?
   - `xlsx@0.18.5` currently loads from jsDelivr in the Support Case Analysis tool.

12. What is the LLM/AI architecture?
   - No model, API key, prompt store, vector DB, or AI provider is configured in the current folder.
   - Release Assistant implies a chat/index/search backend, but the backend is not present.

13. What retention policy applies to:
   - uploaded support exports,
   - uploaded workflow XML,
   - uploaded/customer-completed value calculator files,
   - generated PPTX/XLSX/HTML/script outputs,
   - prompts and responses,
   - logs.

14. Which links must be replaced before production?
   - local `file://` roadmap link,
   - WSL-local paths,
   - potentially external SharePoint/Salesforce/library links depending on audience.

## Recommended Decisions For The Next Cloud Ops Meeting

1. Decide the production boundary:
   - private internal app,
   - private demo site,
   - customer-facing site,
   - or mixed with per-tool permissions.

2. Decide data placement:
   - static embedded data,
   - client-only upload processing,
   - backend ingestion,
   - or database-backed customer records.

3. Decide the Release Assistant backend scope:
   - search only,
   - search plus document generation,
   - search plus PPT/video/tutorial generation,
   - retention and signed URLs.

4. Decide source system integration order:
   - Salesforce/support reports,
   - success plan data,
   - release-note index,
   - workflow XML,
   - value calculator inputs,
   - roadmap/manager data,
   - Elevator account context sources.

5. Decide security baseline:
   - SSO group model,
   - CSP domains,
   - third-party script policy,
   - logging policy,
   - generated file storage policy.

6. Decide what gets cleaned before sharing more broadly:
   - customer names,
   - support case examples,
   - internal owner names,
   - SharePoint links,
   - local paths,
   - customer-specific success-plan details.

## Suggested Sequencing

1. Stabilize static hosting for the hub and fully client-only tools.
2. Remove or isolate customer-confidential embedded data from broad static hosting.
3. Build the Release Assistant backend contract and source index.
4. Add authentication and role-filtered tool registry.
5. Add observability and retention controls.
6. Convert high-value prototypes into API-backed tools only where persistence or automation is truly needed.

