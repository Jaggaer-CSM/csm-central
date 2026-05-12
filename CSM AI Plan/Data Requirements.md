---
title: Data Requirements
created: 2026-05-06
source_folder: /home/yshvadro/CSM Central
tags:
  - csm-ai-plan
  - data
  - requirements
---

# Data Requirements

## Scope

This document lists the data required by the current static tools and the likely data Cloud Ops must plan for when converting this into a production CSM AI application. It does not invent schemas beyond what appears in the current files.

## Cross-Tool Data Categories

The current files point to these major data categories:

- Customer/account profile data.
- Stakeholder/contact data.
- Success plan goals, KPIs, milestones, recommendations, and status.
- Product usage and adoption data.
- Support case exports and case metadata.
- Workflow XML definitions and workflow structure.
- Release notes, feature metadata, product/core/release tags, and generated enablement materials.
- Commercial/value inputs such as spend, transactions, contracts, savings assumptions, subscription, and ROI assumptions.
- Manager planning data for 1:1s, staffing, portfolios, ICP, promotions, and performance flags.
- Meeting, email, Teams, CSM notes, SFDC, FinancialForce, PROD data, and JAGGAER Engage data are referenced by `Elevator.html`, but their actual schemas are not present in this folder.

## Per-Tool Requirements

### CSM Central Launcher

Needs:

- Tool registry: file name, display name, lifecycle category, description, icon, kind.
- Lifecycle stages and quick-action keyword rules.
- Optional user preferences for favorites and recent tools.

Current implementation:

- Tool registry is hard-coded in `htmlFiles`.
- Tool metadata is inferred from filenames and rules.
- Favorites and recent tools are stored locally in browser localStorage.

Production requirement:

- Replace hard-coded registry with a centrally managed manifest or API if Cloud Ops needs permissions, lifecycle ownership, or release governance.

### AI Roadmap

Needs:

- Roadmap tool records: id, number, name, stage, action, team, type, effort, value, priority, status, goal, dependencies, input, hosting, impact, goal date, build hours, purpose, details, outputs, documentation links.
- Lifecycle stages: Implementation, Adoption, Sustain Growth, Renewal.
- Digital Motion tools.
- Manager tools.
- Accelerator drops: status, creator, audience, impacted CSMs, build minutes, saved minutes per CSM, cadence, rollout stage, description, roadmap treatment, next step, optional link.
- ROI assumptions: build FTE hours/year, savings FTE hours/year, team size, mapped tool estimates.

Current implementation:

- Embeds 24 roadmap tool records in `AI_Roadmap.html`.
- References an Excel source link: `AI%20roadmap%20copied%20to%20wsl2.xlsx`, but that source file is not present in the folder.
- Some manager-tool fields explicitly say they are not specified in the workbook.

Production requirement:

- Decide the source of truth for roadmap data: Excel, SharePoint list, database table, static JSON, or admin UI.
- Remove or replace local `file://` references before deployment.

### Elevator

Needs, based on visible HTML:

- Account profile and evidence data from SFDC, FinancialForce, Teams, Email, PROD Data, CSM Notes, and JAGGAER Engage.
- Suggested prompts.
- Quick-create actions.
- Chat/evidence thread.
- Contact list.
- Exportable answers.

Current implementation:

- `Elevator.html` references `styles.css`, `tamu-kb.js`, `app.js`, and `flow-chart.html`, none of which are in this folder.
- The HTML says `POC - Confidential Data` and `A local demo for one view for each account`.

Production requirement:

- Cloud Ops needs the missing files or a replacement design before implementing this tool.
- Data source schemas cannot be confirmed from the current folder.

### Full-Suite Savings Tool

Needs:

- Output setup: prepared for, prepared by, scenario, date, master term years.
- Institution rows: institution name, core suite flag, consortium flag, operating budget, current/future POs, current/future invoices, current/future sourcing events, current contract spend, current/future contracts, current/future consortium spend, annual subscription.
- Assumptions: dollars per PO, savings per PO, dollars per invoice, savings per invoice, sourcing goal, average event size, hours saved/event, FTE hourly rate, sourcing hard savings, contract addressable spend, future on-contract spend, contract savings rate, contracts per dollar, eSignature savings per contract, consortium addressable spend, consortium spend share, consortium rebate, current YoY increase, master YoY increase.
- Export outputs: XLSX and PPTX generated locally.

Current implementation:

- Embeds UT System example data and defaults.
- Generates files in the browser using custom ZIP/OpenXML code.

Production requirement:

- Decide whether customer-entered value model data should remain browser-only, be saved to a database, or be sent to a backend for generated artifacts.

