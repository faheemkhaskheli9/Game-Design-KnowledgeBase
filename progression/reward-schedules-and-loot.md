---
title: Reward schedules and loot
category: progression
tags: [rewards, loot, drop-rates, pity, variable-ratio, rarity, loot-boxes, ethics, diablo]
use_cases:
  - "design a loot table and rarity tiers for drops"
  - "players feel loot is boring or too predictable"
  - "add bad-luck protection so unlucky players are not stuck"
  - "decide whether paid random rewards (loot boxes) are acceptable"
  - "rewards stopped feeling exciting after a few hours"
status: draft
last_verified: 2026-10-14
sources:
  - https://en.wikipedia.org/wiki/Reinforcement
  - https://gamebalanceconcepts.wordpress.com/
  - https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0206767
  - https://celiahodent.com/
  - https://www.gamesbrief.com/
---

# Reward schedules and loot

## Summary
A reward schedule is the rule that decides when and how often a player gets something. Loot is the most common reward vehicle: random items with rarity tiers. Variable schedules create strong anticipation, which is why they drive games like Diablo, but the same mechanism underlies gambling, so the design must be deliberate about excitement versus exploitation.

## Key concepts
- **Schedules (from operant conditioning)**: fixed ratio (every Nth action), variable ratio (on average every Nth, unpredictable), fixed interval (after a set time), variable interval (random time windows). Variable ratio produces the steadiest, most persistent behavior in the research literature, which is why slot machines and monster drops use it.
- **Loot table**: a weighted list of possible drops. Weights set the probability; rarity tiers (common, uncommon, rare, epic, legendary) set the emotional value.
- **Pity / bad-luck protection**: a counter that raises or guarantees the chance after repeated misses, capping the worst case.
- **Itemization depth**: Diablo-style loot works because items have random affixes. Most drops are junk, but each one is a quick decision (equip, salvage, ignore) and any drop might be a build changer.
- **Intrinsic vs extrinsic rewards**: extrinsic rewards are items and points; intrinsic rewards are mastery, discovery, expression. Loot should amplify the intrinsic fun, not stand in for it.
- **Reward prediction**: players enjoy surprise more than certainty; a reward they could see coming has less impact than one with some variance.

## When to use / scenarios
- Action RPGs, roguelikes, survival and looter-shooters (Diablo, Borderlands, Destiny): random gear with meaningful variation.
- Quest and milestone rewards: use fixed schedules so players trust them (finish the quest, get the item).
- Players grind with no excitement: add variance, a rare "jackpot" tier, or make drops change decisions.
- Do NOT rely on random rewards for competitive balance (random power in ranked play) or for core progress that players expect to be earned; use deterministic crafting or currencies as a guaranteed route.

## How it works / example
Mix schedules. A typical looter: enemy kills drop on a variable ratio, bosses give guaranteed drops at a fixed ratio, daily chests are on a fixed interval, and crafting offers a deterministic alternative. Weights below mimic a five-tier table with a pity rule that raises legendary odds after every miss.

```python
import random

TIERS = [("common", 70.0), ("uncommon", 22.0), ("rare", 6.5), ("epic", 1.3), ("legendary", 0.2)]

def roll(misses, rng, pity_step=0.15, pity_cap=60):
    """Weighted draw; legendary weight grows by pity_step per miss, forced at pity_cap."""
    if misses >= pity_cap:
        return "legendary"
    weights = [w + pity_step * misses if n == "legendary" else w for n, w in TIERS]
    return rng.choices([n for n, _ in TIERS], weights=weights)[0]

def drops_until_legendary(rng):
    misses = 0
    while True:
        item = roll(misses, rng)
        if item == "legendary":
            return misses + 1
        misses += 1

rng = random.Random(7)
runs = sorted(drops_until_legendary(rng) for _ in range(20000))
print("median drops:", runs[len(runs) // 2])
print("95th percentile:", runs[int(len(runs) * 0.95)])
print("worst case:", runs[-1])
```

Compare with `pity_step=0` and `pity_cap=10**9`: the median is similar but the tail is huge, and those tail players are the ones who quit and post angry threads. Pity cuts the tail without changing the average feel much. Always report the percentiles, not just the mean.

## Trade-offs
- **Frequency vs value**: frequent small drops keep the loop busy but cheapen loot; rare big drops feel special but frustrate. Use a steep rarity ladder with frequent fillers that feed crafting or salvage.
- **Visible vs hidden pity**: showing the counter reduces frustration and respects players; hiding it keeps mystery but can feel unfair. Disclose the rules either way.
- **Targeted vs random loot**: letting players pick a boss to farm for a specific item (farmable bosses with known drop pools, as in many MMOs and Destiny-style activities) converts randomness into a goal and reduces frustration, at the cost of shorter chase.
- **Power vs cosmetic rewards**: cosmetic randomness is lower stakes; random power affects fairness and balance.

## Gotchas
- Loot that is always worse than what you have makes drops feel like noise; guarantee that some fraction of drops are upgrades or sidegrades in the first hours.
- Flooding the inventory with junk creates chores. Give filters, auto-salvage and fast comparison.
- Rarity colors without meaningful differences train players to ignore the system.
- Reward inflation: raising the average reward each patch to keep players interested leads to power creep.

### Ethics
Variable-ratio rewards sold for money are loot boxes. Zendle and Cairns (2018, PLOS ONE) found a correlation between loot box spending and problem gambling severity among players surveyed; correlation is not proof of causation, but regulators in several countries (Belgium and the Netherlands among them) have acted on the concern. Dark patterns include: undisclosed odds, near-miss animations, time-limited "last chance" offers, targeting children, and making progress impossible without a purchase. Respectful alternatives: disclose odds, offer direct purchase of items at a price (as in many cosmetic stores), keep random rewards earnable in play, impose spending caps, and keep minors out of paid randomness entirely. If you would not show the odds screen to a parent, redesign it.

## Related
- [[progression-systems]] - rewards give the progression ladder its steps.
- [[randomness-and-luck]] - drop randomness shares the same variance and fairness concerns.
- [[game-economy-sources-and-sinks]] - loot is a faucet; salvage and crafting are sinks.
- [[retention-and-session-design]] - reward timing shapes sessions and return habits.
- [[player-motivation-and-player-types]] - collectors and achievers respond differently to loot.

## References
- Reinforcement schedules overview: https://en.wikipedia.org/wiki/Reinforcement
- Ian Schreiber, "Game Balance Concepts" (probability and loot sessions): https://gamebalanceconcepts.wordpress.com/
- Zendle, D. and Cairns, P. (2018), "Video game loot boxes are linked to problem gambling", PLOS ONE: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0206767
- Celia Hodent, "The Gamer's Brain" (motivation, rewards and ethics): https://celiahodent.com/
- Nicholas Lovell, "The Curve" and GamesBrief on monetization ethics: https://www.gamesbrief.com/
