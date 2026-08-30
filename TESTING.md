# Beta testing plan

Keep the repository private until all four stages pass.

## 1. Static validation

From the repository root, validate the skill and plugin with the bundled Codex creator tools available in your installation:

```bash
python3 /path/to/skill-creator/scripts/quick_validate.py plugins/inbox-intelligence-codex/skills/inbox-intelligence
python3 /path/to/plugin-creator/scripts/validate_plugin.py plugins/inbox-intelligence-codex
```

Also verify:

- the manifest name matches the plugin folder;
- no TODO placeholders remain;
- all sample data is fictional;
- no email addresses, tokens, Site IDs, or private URLs are committed;
- the Git working tree contains only intended files.

## 2. Local installation

From the repository root:

```bash
codex plugin marketplace add .
codex plugin add inbox-intelligence-codex@inbox-intelligence
```

Start a new Codex conversation after installation.

## 3. Read-only behavioral test

Begin with an inventory-only request:

```text
$inbox-intelligence Analyze all connected Gmail accounts and create only a recurring subscription inventory. This is a test: use read-only operations and do not build a Site.
```

Pass criteria:

- all connected Gmail accounts are identified;
- no Gmail write operation is proposed or called;
- organization, stream, and account remain separate fields;
- protected messages cannot become unsubscribe candidates;
- counts and dates are supported or marked approximate;
- origin is labeled CONFIRMED, LIKELY, or UNCERTAIN;
- no full message bodies appear in output.

Then test dashboard mode against the generated dataset.

Pass criteria:

- only Subscriptions and Newsletters are primary views;
- Frequency, Portfolio, and Age & Why work as filters;
- dashboard preferences are local-only;
- Demo Mode hides accounts and sensitive evidence;
- a hosted Site remains owner-only by default.

## 4. Personal-data audit

Before making the repository public, run repository-wide searches for:

- real Gmail addresses;
- OAuth or bearer tokens;
- ChatGPT Site project or deployment IDs;
- private Site domains or URLs;
- real inventory JSON;
- copied email bodies;
- absolute paths that reveal a contributor's private directory layout.

Ask one trusted beta tester to install from a private clone and run the inventory-only test with their own Gmail connection. Collect only workflow feedback, never their inventory or screenshots containing personal data.

## Release gate

Publish only when static validation, one fresh-conversation run, Demo Mode review, and one trusted-user beta all pass.
