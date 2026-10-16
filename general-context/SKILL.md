---
name: general-context
description: Manages non-technical project context in `CONTEXT_GENERAL_<PROJECT_NAME>.md` (all uppercase). Triggers on `/general-context`, when updating business context, logging non-technical info, or syncing general context. Inspects the working directory, extracts business, marketing, sales, team, and identity details, translates technical decisions into business terms, deduplicates, and reorganizes content into standard sections.
---

<what-to-do>

1. Determine the `<PROJECT_NAME>` in **ALL UPPERCASE** with underscores for spaces (e.g., `BRIGHTWATER_ACADEMY`):
   * First, look for any existing `CONTEXT_GENERAL_*.md` file in the current working directory.
   * If none exists, identify the core business/organization entity name from project documentation (e.g., brand guidelines, mission statements, pitch decks, client proposals, or course metadata). Fall back to the folder or repo name only if no entity name can be identified.

2. Locate or create `CONTEXT_GENERAL_<PROJECT_NAME>.md`:
   * If the file exists, read its full contents.
   * If it does not exist, create `CONTEXT_GENERAL_<PROJECT_NAME>.md` using the standard structure defined below.

3. Scan the working directory for new or relevant non-technical information:
   * **Team & People:** Team structure, founders, advisors, key contacts, roles, responsibilities.
   * **Identity & Brand:** Vision, value proposition, brand voice, target audience, positioning.
   * **Marketing & Growth:** Acquisition channels, customer personas, launch plans, marketing strategies.
   * **Sales & Revenue:** Pricing tiers, licensing models, distribution channels, monetization rules.
   * **Operations & Vendors:** External services, legal/compliance notes, vendor management, recurring operational expenses.

4. Translate technical choices into plain business terms:
   * Translate technical infrastructure, APIs, and frameworks into cost, vendor risk, time-to-market, or compliance impact before adding.

5. Reorganize, Deduplicate, and Clean Up:
   * Since multiple agents or updates may have added information over time, perform a complete pass to reorganize content under the proper standard headings.
   * Consolidate overlapping or redundant bullet points.
   * Remove exact or near-exact duplicates across different sections.

6. Write the final cleaned, reorganized content back to `CONTEXT_GENERAL_<PROJECT_NAME>.md`.

</what-to-do>

<supporting-info>

## Invocations & Triggers

This skill runs when explicitly invoked by the user through:
* Command: `/generate-general-context`
* Direct requests to update business context, log project non-technical info, deduplicate business context, or synchronize general context.

## Non-Technical Context Scope

The file `CONTEXT_GENERAL_<PROJECT_NAME>.md` captures all operational, strategic, and human elements of the project. Do not include pure technical implementation details or code architecture unless translated for business clarity.

### Technical-to-Business Translation Rules

When technical architecture impacts business strategy, translate it to non-technical concepts:

| Technical Concept | Non-Technical Business Translation |
| :--- | :--- |
| Cloud Hosting / Infrastructure | Operating costs, service reliability/uptime guarantees, data security compliance. |
| Third-party APIs / Services | External vendor dependencies, recurring operational costs, service risk. |
| Tech Stack / Framework Selection | Time-to-market speed, maintenance costs, talent hiring availability. |

## Target File Structure

Always maintain and reorganize `CONTEXT_GENERAL_<PROJECT_NAME>.md` into the following layout:

```markdown
# General Context: <PROJECT NAME>

## Overview & Identity
- **Vision:** ...
- **Target Audience:** ...
- **Brand & Positioning:** ...

## Team & Roles
- ...

## Business & Revenue Model
- **Pricing:** ...
- **Distribution & Channels:** ...

## Marketing & Growth
- ...

## Operational & Vendor Dependencies
- ...
```

</supporting-info>