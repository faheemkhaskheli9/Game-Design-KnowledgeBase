---
title: Game balance
category: mechanics
tags: [balance, dominant-strategy, rock-paper-scissors, cost-curve, power-budget, patching, simulation, asymmetric]
use_cases:
  - "one weapon, class, card or strategy is picked or wins far more than the rest"
  - "how do I price units, cards or items so they are fair for their cost?"
  - "should I buff the weak option or nerf the strong one?"
  - "I have a spreadsheet of stats and need to know if it is balanced"
  - "asymmetric factions or characters feel unfair against each other"
status: draft
last_verified: 2026-10-14
sources:
  - "https://gamebalanceconcepts.wordpress.com"
  - "https://www.gamedeveloper.com/design/gdc-2012-sid-meier-on-how-to-see-games-as-sets-of-interesting-decisions"
---

# Game balance

## Summary
Balance is the practice of tuning a game's numbers and relationships so that the intended range of choices is viable, difficulty and rewards feel right, and no option makes the others pointless. It is not the same as equality: a balanced game can have wildly different options as long as each has a niche and a cost. Use this topic when a strategy dominates, when pricing items or units, or when planning patches.

## Key concepts
- **Dominant strategy**: an option that is best regardless of what the opponent or situation does. It kills choice, see [[meaningful-choices]].
- **Intransitive relationships**: A beats B, B beats C, C beats A (rock-paper-scissors). They stop any single option from dominating and create counterplay. Fire/Water/Grass in Pokemon is the best-known example.
- **Cost curve / power budget**: every option has a cost; its total benefit should equal what the cost buys, using a common currency such as mana, gold or points. Outliers on the curve are either bargains (overpowered) or traps.
- **Symmetric vs asymmetric balance**: symmetric games (Chess pieces, mirror matches) are balanced by construction; asymmetric ones (StarCraft factions, Root, Overwatch heroes) are balanced by approximately equal win rates and by different play patterns, never identical power.
- **Fun over fair**: numbers that are perfectly fair but dull are worse than slightly lopsided options that are exciting. Players tolerate "strong but telegraphed" far better than "weak but safe".
- **Win rate and pick rate**: the two metrics to read together. High pick and high win rate means overpowered; high pick and low win rate means a trap that looks good; low pick and high win rate means undiscovered or too hard.
- **Degenerate strategies**: tactics that exploit a rule loophole (infinite combos, stalling) and break the intended experience.

## When to use / scenarios
- Playtest data shows one choice taking most of the picks, or one faction dominating the ladder.
- You are designing a new unit, card or item and need a price: use the cost curve, then test.
- Players say "there is only one viable build".
- You are choosing between buffing and nerfing in a live patch.
- Single-player games need balance too (difficulty, resource pacing), but the target is a range of difficulty rather than equal win rates; see [[flow-and-difficulty-curves]].

