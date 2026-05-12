---
title: Full AI Roadmap Map
created: 2026-05-06
source_folder: /home/yshvadro/CSM Central
source_file: AI_Roadmap.html
tags:
  - csm-ai-plan
  - roadmap
  - cloud-ops
---

# Full AI Roadmap Map

## Scope

This document maps the full roadmap embedded in `AI_Roadmap.html`, not just the tools currently linked from `CSM_Central.html`.

The current roadmap contains:

- 24 formal roadmap items.
- 4 lifecycle stages: Implementation, Adoption, Sustain Growth, Renewal.
- 2 Digital Motion roadmap items.
- 4 Manager Tools roadmap items.
- 2 accelerator drops tracked outside the formal roadmap.

## Stage Map

| Stage | Roadmap intent |
|---|---|
| Implementation | Provide CSM with account context. |
| Adoption | Assist CSM with meetings and goals. |
| Sustain Growth | Assist CSM with ongoing adoption. |
| Renewal | Assist with renewal readiness and growth. |
| Digital Motion | Structured AI support for scaled, digital-first customer engagement. |
| Manager Tools | Manager-facing planning, coaching, staffing, promotion, portfolio, and ICP support. |

## Current Central Coverage Versus Full Roadmap

`CSM_Central.html` currently links 8 child pages. The roadmap has 24 formal roadmap items, so Central is only a partial surface.

| Current Central file | Roadmap relationship | Confidence / note |
|---|---|---|
| `AI_Roadmap.html` | Roadmap reference page, not a roadmap tool item. | Exact source for this document. |
| `Elevator.html` | `1.2 Elevator` | Exact name match, but missing supporting files in this folder. |
| `Success_Plan.html` | `2.1 Success Plan Creation and Maintenance` | Strong functional match. |
| `Mockup_Release_Assistant.html` | `3.1 Release Assistant`; also overlaps with `3.0 Release Search Library` | Strong functional match; file includes both search and material-generation behavior. |
| `Support_Case_Analysis.html` | `3.4 Support Trends` | Strong functional match. |
| `workflow_analyzer.html` | Not explicitly named in formal roadmap data. | May be an accelerator or adjacent support tool, but the roadmap object does not name it. |
| `Full-suite-savings-tool.html` | Not explicitly named in formal roadmap data. | Adjacent to renewal/value work, but not listed as a formal roadmap item. |
| `New_Value_Calculator.html` | Not explicitly named in formal roadmap data. | Adjacent to value/renewal work, but not listed as a formal roadmap item. |

## Roadmap Summary By Stage

| Stage | Formal items | Prototype | Ideation | High priority |
|---|---:|---:|---:|---:|
| Implementation | 3 | 1 | 2 | 3 |
| Adoption | 4 | 2 | 2 | 4 |
| Sustain Growth | 8 | 3 | 5 | 3 |
| Renewal | 3 | 0 | 3 | 1 |
| Digital Motion | 2 | 0 | 2 | 2 |
| Manager Tools | 4 | 1 | 3 | 0 |

## Full Formal Roadmap

### 1. Implementation

| # | Tool | Status | Type | Owner / team | Goal date | Build hours | Hosting |
|---|---|---|---|---|---|---:|---|
| 1.0 | Implementation Summary | Ideation | Tool with Server | Pre Sales | May 29, 2026 | 45 | Salesforce |
| 1.1 | Implementation Handoff Agent | Prototype | Agent | PS | June 12, 2026 | 80 | HTML tool, GPT |
| 1.2 | Elevator | Ideation | Orchestrating Layer | Ops | September 15, 2026 | 120 | Search layer, warehouse |

#### 1.0 Implementation Summary

- Action: CSM intro call preparation.
- Goal: Share the relevant data from presales discussions with the CSM.
- Dependencies: presales, notes, SFDC.
- Inputs: Couvama? Pre-Sales Notes?
- Impact: Success Plans context.
- Outputs: Presales context summary; known goals and stakeholders; early success-plan inputs.
- Documentation: SharePoint folder link is embedded in `AI_Roadmap.html`.

