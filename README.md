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

> **Early beta:** review the privacy notes and test with a fresh Codex conversation before relying on the results.

## What is included

- A reusable `inbox-intelligence` Codex skill
- A repository-local Codex marketplace for installation and testing
- A normalized subscription-stream schema
- Classification and scoring guidance
- A simplified private dashboard specification
- Fictional demo data with no real inbox information
- Privacy, testing, and demo-video documentation

## Requirements

- Codex with access to the Gmail app for the accounts you want to analyze
- Sites if you want a hosted interactive dashboard
- Permission to create local task artifacts

Connector availability and permissions depend on the user's own ChatGPT/Codex environment. This repository does not contain Gmail credentials or provide a Gmail API server.

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

## Privacy

The repository contains only fictional sample data. The plugin runs no analytics server and collects no inbox data itself. Gmail content is accessed through the user's own connected app and processed within their own Codex workflow.

Read [PRIVACY.md](PRIVACY.md) before testing or sharing a generated dashboard.

## Test before publishing

Follow [TESTING.md](TESTING.md). Keep the repository private until static validation, a fresh-conversation test, and a personal-data audit all pass.

## Demo

The no-voice, one-minute product-demo storyboard is in [docs/demo-storyboard.md](docs/demo-storyboard.md).

## Project status

The initial beta focuses on accurate inventory construction and a clear Subscriptions / Newsletters dashboard. It intentionally does not perform Gmail cleanup actions.

## License

MIT © 2026 Anish Navalgund
