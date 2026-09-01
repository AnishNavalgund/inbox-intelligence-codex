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

- A standalone, reusable `inbox-intelligence` Codex skill
- A normalized subscription-stream schema
- Classification and scoring guidance
- A simplified private dashboard specification

## Requirements

- Codex with access to the Gmail app for the accounts you want to analyze
- Sites if you want a hosted interactive dashboard

Make sure the Codex app has the Gmail plugin installed and the email is connected. Same with Sites.

## Install

Ask Codex to install the skill directly from GitHub:

```text
$skill-installer Install the Inbox Intelligence skill from https://github.com/AnishNavalgund/inbox-intelligence-codex/tree/main/skills/inbox-intelligence
```

Or clone the repository and copy `skills/inbox-intelligence` into your Codex skills directory:

```bash
git clone https://github.com/AnishNavalgund/inbox-intelligence-codex.git
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R inbox-intelligence-codex/skills/inbox-intelligence "${CODEX_HOME:-$HOME/.codex}/skills/"
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