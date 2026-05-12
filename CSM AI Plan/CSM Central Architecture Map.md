---
title: CSM Central Architecture Map
created: 2026-05-06
source_folder: /home/yshvadro/CSM Central
tags:
  - csm-ai-plan
  - architecture
  - cloud-ops
---

# CSM Central Architecture Map

## Scope

This document maps `CSM_Central.html`, the main launcher site named `CSM Central`.

## High-Level Architecture

`CSM_Central.html` is a single static HTML page with:

- Inline CSS for layout and responsive styling.
- Static HTML shell for header, search, filters, quick actions, favorites, recently used tools, and lifecycle grid.
- Inline SVG symbol sprite for icons.
- Inline JavaScript that builds the tool cards from a hard-coded file list.
- Browser-only state for favorites and recently used tools.
- Links to child `.html` tools in the same folder.

There is no server-side rendering, no backend call, and no database interaction in `CSM_Central.html`.

## Page Structure

| Layer | Element / behavior | Source evidence |
|---|---|---|
| Document shell | `<!DOCTYPE html>`, page title `CSM Central`, inline `<style>`. | `CSM_Central.html:1`, `CSM_Central.html:6`, `CSM_Central.html:7` |
| Header | Title block and search panel. | `CSM_Central.html:843`, `CSM_Central.html:853` |
| Search | `input#searchInput`, clear button, lifecycle filter nav. | `CSM_Central.html:857`, `CSM_Central.html:858`, `CSM_Central.html:862` |
| Summary metrics | Total tools, visible tools, favorites, lifecycle areas. | `CSM_Central.html:866` |
| Quick actions | Buttons generated from `quickActions`; clicking applies search terms. | `CSM_Central.html:885`, `CSM_Central.html:1028`, `CSM_Central.html:1211` |
| Roadmap link | Static link to `AI_Roadmap.html`. | `CSM_Central.html:891` |
| Favorites / recent | Mini-tool lists populated from localStorage. | `CSM_Central.html:899`, `CSM_Central.html:1358` |
| Lifecycle grid | Generated columns for lifecycle stages and matching tools. | `CSM_Central.html:914`, `CSM_Central.html:1240` |
| Icons | Inline SVG sprite. | `CSM_Central.html:925` |
| Runtime data | `lifecycleStages`, `htmlFiles`, `quickActions`, rule arrays. | `CSM_Central.html:989`, `CSM_Central.html:1017`, `CSM_Central.html:1028` |

## Runtime Flow

1. Browser loads `CSM_Central.html`.
2. Inline script defines lifecycle stages and child HTML file names.
3. `htmlFiles` is mapped through `createToolFromFile()` into `tools`.
4. Favorites and recent ids are read from localStorage and pruned to match available tools.
5. `init()` renders filters, quick actions, utilities, and lifecycle tool cards.
6. User search/filter/quick-action clicks rerender the lifecycle grid.
7. User favorites or opens a tool; favorites/recent ids are persisted in localStorage.
8. Tool links open child HTML pages in new tabs.
9. Copy-link action writes an absolute URL to clipboard or falls back to a temporary textarea copy path.

## Main Data Objects In The Launcher

| Object | Purpose | Source evidence |
|---|---|---|
| `lifecycleStages` | Defines the five launcher categories: Implementation, Adoption, Sustain Growth, Renewal, Manager Tools. | `CSM_Central.html:989` |
| `htmlFiles` | Defines the child tools visible in the hub. | `CSM_Central.html:1017` |
| `quickActions` | Defines five workflow shortcuts: customer meeting, success plan, account health, renewal, product updates. | `CSM_Central.html:1028` |
| `storageKeys` | Defines localStorage keys for favorites and recent tools. | `CSM_Central.html:1061` |
| `keywordRules` | Infers lifecycle stage from filename keywords. | `CSM_Central.html:1066` |
| `descriptionRules` | Infers card descriptions from filename keywords. | `CSM_Central.html:1074` |
| `iconRules` | Infers card icon from filename keywords. | `CSM_Central.html:1084` |
| `tools` | Derived runtime array of launcher cards. | `CSM_Central.html:1099` |

## Child Tool Registry

The launcher currently registers these child files:

- `AI_Roadmap.html`
- `Elevator.html`
- `Full-suite-savings-tool.html`
- `Mockup_Release_Assistant.html`
- `New_Value_Calculator.html`
- `Success_Plan.html`
- `Support_Case_Analysis.html`
- `workflow_analyzer.html`

There is no dynamic directory scan in the browser. New tools must be added to the `htmlFiles` array or supplied through a future API/config.

## Routing / Navigation Model

The site uses plain hyperlinks. There is no SPA router.

- Roadmap button points to `AI_Roadmap.html`.
- Tool cards link to their encoded HTML filenames.
- Links use `target="_blank"` and `rel="noopener"`.
- Recently used state is updated when a user clicks a tool link.

## Persistence

The launcher persists only:

- `csmToolsHub.favorites`
- `csmToolsHub.recent`

Both are JSON arrays in browser localStorage. No user identity, customer data, search terms, or tool data is persisted by the launcher itself.

## Search And Filtering

Search is client-side. `getVisibleTools()` checks:

- selected lifecycle stage,
- favorites mode,
- the tool's lower-cased searchable string,
- quick-action keyword matches.

Search does not call an API.

## Architecture Gaps For Production

These gaps are not solved in the current launcher:

- Authentication and authorization.
- Centralized tool registry or config service.
- Role-based access to sensitive tools.
- Audit logs for which users open which tools.
- Backend health checks.
- Deployment routing for referenced missing assets.
- Versioning and release process for static files.
- Content security policy and approved external domains.
- Secret management, if the future backend uses LLM or document-generation services.

## Suggested Production Shape

For Cloud Ops, a practical production architecture would be:

1. Private authenticated static hosting for the hub and static client-only tools.
2. Same-origin API service for backend-backed tools like Release Assistant.
3. Server-side config or JSON manifest for tool registry, categories, permissions, and feature flags.
4. Auth-aware file generation service with retention and cleanup.
5. Separate data layer for customer/account/support datasets instead of embedding confidential data in static HTML.
6. CSP allowlist that starts strict and only adds required external domains after review.

