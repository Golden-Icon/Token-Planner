# Token Planner

A single-file, offline web app that works out which Star Citizen ships you can
build from the ships and CCUs you already hold, and what each one costs you
out of pocket.

No install, no server, no network calls. One HTML file. Double-click it on
Windows or Linux and it runs.

## Usage

1. Export two CSVs from [ccugame.app](https://ccugame.app):
   - **Ships** — your account's ships and their `place` (hangar / buyback)
   - **CCUs** — your account's upgrade CCUs and their `isBuyback` flag
2. Drop both files onto the page.
3. Read the two tabs.

Everything is derived from those two files. Nothing is fetched, nothing is
cached, nothing leaves your machine.

## The two tabs

**Obtainable ships** — every ship reachable from what you hold, sorted by
cheapest first. Each row shows the cheapest route; expand any row to see every
other route with its own cost.

**Ships I own** — the hulls sitting in your hangar, one row per hull. These are
the ships you can use right now without spending anything. Buyback ships are
not listed here, because they cost money to release.

## How cost is calculated

Every item on a chain is priced by where it actually sits in your account.
**MSRP is never used** — it is not money you pay.

| Item | Where | Cost |
|---|---|---|
| Base ship | hangar | **$0** |
| Base ship | buyback | its `pledge` |
| CCU | hangar (`isBuyback=false`) | **$0** |
| CCU | buyback (`isBuyback=true`) | its `pledge` |

Where a ship has several buyback hulls carrying different pledges, the cheapest
one is used, because you choose which hull to release.

A ship you already own, upgraded only with CCUs you already own, is genuinely
**$0**. In a typical export that is a handful of ships. Everything else costs
something.

A ship already sitting in your buyback is not filtered out — it appears as a
**release** option alongside its chains, sorted in with them by cost, so you can
compare building it against just letting the hull out.

Each route is priced independently. This does **not** model hull or CCU
consumption, so several routes may compete for the same base ship.

## Requirements

A modern browser. No build step, no dependencies.

## License

MIT — see [LICENSE](LICENSE).