### Release Assistant

Needs:

- Release index or backend feature database.
- Feature metadata: id/source URL, release, product, core, feature name, enablement type, source PDF/page/location, answer/description/value analysis.
- User question.
- Core/product/release filters.
- Selected feature source identifiers (`pdf_ids` in current API payloads).
- Optional video/tutorial context.
- Generated file URLs returned by backend.

Current implementation:

- Expects `data/release_26_1_index.js` for local/offline mode.
- Calls backend APIs in non-file mode.
- `API_BASE` and `BACKEND_BASE` are empty, implying same-origin backend.

Production requirement:

- Cloud Ops needs a backend API and file generation service. See `Backend Integration Contract - Release Assistant.md`.

### New Value Calculator

Needs 88 calculator inputs across 9 process groups:

- General: 9 fields.
- Spend Analytics: 5 fields.
- Supplier Management: 15 fields.
- Sourcing: 5 fields.
- Advanced Sourcing: 14 fields.
- Contract Lifecycle Management: 19 fields.
- eProcurement: 7 fields.
- pCard: 10 fields.
- Accounts Payable: 4 fields.

Current implementation:

- All calculation state is in browser memory.
- Supports downloading a customer Excel template.
- Supports uploading completed `.xlsx`, `.xls`, `.csv`, `.tsv`, text/CSV, and Excel MIME types.
- Parses workbook/text locally in browser and updates calculator inputs.
- Exports via print/PDF and clipboard summary.

Production requirement:

- Decide whether uploaded customer value inputs are allowed to remain entirely local or should be stored/reviewed centrally.

### Success Plan

Needs:

- Customer-specific success plan data: areas, priorities, notes, goals, statuses, KPIs, comments.
- Release timeline: release number, review date, production date.
- Playbook questions: id, goal, question, recommendation.
- Goal/question selections and row notes.
- Export/print mode.

Current implementation:

- Embeds a Kohler CSM Success Plan 2026.
- Uses in-memory selections/notes only; no localStorage or backend persistence was found for these selections.
- Has `?export=1` mode for print/PDF style output.

Production requirement:

- Move customer-specific success plans behind authentication and customer/account scoping if more than a private demo.

### Support Case Analysis Tool

Needs:

- Salesforce support report export with columns:
  - Account Name
  - Case Owner
  - Subject
  - Type
  - Status
  - Date/Time Opened
  - Age
  - Case Number
  - Description
  - Resolution
  - Case Comments
  - Count of Case Emails
  - Severity Level
  - Jira Ticket
  - Escalated
- The parser searches for a header row containing `Account Name`, `Case Number`, and `Severity Level`.
- The dashboard derives filters, summary counts, case types, severity, accounts, owners, themes, monthly trend, recommendations, and examples.

Current implementation:

- Embeds a default support case dataset sourced from `CSM Support Case Analysis Tool-2026-03-25-22-32-58.xlsx`.
- Upload refresh is local in the browser using `FileReader` and external `xlsx` library.

Production requirement:

- Decide whether support exports can be processed in-browser only or uploaded to a controlled backend.
- If backend processing is used, define retention, data minimization, access, and audit logging.

### Workflow Analyzer

Needs:

- JAGGAER workflow XML files.
- XML nodes/attributes:
  - `WorkflowType`
  - `WorkflowSubType`
  - `Version`
  - `VersionDescription`
  - `Usable`
  - `Step`
  - `Activity`
  - `ActivityRelationship`
  - `ActivityType`
  - `Rule`
  - `FolderSelectionRule`
  - `FolderRef`
  - `StepRef`
  - `Attribute`
  - `AttrValue`

Current implementation:

- Parses uploaded XML locally in browser using `DOMParser`.
- Produces structured tables and downloadable text report.

Production requirement:

- Decide whether workflow XML definitions can remain client-side only or whether they need server-side storage/history.

## Detailed New Value Calculator Field Inventory

This inventory is directly extracted from `New_Value_Calculator.html`.

### General

- `totalOperationalSpendM` - Total operational spend - Must Have - `$M/yr`
- `addressableSpendM` - Addressable spend - Good to Have - `$M/yr`
- `tier1Pct` - Tier 1 spend: addressable spend on contract - Must Have - `%`
- `tier2Pct` - Tier 2 spend: addressable spend not on contract - Must Have - `%`
- `tier3Pct` - Tier 3 spend: addressable spend with no contract - Must Have - `%`
- `possibleAddressableSpendM` - Total possible addressable spend - Must Have - `$M/yr`
- `waccPct` - Weighted average cost of capital - Must Have - `%`
- `spendGrowthPct` - Spend growth rate - Good to Have - `%/yr`
- `sumIncreasePct` - Estimated increase in spend under management - Nice to Have - `%/yr`

