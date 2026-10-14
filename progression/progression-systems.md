---
title: Progression systems
category: progression
tags: [progression, xp, levels, unlocks, meta-progression, roguelite, prestige, power-creep]
use_cases:
  - "players feel no sense of growth after the first hours"
  - "design an XP and level curve for an RPG or action game"
  - "add meta-progression so failed roguelite runs still matter"
  - "pace unlocks so the game keeps introducing new things"
  - "our endgame is a treadmill and numbers keep inflating"
status: draft
last_verified: 2026-10-14
sources:
  - https://gamebalanceconcepts.wordpress.com/
  - https://www.artofgamedesign.com/
  - https://en.wikipedia.org/wiki/Hades_(video_game)
  - https://en.wikipedia.org/wiki/Rogue_Legacy
  - https://www.gamesbrief.com/
---

# Progression systems

## Summary
A progression system is the structure through which a player gets better, gets more options, or sees more of the game over time. It answers "why keep playing?" with visible growth. Good progression pairs short-term gains (a new skill every session) with long-term goals (a build, a rank, an ending), and it feeds the core loop rather than replacing it.

## Key concepts
- **Vertical progression**: the player gets more powerful (levels, stats, gear). Easy to feel, but it forces the game to scale enemies and eventually hits a numeric ceiling. Diablo and most JRPGs lean here.
- **Horizontal progression**: the player gets more options at similar power (new weapons, cards, characters, playstyles). Preserves old content and skill relevance. Card games and many MOBAs lean here.
- **Character vs skill progression**: character progression lives in the save file; skill progression lives in the player's head. Celeste has no character power growth at all, yet players feel steady progress through mastery. Mixing both is the usual answer.
- **Meta-progression**: permanent upgrades earned across runs of a roguelite. Rogue Legacy lets you spend gold on the castle after every death; Hades keeps Mirror of Night upgrades, Keepsakes and story beats between escapes.
- **Prestige / reset loops**: the player voluntarily resets progress for a permanent multiplier (idle games, some ARPGs' seasonal ladders). It restarts the fast early game on top of a slow late game.
- **Power creep**: each release must beat the last, so old content becomes obsolete and balance drifts. It is the vertical-progression disease.
- **Unlock pacing**: the schedule on which new mechanics, tools and content appear. Often more important than the XP curve itself.

## When to use / scenarios
- Playtesters say "I am not sure what I am working toward" - add a visible ladder with a next step always within about one session.
- Players mastered the loop in an hour and quit - drip-feed new verbs, enemies or tools (unlock pacing) instead of bigger numbers.
- A roguelite has high failure rates and frustration - add meta-progression, but keep it modest enough that skill still decides runs.
- Do NOT add levels to a game whose appeal is pure skill and fairness (competitive shooters, fighting games); use cosmetics and ranked ladders instead.

## How it works / example
XP curves: `xp_to_next(level)` is the real design lever. Linear curves (constant cost) make every level feel identical and run out of novelty; polynomial curves (cost grows with level^k) are the common compromise; exponential curves slow progress sharply and usually need a cap or a prestige. A heuristic from Schreiber's balance writing: tie time-per-level to what the player gains per level, so early levels take minutes and later ones take hours only if each one still unlocks something meaningful.

```python
# Compare time-to-level under three XP curves, assuming a constant XP/hour income.
def linear(level, base=100):
    return base

def polynomial(level, base=100, power=1.8):
    return base * level ** power

def exponential(level, base=100, growth=1.12):
    return base * growth ** level

def hours_to_reach(target, curve, xp_per_hour=1000):
    total = sum(curve(lv) for lv in range(1, target))
    return total / xp_per_hour

for name, curve in [("linear", linear), ("polynomial", polynomial), ("exponential", exponential)]:
    row = ", ".join(f"L{t}: {hours_to_reach(t, curve):7.1f}h" for t in (5, 10, 20, 40, 60))
    print(f"{name:12s} {row}")
```

Run it and read the shape: linear reaches level 60 in about 6 hours, while polynomial (power 1.8) needs thousands of hours and exponential (1.12) several hundred, so tune `power`/`growth` to your target hours-to-cap. A practical target is a soft polynomial early, then rely on new unlocks (not just bigger numbers) past the midpoint. Hades shows the meta layer done well: each death is rewarded with currency and story, and the early upgrades are small, so a skilled player can still win with nothing.

## Trade-offs
- **Vertical vs horizontal**: vertical gives instant, legible reward; horizontal ages better and keeps skill relevant. Mix them: power for the first stretch, options for the long tail.
- **Meta-progression strength**: strong upgrades reduce frustration but trivialize early content and make wins feel bought. Weak ones feel pointless. Use many small steps, and gate big jumps behind new options rather than raw stats.
- **Prestige**: resets re-create the early-game dopamine but punish players who dislike repetition. Make the reset optional and show the permanent multiplier before they commit.
- **Level scaling of enemies**: scaling everything (Oblivion-style) keeps challenge flat and removes the feeling of growth; fixed-level zones make growth visible but allow trivializing or being walled.

## Gotchas
- A single number that only goes up becomes meaningless; pair every power gain with a new decision or a visible change in play.
- Grind walls: if the next level needs ten times the last with no new content, players read it as a time tax and, in monetized games, as a nudge to pay. Keep an honest answer to "what is different at level N+1?".
- Power creep in live games: new content that outclasses the old forces constant chase. Prefer sidegrades, caps, or seasonal resets and keep the old content relevant.
- Hiding the curve: players should see the next unlock and roughly how far it is; opaque systems feel arbitrary.
- Do not gate the core fun behind progression. If level 1 is boring, a level 30 payoff will not be seen.

## Related
- [[core-gameplay-loop]] - progression is the outer loop that gives the inner loop a purpose.
- [[game-economy-sources-and-sinks]] - XP and currency flows need the same faucet/sink thinking.
- [[reward-schedules-and-loot]] - the reward cadence layered over the progression ladder.
- [[retention-and-session-design]] - how progression pacing translates into session and return behavior.
- [[game-balance]] - curves and scaling live or die by balance testing.

## References
- Ian Schreiber, "Game Balance Concepts" (progression and XP curve sessions): https://gamebalanceconcepts.wordpress.com/
- Jesse Schell, "The Art of Game Design" (interest curves and rewards): https://www.artofgamedesign.com/
- Adams and Dormans, "Game Mechanics: Advanced Game Design" (progression mechanisms and escalation).
- Supergiant Games, Hades overview: https://en.wikipedia.org/wiki/Hades_(video_game)
- Cellar Door Games, Rogue Legacy overview: https://en.wikipedia.org/wiki/Rogue_Legacy
- Nicholas Lovell, "The Curve" and the GamesBrief blog on long-term engagement: https://www.gamesbrief.com/
