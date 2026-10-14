---
title: Core gameplay loop
category: fundamentals
tags: [core-loop, verbs, nested-loops, session, Halo, Stardew-Valley, Hades, Vampire-Survivors]
use_cases:
  - "I have a game idea and need to define what the player actually does repeatedly"
  - "Players enjoy the first hour then quit; the game feels repetitive"
  - "Our feature list is long but the game has no clear center"
  - "How do I structure short, medium and long-term goals?"
status: draft
last_verified: 2026-10-14
sources:
  - https://www.routledge.com/Game-Feel-A-Game-Designers-Guide-to-Virtual-Sensation/Swink/p/book/9780123743282
  - https://www.cambridge.org/core/books/game-mechanics/
  - https://www.gdcvault.com/
  - https://www.gamedeveloper.com/
---

# Core gameplay loop

## Summary
The core loop is the repeating cycle of actions a player performs, the
feedback they get, and the reason to go around again. Good games nest several
loops: seconds, minutes (a session) and weeks (the long game). If the
innermost loop is not satisfying by itself, no amount of meta-progression or
content will fix it. Define the loop first and cut features that do not feed it.

## Key concepts
- **Verbs**: the actions the player takes (jump, shoot, plant, haggle). A game
  is defined by a handful of verbs; more verbs does not mean more depth.
- **Loop anatomy**: intent -> action -> feedback -> reward/consequence -> new
  intent. Each pass should change the game state so the next pass differs.
- **Nested loops**: moment-to-moment (seconds), session (minutes: a run, a
  mission, a day), and long-term (hours to weeks: build, collection, story).
  Each outer loop gives meaning to the inner one.
- **30 seconds of fun**: the Halo team's idea that if the basic 30 seconds of
  play (fight, move, use a weapon) is enjoyable, the game can repeat it in
  varied contexts indefinitely.
- **Variation source**: what keeps repetition fresh: encounters, terrain,
  procedural elements, opponents, or player-chosen builds.

## When to use / scenarios
- Concept stage: write the loop on one page before any content plan.
- Retention problems: check whether the session loop has a natural end and a
  hook to the next one; see [[retention-and-session-design]].
- "Feature creep": test each feature by which loop it feeds and which verb it
  adds or changes.
- Not sufficient for narrative-first games; there the loop may be thin and the
  pacing of story carries more weight ([[narrative-and-player-agency]]).

## How it works / example
**Stardew Valley.** Seconds: swing tool, harvest, get an item with a clear
sound and animation. Session (one in-game day, about 10-15 real minutes): water
crops, mine, talk to villagers, sleep; the day ends with a tally and a reason
to start tomorrow. Long term: expand the farm, complete bundles, build
relationships across seasons. Every inner loop yields progress for the outer one.

**Hades.** Seconds: dash, attack, dodge in combat rooms. Session: a run through
chambers choosing boons, ending in death or victory. Long term: spend resources
in the House of Hades, unlock weapons, advance relationships and story. Death is
not a reset but the bridge to the outer loop, which is the key design move.

**Vampire Survivors.** Seconds: move only; weapons fire automatically. Session:
a 30-minute run where kills yield XP and level-ups present choice cards. Long
term: gold unlocks characters and passives. A single verb (position) plus a
choice mechanic is enough because the session loop escalates fast.

**Diagram a loop** as text, then test it:

```
[Goal/Intent] -> [Action (verb)] -> [Feedback] -> [Reward/State change]
       ^                                                   |
       +-------------- new, different goal <---------------+
```

Test it with a small script: simulate the loop with stub numbers and see if the
reward cadence is sane.

```python
import random
random.seed(1)

def session(minutes=15, action_seconds=20, drop_chance=0.3):
    t, rewards = 0, 0
    while t < minutes * 60:
        t += action_seconds
        if random.random() < drop_chance:
            rewards += 1
    return rewards

runs = [session() for _ in range(1000)]
print("avg rewards/session:", sum(runs) / len(runs))
print("sessions with zero rewards:", sum(r == 0 for r in runs))
```

If a player can plausibly have a session with zero meaningful state change,
the loop needs a floor (guaranteed progress, a consolation reward).

**Playtest check**: ask a tester to play five minutes with all meta-systems
disabled. If it is not enjoyable, the problem is the inner loop.

## Trade-offs
- **Tight vs. broad loops**: a tight loop (Tetris) is easy to master and
  polish; a broad one (a 4X) offers depth but a higher learning cost and more
  places to fail.
- **Variation by content vs. by systems**: handmade variation is expensive and
  finite; systemic variation (roguelike builds) scales but needs balance work.
- **Outer-loop strength**: strong meta-progression retains players but can
  hollow out the inner loop if players tolerate boring play for rewards.
- **Session length**: short sessions suit mobile and commuters; long ones need
  mid-session save points and pacing breaks.

## Gotchas
- Building the meta-game (levels, crafting, shops) before proving the core
  loop is fun on its own.
- A loop with no state change between iterations: the second pass feels
  identical to the first.
- Too many currencies and menus inside the loop interrupting the verb.
- Loops that end only by quitting: no clear "good stopping point" can make
  players feel drained rather than satisfied.
- Confusing a loop with a grind: repeated action needs new decisions or
  escalating mastery, not only a bigger number.
- Skipping the long-term loop in a live-service game: players run out of goals.

## Related
- [[what-makes-a-game-fun]] - the aesthetic the loop is meant to deliver.
- [[progression-systems]] - how outer loops reward the inner ones.
- [[retention-and-session-design]] - designing sessions and return hooks.
- [[reward-schedules-and-loot]] - tuning the feedback and reward step.
- [[prototyping-and-finding-the-fun]] - proving the inner loop before building more.

## References
- Steve Swink, *Game Feel* (moment-to-moment interaction and response).
- Ernest Adams and Joris Dormans, *Game Mechanics: Advanced Game Design*
  (internal economy and loop diagrams): https://www.cambridge.org/core/books/game-mechanics/
- Jaime Griesemer, "Design in Detail: Changing the Time Between Shots for the
  Sniper Rifle from 0.5 to 0.7 Seconds for Halo 3" and related Halo design
  talks (search https://www.gdcvault.com/) discussing the 30 seconds of fun.
- Game Developer articles on core loops: https://www.gamedeveloper.com/
