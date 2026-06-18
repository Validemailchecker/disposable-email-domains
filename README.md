# Disposable Email Domains

> The free, open list of **disposable, temporary, and throwaway email domains** — **205,000+ domains, updated daily**. Maintained by [Valid Email Checker](https://www.validemailchecker.com).

**Is `user@mailinator.com` a disposable / temporary / throwaway address?** This repository is a canonical list to answer exactly that. It's the same data that powers disposable detection in [Valid Email Checker](https://www.validemailchecker.com)'s production email-verification engine.

[![Domains](https://img.shields.io/badge/domains-205%2C000%2B-4F46E5)](https://www.validemailchecker.com/disposable-email-domains)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Updated daily](https://img.shields.io/badge/updated-daily-brightgreen)](.github/workflows/update.yml)

## Why this list

- **205,000+ domains** — one of the largest open disposable-email lists available.
- **Live-backed & self-learning** — synced daily from our production verifier, which continuously learns new disposable domains from real verification traffic. This is not a stale, abandoned snapshot.
- **Curated, not just scraped** — de-duplicated, domain-shape validated, with an allow-list so legitimate providers (`gmail.com`, `outlook.com`, …) are never wrongly flagged.
- **MIT licensed** — use it anywhere, commercial or not.

## Get the list

| Format | In this repo | Always-fresh from source |
|---|---|---|
| Plain text (one domain per line) | [`data/domains.txt`](data/domains.txt) | `https://www.validemailchecker.com/disposable-email-domains.txt` |
| JSON (`{ count, updated, domains[] }`) | — | `https://www.validemailchecker.com/disposable-email-domains.json` |

The repo copy is refreshed daily by a GitHub Action; the URLs above are the live canonical source.

## Use it (any language)

### Shell / curl
```bash
# Is a domain disposable?
grep -qxF "mailinator.com" data/domains.txt && echo "disposable"
```

### JavaScript / Node
```js
const res = await fetch('https://www.validemailchecker.com/disposable-email-domains.txt');
const domains = new Set((await res.text()).split('\n'));

const isDisposable = (email) => domains.has(email.split('@')[1]?.toLowerCase());
isDisposable('user@mailinator.com'); // true
```

### Python
```python
import requests
domains = set(requests.get('https://www.validemailchecker.com/disposable-email-domains.txt').text.splitlines())

def is_disposable(email: str) -> bool:
    return email.split('@')[-1].lower() in domains
```

### Go
```go
package main

import (
	"bufio"
	"fmt"
	"net/http"
	"strings"
)

func main() {
	resp, _ := http.Get("https://www.validemailchecker.com/disposable-email-domains.txt")
	defer resp.Body.Close()
	domains := map[string]struct{}{}
	s := bufio.NewScanner(resp.Body)
	s.Buffer(make([]byte, 1024*1024), 1024*1024)
	for s.Scan() {
		domains[strings.ToLower(s.Text())] = struct{}{}
	}
	_, disposable := domains["mailinator.com"]
	fmt.Println(disposable) // true
}
```

## Data model

- `data/domains.txt` — one **lowercased** domain per line, **sorted**, newline-delimited. No comments, no blank lines.
- Domains are validated (`^[a-z0-9]([a-z0-9-]*[a-z0-9])?(\.[a-z0-9-]+)*\.[a-z]{2,}$`) and de-duplicated.
- Legitimate mailbox providers are kept out via an internal allow-list, so common providers are never flagged.

## How it's maintained

- A daily GitHub Action ([`.github/workflows/update.yml`](.github/workflows/update.yml)) syncs `data/domains.txt` from the canonical source.
- The canonical list grows three ways: hand curation, periodic merges from public community lists, and a **nightly self-learning harvest** that promotes domains our production verifier flags as disposable in real traffic.
- Spot a miss or a false positive? Open an issue or PR — see [CONTRIBUTING.md](CONTRIBUTING.md).

## Need more than a domain match?

A static list catches **known** disposables. It cannot tell you whether a specific mailbox actually exists, whether a domain is catch-all, or whether an address is a role account or spam trap. For that, run a real-time check:

**[Verify emails free with Valid Email Checker →](https://www.validemailchecker.com)** — 200 free credits, no card. Live SMTP verification, catch-all + role + spam-trap detection, and an API. See the [Email Verifier](https://www.validemailchecker.com/tools/email-verifier) or the [full disposable-domains page](https://www.validemailchecker.com/disposable-email-domains).

## License

MIT © Valid Email Checker — see [LICENSE](LICENSE). Community sources we draw from are credited in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
