---
title: Randomness and luck
category: mechanics
tags: [randomness, luck, prd, pity-timer, shuffle-bag, probability, fairness, roguelike, xcom]
use_cases:
  - "players complain that the RNG is unfair or that they got a streak of bad luck"
  - "how much luck should a competitive game have versus skill?"
  - "loot or gacha drops feel awful for unlucky players"
  - "I want replayability but not frustration from random outcomes"
  - "players do not trust the displayed hit chance or drop rate"
status: draft
last_verified: 2026-10-14
sources:
  - "https://gamebalanceconcepts.wordpress.com"
  - "https://dota2.fandom.com/wiki/Random_Distribution"
  - "https://www.gamedeveloper.com/design/gdc-2012-sid-meier-on-how-to-see-games-as-sets-of-interesting-decisions"
---

# Randomness and luck

## Summary
Randomness adds variety, surprise and a way for weaker players to win sometimes; it also breaks the link between decision and outcome, and humans misjudge streaks. The craft is choosing where randomness enters (before the player decides or after), how much, and how to shape the distribution so outcomes feel fair even when they are not independent. Use it to tune the skill and luck mix, and to fix the "bad streak" experience.

## Key concepts
- **Input randomness**: the random event happens before the player decides (card draw, level layout, enemy spawn). The player then uses skill to respond. Usually felt as interesting.
- **Output randomness**: the random event resolves after the decision (hit roll, crit, loot drop). Can feel as though skill was cancelled. Works best when the decision was a risk assessment.
- **Skill/luck balance**: more luck narrows the gap between players; more skill widens it. Poker, Backgammon and Mario Kart sit at different points, all intentionally.
- **Variance vs expected value**: designers tune averages, players feel the extremes. Low variance makes outcomes predictable; high variance makes stories.
- **Pseudo-random distribution (PRD)**: the chance increases after each failure and resets on success, so the long-run rate equals the stated chance but long streaks vanish. Dota 2 uses it for crits, bashes and similar procs.
- **Bad-luck protection (pity timer)**: a guaranteed success after N failures. Common in loot and gacha systems.
- **Shuffle bag**: draw without replacement from a bag, refill when empty. Tetris-like randomisers and card decks bound streaks this way.
- **Seed**: the number that fixes a random sequence, enabling shared runs (daily challenges), replays and debugging.

## When to use / scenarios
- Roguelikes (Slay the Spire, Hades, Spelunky): put randomness on the input side (what you are offered), let the player's skill decide what to do with it.
- Tactical games with percentages (XCOM, Fire Emblem): show the odds so output randomness becomes a visible risk decision, see [[meaningful-choices]].
- Competitive esports: reduce output randomness, bound it with PRD, or remove it. Pure 25 percent crit streaks decide matches unfairly.
- Loot, drops and gacha: use pity counters so the unlucky player eventually gets rewarded, see [[reward-schedules-and-loot]].
- Not for: a puzzle game where the solution must be learnable and fair; use seeded, designed content instead.

## How it works / example
Perceived fairness is not mathematical fairness. People expect "30 percent" to behave like a rotation, not a coin. Real games respond:
- **XCOM** shows the hit chance and has been widely discussed for players recalling misses at "95 percent" more than hits at 50. A displayed number invites scrutiny, so the implementation must match it exactly or the UI must show the adjusted figure.
- **Dota 2** PRD: a "25 percent" proc starts at a smaller chance and grows by a constant each non-proc. A run of eight misses becomes very unlikely while the long-run rate stays 25 percent.
- **Tetris** uses a bag of the seven pieces so you never wait too long for a needed shape; earlier versions used pure random and caused droughts.

A PRD and shuffle bag in plain Python:

