## Token Planner 0.1.0 — first release candidate

Offline planner for Star Citizen CCU chains. Reads your ccugame.app ship and
CCU CSV exports and reports which ships you can build from what you already
hold, and what each one costs out of pocket.

**Download:** `Token-Planner-v0.1.0.zip` — extract it and double-click
`index.html`. No install, no server, no network calls. Works on Windows and
Linux.

### What's in it

- **Obtainable ships** — every reachable ship, cheapest first, each row expanding
  to show every route with its own cost
- **Ships I own** — the hulls in your hangar, one row per hull
- CSV export of the whole table

### Cost model

Every item on a chain is priced by where it sits in your account. MSRP is never
used — it is not money you pay.

| Item | Where | Cost |
|---|---|---|
| Base ship | hangar | $0 |
| Base ship | buyback | its pledge |
| CCU | hangar (`isBuyback=false`) | $0 |
| CCU | buyback (`isBuyback=true`) | its pledge |

Multiple buyback hulls at different pledges use the cheapest, since you choose
which hull to release. A ship you already own, upgraded only with upgrades you
already own, is genuinely $0.

Ships already sitting in buyback are **not** filtered out. Each appears as a
release option alongside its chains, ranked by cost, so building it and just
releasing the hull can be compared directly.

Routes are priced independently — hull and CCU consumption is not modelled, so
several routes may compete for the same base ship.

### Known limitations

- Route enumeration assumes a simple chain (no ship repeated within one route)
- Multiple hulls of the same ship are treated as interchangeable; the cheapest
  pledge wins
- Warbond CCUs are priced at their pledge and flagged, not discounted separately

### Verifying

Cost, hop count and route totals were cross-checked against an independent
implementation across all 60 reachable ships and all 4,021 route options in a
live account export: zero mismatches.