### Spend Analytics

- `analyticsSalary` - Estimated annual salary/blended rate for analytics personnel - Good to Have - `$/yr`
- `analyticsCollectionHrs` - Time spent on spend collection and cleansing - Good to Have - `hrs/yr`
- `analyticsReportHrsWk` - Time spent preparing spend-based reports - Good to Have - `hrs/wk`
- `contractLeakagePct` - Estimate of contract leakage - Nice to Have - `%/yr`
- `invoicePricingInaccuracyPct` - Estimate of invoice pricing inaccuracies - Nice to Have - `%/yr`

### Supplier Management

- `supplierCount` - Number of suppliers - Must Have - `suppliers`
- `diverseSupplierCount` - Number of diverse suppliers - Must Have - `suppliers`
- `supplierSalary` - Estimated annual salary/blended rate for supplier management personnel - Good to Have - `$/yr`
- `supplierDocHours` - Time spent managing supplier documentation - Good to Have - `hrs/supplier`
- `newSuppliersEvaluated` - Number of new suppliers evaluated - Good to Have - `suppliers/yr`
- `newSupplierEvalHours` - Time spent evaluating new suppliers - Good to Have - `hrs/supplier`
- `tinHours` - Time spent managing supplier TIN match - Good to Have - `hrs/supplier`
- `supplierCertHours` - Time spent managing supplier certifications and qualifications - Good to Have - `hrs/supplier`
- `diversityHours` - Time spent managing supplier diversity - Good to Have - `hrs/diverse supplier`
- `secondTierDiversityHours` - Time spent managing 2nd Tier supplier diversity - Good to Have - `hrs/diverse supplier`
- `newSuppliersOnboarded` - Number of new suppliers onboarded each year - Good to Have - `suppliers/yr`
- `onboardingDocHours` - Time spent managing onboarding documentation - Good to Have - `hrs/supplier`
- `suppliersOffboarded` - Number of new suppliers offboarded each year - Good to Have - `suppliers/yr`
- `coldCallSuppliers` - Number of cold call suppliers registered/evaluated - Nice to Have - `suppliers/yr`
- `offboardingDocHours` - Time spent managing offboarding documentation - Nice to Have - `hrs/supplier`

### Sourcing

- `sourcingEvents` - Number of sourcing events - Must Have - `events/yr`
- `sourcingSalary` - Estimated annual salary/blended rate for sourcing personnel - Good to Have - `$/yr`
- `sourcingEventHours` - Time spent creating, executing, and evaluating a sourcing event - Good to Have - `hrs/event`
- `avgSourcingEventSize` - Average size of a typical sourcing event - Good to Have - `$/event`
- `avgSourcingSavingsPct` - Average savings achieved through sourcing - Nice to Have - `%/event`

### Advanced Sourcing

- `advancedCategories` - Number of categories sourced - Good to Have - `categories`
- `advancedDollars` - Anticipated aggregate dollars to be sourced - Must Have - `$`
- `advancedEvents` - Number of sourcing events per year - Must Have - `events/yr`
- `advancedProcurementDollars` - Total estimated procurement dollars - Inherited from Spend Data Input tab - `$`
- `advancedSpendUnderMgmtPct` - Total spend under management that uses advanced sourcing techniques - Calculated from inherited information - `%`
- `advancedSuppliers` - Planned number of suppliers in a typical advanced sourcing event - Good to Have - `suppliers`
- `advancedHistoricalSavingsPct` - Average cost savings achieved using current/conventional sourcing methods - Must Have - `%`
- `advancedAdditionalSavingsPct` - Anticipated savings using advanced sourcing techniques - VA team estimate - `%`
- `advancedTeamMembers` - Number of team members currently involved in sourcing - Must Have - `FTE`
- `advancedFteSalary` - Average salary of FTE - Must Have - `$/yr`
- `advancedBurdenPct` - Overhead/Burden rate - Nice to Have - `%`
- `advancedDurationMonths` - Average duration of a sourcing event - Good to Have - `months`
- `advancedFteReduction` - Estimated reduction in FTEs necessary to execute sourcing events - VA team estimate - `FTE`
- `advancedTimeReductionMonths` - Estimated reduction in time to market - VA team estimate - `months`

### Contract Lifecycle Management