#### 1.1 Implementation Handoff Agent

- Action: Handoff readiness and risk check.
- Goal: Prepare a clean CSM-ready account brief with context gaps, stakeholder map, goals, KPI alignment, and handoff risks.
- Dependencies: API, presales, scope.
- Inputs: Implementation notes, stakeholder list, scope, goals, KPIs, open actions, training status.
- Impact: Define one output pack and readiness score.
- Outputs: CSM handoff summary; adoption readiness score; missing-data checklist; first 30-day action plan.
- Documentation: SharePoint folder link is embedded in `AI_Roadmap.html`.

#### 1.2 Elevator

- Action: Shared account memory.
- Goal: Create one place where data from these tools is stored and searchable.
- Dependencies: CRM, support, warehouse.
- Inputs: CRM, support, notes, product usage, contracts.
- Impact: Shared searchable orchestration layer.
- Outputs: Central account context; searchable customer record; shared orchestration layer.
- Note: `Elevator.html` exists in Central, but its supporting files are missing from this folder.

### 2. Adoption

| # | Tool | Status | Type | Owner / team | Goal date | Build hours | Hosting |
|---|---|---|---|---|---|---:|---|
| 2.0 | CSM Intro Prep | Ideation | Custom GPT | CSM | June 19, 2026 | 24 | GPT, CRM notes |
| 2.1 | Success Plan Creation and Maintenance | Prototype | Tool with Server | CSM | June 30, 2026 | 72 | CRM, templates, GPT |
| 2.2 | KPI Analyzer | Prototype | Custom GPT | CSM | July 10, 2026 | 40 | BI layer, GPT |
| 2.3 | Meeting Prep and Follow-Up Agent | Ideation | Agent | CSM | July 17, 2026 | 70 | GPT, CRM |

#### 2.0 CSM Intro Prep

- Action: Second intro call preparation.
- Goal: Draft the first CSM intro brief, agenda, and account snapshot.
- Dependencies: handoff, stakeholders, goals.
- Inputs: Handoff pack, contacts, goals, open actions.
- Impact: Faster first calls with less prep.
- Outputs: Intro call brief; agenda; account snapshot.

#### 2.1 Success Plan Creation and Maintenance

- Action: Create success plan.
- Goal: Create, maintain, and review the success plan with milestones, KPIs, owners, and drift detection.
- Dependencies: templates, cadence, CRM.
- Inputs: Customer goals, milestones, stakeholders, scope, timelines, KPIs, meeting outcomes.
- Impact: Design one shared success-plan workflow.
- Purpose: Drive onboarding and early value realization after go-live.
- Outputs: Success plan; milestone status; recommended enablement actions; plan drift alerts.

#### 2.2 KPI Analyzer

- Action: Introduce value dashboard.
- Goal: Review usage and recommend next steps.
- Dependencies: playbook, prompt, Snowflake.
- Inputs: Snowflake.
- Impact: Faster proof of value.
- Outputs: KPI summary; usage recommendations; proof-of-value talking points.

#### 2.3 Meeting Prep and Follow-Up Agent

- Action: Adoption cadence and follow-through.
- Goal: Draft agenda, notes, and action recap for customer touchpoints.
- Dependencies: notes, stakeholders, actions.
- Inputs: CRM notes, emails, success plan, support updates.
- Impact: Saves prep time and improves follow-through.
- Outputs: Meeting agenda; customer recap; owner action list.

### 3. Sustain Growth

