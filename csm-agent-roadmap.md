# AI Agent Roadmap for JAGGAER CSM

## Goal

Create a roadmap similar to the GCC example, but focused on the JAGGAER Customer Success Management lifecycle:

1. Implementation
2. Onboarding
3. Sustain Growth
4. Renewal

The best place to start is not a large fleet of agents. It is 3-4 tightly scoped agents that help CSMs with repeatable work, make customer health visible earlier, and improve renewal readiness.

## What The CSM Process Image Adds

Your `CSM process.png` shows the actual CSM operating motion, which is more useful than a generic customer-success model.

It breaks the lifecycle into:

1. Implementation
2. Onboarding
3. Sustain Growth
4. Renewal

And it shows the work items under each stage:

- Implementation: CSM intro call, steerco participation, goal and KPI alignment, help-resource enablement, escalation management
- Onboarding: second intro call, create success plan, enable help resources, introduce value dashboard
- Sustain Growth: regular touchpoints, product release enablement, review or update success plan, operational performance review, coordinate references, identify expansion, manage escalations
- Renewal: QBR, renewal assessment, identify expansion opportunities

That means the roadmap should be anchored to those stage tasks directly.

## Why These First Agents

Public JAGGAER messaging emphasizes:

- faster onboarding and higher adoption
- measurable KPIs and quantifiable success metrics
- proactive guidance aligned to strategic objectives
- structured guidance aligned to product innovation and releases
- value tracking across initiatives, categories, business units, and outcomes

That makes the first-wave CSM agents relatively clear.

## Recommended Phase 1 Agents

### 1. Implementation Handoff Agent

Purpose:
Turn implementation outputs into a clean CSM-ready account brief.

Main job:
- collect project closure details
- prepare the CSM intro call brief
- check whether steerco participation is needed
- confirm goal and KPI alignment inputs exist
- confirm help-resource enablement status
- identify missing onboarding prerequisites
- summarize goals, scope, modules, risks, open actions, and stakeholders
- create the first CSM action list

Why it should be first:
- it removes a common failure point between implementation and customer success
- it creates the structured account record that every other agent depends on

Key outputs:
- CSM handoff summary
- onboarding readiness score
- missing-data checklist
- first 30-day action plan

CSM process alignment:
- supports `CSM Intro Call`
- supports `Attend Steerco Calls`
- supports `Goal & KPI Alignment`
- supports `JAGGAER Help Resources Enablement`
- supports `Manage Customer Escalations`

### 2. Success Plan and Adoption Agent

Purpose:
Drive onboarding and early value realization after go-live.

Main job:
- create or update the success plan
- prepare the second intro call
- map customer goals to JAGGAER capabilities
- track onboarding tasks to completion
- confirm value dashboard introduction status
- monitor adoption signals by module, role, and business unit
- recommend training, enablement, and next-best actions

Why it should be first:
- JAGGAER publicly emphasizes adoption, utilization, rollout, training, and supplier enablement
- this is where CSM teams usually get the fastest operational ROI

Key outputs:
- success plan
- adoption score
- milestone status
- recommended enablement actions

CSM process alignment:
- supports `CSM Intro Call 2`
- supports `Create Success Plan`
- supports `JAGGAER Help Resources Enablement`
- supports `Introduce Value Dashboard`

### 3. Health and Risk Agent

Purpose:
Continuously detect risk, stalled adoption, weak engagement, and escalation triggers.

Main job:
- combine product adoption, stakeholder engagement, support signals, and technical risk
- score each account red/amber/green
- detect downward trends
- watch for escalation risk and stalled touchpoints
- flag when the success plan needs review
- suggest recovery playbooks and owner actions

Why it should be first:
- it gives the CSM team a proactive book-of-business view
- it creates the decision point for intervention before renewal is at risk

Key outputs:
- overall health score
- risk reasons
- next-best action
- escalation recommendation

CSM process alignment:
- supports `Regular Touchpoints`
- supports `Review/Update Success Plan`
- supports `Operational Performance Review`
- supports `Manage Customer Escalations`

### 4. Value and Renewal Agent

Purpose:
Prepare QBRs, renewal plans, and expansion hypotheses using measured value.

Main job:
- compile achieved outcomes versus plan
- pull initiative progress and value metrics
- generate QBR packs
- flag renewal risk 90-120 days before contract end
- identify cross-sell and upsell opportunities
- suggest reference-readiness candidates

Why it should be fourth:
- it becomes much more reliable once handoff, adoption, and health data already exist
- it maps directly to the Renewal stage in your lifecycle

Key outputs:
- QBR draft
- renewal readiness score
- expansion opportunity summary
- executive value narrative

CSM process alignment:
- supports `Coordinate Customer References`
- supports `Identify Expansion Opportunities`
- supports `Quarterly Business Review`
- supports `Renewal Assessment`

## Best 2-Agent Start

If you want to start with only 2 agents:

1. Success Plan and Adoption Agent
2. Health and Risk Agent

Reason:
This gives the fastest business impact with the lowest integration complexity. One agent drives progress; the other watches for problems.

Best fit against the CSM process image:
- covers most recurring work in `Onboarding`
- covers most recurring work in `Sustain Growth`

## Best 3-Agent Start

If you want a stronger operational design:

