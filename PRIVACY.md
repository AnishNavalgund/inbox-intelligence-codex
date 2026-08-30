# Privacy

Inbox Intelligence is designed for local, user-directed analysis of recurring Gmail communication.

## What this repository collects

Nothing. The repository includes no tracking, analytics service, hosted database, Gmail credentials, or telemetry endpoint.

The plugin itself is an instruction package. Gmail access occurs through the user's own connected Gmail app in ChatGPT/Codex and is subject to the user's account, workspace, connector permissions, and applicable OpenAI and Google terms.

## Read-only behavior

The skill instructs Codex to use only Gmail search and read operations. It prohibits:

- deleting or archiving email;
- applying or removing labels;
- marking messages read or unread;
- sending or drafting email;
- unsubscribing;
- modifying Gmail in any way.

Users should review the Gmail app's permissions in their own environment before running the workflow.

## Data minimization

The workflow prefers message metadata, snippets, and aggregate counts. Full message bodies should be read only when necessary for classification and must not be reproduced in datasets or dashboards.

Security codes, authentication messages, private transaction content, and full financial or regulatory documents must not appear in shareable output.

## Generated artifacts

An Inbox Intelligence run may create a structured dataset and a private Site in the user's own task context. Those artifacts can contain sensitive derived information even when they do not contain full messages.

Before sharing any generated artifact:

1. enable Demo Mode;
2. remove Gmail addresses and private identifiers;
3. generalize sensitive organizations and sender evidence;
4. verify the Site's audience;
5. inspect screenshots and recordings frame by frame.

The plugin repository must never contain a user's real inventory, email addresses, Site project IDs, access tokens, private Site URLs, or exported message content.

## Responsible disclosure

Report privacy or security concerns through the repository's GitHub issue tracker without attaching real email data.