## How it works / example
Method (after Ian Schreiber's balance course): choose a currency, price each option, then check against the curve, then simulate, then playtest.

1. **Pick a cost resource and fit a line.** In many card games, each mana point buys roughly a fixed amount of stats. Hearthstone's vanilla minions were famously on the curve of 2x+1 total stats for x mana (commonly cited by players; check against the current game before using the exact numbers).
2. **Price abilities in the same currency** (a draw is worth some stats, a charge is worth some stats) by testing, then keep a table.
3. **Check outliers**, then decide: an option above the curve must be nerfed or given a downside; below the curve is a trap or must have a hidden utility.
4. **Test the matchups** with a simulation or a matrix of win rates.

A cost-curve check plus a small intransitive matchup test in stdlib Python:

```python
# 1) Cost curve: fit stats = a*cost + b by least squares, flag outliers.
cards = {"Wisp": (1, 2), "Imp": (2, 5), "Knight": (3, 7), "Golem": (4, 9),
         "Ogre": (5, 11), "Dragon": (6, 20), "Rat": (3, 3)}  # name: (cost, stats)
xs = [c for c, _ in cards.values()]
ys = [s for _, s in cards.values()]
n = len(xs)
mx, my = sum(xs) / n, sum(ys) / n
a = sum((x - mx) * (y - my) for x, y in zip(xs, ys)) / sum((x - mx) ** 2 for x in xs)
b = my - a * mx
print(f"stats ~= {a:.2f}*cost + {b:.2f}")
for name, (c, s) in cards.items():
    resid = s - (a * c + b)
    tag = "OVERPOWERED?" if resid > 3 else "TRAP?" if resid < -3 else "ok"
    print(f"{name:7s} cost {c} stats {s:2d} resid {resid:+.1f} {tag}")

# 2) Intransitive matchups: fraction of random picks each type wins vs a random opponent.
beats = {("Fire", "Grass"), ("Grass", "Water"), ("Water", "Fire")}
types = ["Fire", "Water", "Grass", "Brute"]  # Brute: strong generic, loses to nothing...
power = {"Fire": 1.0, "Water": 1.0, "Grass": 1.0, "Brute": 1.1}
def edge(x, y):
    if (x, y) in beats: return 1.5 * power[x]
    if (y, x) in beats: return 0.5 * power[x]
    return power[x] / power[y]
for t in types:
    avg = sum(edge(t, o) / (edge(t, o) + edge(o, t)) for o in types if o != t) / (len(types) - 1)
    print(f"{t:6s} average win share {avg:.2f}")
```

The cost-curve part flags Dragon as above the line and Rat below it. The matchup part demonstrates that a "Brute" with a small raw bonus and no counters wins more than the three typed units on average: when adding a generic option to a rock-paper-scissors ring it must carry a cost or a counter, or it dominates.

Patch strategy:
- **Prefer buffs to nerfs** when possible: buffs add fun, nerfs remove it. Players remember what they lost.
- **Nerf when the option crowds out others** or is both strong and unfun (hard to counter, no skill expression).
- **Change one variable at a time** and make small steps so the result is attributable; move a number by 5 to 10 percent, not 50.
- **Communicate intent** in patch notes ("we want X to be a mid-range specialist").

## Trade-offs
- **Perfect balance vs variety**: removing all outliers also removes personality. Keep a visible power band, not a flat line.
- **Data vs design intent**: win rates reflect skill distribution and popularity, not just power. A hard character with a 48 percent win rate across all players may be strongest at top level.
- **Frequent patches vs stability**: fast adjustment fixes problems early but forces relearning; competitive scenes want a stable meta.
- **Balance for the top vs for the majority**: pro-level and casual-level problems differ, and each patch typically favours one.

## Gotchas
- **Balancing on averages**: variance matters; two options with equal expected value can feel very different, see [[randomness-and-luck]].
- **Interactions**: items balanced alone combine into broken sets. Test pairs, and expect combinatorial outliers in deckbuilders and RPGs.
- **Spreadsheet confidence**: a model is only as good as its currency; it will not tell you that a mechanic is boring.
- **Hidden positive feedback** makes the strongest option strengthen itself, see [[feedback-loops-and-snowballing]].
- **Nerfing the symptom**: if a build is strong because of a system (a scaling stat, a cheap resource) nerfing the item leaves the system to produce the next outlier.
- **Counterplay vacuum**: an option that cannot be countered cannot be balanced by numbers alone; give players a way to respond, see [[combat-and-encounter-design]].

## Related
- [[meaningful-choices]] - balance is the means by which choices stay interesting rather than dominated.
- [[feedback-loops-and-snowballing]] - runaway power is a feedback problem, not only a numbers problem.
- [[playtesting-and-metrics]] - win rates, pick rates and telemetry feed balance decisions.
- [[combat-and-encounter-design]] - matchups, counters and enemy roles are the structure of combat balance.
- [[game-economy-sources-and-sinks]] - the economy is balanced with the same currency and flow thinking.

## References
- Ian Schreiber, "Game Balance Concepts" (course), especially on cost curves, intransitive mechanics and dominant strategies: https://gamebalanceconcepts.wordpress.com
- Ernest Adams and Joris Dormans, "Game Mechanics: Advanced Game Design" (2012).
- Jesse Schell, "The Art of Game Design", chapter on balance and lenses of fairness and meaningful choices.
- Sid Meier, "Interesting Decisions", GDC 2012: https://www.gamedeveloper.com/design/gdc-2012-sid-meier-on-how-to-see-games-as-sets-of-interesting-decisions
- Elias, Garfield, Gutschera, "Characteristics of Games" (2012).
