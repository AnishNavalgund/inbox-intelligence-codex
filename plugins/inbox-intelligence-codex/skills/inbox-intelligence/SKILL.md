---
name: inbox-intelligence
description: Analyze recurring subscriptions and newsletters across multiple connected Gmail accounts and optionally build a private Inbox Intelligence dashboard. Use for subscription inventories, newsletter analysis, recurring-email frequency, subscription age and origin, inbox value/noise analysis, or cross-account overlaps. Do not use for reading, replying to, or managing individual messages.
---

# Inbox Intelligence

Turn recurring email into a structured map of the user's subscriptions, newsletters, and digital relationships.

## Non-negotiable safety boundary

Gmail access is read-only for this workflow.

- Use only search, list, fetch, and other read operations.
- Never delete, archive, label, move, mark read/unread, unsubscribe, send, draft, or modify Gmail.
- Never treat security, authentication, financial/regulatory, billing/renewal, receipts, or developer/system notifications as ordinary unsubscribe candidates.
- Prefer headers, metadata, snippets, and aggregate counts. Read message content only when it is genuinely necessary to classify a stream, and never reproduce full message bodies.
- Do not publish a dashboard unless its access is verified as owner-only or the user explicitly approves the resolved sharing audience.
- Store generated inbox data only in the user's task workspace or Site. Never write it into this plugin's source directory.

At the start, identify every Gmail account the connector can access. Tell the user how many accounts will be analyzed and keep account handling explicit throughout the workflow.

## Choose the requested mode

1. **Inventory** — discover and normalize recurring streams.
2. **Enrich** — add relationship, origin, value, noise, protection, and recommendations to an existing inventory. Reuse it; do not rebuild it.
3. **Dashboard** — build the simplified private Subscriptions and Newsletters experience from an existing structured dataset.
4. **End to end** — run Inventory, Enrich, and Dashboard in that order.

If the user's request clearly selects a mode, begin without asking. If a required connector is unavailable, complete the parts that are still possible and state the missing capability.

## Inventory workflow

Read [references/analysis-playbook.md](references/analysis-playbook.md) before searching Gmail. Read [references/data-model.md](references/data-model.md) before creating the dataset.

Use the last 12 months as the primary window. Search older history only for important or long-running streams where the earliest relationship date or subscription origin materially improves the result.

Do not equate a sender address with a subscription. Normalize using:

**Organization → Subscription stream → Receiving Gmail account**

Merge obvious aliases for one organization, but keep functionally different streams separate. Detect the same organization or stream across more than one account.

Produce a structured JSON dataset plus a concise inventory summary. Label dates as earliest observed, not guaranteed signup dates.

## Enrichment workflow

Read [references/data-model.md](references/data-model.md). Enrich every existing stream-account row.

Infer why the user receives a stream from evidence already found in Gmail:

- **CONFIRMED** — direct evidence exists, such as a welcome email, registration, account creation, saved alert, purchase, or event confirmation.
- **LIKELY** — strong inference from account history or repeated personalized activity.
- **UNCERTAIN** — the available evidence does not establish the origin.

Never turn an inference into a fact. Protected communication always receives the `PROTECTED` action regardless of its noise score.

## Dashboard workflow

Read [references/dashboard-spec.md](references/dashboard-spec.md). Use only the structured Inbox Intelligence dataset, never raw message bodies.

Build the dashboard with Sites when available and keep it private by default. If Sites is unavailable, build a local equivalent or return the dataset and dashboard specification without blocking the analysis.

All dashboard controls are local presentation state. They must not invoke Gmail actions.

## Completion checks

Before finishing, verify:

- every connected Gmail account was included or explicitly reported unavailable;
- the dataset uses organization/stream/account normalization;
- protected communication cannot appear as an unsubscribe candidate;
- origin claims carry CONFIRMED, LIKELY, or UNCERTAIN status;
- no full message bodies, authentication content, credentials, or private identifiers appear in shareable output;
- Gmail was not modified;
- a hosted dashboard is private unless the user approved broader access.