1. Implementation Handoff Agent
2. Success Plan and Adoption Agent
3. Health and Risk Agent

Reason:
This creates a clean lifecycle from post-implementation into onboarding and then into ongoing risk monitoring.

Best fit against the CSM process image:
- covers the first three lifecycle columns directly
- leaves renewal automation as the second-wave addition

## Suggested Roadmap Layout

To match the GCC example, use a left-to-right lifecycle with 4 agent columns:

1. Handoff Agent
2. Adoption Agent
3. Health Agent
4. Value and Renewal Agent

Decision points:

- Is implementation complete enough for CSM onboarding?
- Is adoption above target by milestone?
- Is account health stable enough to stay in standard cadence?
- Is renewal readiness strong enough to move to commercial planning?

Using the language in your CSM process file, these become:

- Are goals, KPIs, resources, and stakeholders complete enough to move from `Implementation` to `Onboarding`?
- Has the success plan and value dashboard setup progressed enough to move from `Onboarding` to `Sustain Growth`?
- Do touchpoints, operational results, and health signals support standard growth management, or does the account need escalation?
- Is the account ready for `Quarterly Business Review` and `Renewal Assessment`, and is there a credible expansion case?

Closed-loop feedback:

- renewal outcomes feed back into health model tuning
- adoption barriers feed training and release enablement
- escalations feed implementation and onboarding improvements
- QBR insights feed future success-plan templates

## Core Data Fields Needed

These are the minimum fields to make the first agents work well.

### Account and Contract

- account_id
- account_name
- parent_account
- segment
- industry
- region
- contract_start_date
- contract_end_date
- renewal_date
- ARR or contract_value
- products/modules purchased
- licensed users
- active users target
- procurement model or use case

### Stakeholders and Relationship Map

- executive sponsor
- business owner
- system administrator
- procurement lead
- IT lead
- renewal owner
- stakeholder role
- stakeholder email
- stakeholder influence level
- stakeholder sentiment
- last meeting date

### Implementation and Handoff

- implementation_status
- go_live_date
- modules deployed
- modules pending
- integrations completed
- integrations pending
- open risks
- open actions
- known support issues
- training completed
- handoff complete flag

### Success Plan and Outcomes

- customer goals
- agreed KPIs
- baseline KPI values
- target KPI values
- target dates
- milestone list
- milestone owner
- status by milestone
- blockers
- success plan last updated date

### Adoption and Usage

- logins by week or month
- active users by role
- feature adoption by module
- workflow completion rates
- supplier onboarding progress where relevant
- catalog enablement progress where relevant
- transaction volume
- request volume
- sourcing event volume
- contract volume
- invoice volume

### Support, Risk, and Sentiment

- ticket count
- ticket severity mix
- unresolved critical tickets
- escalation count
- time to resolution
- CSAT or feedback score
- meeting sentiment
- executive engagement level
- release impact flags
- compliance or data quality issues

### Value Realization and Renewal

- savings target
- savings realized
- efficiency gains
- cycle time improvement
- supplier adoption improvement
- business case assumptions
- value narrative
- QBR date
- renewal stage
- renewal probability
- expansion opportunity type
- expansion opportunity value

## Example Health Model

Start simple:

- Product adoption: 50%
- Customer engagement and expertise: 20%
- Technical/support health: 30%

That weighting is directionally consistent with how Salesforce publicly frames customer success scoring, and it is a practical starting model for JAGGAER CSM. You can tune it later by segment or product family.

## Practical Build Plan

### Phase 0: Data Foundation

- define canonical account record
- define health inputs and field ownership
- map source systems: CRM, JAGGAER product usage, support, CS notes, contract data
- clean customer identifiers across systems

### Phase 1: Human-in-the-Loop Copilots

- launch Success Plan and Adoption Agent
- launch Health and Risk Agent
- keep approvals and outreach with the CSM

### Phase 2: Lifecycle Expansion

- add Implementation Handoff Agent
- add Value and Renewal Agent
- generate QBR drafts and renewal prep automatically

### Phase 3: Closed-Loop Optimization

- use renewal outcomes to retrain risk logic
- use adoption barriers to improve onboarding playbooks
- use release-impact data to trigger enablement campaigns

## Good Final Roadmap Headline

AI-Powered CSM Lifecycle for JAGGAER

Subtitle:
Multiple AI agents working together to improve onboarding, accelerate adoption, surface risk early, and strengthen renewal outcomes.

## Sources

- JAGGAER Customer Success page: https://www.jaggaer.com/contact-csm
- JAGGAER Adopt: https://www.jaggaer.com/solutions/adopt
- JAGGAER Customer Success Packages: https://www.jaggaer.com/blog/customer-success-packages
- JAGGAER Value Tracker: https://www.jaggaer.com/solutions/value-tracker
- JAGGAER JAI: https://www.jaggaer.com/solutions/jai
- Salesforce Customer Success Score: https://trailhead.salesforce.com/content/learn/modules/customer-success-score/get-to-know-the-salesforce-customer-success-score
- Salesforce score weighting: https://trailhead.salesforce.com/content/learn/modules/customer-success-score/learn-how-we-calculate-the-score
- HubSpot renewal timing guidance: https://blog.hubspot.com/service/customer-success-renewals
