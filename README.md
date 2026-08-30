# Inbox Intelligence for Codex

Inbox Intelligence is a privacy-conscious Codex workflow that turns recurring email across multiple connected Gmail accounts into a structured map of subscriptions and newsletters.

It answers:

- What am I subscribed to?
- Which Gmail account receives it?
- How long has it been arriving?
- Why do I probably receive it?
- How frequently does it email me?
- Which streams appear useful, noisy, duplicated, or protected?

The workflow is strictly read-only. It does not delete, archive, label, send, mark, or unsubscribe from email.

## What is included

- A reusable `inbox-intelligence` Codex skill
- A repository-local Codex marketplace for installation and testing
- A normalized subscription-stream schema
- Classification and scoring guidance
- A simplified private dashboard specification

## Requirements

- Codex with access to the Gmail app for the accounts you want to analyze
- Sites if you want a hosted interactive dashboard

Make sure the Codex app has the Gmail plugin installed and the email is connected. Same with Sites.

## Install locally

Clone the repository, then from its root:

```bash
codex plugin marketplace add .
codex plugin add inbox-intelligence-codex@inbox-intelligence
```

Start a **new Codex conversation** after installation so the skill is discovered.

## Use

Run the full workflow:

```text
$inbox-intelligence Analyze all of my connected Gmail accounts read-only and build my private subscriptions and newsletters dashboard.
```

Or run only one stage:

```text
$inbox-intelligence Create a read-only master subscription inventory from all connected Gmail accounts. Do not build a dashboard yet.
```

```text
$inbox-intelligence Enrich the existing inventory with subscription age, probable origin, value, noise, protection, and recommendations. Do not rebuild it.
```

## Data model

Inbox Intelligence does not assume that a sender address equals a subscription. It organizes recurring email as:

```text
Organization → Subscription stream → Receiving Gmail account
```

This keeps editorial newsletters, product announcements, saved alerts, receipts, and system notifications from being incorrectly merged.

## License

MIT © 2026 Anish Navalgund
