# Property-management operations automation

**Role:** operations workflow design, AI-assisted integration, delivery and maintenance  
**Stack:** Jira · Supabase · Google Sheets · Apps Script · lightweight web forms · LLM workflows  
**Scope:** real operational work; diagrams and all records below are anonymized or fictional.

![System-specific data flows across Telegram, Supabase, Jira, finance tools and scheduled publishing](ops-architecture.svg)

The diagram separates **four implemented workflows**, rather than suggesting that guest conversations, Jira issues, financial records and social posting all pass through a single pipeline. It describes integrations at the system level without exposing endpoints, credentials, customer details or private repositories.

## The problem

Managing an apartment portfolio means processing bookings, guest requests, check-ins/check-outs, cleaning, repairs, utilities, staff assignments, owner communication and expenses. When the relevant facts are spread across several channels, small teams lose time cross-checking spreadsheets and chats, and urgent work can become ownerless.

## What I built and operated

**A structured apartment information layer.** Organized property identifiers and operational details in a Supabase-backed database, so an assistant and internal tools could refer to one property record rather than relying on ambiguous room names in messages.

**Task and issue coordination.** Designed Jira workflows for assignments, priorities, maintenance issues and follow-ups, using AI-generated scripts and integrations for routine administration. Human decisions — such as approvals and guest promises — remained assigned to responsible staff.

**Expense input and review.** Designed lightweight HTML/Apps Script interfaces around Google Sheets for expenses and reimbursements. The difficult part was not just the form: the interface had to reflect changes entered elsewhere in the same table, including entries recorded by a teammate.

**LLM-assisted operational retrieval.** Used structured queries and an AI assistant to speed up looking up apartment information and turning natural-language requests into reviewable operational actions. LLM output is not automatically authoritative; the source records and user confirmation matter.

**Owner and staff communication.** Prepared data views and reporting workflows that combine records from different parts of the operation.

### My contribution

I mapped requirements, chose record structures and responsibilities, specified changes to AI coding assistants, configured integrations, debugged failures, validated results and trained the workflow around how colleagues actually worked. This is **AI-assisted implementation**, not a claim of expert hand-written Python or a standalone production SaaS.

## Example 1 · From guest problem to a resolved issue

All entities in this example are fictional.

| Stage | Example record | Review rule |
| --- | --- | --- |
| Incoming request | `EX-102`: no hot water | Resolve apartment ID and booking context |
| Structured issue | `ISSUE-0007`, category `maintenance` | Explicit owner, priority, current status |
| Assignment | Technician A, due 2026-11-08 | No unconditional promise to guest before confirmation |
| Follow-up | `assigned → in_progress → resolved` | Status must reflect actual work, not an LLM guess |
| Report | Resolution time and expense reference | Preserve audit trail and avoid exposing guest contacts |

## Example 2 · Expense reconciliation

A fictional employee enters a 25 GEL repair expense using an internal form. Another teammate records a different expense directly in Google Sheets. Both records must appear in the review interface, and the same expense must not be entered twice.

```json
{
  "expense_id": "DEMO-EXP-0004",
  "property_id": "EX-102",
  "date": "2026-11-06",
  "category": "repair",
  "amount": 25,
  "currency": "GEL",
  "reimbursement_status": "pending"
}
```

**Acceptance criteria used when reviewing this kind of workflow:** a stable row ID, read-after-write confirmation, timestamp and currency validation, duplicate handling, and a clear error state when the source table cannot be reached. A good-looking interface alone is not proof that its data is synchronized.

## Three workflows · recreated from actual tools, with synthetic records

These screens **reconstruct the layout and task flow** of internal tooling used in day-to-day operations: a spreadsheet-backed expense interface, an owner settlement/reporting workflow, and an assistant retrieving guest messages from a private database. They use real types of controls, calculations and integration boundaries. **All apartment IDs, people, dates, financial values and messages are invented.** They are not pixel-for-pixel screenshots from the internal deployment.

