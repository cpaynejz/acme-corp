# acme-corp

Plain single-page HTML fixture for TraceConverge end-to-end testing. Default persona: **ACME Corp**.

**Live URL:** `https://cpaynejz.github.io/acme-corp/`

## Test plan scenarios served

- TC-1.1.* (most brownfield happy paths) — paste a GTM snippet, mutate the GTM container in tag manager to produce each variant
- TC-1.2.* (greenfield happy paths) — leave fixture clean (no snippet) → run greenfield → paste resulting snippet → re-run as brownfield
- TC-1.3.* (verify-only) — once configured, click Verify
- TC-2.1.* (UNSUPPORTED_CONFIGURATION variants) — paste GTM snippet, configure GTM with the misuse pattern under test
- TC-2.2.* (COLLISION_BLOCKED) — paste GTM snippet, configure container with multiple competing tags
- TC-2.3.* (EM overlap) — paste GTM snippet, enable matching EM toggles in GA4
- TC-3.4.1 (direct gtag.js) — paste gtag loader instead of GTM snippet

## How to configure

Edit `index.html`:

1. **Head section** — paste the GTM snippet (the `<script>...gtag.js...</script>` block GTM gives you) where the marker comment says.
2. **Body section** — paste the GTM `<noscript>` block where the second marker says.
3. Commit and push. GitHub Pages serves the new version in ~30 seconds.

For direct-gtag tests, replace the GTM snippet with:

```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

## Resetting

To reset to greenfield baseline, edit `index.html` and remove the snippet content (leave the marker comments in place).
