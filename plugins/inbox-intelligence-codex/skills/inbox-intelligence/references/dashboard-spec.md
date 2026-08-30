# Simplified Inbox Intelligence dashboard

Build a calm, high-density working surface from the structured dataset. The dashboard must never call Gmail or expose full message bodies.

## Product structure

Use two primary views only:

1. **Subscriptions** — recurring cleanup-eligible streams except editorial newsletters.
2. **Newsletters** — streams classified as Newsletter / Editorial.

Protected operational mail may be acknowledged in privacy copy but should not clutter these views.

## First viewport

- Product title and one-sentence explanation.
- Read-only status.
- Subscriptions / Newsletters switch.
- Three concise summary cards: stream count, estimated emails per month, and overall value/noise signal.

Avoid an oversized marketing hero, dense KPI grids, an attention scatterplot, or a sentence-heavy insight strip.

## Insight explorer

Show one visualization at a time:

- **Frequency ladder** — daily/near-daily, several times weekly, weekly, monthly/occasional, inactive. Clicking filters the cards.
- **Portfolio** — categories sized or ranked by volume, with stream count and average value. Clicking filters the cards.
- **Age & Why** — age bands alongside probable subscription-origin groups. Clicking filters the cards.

Do not add an aggregate origin-confidence panel. Confidence belongs on individual cards and details where it has context.

## Subscription cards and detail

Each card should show organization, stream, neutral account label, category, recent volume, value, noise, earliest-observed age, probable reason, and CONFIRMED/LIKELY/UNCERTAIN status.

The detail view may add sender domain, first/last seen, cadence, unread count, relationship type, origin evidence summary, recommendation, and explanation.

Dashboard preferences such as Keep, Digest, Review, or Hide must be device-local state and must explicitly say they do not change Gmail.

## Demo Mode

Include a Personal / Demo toggle. Demo Mode must:

- replace Gmail addresses with neutral labels;
- generalize sensitive organization, financial, sender, and origin-evidence details;
- hide private identifiers and authentication/security content;
- keep aggregate analytics and interactions visible;
- default to safe content for screenshots and recordings.

## Hosting and privacy

Use Sites when available. Keep a newly generated dashboard owner-only by default. Verify access immediately before deployment. If access is shared, public, or ambiguous, ask the user to approve the resolved audience before deploying.

Do not put the user's dataset, email addresses, Site project ID, tokens, or generated private Site URL into the plugin repository.
