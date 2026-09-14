# netmonitor-data

Daily Czech Netmonitor (gemiusAudience / SPIR) category stats. Auto-pushed every day ~08:05 Europe/Prague for the previous day. History starts 2026-08-30.

## Layout

- `data/<YYYY-MM-DD>.json` — full day payload (overview of 26 categories + per-site detail for 5 tracked categories)
- `data/latest.json` — newest day, same structure

## Payload fields

Per row: `rank`, `category`/`name`, `real_users` (int), `views` (int), `time` (raw string, e.g. "53y 142d"), `time_seconds` (int — use this), `visits` (int or null).

Categories with per-site detail: Zpravodajství, Sport, Bulvární magazíny, Auto-Moto - obsah, Magazíny zaměřené na ženy a módu.

## Reading from an external agent (private repo)

Requires a GitHub token with read access to this repo (fine-grained PAT, Contents: Read-only, is enough):

```bash
TOKEN="<github_pat_...>"

# latest day
curl -s -H "Authorization: Bearer $TOKEN" \
  https://raw.githubusercontent.com/davidrynes/netmonitor-data/main/data/latest.json

# specific day
curl -s -H "Authorization: Bearer $TOKEN" \
  https://raw.githubusercontent.com/davidrynes/netmonitor-data/main/data/2026-09-13.json

# list available days (GitHub Contents API)
curl -s -H "Authorization: Bearer $TOKEN" \
  https://api.github.com/repos/davidrynes/netmonitor-data/contents/data
```

404 on a day = not measured yet or scrape failed. This mirror exists because restrictive proxies that block custom domains usually allow `raw.githubusercontent.com`.