### 1. Expense management and employee reimbursements

![Expense and reimbursement interface recreated with fictional rows](screens/expenses.svg)

**Real workflow:** entries are created or reviewed through a lightweight browser interface, while a Google Sheet is also used to record expenses and employee reimbursements. The workflow has to reconcile entries regardless of whether a colleague entered them in the form or in the spreadsheet.

**Displayed scenario:** choose the month and property, filter status, inspect entries from the web form or Google Sheets, and check pending versus approved reimbursements. The displayed sample amounts and employee labels are fictional.

**Technical boundaries:** Google Sheets is the expense ledger; the UI needs to refresh source rows and surface write/read failures. The illustration is not a claim that all data synchronization edge cases have been independently tested.

### 2. Owner settlement reports with PDF export

![Owner statement workflow reconstructed from actual reporting features](screens/owners.svg)

**Real workflow:** import bookings for the selected property and period, calculate amounts attributable to an owner, convert currency using the National Bank of Georgia rate, incorporate expenses, review the settlement and save the statement as a PDF.

**Displayed scenario:** a fictional property with three bookings, a sample USD/GEL rate and deductions. This screen follows the actual business structure of the report: **Bookings → Expenses → Final settlement**, including owner amounts, currency conversion and net owner income. Neither the numbers nor the apartment refer to a real owner.

**Technical boundaries:** a displayed exchange rate needs a source and reporting date; financial periods, booking ownership and expenses must be checked before PDF export. The real PDF format informed this sanitized layout; no real PDF or client details are embedded.

### 3. ChatGPT-assisted guest conversation search

![Assistant conversation with retrieved Telegram records and a manually reviewed draft](screens/guest-assistant.svg)

**Real workflow:** a Telegram listener stores incoming and outgoing messages in Supabase through an ingestion function. The database associates people, chats, messages and bookings; ChatGPT can retrieve relevant history and help prepare a proposed reply. A staff member checks, edits and sends the message.

**Displayed scenario:** an operator searches for a fictional guest's hot-water complaint and receives two cited messages plus a suggested reply. The illustration follows the **actual assistant-based workflow**, not a fictional standalone guest-support product.

**Technical boundaries:** retrieval must respect chat exclusions and message identity; ChatGPT text is a draft, not an automatically sent message. Muted or excluded chats are not treated as searchable sources.

### 4. Scheduled listing publisher

The internal publishing tool has controls for **Telegram destination chats, properties, listing text, photos and a publication queue**. It schedules posts and includes background execution/restart handling. This is a separate integration path in the architecture diagram, not a feature of the expense UI or guest conversation search.

The public portfolio shows the architecture and scope, not real posting logs, private channels or credentials. No unmeasured reach, delivery-rate or time-savings claim is made.

## System design decisions

- **Source of truth:** operational records live in structured tools; the LLM is an interface, not a replacement database.
- **Identity:** property, booking, task and expense records use separate identifiers; do not join by display names.
- **Idempotency:** repeated requests should not silently create duplicates.
- **Permissions:** guest and owner details stay in private company systems. Public demos use synthetic records.
- **Human-in-the-loop:** financial approvals, guest commitments and destructive changes remain explicit actions.
- **Observability:** errors, stale data and unmatched records must be visible rather than covered with optimistic UI messages.

## Why this is a portfolio case and not an open-source product

The workflows were created for an actual operation, but the original repositories and production data are not publicly available. The architecture and interface recreations are based on implemented workflows and source documentation, but they are **not pixel-perfect screenshots of deployed company systems**. No percentage of time saved or ROI is claimed without measurement. The value shown here is operational systems thinking, implementation through AI-assisted tools and practical troubleshooting.

See also the public code examples: [RentGram](https://github.com/AlenaYashkina/rent_gram), [Cluster Forge](https://github.com/AlenaYashkina/cluster-forge), and [Photo Report Generator](https://github.com/AlenaYashkina/photo-report-generator).
