# K-Dash Brain

Signed reference bundles for K-Dash / Distributor Dashboard.

**This repository contains no code and no customer data.** It holds small signed
JSON files carrying general trade reference knowledge — Tally/Excel column-name
synonyms, statutory dates, freight thresholds — which installed copies of the
app can pull and apply.

## Why it is public

Every bundle is signed with Ed25519 and verified inside the app against a key
compiled into the application. A host can withhold a bundle or serve an old one;
it cannot forge one. The transport therefore needs no trust, no token and no
credentials — so the simplest correct host is a public static one.

## What a bundle may contain

Only these sections, enforced by an allow-list in the app:

`colour_codes` · `parse_hints` · `compliance_dates` · `freight_rules` ·
`import_layouts` · `taxonomy_rules`

Applying a bundle is **additive only** — it can add a row the install has never
seen, never edit or delete one the owner created — and everything lands in
separate `brain_*` tables, so removing it is one statement the owner can reason
about.

### `taxonomy_rules` — the one that changes behaviour

The other sections are reference material an install looks things up in.
`taxonomy_rules` feeds the product lookups themselves, so it carries tighter
rules:

* **Two kinds only**, `shade` and `series_keyword`. They are the only two the
  app's local layer can overlay; a row aimed at anything else would apply to
  nothing and report success, so it is refused instead.
* **Precedence is base < brain < owner.** A bundle extends the catalogue the
  app shipped with. Whatever the person running that install corrected by hand
  wins over both, permanently — a bundle can never overwrite it.
* **No shade rows are published here.** Shade catalogues belong to whoever
  compiled them; they stay on the machine they were uploaded to. This
  repository carries vocabulary — wood species, stone types — not anyone's
  colour book. The app's own gate (`tools/bundle_check.py`) fails the build if
  a published bundle contains one.

## Rights

See LICENSE. Published for one purpose - so installed copies can fetch signed
bundles. The compiled work (selection, arrangement, classification) is
protected; the individual facts inside are not claimed as property.

## What will never be here

Anything derived from a customer's data, and anything belonging to a customer —
including supplier catalogues, which stay on the machine they were uploaded to.