| # | Tool | Status | Type | Owner / team | Goal date | Build hours | Hosting |
|---|---|---|---|---|---|---:|---|
| 3.0 | Release Search Library | Prototype | Tool with Server | CSM | June 26, 2026 | 56 | Search index, web app |
| 3.1 | Release Assistant | Ideation | Custom GPT | CSM | July 24, 2026 | 24 | GPT |
| 3.2 | Operational Performance Reviews | Prototype | Matik | CSM | August 7, 2026 | 30 | Matik, GPT |
| 3.3 | Health and Risk Agent | Ideation | Agent | AM | August 21, 2026 | 90 | Tool with Server |
| 3.4 | Support Trends | Ideation | Tool with Server | GCC | July 31, 2026 | 44 | Support system, GPT |
| 3.5 | Escalation Management Agent | Ideation | Agent | GCC | September 12, 2026 | 68 | GPT, workflow tool |
| 3.6 | Single Threaded Detection | Ideation | Tool with Server | AM | September 1, 2026 | 48 | CRM, rules engine |
| 3.7 | Executive Relationship Building | Ideation | Custom GPT | AM | August 28, 2026 | 20 | CRM, GPT |

#### 3.0 Release Search Library

- Action: Product release enablement.
- Goal: Search release content and map updates to customer impact.
- Dependencies: releases, library, index.
- Inputs: Release notes, KB articles, enablement docs.
- Impact: Faster release prep.
- Outputs: Searchable release library; customer impact matches; enablement references.

#### 3.1 Release Assistant

- Action: Release talking points.
- Goal: Turn release notes into customer-ready talking points.
- Dependencies: library, releases, modules.
- Inputs: Release notes, customer modules, open asks.
- Impact: Clearer release conversations.
- Outputs: Customer-ready release summary; module-specific talking points; follow-up prompts.

#### 3.2 Operational Performance Reviews

- Action: Operational performance review.
- Goal: Draft review decks with KPI movement, risks, and actions.
- Dependencies: KPIs, dashboard, Matik.
- Inputs: KPI trends, adoption data, support trends, goals.
- Impact: Faster review creation.
- Outputs: Operational review deck; KPI movement story; risk and action summary.

#### 3.3 Health and Risk Agent

- Action: Health monitoring.
- Goal: Score health using adoption, support, engagement, and escalation signals.
- Dependencies: usage, support, meetings.
- Inputs: Product usage, tickets, meeting cadence, stakeholder sentiment.
- Impact: Earlier risk detection.
- Purpose: Continuously detect risk, stalled adoption, weak engagement, and escalation triggers.
- Outputs: Overall health score; risk reasons; next-best action; escalation recommendation.
- Note from roadmap details: starting health composition suggested as product adoption 50%, customer engagement/expertise 20%, technical or support health 30%.

#### 3.4 Support Trends

- Action: Support pattern detection.
- Goal: Summarize support patterns, root issues, and friction signals.
- Dependencies: support, cases, GCC.
- Inputs: Case volume, severity, product area, time to resolution.
- Impact: Better issue context before meetings.
- Outputs: Support trend summary; root issue patterns; meeting prep context.

#### 3.5 Escalation Management Agent

- Action: Manage customer escalations.
- Goal: Coordinate escalations with owners, updates, risks, and next steps.
- Dependencies: KPI, SFDC, Snowflake.
- Inputs: SF or Snowflake.
- Impact: Faster escalation follow-up.
- Outputs: Escalation summary; owner tracker; next-step update.

#### 3.6 Single Threaded Detection

- Action: Stakeholder coverage risk.
- Goal: Flag accounts that rely on too few customer contacts.
- Dependencies: contacts, engagement, CRM.
- Inputs: CRM contacts, meeting attendance, email activity.
- Impact: Reduces relationship risk.
- Outputs: Relationship risk flag; coverage gaps; suggested stakeholder actions.

#### 3.7 Executive Relationship Building

- Action: Executive stakeholder focus.
- Goal: Brief AMs on executive stakeholders, gaps, and outreach chances.
- Dependencies: orgmap, history, CRM.
- Inputs: Stakeholder map, meeting history, sponsor notes.
- Impact: Stronger sponsor coverage.
- Outputs: Executive brief; stakeholder gaps; outreach recommendations.

### 4. Renewal