- `contractCreationPeople` - People participating in/managing contract creation - Must Have - `people`
- `contractCreationSalary` - Salary/blended rate for contract creation process - Good to Have - `$/yr`
- `contractExecutionPeople` - People participating in/managing contract review, negotiation, and approval - Must Have - `people`
- `contractExecutionSalary` - Salary/blended rate for contract review, negotiation, and approval - Good to Have - `$/yr`
- `contractStoragePeople` - People participating in/managing contract scanning, filing, and archiving - Must Have - `people`
- `contractStorageSalary` - Salary/blended rate for contract scanning, filing, and archiving - Good to Have - `$/yr`
- `contractSearchPeople` - People participating in/managing contract searching, tracking, and finding - Must Have - `people`
- `contractSearchSalary` - Salary/blended rate for contract searching, tracking, and finding - Good to Have - `$/yr`
- `contractCount` - Number of contracts - Good to Have - `contracts`
- `newContractsAnnual` - Annual number of new contracts - Good to Have - `contracts/yr`
- `missedCommitmentContracts` - Contracts with missed or underperformed commitments - Good to Have - `contracts`
- `contractResolutionHours` - Time managing resolution/corrective action for missed commitments - Good to Have - `hrs/contract`
- `contractExpirePct` - Spend under contract that expires each year - Must Have - `%`
- `contractAutoRenewPct` - Spend under contract that auto-renews - Must Have - `%`
- `contractCreationHours` - Time spent managing contract creation - Nice to Have - `hrs/contract`
- `contractExecutionHours` - Time spent managing contract review, negotiation, and approval - Nice to Have - `hrs/contract`
- `contractStorageHours` - Time spent managing contract scanning, filing, and archiving - Nice to Have - `hrs/contract`
- `contractSearchHours` - Time spent managing contract searching, tracking, and finding - Nice to Have - `hrs/contract`
- `autoRenewSavingsPct` - Savings from re-sourcing or renegotiating auto-renewing contracts - Nice to Have - `%/contract`

### eProcurement

- `poCount` - Total number of POs - Must Have - `POs/yr`
- `maverickRedirectPct` - Maverick spend that can be redirected to existing contracts - Good to Have - `%/yr`
- `poProcessHours` - Time to process a PO from request to order placement - Good to Have - `hrs/PO`
- `nonPoReviewHoursWk` - Time reviewing non-PO, restricted, or non-catalog transactions - Good to Have - `hrs/wk/person`
- `redirectedTier2SavingsPct` - Redirected Tier 2 savings - Nice to Have - `%`
- `poProcessCost` - Cost to process a PO from request to order placement - Nice to Have - `$/PO`
- `nonPoRequestCount` - Annual requests for non-PO, restricted, or non-catalog goods and services - Nice to Have - `requests/yr`

### pCard

- `pCardDoAMin` - Minimum spend/transaction requiring delegation of authority approval - Must Have - `$/transaction`
- `pCardDoASpend` - Total spend requiring delegation of authority approval - Must Have - `$/yr`
- `pCardDoATransactions` - PO/non-PO transactions requiring delegation of authority approval - Must Have - `transactions/yr`
- `pCardBelowDoASpend` - Total spend that does not require delegation of authority approval - Must Have - `$/yr`
- `pCardBelowDoATransactions` - Transactions that do not require delegation of authority approval - Must Have - `transactions/yr`
- `pCardBudgetOwners` - People/budget owners participating in pCard reporting - Must Have - `people`
- `pCardSalary` - Estimated annual salary/blended rate for pCard management personnel - Good to Have - `$/yr`
- `pCardReportHoursWk` - Time spent generating pCard spend reports - Good to Have - `hrs/wk/person`
- `pCardDoAPct` - Spend requiring delegation of authority that could be paid with pCard - Nice to Have - `%`
- `pCardOverrideSpend` - Spend requiring delegation of authority that could be paid with pCard - Nice to Have - `$/yr`

### Accounts Payable

- `manualInvoices` - Total number of manually processed invoices - Must Have - `invoices/yr`
- `poInvoicePct` - PO-related invoices as a percent of total - Must Have - `%`
- `invoiceProcessHours` - Time to process an invoice from receipt to approval for payment - Nice to Have - `hrs/invoice`
- `invoiceProcessCost` - Cost to process an invoice from receipt to approval for payment - Nice to Have - `$/invoice`

## Questions For Cloud Ops

- Which data categories should be stored server-side versus kept client-only?
- Which source systems are approved for automated ingestion?
- Will the app need row-level or customer-level permissions?
- What is the retention policy for uploaded support exports, workflow XML, generated PPTX/XLSX, generated training tools, and LLM prompts/responses?
- Should customer-specific static HTML pages be replaced by API-backed views?
