CLAUDE.md
Project summary

This project builds a new Eclipse/Avalara integration that downloads Avalara AvaTax transactions by API instead of relying on manual portal reports and tab-delimited imports.

The immediate goal is Phase 1 only: retrieve Avalara transactions for reporting and comparison, while leaving clean extension points for reconciliation and proactive tax validation in later phases.

Current scope

Focus on Phase 1:

Retrieve Avalara transactions for:
A specific document ID.
A user-supplied date range.
Operational reporting periods such as daily, MTD, and prior-month final pull.
Store retrieved Avalara transaction detail in AVALARA_PORTAL.
Use Avalara Doc ID as the key; this corresponds to Eclipse AR AR.ID / @ID.
Design the code so later phases can add reconciliation and corrective workflows without major rearchitecture.

Do not implement Phase 2 or Phase 3 logic yet unless needed for architecture boundaries, interfaces, or placeholders.

Reference implementations

Primary example repo for coding style and prior Avalara integration patterns:

UD.AVA.ECMS.SYNC
GitHub: https://github.com/kerrykincaid/UD.AVA.ECMS.SYNC

Use this repo as the primary reference for:

Avalara API calling patterns previously used successfully.
Eclipse integration conventions.
Coding style and naming patterns that match existing internal systems.

If the old implementation conflicts with current Avalara API requirements, prefer current API requirements while preserving local coding style.

Avalara references

AvaTax API product docs:

https://developer.avalara.com/products/avatax/api/
REST reference: https://developer.avalara.com/api-reference/avatax/rest/v2/

Available MCP server for docs:

{
  "mcpServers": {
    "avalara-docs": {
      "type": "http",
      "url": "https://mcp.avalara.com/docs"
    }
  }
}

Additional reference:

Postman collection: AvaTax-API-postman-collection.json

Note: previous work followed the C# SDK, but current AvaTax SDK/API patterns may have changed. Verify against current docs before implementing new API wrappers.

Business context

Current process is manual:

Run a report in the Avalara web portal.
Download report output.
Extract and transform data.
Import as a tab-delimited file into Eclipse.

This project replaces that manual reporting flow with an API-driven pull-on-demand process.

Domain rules
Eclipse is the operational system of record for which invoice/document IDs should be queried during the current month.
During the current month, Avalara transactions may be uncommitted.
After month end, committed Avalara transactions must also be pulled for full-period comparison.
The design must support identifying:
Transactions present in Avalara but not expected for the Eclipse period.
Transactions expected from Eclipse but not yet committed or not present in Avalara.

These comparison behaviors are primarily for later phases, but Phase 1 design should leave room for them.

Architecture expectations

Build the solution with clear separation of concerns:

Avalara API client layer.
Request/query orchestration layer.
Eclipse/Universe file integration layer.
Mapping/transformation layer.
Logging/error handling layer.

Design for future phases by keeping these concerns separate:

Retrieval.
Reconciliation.
Exception classification.
Corrective action hooks.

Avoid a design where retrieval logic is tightly coupled to reconciliation or UI/reporting logic.

Working rules

When making changes:

Read this file first.
Review the reference repo before proposing architecture.
Propose a short implementation plan before writing major code.
Reuse existing local coding patterns where reasonable.
Prefer small, reviewable changes.
Preserve backward compatibility with Eclipse-side data expectations.
Do not invent Avalara fields or API behavior; verify against current docs.
Flag assumptions clearly when API behavior is uncertain.
Deliverables for Phase 1

Phase 1 should produce:

A way to fetch one transaction by document ID.
A way to fetch transactions for a date range or reporting period.
A transformation path to store results in AVALARA_PORTAL.
Logging for request/response status and exception cases.
Clear extension points for later reconciliation logic.
Non-goals for now

Do not fully implement yet:

Automated reconciliation decisions.
Auto-cancellation logic for zero-value/no-GL-impact transactions.
Real-time proactive invoice tax correction workflows.

These belong to later phases unless scaffolding is needed.

Questions to resolve before coding

Before implementing, identify and confirm:

Exact Avalara endpoints to use for transaction retrieval.
Authentication pattern and credential storage approach.
Expected fields to persist in AVALARA_PORTAL.
Whether paging, throttling, or incremental sync checkpoints are required.
Whether Eclipse will invoke this interactively, by scheduled control program, or both.
Related docs

Detailed requirements should live outside this file:

docs/project-spec.md
docs/phase-1.md
docs/data-mapping.md
docs/api-notes.md