| # | Tool | Status | Type | Owner / team | Goal date | Build hours | Hosting |
|---|---|---|---|---|---|---:|---|
| 4.0 | Success Stories | Ideation | Custom GPT | CSM | August 14, 2026 | 24 | GPT, templates |
| 4.1 | Whitespace Analysis | Ideation | Tool with Server | AM | August 21, 2026 | 64 | CRM, product data |
| 4.2 | Renewal Report Agent | Ideation | Agent | AM | September 5, 2026 | 60 | GPT, CRM |

#### 4.0 Success Stories

- Action: Coordinate customer references.
- Goal: Turn results and quotes into short success stories.
- Dependencies: approval, quotes, outcomes.
- Inputs: Meeting notes, KPI gains, quotes, reference data.
- Impact: Reusable proof points for AM and marketing.
- Outputs: Success story draft; reference proof points; approval-ready narrative.

#### 4.1 Whitespace Analysis

- Action: Identify expansion opportunities.
- Goal: Identify cross-sell whitespace from product fit and usage.
- Dependencies: product, usage, CRM.
- Inputs: Product footprint, usage, org structure, goals.
- Impact: Surfaces expansion paths earlier.
- Outputs: Whitespace map; expansion hypotheses; product-fit rationale.

#### 4.2 Renewal Report Agent

- Action: Renewal assessment.
- Goal: Draft a renewal-ready summary with value, risks, and expansion.
- Dependencies: health, value, contracts.
- Inputs: Contract data, KPI gains, support trends, stakeholder status.
- Impact: Shortens renewal prep.
- Purpose: Prepare renewal plans and expansion hypotheses using measured value.
- Outputs: Renewal-ready summary; risk and value narrative; expansion opportunity summary.

### D. Digital Motion

| # | Tool | Status | Type | Owner / team | Goal date | Build hours | Hosting |
|---|---|---|---|---|---|---:|---|
| D.1 | Digital Motion 1 - Adoption | Ideation | Agent | CSM | TBD | 108 | CRM, digital engagement platform, GPT workflow |
| D.2 | Digital Motion 2 - Renewal | Ideation | Agent | CSM | TBD | 96 | CRM, renewal workflow, GPT |

#### D.1 Digital Motion 1 - Adoption

- Action: Proactive adoption outreach.
- Goal: Proactively reach out to customers to increase adoption and recommend action items.
- Dependencies: usage, contacts, success plan, engagement signals.
- Inputs: Product usage, adoption gaps, customer contacts, success-plan milestones, meeting history.
- Impact: Scales adoption nudges and turns usage signals into recommended customer actions.
- Purpose: Create a digital-first motion that keeps customers moving toward adoption goals between human touchpoints.
- Source: `AI roadmap copied to wsl2.xlsx`.
- Outputs: Targeted adoption outreach; recommended action items; usage-gap summary; CSM follow-up prompts.

#### D.2 Digital Motion 2 - Renewal

- Action: Renewal recommendation outreach.
- Goal: Reach out to AMs and CSMs with renewal recommendations.
- Dependencies: renewal date, health, usage, value, risks, stakeholder coverage.
- Inputs: Contract timeline, health score, adoption trends, value proof points, open risks, stakeholder activity.
- Impact: Creates earlier renewal readiness prompts and keeps CSMs and AMs aligned on recommended actions.
- Purpose: Use renewal signals to trigger timely recommendations before renewal preparation becomes reactive.
- Source: `AI roadmap copied to wsl2.xlsx`.
- Outputs: Renewal action recommendation; AM and CSM prompt; risk and value summary; renewal readiness cue.

### M. Manager Tools

| # | Tool | Status | Type | Owner / team | Goal date | Build hours | Hosting |
|---|---|---|---|---|---|---:|---|
| M.0 | Manager's Assistant | Ideation | Managers 1:1 | CSM | Not specified | Not specified | Not specified |
| M.1 | Manager's Overview | Ideation | Managers promotion | CSM | Not specified | Not specified | Not specified |
| M.2 | Manager Capacity and Portfolios | Ideation | Managers account assignments | CSM | Not specified | Not specified | Not specified |
| M.3 | Manager ICP | Prototype | Managers ICP | CSM | Not specified | Not specified | Not specified |

