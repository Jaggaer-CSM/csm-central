---
title: Deployment Readiness Checklist
created: 2026-05-06
source_folder: /home/yshvadro/CSM Central
tags:
  - csm-ai-plan
  - deployment
  - cloud-ops
---

# Deployment Readiness Checklist

## Before Any Shared Deployment

- Confirm audience and access model.
- Put the site behind SSO if any current customer/account/support data remains embedded.
- Remove or protect customer-specific static data.
- Remove local `file://` links.
- Resolve missing assets for `Elevator.html`, `Mockup_Release_Assistant.html`, and `Success_Plan.html`.
- Decide whether third-party scripts are allowed.
- Add CSP and security headers.
- Confirm all external links open with `rel="noopener noreferrer"` where appropriate.
- Review pages that use `innerHTML` before connecting to untrusted backend/user content.

## Static Hosting Readiness

Ready-ish as static private tools:

- `CSM_Central.html`
- `AI_Roadmap.html`, if treated as internal and local links are removed.
- `Full-suite-savings-tool.html`, if UT example/customer value data is acceptable for the audience.
- `New_Value_Calculator.html`, if browser-only handling is acceptable.
- `workflow_analyzer.html`, if XML data remains local and users understand report export sensitivity.
- `Support_Case_Analysis.html`, if support case data is restricted and jsDelivr dependency is approved or vendored.

Not ready from this folder alone:

- `Elevator.html`, due to missing local assets/data scripts.
- `Mockup_Release_Assistant.html`, due to missing static index and backend dependency.
- `Success_Plan.html`, due to external tracking/widget scripts, missing `/static` assets, and embedded customer-specific content.

## Backend Readiness

Required for Release Assistant production:

- Authenticated API service.
- Release source index.
- Search/chat endpoint.
- Feature rows and metrics endpoints.
- Document/PPT/video generation endpoints.
- Generated file storage with authenticated or expiring links.
- Retention cleanup job.
- Request validation and rate limits.
- Logging/redaction policy.

## Observability

Current files do not define production observability. Cloud Ops should add:

- application health endpoint for backend,
- structured error logging,
- generated file audit logs,
- user/action audit events for sensitive tools,
- metrics for API latency, failures, and generation volume,
- alerts for failed generation, storage cleanup failures, and auth failures.

## Rollout Recommendation

1. Private static pilot for `CSM_Central.html` plus client-only tools.
2. Remove/replace embedded confidential data where not needed for pilot.
3. Build Release Assistant backend separately behind auth.
4. Add role-filtered tool registry.
5. Promote tools one by one after data/security review.

