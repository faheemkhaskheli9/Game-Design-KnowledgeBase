---
title: Combat and encounter design
category: mechanics
tags: [combat, encounters, telegraphing, enemy-roles, bosses, type-matchups, turn-based, real-time, creature-battler]
use_cases:
  - "fights feel unfair, cheap or impossible to read"
  - "every encounter plays the same, enemies are just bags of hit points"
  - "how do I design a boss fight that teaches and then tests the player?"
  - "I am building a turn-based or creature-battler combat system with type matchups"
  - "encounters come too fast or too slow and the pacing feels flat"
status: draft
last_verified: 2026-10-14
sources:
  - "https://gamebalanceconcepts.wordpress.com"
  - "https://www.gamedeveloper.com/design/gdc-2012-sid-meier-on-how-to-see-games-as-sets-of-interesting-decisions"
---

# Combat and encounter design

## Summary
Combat is a conversation between the player's toolset and the enemy's behaviour, and each encounter is a question you ask the player: can you read this, counter it, and manage risk? Good encounters make the player's options matter, make threats readable before they land, and vary the question from fight to fight. This topic covers attack readability, enemy roles and combinations, counterplay, matchup systems, turn-based versus real-time choices, bosses and encounter pacing.

## Key concepts
- **Telegraphing**: the enemy signals an attack before it lands (wind-up animation, sound, ground marker) so the player has a fair chance to react. Dark Souls enemy wind-ups, Zelda boss tells and Slay the Spire's displayed enemy intents are all telegraphs.
- **Counterplay**: every threat should have at least one answer the player can learn (dodge, block, interrupt, out-range, kill first). Threats without answers are damage checks, not challenges.
- **Enemy roles**: distinct jobs such as rusher, ranged harasser, tank, support/healer, area denial, summoner. Roles force different responses and mixing them creates puzzles.
- **Risk/reward**: strong player options come with exposure (a heavy attack has recovery, a parry demands precision). The reward must be greater than the risk when done well.
- **Matchup systems**: rock-paper-scissors structures (Pokemon types, Fire Emblem's weapon triangle) that reward knowledge and preparation, see [[game-balance]].
- **Encounter pacing**: the rhythm of tension and rest between fights, within a fight, and across a level.
- **Legibility**: the player can tell what happened and why they lost; combat that is chaotic but unreadable feels random.

## When to use / scenarios
- Playtesters say "I died and did not know why": the problem is telegraphing or feedback; see [[game-feel-and-juice]].
- Combat is "hit it until it dies": introduce roles, resistances and positional demands so that different tools matter.
- A creature battler or RPG needs a type system and a reason to carry a diverse team.
- Boss fights feel like big health bars: restructure into phases that introduce one idea at a time.
- Encounters feel repetitive: change the question (kill priority, terrain, timer, protect target), not only the stat numbers.
- Not for puzzle or narrative games where combat is incidental; use the simplest system that serves the loop, see [[core-gameplay-loop]].

## How it works / example
**Read, react, resolve.** Every attack gives three beats: tell (the player notices), window (the player can act), impact (the result). In real-time games the window length is the difficulty dial: longer for early enemies, shorter or with feints for late. In turn-based games the tell is the visible intent, as in Slay the Spire where an enemy shows the exact damage it will deal next turn so the decision is about the player's block and attack, not about guessing.

**Enemy combinations beat enemy stat inflation.** A single melee rusher is a trivial tuning problem. Pair it with a ranged enemy behind it and a healer further back and the player must prioritise, move, and use area attacks. Doom (2016) uses this with roles that push the player to switch weapons and keep moving rather than stand and shoot; XCOM mixes flankers, snipers and support so that cover and positioning decisions matter.

**Type matchups (creature battlers).** Pokemon's type chart gives double damage, half damage or none. Design rules that keep it healthy:
- Each type should have both good and bad matchups, so none is strictly best.
- Keep the multipliers large enough that team composition matters, small enough that the underdog can still win with skill or items.
- Give weak types utility (coverage moves, status effects) so they stay interesting.
- Show matchup hints in the UI so new players learn the chart from play rather than from a wiki.

A tiny expected-damage tool for checking a type chart for dominant attackers:

```python
# Rows = attacking type, columns = defending type; 2.0 strong, 0.5 weak, 1.0 neutral.
T = ["Fire", "Water", "Grass", "Normal"]
chart = {
    "Fire":   {"Fire": .5, "Water": .5, "Grass": 2, "Normal": 1},
    "Water":  {"Fire": 2, "Water": .5, "Grass": .5, "Normal": 1},
    "Grass":  {"Fire": .5, "Water": 2, "Grass": .5, "Normal": 1},
    "Normal": {"Fire": 1, "Water": 1, "Grass": 1, "Normal": 1},
}
for a in T:
    offense = sum(chart[a][d] for d in T) / len(T)          # avg multiplier dealt
    defense = sum(chart[o][a] for o in T) / len(T)          # avg multiplier taken
    print(f"{a:6s} offense {offense:.2f}  defense-taken {defense:.2f}")
# A type with offense >> 1 and taken << 1 is dominant; the chart should keep both near 1.
```

**Boss design.** Use the pattern teach, test, twist: the first phase uses attacks the player already met, the second combines them, the final phase adds one new mechanic or raises tempo. Give a recovery window after the boss's hardest attack so the player can punish; the fight loop is pressure then opening. Checkpoint close to the boss with a short run-back, so failure teaches rather than bores.

**Pacing.** Alternate intensities: skirmish, breather, set piece, rest. A common rule of thumb is to escalate each encounter by one new variable (a new role, a terrain feature, a time limit), not three. Use the fights between as the place to restore resources and let players spend them on choices, see [[level-design-and-pacing]].

## Trade-offs
- **Turn-based vs real-time**: turn-based favours planning, information and approachability; it needs strong decisions each turn to avoid tedium. Real-time favours reflex, spectacle and flow, but demands precise telegraphing and tuned input responsiveness. Hybrid (active time, pause-and-plan) is an option when you want both.
- **Readability vs challenge**: more tell makes fights fair but easier; feints, delayed attacks and combos raise difficulty without removing fairness if the base tell remains legible.
- **Variety vs mastery**: many enemy types keep fights fresh, but fewer well-designed ones let players master timing. Prefer a small cast with several behaviours each.
- **Static vs scaling difficulty**: scaled enemies keep pace with the player but dull the sense of progress; handcrafted encounters give discovery but need careful level pacing.

## Gotchas
- **Damage sponges**: raising HP instead of changing behaviour makes fights longer, not harder or deeper.
- **Off-screen or unreadable attacks**: damage the player could not see is perceived as cheating, regardless of numbers.
- **Instant-kill and one-shot mechanics** without a clear tell destroy trust, unless the game's whole identity is lethality and players see it coming.
- **Dominant tactic**: kiting, door-dancing or one overpowered spell trivialises everything; give enemies tools against it (gap-closers, ranged units).
- **Stun-lock and chain crowd control** remove agency; add diminishing returns or recovery invulnerability.
- **Type chart bloat**: more types multiplies pairings, and balance cost rises faster than player benefit.
- **Boss as an exam of the last tutorial**: if a boss tests a skill that was never practised, the fight is a spike rather than a peak, see [[onboarding-and-tutorials]].

## Related
- [[game-balance]] - matchups, cost curves and counters underlie combat tuning.
- [[randomness-and-luck]] - hit chances, crits and procs shape how much luck enters combat.
- [[meaningful-choices]] - targeting, positioning and ability use should be real decisions.
- [[level-design-and-pacing]] - encounters live inside a level's rhythm of tension and rest.
- [[game-feel-and-juice]] - hit feedback, animation timing and sound make attacks readable and satisfying.
- [[flow-and-difficulty-curves]] - encounter difficulty should track player skill growth.

## References
- Ian Schreiber, "Game Balance Concepts", levels on intransitive relationships and combat math: https://gamebalanceconcepts.wordpress.com
- Steve Swink, "Game Feel" (2008), on responsiveness and the feel of real-time combat.
- Jesse Schell, "The Art of Game Design", chapters on balance and challenge.
- Sid Meier, "Interesting Decisions", GDC 2012: https://www.gamedeveloper.com/design/gdc-2012-sid-meier-on-how-to-see-games-as-sets-of-interesting-decisions
- Ernest Adams and Joris Dormans, "Game Mechanics: Advanced Game Design" (2012).
