---
title: Level design and pacing
category: experience
tags: [level-design, pacing, kishotenketsu, intensity-curve, landmarks, gating, metroidvania, open-world, guidance]
use_cases:
  - "my levels feel like a flat sequence of the same challenge"
  - "players get lost and do not know where to go"
  - "how do I structure a level around one mechanic"
  - "the game is exhausting with no moments to breathe"
  - "my open world feels empty or overstuffed"
  - "how should gating and backtracking work in a metroidvania"
status: draft
last_verified: 2026-10-14
sources:
  - https://www.youtube.com/watch?v=dBmIkEvEBtA
  - https://www.youtube.com/@GMTK
  - https://www.routledge.com/An-Architectural-Approach-to-Level-Design/Totten/p/book/9781138595295
  - https://steamcdn-a.akamaihd.net/apps/valve/2009/ai_systems_of_l4d_mike_booth.pdf
---

# Level design and pacing

## Summary
Level design arranges space, challenges and information so the player is taught, tested, surprised and given rest in a deliberate rhythm. Pacing is the shape of intensity over time; good levels rise and fall rather than staying at one level. Use it when levels feel samey, players get lost, or sessions feel either monotonous or exhausting.

## Key concepts
- **Kishotenketsu** (four-act structure used by Nintendo designers, explained by Mark Brown in Game Maker's Toolkit): Ki, introduce a mechanic safely; Sho, develop it with harder variations; Ten, twist it with an unexpected combination or context; Ketsu, conclude with a payoff that resolves the idea. Notably it needs no enemy-driven conflict; the "twist" is a new understanding, not a new threat. Super Mario 3D World levels follow it closely.
- **Intensity curve**: plot challenge or emotional pressure over time. A saw-tooth with a gradually rising baseline works: tension, release, a little more tension. Valve's Left 4 Dead director deliberately alternates build-up, peak and relax periods (Michael Booth's talk).
- **Rest beats**: calm spaces after peaks for recovery, exploration, story and resource management. They make the next peak land.
- **Guiding the player** (Christopher Totten and others): use landmarks (a unique silhouette visible from afar), light (players move toward brighter areas), leading lines (architecture that points the way), colour coding (Mirror's Edge red), movement (animals or NPCs heading off), and breadcrumbs (pickups placed along the path). Prefer environmental cues to arrows.
- **Gating**: hard gates (locked door needing an item) and soft gates (a path guarded by enemies tougher than you) pace progress and control the order of teaching.
- **Metroidvania loop**: see a gate, leave, gain an ability, return. The map is a memory puzzle, and backtracking is the reward for earlier curiosity.
- **Density in open worlds**: points of interest at spacing the player can reach in a comfortable time, so the horizon always offers a next target.

## When to use / scenarios
- Playtest heatmaps show players circling or retracing: guidance problem, add landmarks or lighting.
- Every room is "enemies then door": introduce variety through a beat sheet (see below).
- Players report fatigue after 30 minutes: add rest beats and vary the verb being exercised.
- Designing a new mechanic: build its kishotenketsu sequence in 4 to 6 rooms before using it elsewhere.
- NOT for systemic sandbox games where players author their own pace; there, tune the generator or director instead (see [[feedback-loops-and-snowballing]]).

## How it works / example
A beat sheet for one level built on a "jump on a moving platform" mechanic:

```
beat  act   description                              intensity
1     Ki    one slow platform over a shallow pit      1
2     Sho   two platforms, timing matters             3
3     rest  safe ledge, collectible visible beyond    1
4     Sho   moving platform plus one enemy            4
5     Ten   platforms vanish when you land (new rule) 6
6     Ketsu use the new rule to reach a secret room   5
7     rest  checkpoint, vista of next area            1
```

Check each beat for: what is the single new idea, what happens if the player fails, and how far is the next rest.

Guidance example: Half-Life 2 and Dishonored use light and architecture to pull players forward; The Legend of Zelda: Breath of the Wild lets you see a distant tower or smoke column and choose to walk to it, which creates a self-guided breadcrumb trail.

Metroidvania example: Hollow Knight and Super Metroid show unreachable ledges early; remembering them is the player's own to-do list, and the ability that unlocks them gives an immediate satisfying return trip. Add shortcuts (one-way doors that open back toward the hub) so backtracking gets faster over time.

Open-world density: a common heuristic is to ensure the player always sees something interesting when looking around from any location, and that the travel time between points of interest is short enough to keep momentum. Ubisoft-style map icon counts are a cautionary tale: density without variety turns the world into a checklist.

## Trade-offs
- **Linear vs open**: linear levels allow tight pacing, authored set pieces and reliable teaching; open spaces give agency but weaker rhythm control. Hybrids (hub plus linear spokes, or a wide path with guarded gates) mix both.
- **Hand-holding vs discovery**: strong guidance reduces frustration; light guidance heightens exploration. Offer opt-in hints rather than choosing for everyone.
- **Gating strictness**: hard gates guarantee order but feel arbitrary; soft gates feel natural but players may bypass content. Sequence-break friendliness is a deliberate decision, celebrated in Metroid and Zelda speedrun culture.
- **Handcrafted vs procedural**: handcrafted levels pace better; procedural ones need rules for rest rooms and intensity budgets.
- **Backtracking**: rewarding for explorers, tedious for others; mitigate with fast travel and shortcuts.

## Gotchas
- Difficulty spikes confused with pacing: a spike without a preceding rest and teaching beat is just unfair.
- Rest beats that are empty. Give them something to do (a view, a story beat, a shop) or they feel like dead time.
- Landmarks that look like everything else: a unique silhouette beats a bright colour when many things are bright.
- Placing the critical path indicator where the camera does not face; test with players who look around instead of straight ahead.
- Backtracking that repeats the same enemies at the same toughness. Change the context or let the new ability trivialize old threats to feel powerful.
- Open world filled evenly: uniform density removes the sense of place and the value of quiet areas.
- Ignoring sightlines: players decide where to go from what they can see in the first second of entering a space.
- Teaching a mechanic and never using it again, or using it in the next level at full complexity; return to it in a later twist.

## Related
- [[onboarding-and-tutorials]] - the same teach/test/twist structure drives tutorial level design.
- [[flow-and-difficulty-curves]] - intensity curves are the level-scale version of the difficulty curve.
- [[combat-and-encounter-design]] - encounters are the beats inside the level's rhythm.
- [[progression-systems]] - gates tie spatial progress to abilities and power.
- [[narrative-and-player-agency]] - environmental storytelling lives in the same spaces.

## References
- Mark Brown (Game Maker's Toolkit), "Super Mario 3D World's 4 Step Level Design": https://www.youtube.com/watch?v=dBmIkEvEBtA
- Christopher Totten (ed.), "An Architectural Approach to Level Design" (2nd ed.), CRC Press.
- Michael Booth (Valve), "The AI Systems of Left 4 Dead": https://steamcdn-a.akamaihd.net/apps/valve/2009/ai_systems_of_l4d_mike_booth.pdf
- Game Maker's Toolkit channel, level design series: https://www.youtube.com/@GMTK
