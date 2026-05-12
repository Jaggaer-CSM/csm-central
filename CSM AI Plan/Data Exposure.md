---
title: Data Exposure
created: 2026-05-06
source_folder: /home/yshvadro/CSM Central
tags:
  - csm-ai-plan
  - data-exposure
  - cloud-ops
---

# Data Exposure

## Key Point

Static HTML exposes embedded data to anyone who can access the file. Several current files embed customer, account, support, roadmap, and commercial example data directly in the source. If these files are hosted without authentication, that data is exposed.

## Exposure Inventory

| File | Exposure type | Confirmed details |
|---|---|---|
| `CSM_Central.html` | Low data exposure from launcher itself. | Exposes tool names, lifecycle categories, and local filenames. Stores favorites/recent tool ids in localStorage. |
| `AI_Roadmap.html` | Internal roadmap data and links. | Embeds roadmap tool strategy, dependencies, inputs, hosting notes, goal dates, hours, outputs, SharePoint links, accelerator records, and a local `file://` link. |
| `Elevator.html` | Confidential demo indicator and source-system references. | HTML says `POC - Confidential Data`; references SFDC, FinancialForce, Teams, Email, PROD Data, CSM Notes, JAGGAER Engage. Missing JS/data files may contain more. |
| `Full-suite-savings-tool.html` | Commercial and value-model data. | Embeds UT System example institutions, budgets, transaction data, assumptions, and generates customer-facing PPTX/XLSX outputs. |
| `Mockup_Release_Assistant.html` | Backend request/response and generated files. | Sends user questions, selected source IDs, and tutorial context to backend in non-file mode; displays generated file URLs returned by backend. |
| `New_Value_Calculator.html` | Customer value inputs and exports. | Uploaded customer Excel/CSV data is parsed locally; summary can be copied to clipboard; print/PDF and Excel template outputs can contain customer financial and operational data. |
| `Success_Plan.html` | Customer-specific account plan. | Embeds Kohler success-plan goals, KPIs, notes, business-system references, recommendations, release timeline, and selectable progress notes. |
| `Support_Case_Analysis.html` | Support case/customer data. | Embeds customer/account names, case owners, case numbers, case subjects, severity, Jira status, counts, and Salesforce report link. Uploaded exports are parsed locally. |
| `workflow_analyzer.html` | Workflow configuration data. | Uploaded XML is parsed locally and displayed; generated text reports can expose workflow structure, folders, rules, and routing details. |
| `*:Zone.Identifier` files | Minimal metadata. | Each contains Windows zone metadata `ZoneId=3`; no business data beyond filenames. |

## Browser Storage

Confirmed browser persistence:

- `CSM_Central.html` stores `csmToolsHub.favorites` and `csmToolsHub.recent` in localStorage.

Not found:

- No IndexedDB usage.
- No sessionStorage usage.
- No explicit cookies set by the project itself, except `Success_Plan.html` reads an `eaHost` cookie from the EverAfter shell snippet.
- No persistence of New Value Calculator inputs in localStorage.
- No persistence of Success Plan selections in localStorage.

## File Upload Behavior

| Tool | Upload type | Where data goes in current code |
|---|---|---|
| `Support_Case_Analysis.html` | `.xlsx`, `.xls`, `.csv` | Read in browser by `FileReader`; parsed by external `xlsx` library loaded from jsDelivr. No `fetch` upload found. |
| `New_Value_Calculator.html` | `.xlsx`, `.xls`, `.csv`, `.tsv`, text/CSV, Excel MIME types | Read and parsed locally in browser; no `fetch` upload found. |
| `workflow_analyzer.html` | XML | Read by `file.text()` and parsed locally by `DOMParser`; no `fetch` upload found. |
| `Mockup_Release_Assistant.html` | No local file upload in visible HTML | Sends questions, selected source IDs, and context to backend APIs when not in file/demo mode. |

## Generated Outputs

| Tool | Output | Exposure note |
|---|---|---|
| `Full-suite-savings-tool.html` | XLSX and PPTX downloads | Outputs include prepared-for/by values, scenario, date, assumptions, formulas, module savings, institution detail, budgets, transaction values, and creator metadata from `preparedBy`. |
| `New_Value_Calculator.html` | Customer Excel template, copied summary, print/PDF | Outputs can contain operational spend, supplier counts, contract values, salary/blended rates, ROI, NPV, payback, and annual value. |
| `workflow_analyzer.html` | Text report download | Output includes workflow metadata, steps, activities, routing mix, rule groups, folder/robot references, signals, opportunities, questions, and checklist. |
| `Mockup_Release_Assistant.html` | Backend-generated files | Backend returns `file_url`, `html_url`, `template_used`, and generated content. Access controls and retention are unknown from current files. |

## External Network Exposure

The following external domains or paths are referenced:

- `fonts.googleapis.com`
- `fonts.gstatic.com`
- `cdn.jsdelivr.net`
- `www.googletagmanager.com`
- `cdn.embedly.com`
- `www.jaggaer.com`
- `library.jaggaer.com`
- `jaggaer.lightning.force.com`
- `jaggaer.sharepoint.com`

Only `Mockup_Release_Assistant.html` contains active application `fetch()` API calls, and they are same-origin by default because `API_BASE` and `BACKEND_BASE` are empty.

## Major Exposure Risks

1. Static embedded customer data can be viewed by any user who can access the HTML source.
2. External scripts/fonts/tracking can disclose page loads, referrers, IPs, user agents, and possibly page context depending on browser/referrer policy.
3. `Success_Plan.html` includes Google Tag Manager and Embedly code in a page that also embeds customer-specific success-plan details.
4. The Release Assistant backend file URLs may expose generated assets if unauthenticated or long-lived.
5. Support case exports and workflow XML contain operationally sensitive details even when processed locally.
6. The roadmap includes SharePoint and local file links that may reveal internal structure or break in hosted environments.

## Recommended Data Minimization

- Remove customer-specific demo data from static HTML before broad deployment, or restrict hosting to authenticated users.
- Replace embedded datasets with authenticated APIs scoped by user/customer.
- Keep browser-only parsing for sensitive uploads where possible, unless there is a clear need for backend storage.
- If backend processing is needed, store only derived summaries when possible and delete raw uploads quickly.
- Avoid third-party tracking scripts on pages with customer data.
- Remove `file://` links and non-production local paths.

