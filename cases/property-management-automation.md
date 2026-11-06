# Connected operations workspace · property management

**My role:** workflow and data-model design, AI-assisted implementation, integration, verification and operational use.  
**Tools:** Supabase · ChatGPT plugins · Jira / Forge · Telegram / Telethon · Confluence · Google Sheets / Apps Script.

## What I built

I connected **business records, guest conversations and team tasks** into one practical working process. Instead of searching separate apartment spreadsheets, chats and task boards, a team member can ask ChatGPT a question in ordinary language. It checks connected sources, retrieves relevant context and helps prepare the next action.

**Supabase holds business facts. Jira holds work and decisions. ChatGPT is the conversational interface to both.**

![System-specific integration map: Supabase, messages, Jira and related reporting tools](ops-architecture.svg)

## How it works

### 1. Supabase: linked operational data

A structured database contains apartment and complex profiles, owners and contacts, bookings and payments, distribution listings, utilities and access/payment references, content records, and **Telegram conversations**. Stable IDs link people, messages, bookings and apartments when an association is known.

- **Messages:** a Telethon listener ingests incoming and outgoing Telegram messages through a Supabase function, with checkpoints, retry handling and exclusions.
- **Bookings:** the booking provider has **not made an integration API available to this team**. I therefore use its exports and reconcile new or changed bookings in Supabase, rather than claim a real-time automatic feed. Information can become outdated between imports.
- **Apartments and reference codes:** new property records, utility accounts and payment references can be maintained in their respective tables. Completeness is not assumed: a missing code must be verified, never guessed.

### 2. ChatGPT: search and context in plain language

Connected **Supabase and Atlassian/Jira plugins** let ChatGPT look up apartment information, find a specific guest's conversation, inspect newly stored messages, and check linked booking and issue context.

**Example request:**

> “Find the latest guest messages about the hot-water problem, identify the apartment, check its open Jira issue and draft a reply.”

The assistant retrieves the records, helps identify the next step and proposes a message. **A human checks the facts and sends the response.** These actions happen through the connected ChatGPT workspace; there is no separate guest-support dashboard to demonstrate.

### 3. Jira + Forge: work tied to the same apartment records

Jira manages tasks, incidents, leads, priorities, assignees, statuses, blockers and follow-ups. I built/configured a **Supabase-backed apartment custom field using Jira Forge**: users select a residential complex and then an apartment, while apartment identity and derived details come from the database rather than a duplicate list.

The assistant can find work linked to an apartment, create/update tasks and follow-ups, and help reconcile new guest information with existing lead records. **Jira remains authoritative for task state; Supabase remains authoritative for property and booking data.**

## Other tools in the same operational environment

### Expenses and reimbursements

![Reconstruction of the actual expenses form, filters, ledger and printable balance view](screens/expenses.svg)

A **Google Sheets + Apps Script** interface for recording expenses and cash reimbursements, filtering transactions and inspecting employee balances. The image reproduces the implemented two-column layout using invented records. This is a separate finance ledger, **not an assertion that every expense is stored in Supabase**.

### Owner settlement reports

![Reconstruction of actual booking/expense editor and printable PDF report](screens/owners.svg)

An HTML reporting tool imports booking CSV data, calculates the owner's share where needed, converts amounts using National Bank of Georgia exchange rates, supports expense adjustments, and previews/exports a PDF. The published image follows the working layout but contains fictional owners, units and amounts.

### Scheduled Telegram listings

I also built a scheduler with controls for posting channels, apartments, listing text, photos and the publication queue, plus background operation and restart handling. This is a **separate publishing process**, not part of the guest-message archive.

## My contribution and boundaries

I structured the data and workflows, designed the interaction between tools, implemented integrations with AI coding assistants, diagnosed failures, tested operational scenarios and maintained the setup used by the team. I do **not** claim that I hand-coded every module, that booking exports synchronize in real time, or that an AI assistant autonomously sends guest replies or approves financial decisions.

**Privacy:** all public screen examples and identifiers are synthetic or anonymized. Production data, messages, company name, credentials and private repository contents are not published here.

[Technical verification notes](technical-verification.md) · [Public code examples](https://github.com/AlenaYashkina)
