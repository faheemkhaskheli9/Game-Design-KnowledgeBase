---
title: Feedback loops and snowballing
category: mechanics
tags: [feedback-loop, snowball, rubber-banding, catch-up, comeback, machinations, mario-kart, strategy]
use_cases:
  - "the player who gets ahead early always wins and the rest of the match is pointless"
  - "matches drag on because nobody can close out a lead"
  - "how do I give trailing players a chance without making leading feel pointless?"
  - "my racing or party game feels unfair because of rubber-banding"
  - "I need a system that makes a game end in a satisfying finish"
status: draft
last_verified: 2026-10-14
sources:
  - "https://gamebalanceconcepts.wordpress.com"
  - "https://machinations.io"
---

# Feedback loops and snowballing

## Summary
A feedback loop is a rule where the output of the system feeds back into its input. Positive loops amplify (the leader gets stronger, so the leader gets further ahead); negative loops dampen (the leader is slowed or the trailer helped). Choosing how much of each your game has decides whether matches are decisive, close, comeback-friendly or dull, and it is among the cheapest levers to shape the arc of a session.

## Key concepts
- **Positive feedback**: success produces resources or power that make further success easier. Monopoly money, XP-gated gear, snowballing kills in a MOBA. Result: divergence, runaway leader, fast endings.
- **Negative feedback**: success makes further success harder or failure easier to recover from. Mario Kart item odds, Catan's robber targeting leaders, rising costs of expansion. Result: convergence, close games, risk of stalling.
- **Snowballing**: the player experience of positive feedback. Early advantage compounds.
- **Death spiral**: the same loop seen from the loser's side. The player is still "playing" long after the game is decided.
- **Catch-up mechanics**: explicit negative feedback that helps the trailing player (more XP for lower-level characters, better items for the last place player).
- **Rubber-banding**: AI or systems that adjust to keep players close, typical in racing games. Can be invisible or very visible.
- **Machinations-style diagrams**: sources, pools, converters and gates connected by arrows, used by Adams and Dormans to model loops and simulate them before building.

## When to use / scenarios
- A game is decided by minute 10 of a 40 minute match: add negative feedback or soften compounding.
- Matches never end because comebacks are always possible: add positive feedback near the end (escalating costs of defence, a shrinking play area, a timer).
- Party games where players of mixed skill should all feel in contention: use negative feedback and bounded luck.
- Competitive games where skill must be rewarded: keep loops weak or capped, so that skill difference is not masked by catch-up.
- Not the tool for a single-player difficulty problem; see [[flow-and-difficulty-curves]] for dynamic difficulty.

## How it works / example
Real games:
- **Mario Kart**: item boxes give stronger items (blue shell, bullet) to players further back. This is negative feedback by design, so a leader's skill advantage is partially cancelled. It makes the game fit mixed-skill groups and also produces a lot of "that was unfair" moments for the leader.
- **Monopoly**: rent income funds more property, which yields more rent. Strongly positive, so the game is largely decided long before it ends, which is why it is often criticised for lasting too long after the result is obvious.
- **Catan**: resources from settlements fund more settlements (positive), but the robber and trading (players refuse to trade with the leader) provide soft negative feedback.
- **StarCraft / MOBAs**: a kill gives gold, gold gives items, items give kills. Many MOBAs add bounties for killing a leading player and extra XP for lower-level heroes to temper it.
- **Chess**: material advantage is a positive loop, and it is intended: it brings the game to an end.

A tiny simulation to see how the strength of a loop changes how often the early leader wins (two players with equal skill, random luck on each round):

```python
import random

def play(rounds=30, snowball=0.1, catchup=0.0, seed=None):
    rng = random.Random(seed)
    a = b = 10.0
    lead_after_5 = None
    for r in range(rounds):
        # chance to win a round starts at 50%, shifted by lead
        diff = (a - b) / (a + b)
        p_a = 0.5 + diff * (snowball - catchup)
        p_a = min(0.95, max(0.05, p_a))
        if rng.random() < p_a:
            a += 1 + snowball * a * 0.1
        else:
            b += 1 + snowball * b * 0.1
        if r == 4:
            lead_after_5 = "a" if a > b else "b"
    final = "a" if a > b else "b"
    return lead_after_5 == final

for snow, catch in [(0.0, 0.0), (1.0, 0.0), (1.0, 1.0), (1.0, 1.5)]:
    n = 5000
    wins = sum(play(snowball=snow, catchup=catch, seed=i) for i in range(n))
    print(f"snowball={snow} catchup={catch}: early leader wins {wins/n:.0%}")
```

Read the output as a rough comparison, not a calibrated model. With no loops the early leader still wins more than half the time (early rounds count toward the final score); with a strong positive loop the share rises further; adding catch-up pulls it back toward a coin flip. The same method works in a spreadsheet or a Machinations diagram: draw the loop, give each pool a rate, run it hundreds of times, read the distribution of outcomes.

Design recipe:
1. Draw your resource flow. Mark every arrow where "more X gives more X".
2. Decide the intended match arc (tense throughout, or a decisive middle, then a finish).
3. Add positive loops to end the game and negative loops to keep it contested early; the ratio sets the feel.
4. Cap both: a ceiling on snowball (diminishing returns, upkeep costs) and a floor on catch-up (the trailer must still need to play well).

## Trade-offs
- **Fairness to skill vs fairness to fun**: catch-up protects weaker players' engagement but reduces the reward for playing well. Esports titles generally keep it minimal; party games lean on it.
- **Visible vs hidden catch-up**: visible mechanics (a shell warning) feel fair and teachable; hidden rubber-banding (AI cars that cheat) feels manipulative once discovered.
- **Early vs late**: negative loops early and positive late gives a tight start and a clean finish, but removes dramatic early-lead payoffs.
- **Cooperative games** often invert the situation: the game itself is the negative-feedback engine against the players.

## Gotchas
- **Leader punishment feels like sandbagging**: if getting ahead is penalised too heavily, players hold back on purpose. Soften the penalty or make the trailing help conditional.
- **Stalemates**: pure negative feedback with no ending condition makes the game circle forever. Always add a positive loop or a timer.
- **Hidden loops from content**: the loop is not only in the formulas; a strong item reachable only by winning fights also snowballs. Walk through the whole economy, see [[game-economy-sources-and-sinks]].
- **Rubber-banding in single-player racers** can drain the satisfaction of a perfect lap if the AI always catches up. Keep it modest and let the player feel earned leads.
- **Multiple loops cancelling or compounding unintentionally**: simulate before shipping, because the combined effect is rarely the sum of what you intended.

## Related
- [[game-balance]] - loops are a primary tool when a lead or strategy snowballs out of control.
- [[randomness-and-luck]] - luck is itself a negative feedback on skill; the two are traded against each other.
- [[game-economy-sources-and-sinks]] - economy loops are feedback loops in resource form.
- [[progression-systems]] - XP and power curves create positive loops in the long term.
- [[multiplayer-and-social-play]] - mixed-skill groups are the main reason to add catch-up.

## References
- Ernest Adams and Joris Dormans, "Game Mechanics: Advanced Game Design" (2012), chapters on feedback and Machinations.
- Machinations (diagramming tool and framework): https://machinations.io
- Ian Schreiber, "Game Balance Concepts", levels on positive and negative feedback: https://gamebalanceconcepts.wordpress.com
- Jesse Schell, "The Art of Game Design", lens of balance and chapter on game balance.
- Salen and Zimmerman, "Rules of Play", chapter on systems and feedback.