```python
import random

def prd_constant(p, tol=1e-9):
    """Find C so that the long-run proc rate under P(n)=C*n equals p."""
    def rate(c):
        # expected attempts to proc = sum over n of prob(no proc through n-1)
        expected, survive, n = 0.0, 1.0, 1
        while survive > 1e-12:
            chance = min(1.0, c * n)
            expected += survive
            survive *= 1 - chance
            n += 1
        return 1 / expected
    lo, hi = 0.0, p
    while hi - lo > tol:
        mid = (lo + hi) / 2
        lo, hi = (mid, hi) if rate(mid) < p else (lo, mid)
    return (lo + hi) / 2

class PRD:
    def __init__(self, p, rng=None):
        self.c, self.n, self.rng = prd_constant(p), 0, rng or random.Random()
    def roll(self):
        self.n += 1
        if self.rng.random() < min(1.0, self.c * self.n):
            self.n = 0
            return True
        return False

def shuffle_bag(items, rng=None):
    rng = rng or random.Random()
    while True:
        bag = list(items)
        rng.shuffle(bag)
        yield from bag

def longest_dry(rolls):
    best = cur = 0
    for r in rolls:
        cur = 0 if r else cur + 1
        best = max(best, cur)
    return best

rng = random.Random(1)
pure = [rng.random() < 0.25 for _ in range(100000)]
prd = PRD(0.25, random.Random(1))
pr = [prd.roll() for _ in range(100000)]
print("pure  rate %.3f  longest dry %d" % (sum(pure) / len(pure), longest_dry(pure)))
print("prd   rate %.3f  longest dry %d" % (sum(pr) / len(pr), longest_dry(pr)))
bag = shuffle_bag("IJLOSTZ", random.Random(2))
print("".join(next(bag) for _ in range(14)))
```

The PRD run should show the same proc rate with a much shorter worst drought. Seed every generator (as above with `random.Random(seed)`) so bugs and daily-challenge runs are reproducible.

## Trade-offs
- **Luck vs skill**: more luck suits party games and mixed audiences; less suits competitive ladders. Choose by audience, not by taste.
- **True random vs managed random**: managed (PRD, bags, pity) feels fairer and protects players, but exploitable patterns appear (counting a deck, resetting a counter) and the maths no longer matches player intuition about independent events.
- **Transparency vs mystique**: showing exact odds builds trust but exposes streaks to blame; hiding odds avoids that but harms trust and, in some markets, is regulated for paid random items.
- **Input vs output**: input randomness keeps agency but needs adaptable systems; output randomness gives drama but can cancel decisions.

## Gotchas
- **Hidden fudging that contradicts the UI**: if the UI says 85 percent and you quietly adjust, players who do the maths will find out. Either show the adjusted number or do not adjust.
- **Streaks in small samples**: a 5 percent drop is gone for dozens of fights for some players. Always provide a bounded worst case.
- **Players blame RNG for losses and take credit for wins**: expect complaints about fairness even at the stated odds; verify the implementation with a large-sample test before changing the design.
- **Multiple stacked rolls** (hit, then crit, then block) compound variance beyond intuition.
- **Reroll and save-scum loopholes**: if a seed is tied to a save, players will reload until it suits them. Decide whether that is acceptable.
- **Quoted percentages in marketing** must match the code, and in some jurisdictions loot-box odds must be disclosed.

## Related
- [[meaningful-choices]] - randomness only pays off if the player has a choice in how to respond.
- [[reward-schedules-and-loot]] - drop tables, pity timers and variable ratio rewards.
- [[game-balance]] - balance with expected value and variance, not only averages.
- [[feedback-loops-and-snowballing]] - luck acts as a negative feedback on skill advantage.
- [[combat-and-encounter-design]] - hit chances and crits are the most common output randomness.

## References
- Ian Schreiber, "Game Balance Concepts", levels on probability and randomness: https://gamebalanceconcepts.wordpress.com
- Dota 2 wiki, Random Distribution (PRD): https://dota2.fandom.com/wiki/Random_Distribution
- Elias, Garfield, Gutschera, "Characteristics of Games" (2012), on luck and skill.
- Jesse Schell, "The Art of Game Design", lenses on chance and probability.
- Sid Meier, "Interesting Decisions", GDC 2012: https://www.gamedeveloper.com/design/gdc-2012-sid-meier-on-how-to-see-games-as-sets-of-interesting-decisions
