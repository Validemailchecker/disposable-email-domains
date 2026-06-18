# Contributing

Thanks for helping keep this list accurate.

## Found a disposable domain we're missing?
Open an issue (or a PR adding it to `data/domains.txt`) with the domain. Bulk additions are welcome — include a one-line note on the source if you have one.

## Found a false positive (a legitimate provider listed)?
This matters most — a wrongly-listed provider blocks real users. Open an issue with the domain and we'll add it to our allow-list so it's removed and never re-added.

## How the list is generated
`data/domains.txt` is **auto-synced daily** from the canonical source at
`https://www.validemailchecker.com/disposable-email-domains.txt`. That source is
where curation, community-list merges, and the self-learning harvest all land.

Because the file is regenerated from the source, a PR that only edits
`data/domains.txt` will be reconciled on the next sync — so for permanent
changes, an **issue** (which we apply to the canonical source) is usually the
faster path. PRs are still welcome for docs and tooling.

## Formatting
- One lowercased domain per line, sorted, no comments or blank lines.
- ASCII / punycode for IDNs.
