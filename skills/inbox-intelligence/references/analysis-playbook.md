# Gmail analysis playbook

Use this playbook for Inventory mode or the discovery phase of an end-to-end run.

## 1. Establish scope

Resolve all Gmail accounts exposed by the connected Gmail app. Keep queries and counts account-specific so results are not silently attributed to the wrong inbox.

Use a rolling 12-month primary window. Record the analysis date in the dataset metadata.

## 2. Discover candidate recurring sources

Use several complementary searches rather than relying on Gmail categories alone. Depending on connector capabilities, useful signals include:

- Promotions and Updates categories within the time window;
- unsubscribe or preference-management language;
- newsletter/editorial phrasing;
- recurring job, career, price, travel, event, community, and product alerts;
- repeated sender domains and display names;
- subjects with stable recurring prefixes.

Treat Gmail categories as signals, not labels. A receipt in Promotions is still transactional; a newsletter in Updates is still editorial.

Page through enough results to capture recurring senders across the window. Stop expanding a candidate when its stream identity, recent count, annual count, and classification are supported; do not read every message from a high-volume sender.

### Connector search fallback

Do not conclude that an inbox or time window is empty from a summary-style email search alone. If a search unexpectedly returns no messages, or its result count conflicts with label totals or another equivalent query:

1. Verify the account has mail using read-only label counts such as `INBOX`.
2. Repeat the query with message-ID search and pagination.
3. Read only the returned messages' metadata needed for classification; do not fetch message bodies by default.
4. Treat the ID-based result as authoritative when the summary and ID paths disagree, and record the connector discrepancy as a coverage limitation.

Only report an empty result after the broad ID-based check also returns no messages. Keep all fallback queries account-specific and within the same read-only safety boundary.

## 3. Split organizations into streams

Group aliases at the organization level, then separate meaningful purposes. Subject patterns, sender local parts, list headers, cadence, and content descriptions can distinguish streams.

Examples:

- one company may have a newsletter, product announcements, and saved alerts;
- one sender address may carry both receipts and marketing and therefore requires separate streams;
- two sender addresses may represent the same weekly newsletter.

## 4. Count and date

For every stream-account row, estimate or count:

- messages in the last 30 days;
- messages in the last 12 months;
- recent unread messages when the connector exposes that state;
- latest matching date;
- earliest observed date.

For important, high-volume, or apparently long-running streams, search farther back to improve `first_seen` and origin evidence. Do not search older history indiscriminately.

Translate counts into a readable cadence: daily/near-daily, several times weekly, weekly, monthly/occasional, or currently inactive.

## 5. Protect operational mail

Before cleanup classification, separate receipts, authentication, statements, invoices, renewals, government messages, regulatory notices, and developer/system alerts. Frequency or promotional styling does not override protection.

If a mixed sender cannot be split confidently, mark it protected or REVIEW rather than recommending unsubscribe.

## 6. Infer origin carefully

Search for high-signal historical evidence only when it changes the explanation:

- welcome or subscription confirmation;
- account registration;
- saved search or alert creation;
- purchase, membership, loyalty enrollment, or event registration;
- personalized activity tied to an account.

Record a short evidence summary without copying sensitive content. Use CONFIRMED, LIKELY, or UNCERTAIN exactly as defined in the main skill.

## 7. Validate coverage

Compare the final candidate set against the initial searches. Check for:

- major sender domains left unclassified;
- duplicate aliases not normalized;
- functionally different streams merged together;
- the same organization appearing in multiple accounts;
- protected messages leaking into cleanup candidates.

If connector limits prevent exact counts, keep the best supported estimate and lower confidence instead of fabricating precision.
