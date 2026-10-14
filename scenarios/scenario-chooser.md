---
title: Scenario chooser - what to read for this design problem
category: scenarios
tags: [chooser, router, symptoms, diagnosis, design-problems]
use_cases:
  - "my game is boring and I do not know why"
  - "players quit early or do not come back"
  - "map a playtest complaint to the design topic that fixes it"
  - "starting a new game and want to know what to design first"
status: stable
last_verified: 2026-10-14
sources:
  - https://schellgames.com/art-of-game-design
  - https://users.cs.northwestern.edu/~hunicke/MDA.pdf
  - https://www.theoryoffun.com/
---

# Scenario chooser - what to read for this design problem

## Summary
A router from symptoms (playtest complaints, metrics, design goals) to the topic files that address them. Find the row closest to the problem, read the linked topics in order, and apply them to the game's genre and audience. Playtest feedback usually names a symptom, not a cause; this table maps the common symptoms to their usual causes.

## Key concepts
- Diagnose before prescribing. "Combat is boring" can mean no meaningful choices, no feedback, wrong difficulty or no reason to fight. Check what players actually do in [[playtesting-and-metrics]] before changing anything.
- Fix the innermost loop first. If the moment-to-moment action is not satisfying, no progression system or reward will save it ([[core-gameplay-loop]], [[game-feel-and-juice]]).
- One change per playtest round where possible, so you can tell what worked.
- Rows list 2-4 topics: the first is the main answer, the rest are what you will need next.

## When to use / scenarios

| Symptom or goal | Read, in order |
|---|---|
| Starting a new game from an idea | [[what-makes-a-game-fun]], [[core-gameplay-loop]], [[prototyping-and-finding-the-fun]] |
| "It's boring" / players feel nothing | [[core-gameplay-loop]], [[meaningful-choices]], [[game-feel-and-juice]], [[what-makes-a-game-fun]] |
| Controls feel floaty, hits feel weak | [[game-feel-and-juice]], [[combat-and-encounter-design]] |
| Too hard / too easy / players stuck at one spot | [[flow-and-difficulty-curves]], [[level-design-and-pacing]], [[playtesting-and-metrics]] |
| Players quit in the first minutes | [[onboarding-and-tutorials]], [[core-gameplay-loop]], [[playtesting-and-metrics]] |
| Players do not come back the next day | [[retention-and-session-design]], [[progression-systems]], [[player-motivation-and-player-types]] |
| "Too grindy" | [[progression-systems]], [[reward-schedules-and-loot]], [[game-economy-sources-and-sinks]] |
| Everyone uses the same build/unit/monster | [[game-balance]], [[meaningful-choices]], [[combat-and-encounter-design]] |
| The leader always wins, games are decided early | [[feedback-loops-and-snowballing]], [[game-balance]] |
| "It's unfair" / RNG complaints | [[randomness-and-luck]], [[feedback-loops-and-snowballing]] |
| Loot or rewards feel worthless | [[reward-schedules-and-loot]], [[game-economy-sources-and-sinks]], [[progression-systems]] |
| Currency inflation, everything is cheap or unaffordable | [[game-economy-sources-and-sinks]] |
| Fights are repetitive | [[combat-and-encounter-design]], [[level-design-and-pacing]], [[meaningful-choices]] |
| Players get lost or skip content | [[level-design-and-pacing]], [[onboarding-and-tutorials]] |
| Story does not land, players skip it | [[narrative-and-player-agency]], [[level-design-and-pacing]] |
| Adding PvP, co-op or social features | [[multiplayer-and-social-play]], [[game-balance]], [[player-motivation-and-player-types]] |
| Monetization or live-ops without dark patterns | [[retention-and-session-design]], [[reward-schedules-and-loot]], [[game-economy-sources-and-sinks]] |
| Gamifying a non-game app (learning, fitness, finance) | [[player-motivation-and-player-types]], [[progression-systems]], [[reward-schedules-and-loot]] |
| Reviewing a design doc or feature before building | [[design-review-checklist]] |

## How it works / example
A creature-battler playtest reports "battles get boring after an hour". Diagnosis path: [[core-gameplay-loop]] asks whether a single turn involves a decision; the playtest shows players spam their strongest move. That is a [[meaningful-choices]] problem (one dominant option) and a [[game-balance]] problem (move cost curve). Fixes: give moves real costs or cooldowns, add type matchups that change the best move per enemy ([[combat-and-encounter-design]]), then re-run the playtest and watch whether move usage spreads out.

A learning app with streaks reports high day-1 usage but a cliff after a missed day. Path: [[retention-and-session-design]] (streak loss is a punishing loss-aversion mechanic; add streak freezes or soft streaks), then [[player-motivation-and-player-types]] (shift from extrinsic streak pressure to intrinsic competence feedback).

## Trade-offs
- Quick fix vs root cause: adding rewards to a boring loop raises short-term engagement but hides the real problem and can trigger the overjustification effect. Prefer fixing the loop.
- Data vs feel: metrics show where players leave, not why. Pair telemetry with observed playtests.
- Genre conventions vs novelty: conventions lower onboarding cost; novelty is the reason to play. Break one convention at a time.

## Gotchas
- Players are good at reporting problems and bad at proposing fixes. Treat their suggestions as evidence of the symptom, not as the design.
- Several rows can share one cause. A weak core loop shows up as boredom, poor retention and "grindy" complaints all at once.
- Designing for yourself: the designer has mastered the game and cannot feel its difficulty or confusion. Always test with fresh players.

## Related
- [[design-review-checklist]] - question list for reviewing a design before building it.
- [[what-makes-a-game-fun]] - the lens most rows start from.
- [[playtesting-and-metrics]] - how to find out which symptom you actually have.

## References
- Jesse Schell, The Art of Game Design: A Book of Lenses - lens-based diagnosis.
- Hunicke, LeBlanc, Zubek, "MDA: A Formal Approach to Game Design and Game Research" (2004).
- Raph Koster, A Theory of Fun for Game Design.
