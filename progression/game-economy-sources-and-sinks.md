---
title: Game economy - sources and sinks
category: progression
tags: [economy, faucets, sinks, inflation, currency, crafting, trading, eve, wow, diablo-3]
use_cases:
  - "in-game currency is worthless because players have too much"
  - "design currencies, crafting and shops for an RPG or survival game"
  - "decide whether to allow player-to-player trading"
  - "separate soft and hard currency without making the game pay to win"
  - "simulate an economy before shipping it"
status: draft
last_verified: 2026-10-14
sources:
  - https://gamebalanceconcepts.wordpress.com/
  - https://machinations.io/
  - https://en.wikipedia.org/wiki/Diablo_III
  - https://en.wikipedia.org/wiki/Eve_Online
  - https://www.gamesbrief.com/
---

# Game economy - sources and sinks

## Summary
A game economy is the set of resources, how they enter the game (sources or faucets), how they leave (sinks or drains), and how players convert them. The designer's job is to keep flows balanced so rewards stay meaningful over months. Unbalanced flows cause inflation, scarcity or exploits that no combat tuning can fix.

## Key concepts
- **Sources (faucets)**: quest rewards, enemy drops, passive income, daily bonuses. **Sinks (drains)**: repairs, shop purchases, upgrade costs, consumables, taxes, death penalties.
- **Flow balance**: if faucets exceed sinks, stock grows and prices rise (inflation). If sinks exceed faucets, players feel starved and stop spending.
- **Stock vs flow**: track both what players hold and how fast it moves. A stock that grows without bound is the warning sign.
- **Multiple currencies**: separate currencies let you control different loops. Soft currency is earned in play; hard (premium) currency is bought with money. Gate things with the right one so each loop stays independent.
- **Conversion points**: crafting, salvage and exchanges convert one resource to another and are the places exploits appear.
- **Player markets**: trading adds emergent economics but removes designer control of flow.
- **Machinations-style modeling**: the Adams and Dormans approach: draw resources as pools, flows and converters and simulate them.

## When to use / scenarios
- Currency piles up and nothing is worth buying: add sinks that players want (cosmetics, upgrades, housing), not penalties.
- Everything feels expensive and players feel poor: check faucets and whether early-game rewards are tuned to early prices.
- Considering trading: only if you can monitor it, and only if the game benefits from social economy (EVE, Albion Online).
- Do NOT add a currency for its own sake. Every currency needs its own faucets, sinks and a reason to exist; otherwise fold it into an existing one.

## How it works / example
Real cases: WoW's gold inflates over expansions because new content adds faucets faster than sinks, so Blizzard introduced big sinks (mounts, the token system, repair costs, auction house fees). EVE Online runs a mostly player-driven economy in which destruction of ships is the dominant sink; the studio publishes monthly economic reports and employs economists. Diablo 3 launched a real-money and gold auction house; because players could buy gear instead of finding it, the loot loop lost value, and Blizzard shut the auction house down in 2014 and rebalanced loot toward finding items in play.

A minimal simulation shows how a sink rate reaches equilibrium.

```python
import random

def simulate(players=1000, days=60, income=(80, 120), spend_rate=0.03, tax=0.0, seed=1):
    """Each player earns daily gold; spends a fraction of savings on a sink; optional flat tax on income."""
    rng = random.Random(seed)
    wallets = [0.0] * players
    history = []
    for day in range(days):
        for i in range(players):
            earned = rng.uniform(*income) * (1 - tax)
            wallets[i] += earned
            wallets[i] -= wallets[i] * spend_rate
        history.append(sum(wallets) / players)
    return history

for label, kwargs in [("weak sink", dict(spend_rate=0.01)),
                      ("strong sink", dict(spend_rate=0.08)),
                      ("weak sink + tax", dict(spend_rate=0.01, tax=0.2))]:
    h = simulate(**kwargs)
    print(f"{label:16s} day10={h[9]:8.0f} day30={h[29]:8.0f} day60={h[59]:8.0f}")
```

With a proportional sink, average wealth converges toward income divided by spend rate. A weak sink lets wealth keep growing for months, so prices must inflate, while a strong one stabilizes early. Real games use sinks that scale with wealth (percentage repair costs, high-end upgrade tiers), because flat sinks do nothing against rich veterans.

## Trade-offs
- **Closed vs open economy**: closed (no trading) is fully controllable and cheat-resistant; open has emergent depth and community, but needs active monitoring and fighting RMT (real-money trading) and bots.
- **Soft vs hard currency**: separating them protects progression from pay-to-win, but conversion between them must be one-way or very tightly limited.
- **Sink type**: mandatory sinks (repairs) feel like taxes; optional aspirational sinks (cosmetics, housing, prestige items) feel like rewards. Prefer the second and keep a little of the first for tension.
- **Fixed vs dynamic prices**: dynamic prices follow supply but can be gamed; fixed prices are legible but drift out of date.

## Gotchas
- Duping or exploit bugs flood the economy; log currency creation and alert on anomalies.
- Faucets added in new content are often forgotten when computing inflation. Audit all sources each patch.
- Sinks that punish (steep death penalties) hurt retention more than they drain gold.
- Time-gated premium currency used to rush progress turns a sink into a pay-to-win lever; be explicit about what money can and cannot buy.
- Players hoard when they fear needing resources later; give regular convenient sinks so hoards do not become stockpiles that break balance.

## Related
- [[progression-systems]] - XP and currency are both flows with sources and sinks.
- [[reward-schedules-and-loot]] - drops are the main faucet; salvage and crafting are sinks.
- [[retention-and-session-design]] - daily income caps and long-term goals shape economy flow.
- [[feedback-loops-and-snowballing]] - rich-get-richer dynamics in an economy are a feedback loop.
- [[game-balance]] - economy tuning is balance work at the systemic level.

## References
- Ian Schreiber, "Game Balance Concepts" (economy and resource sessions): https://gamebalanceconcepts.wordpress.com/
- Adams and Dormans, "Game Mechanics: Advanced Game Design" and Machinations: https://machinations.io/
- Diablo III overview, including the auction house removal: https://en.wikipedia.org/wiki/Diablo_III
- EVE Online overview and economic reports: https://en.wikipedia.org/wiki/Eve_Online
- Nicholas Lovell, GamesBrief on free-to-play economies: https://www.gamesbrief.com/
