# Wicky hosted site

This is the hosted, automatically updating version of Wicky. Victorian Premier Cricket is the default. The front page lists verified Victorian associations and shows the season, official source and latest check.

## Publish with GitHub Pages

1. Create a new GitHub repository and upload this folder.
2. In **Settings → Pages**, set **Source** to **GitHub Actions**.
3. Push to the `main` branch. The **Deploy Wicky** workflow publishes the public URL.
4. In **Actions**, run **Refresh rule books** once. It then runs every Monday.

No API key is needed. Questions are answered in the visitor's browser.

## Add or verify an association source

Edit `data/sources.json`. Add an association's official public `rule_url`, `season`, `source_label` and `source_url`. The refresh job supports PDF, DOCX, TXT, MD and HTML. Example:

```json
{
  "id": "example-association",
  "name": "Example Cricket Association",
  "group": "Country",
  "season": "2026–27",
  "rule_url": "https://example.org/playing-conditions.pdf",
  "source_url": "https://example.org/rules",
  "source_label": "Official association website"
}
```

The updater extracts searchable sections, rejects binary/scanned rubbish, records a checksum and retains the last good version if a later refresh fails. A changed official document is committed and deployed automatically.

## Important safeguard

Wicky never guesses a missing rule source. Associations without a verified public rule book are labelled **source needed** and can still use the manual upload option. A formal ruling should always be confirmed with the relevant competition administrator.
