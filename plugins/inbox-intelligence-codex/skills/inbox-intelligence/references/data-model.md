# Inbox Intelligence data model

Use one row per normalized subscription stream per receiving Gmail account.

## Identity hierarchy

`organization_name` represents the company, publisher, community, or service.

`stream_name` represents a distinct recurring communication purpose, such as "Weekly newsletter", "Saved job alerts", or "Product announcements".

`receiving_account` identifies the connected Gmail account. In public or demo output, replace addresses with neutral labels such as `Primary inbox` and `Secondary inbox`.

Create a stable `service_id` from normalized organization and stream identity. Do not include the receiving account in the ID; the same stream can have multiple account rows.

## Required fields

```text
service_id
organization_name
stream_name
sender_name
sender_domain
receiving_account
message_type
category
relationship_types
first_seen
last_seen
emails_last_30_days
emails_last_12_months
estimated_frequency
recent_unread_count
content_description
probable_reason_for_subscription
subscription_origin_status
subscription_origin_evidence
protected_status
classification_confidence
value_score
noise_score
recommended_action
recommendation_confidence
recommendation_reason
potential_annual_email_reduction_if_removed
duplicate_across_accounts
alternative_delivery_recommendation
```

Use ISO `YYYY-MM-DD` dates. `first_seen` means earliest observed matching message, not necessarily the true signup date.

## Message types

Cleanup-eligible:

- Newsletter / Editorial
- Promotion / Marketing
- Job / Opportunity Alert
- Event / Community
- Product / Account Update

Protected:

- Transactional / Receipt
- Security / Authentication
- Financial / Regulatory
- Service / Billing / Renewal
- Developer / System Notification

## Categories

- AI & Technology
- Developer Tools
- Career & Jobs
- Professional Network
- Education
- News & Media
- Finance & Investing
- Travel
- Shopping
- Food & Delivery
- Productivity
- SaaS
- Events & Communities
- Entertainment
- Government / Utilities
- Health Insurance / Administrative
- Telecommunications
- Other

## Relationship types

- Newsletter subscriber
- Free account user
- Paid customer
- Former customer
- Developer ecosystem member
- Community member
- Event attendee
- Job seeker / candidate
- Professional network member
- Financial customer
- Investor
- Shopper / consumer
- Traveler / loyalty member
- Service subscriber
- Unknown

Use an array when more than one applies.

## Scores

`value_score` is 0–100. Consider relevance, uniqueness, professional usefulness, active relationship evidence, personalization, and actionable information. High frequency is not automatically low value.

`noise_score` is 0–100. Consider frequency, repetition, promotional density, duplicate topics, unread accumulation, and low information density.

Assign exactly one `recommended_action`:

- KEEP — IMPORTANT
- KEEP
- DIGEST
- REDUCE FREQUENCY
- REVIEW
- UNSUBSCRIBE CANDIDATE
- PROTECTED

General logic:

- High value + low noise → KEEP
- High value + high noise → DIGEST or REDUCE FREQUENCY
- Medium value + medium noise → REVIEW
- Low value + high noise → UNSUBSCRIBE CANDIDATE
- Protected → PROTECTED

`alternative_delivery_recommendation` must be one of: Immediate, Daily, Weekly Digest, Monthly Digest, No email needed.

Estimate annual reduction conservatively from recent and 12-month history. Do not claim that a dashboard preference actually changes delivery.
