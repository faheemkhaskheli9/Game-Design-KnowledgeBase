---
title: Onboarding and tutorials
category: experience
tags: [onboarding, tutorial, ftue, progressive-disclosure, teach-by-doing, portal, super-mario-bros, drop-off]
use_cases:
  - "new players quit in the first five minutes"
  - "my tutorial is a wall of text and nobody reads it"
  - "how do I teach a complex mechanic without a lecture"
  - "players do not understand the core mechanic after the tutorial"
  - "where in the tutorial are people dropping off"
status: draft
last_verified: 2026-10-14
sources:
  - https://www.youtube.com/@ExtraCreditz
  - https://www.youtube.com/@GMTK
  - https://celiahodent.com/
  - https://www.schellgames.com/art-of-game-design
---

# Onboarding and tutorials

## Summary
Onboarding is everything between first launch and the moment the player can play the game on their own and wants to continue: first-time user experience (FTUE), tutorials, early levels and the first rewards. The best onboarding is mostly invisible: the game teaches by getting the player to do the thing in a safe space, then raising the stakes. It solves early churn, confusion and the "I read it but still do not get it" problem.

## Key concepts
- **Teach by doing**: a mechanic is learned when the player performs it and sees the consequence, not when they read about it. Text describes; practice teaches.
- **Cognitive load** (Celia Hodent, "The Gamer's Brain"): working memory is small. Introduce one new idea at a time, and do not ask the player to hold earlier instructions while learning new ones.
- **Progressive disclosure / gating**: reveal systems as they become relevant. Hide menus, currencies and crafting until the player has a reason to care. Gate by capability, not by a timer.
- **Safe practice space**: a context where failure is cheap and non-punishing (no enemies, no timer, a respawn at the same spot) so the verb can be tried without fear.
- **Teach-test-twist**: introduce a mechanic in isolation, test it in a simple challenge, then combine it with something already known. This is the same structure as kishotenketsu (see [[level-design-and-pacing]]).
- **Just-in-time information**: show the instruction at the moment and place it is needed, next to the object it concerns, and remove it once the player succeeds.
- **FTUE**: the first session as a designed sequence. The goal is a first success and a reason to return, not completeness.

## When to use / scenarios
- Analytics show a steep funnel drop in the first session, or many players quit at one specific step.
- Playtesters ask questions the tutorial claims to answer, or ignore on-screen prompts.
- A new mechanic arrives mid-game and players misuse it for hours.
- Complex genres (4X, deck builders, roguelikes with meta-progression) where the full system cannot be understood up front.
- NOT a substitute for a clear core verb: if the mechanic cannot be taught in a minute, simplify it first. See [[core-gameplay-loop]].
- Skippable tutorials: returning players and genre veterans must be able to opt out or fast-forward.

## How it works / example
**Super Mario Bros World 1-1.** No text. The first screen is empty ground and a lone Goomba moving toward you: you either jump or die, and dying is cheap and instructive. A row of blocks and a mushroom that moves toward you in a spot where it cannot be avoided teaches that power-ups are good. Pits appear only after you have the jump. This is a safe space, a test, then a twist, with the level itself as the teacher. Mark Brown's Game Maker's Toolkit videos analyse this style.

**Portal test chambers.** Chamber 1 shows a portal in a room with no hazards; the next adds a launch, then a moving platform, then a turret, each only after the previous idea is solid. Each chamber introduces exactly one new idea, tests it, then recombines it. The writing (GLaDOS) fills time while the player acts, never blocking input.

A funnel table is the practical measurement tool:

```
step                          reached   % of previous
launch                          1000      -
first move input                 940      94%
first jump                       890      95%
completed tutorial level         610      69%   <- investigate here
first real level started         540      89%
```

The step with the sharpest relative drop is the hotspot. Watch recordings or run a moderated playtest at that step; the cause is usually a confusing prompt, a spike in difficulty or a long no-control stretch.

Design checklist for each tutorial beat:
1. What single idea does this teach?
2. Can the player only succeed by using it?
3. Is failure cheap and is the cause of failure visible?
4. Is there a reward or visible payoff immediately?
5. Is the prompt placed at the object, and does it disappear after success?

## Trade-offs
- **Forced vs optional**: forcing the tutorial protects novices but irritates veterans. Offer a skip, or make it short and fast enough that skipping is not tempting.
- **Explicit vs implicit teaching**: environmental teaching is elegant but fails for abstract systems (economy, builds), where a short explicit card helps.
- **Early depth vs early simplicity**: stripping features gets a cleaner first hour but may hide what makes the game special; show a taste of the hook early (a flashy ability, a boss glimpse).
- **Hand-holding vs discovery**: a sandbox with minimal hints rewards curious players (Dark Souls, Outer Wilds) but loses those who need structure; a codex or opt-in hint system serves both.
- **Dedicated tutorial level vs integrated onboarding**: a separate tutorial is easy to build and measure; integrated teaching feels better but is harder to rework later.

## Gotchas
- Text walls and modal popups at launch: players dismiss them without reading. Cap each prompt at one sentence and one action.
- Teaching controls by diagram only: players retain what they press. Make them press it.
- Locking the player in a no-control cutscene for the first minute; the first input should come within seconds.
- Tutorials that test knowledge never taught (a boss that needs a dodge you showed once).
- Testing onboarding with the team: designers cannot unsee the game. Use players who have never seen it, and stay silent while they play.
- Not re-onboarding: players who return after weeks have forgotten; provide quick refreshers and always-accessible help.
- Praise noise: congratulating every trivial step ("Great job!") reads as patronising. Reward real progress.
- Assuming all platforms share mental models: a mobile player expects touch gestures to be self-evident; a PC player may expect a key-rebind menu in the first minute.

## Related
- [[level-design-and-pacing]] - the introduce/develop/twist structure is the backbone of level-based teaching.
- [[retention-and-session-design]] - the first session is the first retention test.
- [[playtesting-and-metrics]] - funnel analytics and observation find where onboarding fails.
- [[progression-systems]] - gate new systems through progression, not through menus.
- [[player-motivation-and-player-types]] - explorers and achievers want different amounts of guidance.

## References
- Celia Hodent, "The Gamer's Brain: How Neuroscience and UX Can Impact Video Game Design" (2017); site https://celiahodent.com/
- Jesse Schell, "The Art of Game Design: A Book of Lenses", sections on interest curves and teaching through play; https://www.schellgames.com/art-of-game-design
- Extra Credits tutorial episodes: https://www.youtube.com/@ExtraCreditz
- Mark Brown, Game Maker's Toolkit, level design and tutorial analyses (Super Mario Bros, Portal): https://www.youtube.com/@GMTK
