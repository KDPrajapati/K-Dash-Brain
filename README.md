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

`colour_codes` · `parse_hints` · `compliance_dates` · `freight_rules` · `import_layouts`

Applying a bundle is **additive only** — it can add a row the install has never
seen, never edit or delete one the owner created — and everything lands in
separate `brain_*` tables, so removing it is one statement the owner can reason
about.

## Rights

See LICENSE. Published for one purpose - so installed copies can fetch signed
bundles. The compiled work (selection, arrangement, classification) is
protected; the individual facts inside are not claimed as property.

## What will never be here

Anything derived from a customer's data, and anything belonging to a customer —
including supplier catalogues, which stay on the machine they were uploaded to.
