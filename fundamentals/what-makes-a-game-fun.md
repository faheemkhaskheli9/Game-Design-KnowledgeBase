---
title: What makes a game fun
category: fundamentals
tags: [fun, MDA, aesthetics, dynamics, mastery, learning, Lazzaro, theory]
use_cases:
  - "I need a vocabulary to say what kind of fun my game is supposed to deliver"
  - "Players say the game is fine but get bored after a few hours"
  - "We keep adding features and the game does not feel any better"
  - "Design discussions turn into taste arguments with no shared frame"
status: draft
last_verified: 2026-10-14
sources:
  - http://users.cs.northwestern.edu/~hunicke/MDA.pdf
  - https://www.theoryoffun.com/
  - https://www.routledge.com/Game-Feel-A-Game-Designers-Guide-to-Virtual-Sensation/Swink/p/book/9780123743282
  - https://www.gdcvault.com/
---

# What makes a game fun

## Summary
"Fun" is not one thing. The most useful working definitions treat fun as the
pleasure of a player doing something their brain finds rewarding: learning a
pattern, expressing themselves, beating a challenge, or being with others. A
designer who can name which kind of fun they are building can choose mechanics
on purpose, and can diagnose why a game stopped being fun. Use this file as the
base lens before reaching for any specific system.

## Key concepts
- **MDA framework** (Hunicke, LeBlanc, Zubek). Designers build **Mechanics**
  (rules, data, algorithms); running them produces **Dynamics** (runtime
  behaviour: player strategies, emergent patterns); dynamics evoke
  **Aesthetics** (the emotional response). Designers work mechanics-up; players
  experience aesthetics-down. You never set the feeling directly.
- **Eight kinds of fun** named in the MDA paper: sensation, fantasy, narrative,
  challenge, fellowship, discovery, expression, submission (pastime). Most good
  games lead with two or three, not all eight.
- **Koster's theory**: fun is the feedback the brain gives when it learns and
  masters a pattern. Once a pattern is fully mastered the game turns into a
  chore ("boring"); if patterns are too hard to learn it feels like noise.
- **Lazzaro's four keys to fun**: hard fun (goals and obstacles), easy fun
  (curiosity, exploration, immersion without pressure), people fun
  (social interaction), serious fun (purpose, rewarding change in the real
  world). Players switch keys within one session.
- **Aesthetic target**: a one-line statement such as "tense, scrappy survival"
  that every mechanic must serve.

## When to use / scenarios
- Start of a project: write the aesthetic target before the feature list.
- A feature request arrives and you cannot tell if it helps: ask which
  aesthetic it serves and which dynamic it produces.
- Playtesters say "it gets repetitive": usually a mastered-pattern problem
  (see Koster), not a content-quantity problem.
- Two designers disagree: check whether they are aiming at different kinds of
  fun (challenge vs. expression) before arguing about mechanics.
- Not the right tool for tuning numbers; use [[game-balance]] and
  [[flow-and-difficulty-curves]] for that.

## How it works / example
**Tracing a game through MDA.** Take *Dark Souls*: mechanics include stamina
costs, slow attack commitments, bonfire respawns and corpse-run penalties.
Dynamics that emerge: cautious spacing, baiting enemy attacks, memorising
routes, tense decisions about banking souls. Aesthetics: challenge, discovery,
and a strong sense of earned mastery. Change one mechanic (say, free infinite
stamina) and the dynamics collapse into button mashing, and the aesthetic
changes with them.

**Tracing a pattern-mastery curve.** *Tetris*: the learning phase is spatial
fit and rotation; mastery arrives as stacking strategies; speed ramps keep
introducing new patterns (fast play needs different habits). *Chess* stays fun
for decades because opponents keep creating new patterns. Single-player games
without this face "solved" states: once the optimal build or route is known,
play becomes execution only.

**A design-lens checklist** you can run on any feature:
1. Which aesthetic does it serve (name it from the eight)?
2. What dynamic will players actually do with it? Playtest, do not assume.
3. Is there a pattern to learn, and does depth continue after the first win?
4. Which of Lazzaro's keys is active; is the session balanced between hard and
   easy fun? Games that are only hard fun exhaust players; *Stardew Valley*
   alternates easy fun with small hard-fun goals.

A rough sketch of "fun as learning rate": fun is high while the player's
skill estimate is still changing.

```python
import math

def learning_fun(trials: int, rate: float = 0.15) -> float:
    """Fun proportional to how fast mastery is still improving."""
    mastery = lambda n: 1 - math.exp(-rate * n)
    return mastery(trials + 1) - mastery(trials)

for n in (0, 5, 10, 20, 40):
    print(n, round(learning_fun(n), 4))   # decays toward 0 = "boring"
```

The point: refreshing the pattern space (new enemies, modifiers, opponents)
resets the curve; adding more of the same does not.

## Trade-offs
- **Breadth vs. focus**: supporting many kinds of fun widens the audience but
  blurs identity. Pick a primary aesthetic and make the rest supportive.
- **Mastery depth vs. accessibility**: deeper pattern spaces reward veterans
  but raise the learning cost for newcomers; layer depth behind simple entry.
- **Authored vs. emergent patterns**: authored content is controlled but is
  consumed; systems that generate dynamics last longer but are harder to
  predict and balance.
- **Theory vs. data**: MDA tells you what to look for; only playtests tell you
  what players actually felt.

## Gotchas
- Treating aesthetics as a mechanic: you cannot add "tension"; you add
  mechanics (scarcity, timers, risk) that produce it.
- Assuming your own aesthetic is everyone's. Players differ in what they find
  fun; see [[player-motivation-and-player-types]].
- Equating fun with ease or with constant rewards. Frustration that precedes a
  breakthrough is part of the pleasure of hard fun.
- Confusing "fun" with "engaging". Compulsion loops can retain players who do
  not enjoy themselves; check whether players would recommend the game.
- Reading the eight kinds of fun as a scoring rubric. It is a vocabulary, not a
  checklist to satisfy.

## Related
- [[core-gameplay-loop]] - the repeating structure where the fun is delivered.
- [[flow-and-difficulty-curves]] - keeping challenge matched to a changing skill.
- [[player-motivation-and-player-types]] - why different players want different fun.
- [[meaningful-choices]] - the mechanic-level source of discovery and mastery.
- [[prototyping-and-finding-the-fun]] - testing the aesthetic cheaply.

## References
- Hunicke, LeBlanc, Zubek, "MDA: A Formal Approach to Game Design and Game
  Research": http://users.cs.northwestern.edu/~hunicke/MDA.pdf
- Raph Koster, *A Theory of Fun for Game Design*: https://www.theoryoffun.com/
- Nicole Lazzaro, "Why We Play Games: Four Keys to More Emotion Without
  Story" (GDC 2004 paper, searchable on https://www.gdcvault.com/).
- Jesse Schell, *The Art of Game Design: A Book of Lenses* (the lens of fun,
  the lens of curiosity).
