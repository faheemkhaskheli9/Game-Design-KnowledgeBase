---
title: Prototyping and finding the fun
category: process
tags: [prototype, paper-prototype, greybox, vertical-slice, kill-criteria, iteration, Tetris, Portal]
use_cases:
  - "I have a game idea; how do I know if it is fun before building it fully?"
  - "We are months in and the game still does not feel good"
  - "How should I scope and sequence early development?"
  - "When should we kill or pivot a concept?"
status: draft
last_verified: 2026-10-14
sources:
  - https://www.routledge.com/Game-Design-Workshop-A-Playcentric-Approach-to-Creating-Innovative-Games/Fullerton/p/book/9781138098770
  - https://www.gdcvault.com/
  - https://www.gamedeveloper.com/
---

# Prototyping and finding the fun

## Summary
Prototyping is building the cheapest thing that can answer one design question,
then playing it. "Find the fun" means proving the core interaction is enjoyable
before investing in content, art and systems. Fast, disposable prototypes
across paper, greybox and vertical slice stages expose problems when they are
cheap to fix, and give you honest grounds to kill an idea.

## Key concepts
- **Question-driven prototype**: each prototype exists to answer one question
  ("is jumping fun?", "does trading create tension?"), not to be a mini-game.
- **Paper prototype**: cards, dice, tokens and a spreadsheet to test rules,
  economy and decisions with no code. Best for turn-based, strategy,
  economy and card systems.
- **Toy before game**: a toy is fun to play with without goals (Swink's
  game-feel focus: a character that is satisfying to move). Add goals and
  rules after the toy works.
- **Greybox**: placeholder geometry, no art, to test movement, camera,
  encounter layouts and pacing in 3D or 2D levels.
- **Vertical slice**: a thin, polished piece of the final game (one level,
  full quality) proving the whole pipeline and target feel. Build after the
  core loop is proven, not before.
- **Kill criteria**: pre-agreed conditions to stop or pivot, written before
  the prototype is played.

## When to use / scenarios
- Start of any project: build the 30-seconds-of-fun prototype first.
- Doubts about a mechanic: isolate it in a one-day prototype rather than
  debating it.
- Economy or balance questions: paper or spreadsheet before code
  ([[game-economy-sources-and-sinks]]).
- Not for polish questions late in production; those need in-context testing.
- Be wary of building tools or engines "for the prototype"; use what you
  already know.

## How it works / example
**Process.**
1. Write the question and the kill criteria. Example: "Within 2 hours of
   iteration, 4 of 5 testers should replay voluntarily; otherwise change the
   core verb or stop."
2. Pick the cheapest medium: paper, 1-day code, or greybox.
3. Build for hours or days, not weeks. Hard-code values, use placeholder
   assets, ignore menus.
4. Playtest immediately ([[playtesting-and-metrics]]); change one variable at
   a time.
5. Decide: continue, pivot, or kill. Only then escalate fidelity.

**Real cases.**
- *Tetris* began as Pajitnov's minimal text-mode puzzle: a tiny, abstract toy
  whose appeal was visible immediately.
- *Portal* grew from *Narbacular Drop*, a DigiPen student project whose
  portal mechanic was proven fun; Valve hired the team and built authored
  puzzles around that mechanic.
- *Spore* is a cautionary and instructive case: its creature creator was
  immediately delightful, but the game's multi-scale ambition made it hard
  to prove a satisfying overall loop (a point widely discussed in
  postmortems; see Game Developer and GDC talks).
- Many studios, including Supergiant and Double Fine, discuss rapid
  prototyping or game-jam-style prototypes in public talks and devlogs.

**Quick tool**: a paper-prototype economy checked in a few lines:

```python
import random
random.seed(7)

def turn(gold, income=3, cost_choices=(2, 5, 8)):
    gold += income
    cost = random.choice(cost_choices)
    return gold - cost if gold >= cost else gold   # buy if affordable

gold, history = 0, []
for _ in range(20):
    gold = turn(gold)
    history.append(gold)
print(history)   # does gold pile up (no tension) or stay at 0 (no choice)?
```

If numbers pile up, the economy lacks pressure; if it sits at zero,
players never get to choose. This kind of check is faster than building UI.

**Prototype ladder:** paper (hours) -> greybox core mechanic (days) ->
first playable with one level and placeholder art (weeks) -> vertical slice
(months) -> production. A project that cannot survive a step should stop there.

## Trade-offs
- **Throwaway vs. reusable code**: throwaway code is fast and honest but
  tempts teams to ship it; budget time to rewrite.
- **Low vs. high fidelity**: low fidelity gets truthful feedback on
  mechanics, but game feel and juice need some polish to judge fairly
  ([[game-feel-and-juice]]).
- **Many small vs. one deep prototype**: several small prototypes explore
  more ideas; one deep one tests long-term depth.
- **Vertical slice timing**: early slices reveal pipeline problems; premature
  slices lock in unproven design.

## Gotchas
- Prototyping the wrong question (art style) while the core verb is untested.
- Sunk-cost bias: a prototype that was weeks of work is hard to kill;
  time-box up front.
- Judging an idea by one enthusiastic tester (often yourself). Fresh players
  are the test.
- Never writing the kill criteria, so no result is ever "bad enough".
- Treating the vertical slice as marketing polish only; it should prove
  production scope and cost.
- Adding features to rescue a prototype whose core is not fun; features
  rarely fix a weak core.

## Related
- [[what-makes-a-game-fun]] - the aesthetic target a prototype is checked against.
- [[core-gameplay-loop]] - the loop whose fun you are trying to find first.
- [[playtesting-and-metrics]] - how to observe a prototype session.
- [[game-feel-and-juice]] - the toy-level feel of movement and action.
- [[design-review-checklist]] - a review pass before escalating fidelity.

## References
- Tracy Fullerton, *Game Design Workshop: A Playcentric Approach to Creating
  Innovative Games*: https://www.routledge.com/Game-Design-Workshop-A-Playcentric-Approach-to-Creating-Innovative-Games/Fullerton/p/book/9781138098770
- Jesse Schell, *The Art of Game Design* (chapters on iteration and the
  loop of prototyping).
- Steve Swink, *Game Feel* (toy-first thinking).
- GDC Vault talks on prototyping and postmortems: https://www.gdcvault.com/
- Game Developer postmortems: https://www.gamedeveloper.com/