#### M.0 Manager's Assistant

- Action: Managers 1:1.
- Goal: Assist managers in the 1:1s, recommend actions on CSM, mentoring areas, performance flags.
- Source: `AI roadmap copied to wsl.xlsx`.
- Outputs: 1:1 talking points; mentoring areas; performance flags; recommended manager actions.
- Gap: Dependencies, data inputs, hosting, impact, and goal date are not specified in the roadmap object.

#### M.1 Manager's Overview

- Action: Managers promotion.
- Goal: Assist managers with promotions, merits and staff planning.
- Source: `AI roadmap copied to wsl.xlsx`.
- Outputs: Promotion planning context; merit discussion inputs; staff planning prompts.
- Gap: Dependencies, data inputs, hosting, impact, and goal date are not specified in the roadmap object.

#### M.2 Manager Capacity and Portfolios

- Action: Managers account assignments.
- Goal: Assist managers to assign accounts and portfolio capacity.
- Source: `AI roadmap copied to wsl.xlsx`.
- Outputs: Portfolio capacity view; account assignment support; load-balancing prompts.
- Gap: Dependencies, data inputs, hosting, impact, and goal date are not specified in the roadmap object.

#### M.3 Manager ICP

- Action: Managers ICP.
- Goal: Assist managers with ICP calculations.
- Source: `AI roadmap copied to wsl.xlsx`.
- Outputs: ICP calculation support; planning assumptions; manager review inputs.
- Gap: Dependencies, data inputs, hosting, impact, and goal date are not specified in the roadmap object.

## Accelerator Drops

Accelerators are tracked separately from the formal roadmap unless they are promoted.

| Accelerator | Status | Audience | Time to create | Estimated saving | Roadmap treatment | Next step |
|---|---|---|---:|---:|---|---|
| NPS Response Templates | Shipped | Initial CSM rollout; EU expansion next | 20 min | 30 min per CSM; 12 CSMs impacted | Count as accelerator savings, not as a roadmap tool | Track reuse and collect feedback from CSMs. |
| JAI Assist CSM Dashboard | Prototype | CSMs and CSM leadership | TBD | TBD | Track as accelerator candidate; estimated saving is TBD | Validate with additional customer exports and estimate repeatable CSM review time saved. |

## Accelerator Rules

| Rule | Threshold | Treatment |
|---|---|---|
| Track | Any automation that saves time, improves consistency, or removes manual formatting. | Add to the Accelerator Drops table. |
| Mention | 5+ team-hours saved, 3+ CSMs impacted, or visible manager/customer-facing value. | Include in the monthly roadmap update as accelerator savings. |
| Promote | Recurring workflow, cross-team dependency, productized data flow, or meaningful build effort. | Move into the formal roadmap; then count it as a roadmap tool. |

## Cloud Ops Implications

The full roadmap needs more than static page hosting. Based on the roadmap data, Cloud Ops should expect these platform capabilities:

- Authenticated CRM/SFDC access.
- Search layer or warehouse for Elevator/shared account memory.
- Support-system access for support trend and escalation tools.
- Snowflake or BI-layer access for KPI/value/adoption analysis.
- Release content index and document generation backend.
- CRM/product-data integration for whitespace and renewal tools.
- Digital engagement platform integration for digital motion outreach.
- Generated document storage with permissions and retention.
- Role-based access for CSM, AM, GCC, PS, Pre Sales, Ops, and manager audiences.

## Data Gaps In Roadmap Source

These are not defined or complete in `AI_Roadmap.html`:

- Manager Tools dependencies, inputs, hosting, impact, hours, and goal dates.
- Exact data contracts for CRM, support, Snowflake, warehouse, release library, Matik, or digital engagement platform integrations.
- Authentication model.
- Data retention model.
- Production hosting model.
- LLM provider/model selection.
- Whether current Central prototypes should be renamed or mapped one-to-one to formal roadmap item ids.

