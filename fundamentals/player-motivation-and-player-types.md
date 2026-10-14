---
title: Player motivation and player types
category: fundamentals
tags: [motivation, SDT, Bartle, Quantic-Foundry, intrinsic, extrinsic, overjustification]
use_cases:
  - "Who is this game for and what will keep them playing?"
  - "Should we add achievements, badges and daily rewards?"
  - "Different players want different things; how do I design for all of them?"
  - "Players stopped enjoying the game once we added rewards"
status: draft
last_verified: 2026-10-14
sources:
  - https://selfdeterminationtheory.org/
  - https://mud.co.uk/richard/hcds.htm
  - https://quanticfoundry.com/
  - https://www.gdcvault.com/
---

# Player motivation and player types

## Summary
Players come to games for different reasons, and the reasons predict which
mechanics will please them. Self-Determination Theory (SDT) gives a
research-backed core: people are intrinsically motivated by competence,
autonomy and relatedness. Player-type models (Bartle, Quantic Foundry) are
useful for brainstorming audiences but are coarse. Add extrinsic rewards
carefully, since they can crowd out the enjoyment they were meant to boost.

## Key concepts
- **Self-Determination Theory** (Deci and Ryan; applied to games by Ryan,
  Rigby, Przybylski): satisfaction of **competence** (feeling effective,
  mastering), **autonomy** (meaningful choice, volition) and **relatedness**
  (connection with others) drives intrinsic motivation. Their work links
  need satisfaction in play with enjoyment and desire to continue playing.
- **Bartle types**: Achievers, Explorers, Socializers, Killers, from Richard
  Bartle's 1996 analysis of MUD players. Born of one text-game community,
  it is a heuristic, not a validated personality test.
- **Quantic Foundry model** (Nick Yee): survey-based motivations grouped
  into clusters such as Action (destruction, excitement), Social (competition,
  community), Mastery (challenge, strategy), Achievement (completion, power),
  Immersion (fantasy, story) and Creativity (design, discovery). Players
  score on several, so profiles are mixes.
- **Intrinsic vs. extrinsic motivation**: intrinsic means the activity is the
  reward; extrinsic means an external payoff (points, loot, badges).
- **Overjustification effect**: attaching rewards to something already
  enjoyed can shift the reason for playing toward the reward and lower
  interest when the reward disappears.

## When to use / scenarios
- Audience definition: name the top two or three motivations of your target
  player and design the core loop to serve them.
- Reward and achievement planning: ask which need (competence, autonomy,
  relatedness) each reward supports.
- Feature gaps: a game rich in challenge but with no chance for expression
  often loses players seeking autonomy; a solo game may need optional social
  hooks.
- Avoid using types as marketing segments without data. Use survey or
  telemetry from your own players ([[playtesting-and-metrics]]).

## How it works / example
**Mapping features to SDT needs.**

| Need | Design levers | Example |
|---|---|---|
| Competence | Clear feedback, scaling challenge, visible skill growth | *Celeste* chapter checkpoints; *Tetris* rising speed |
| Autonomy | Multiple viable builds, open order of goals, opt-in challenges | *Skyrim* or *Elden Ring* route choice; *Hades* boon picks |
| Relatedness | Co-op, shared goals, trading, characters you care about | *Animal Crossing* visiting; *Overcooked* co-op; *Hades* cast |

**Spotting a gap** with a quick audit script: score a feature list by need
and see what a design never touches.

```python
features = {
    "daily login bonus": {"competence": 0, "autonomy": 0, "relatedness": 0},
    "skill-tree respec": {"competence": 1, "autonomy": 2, "relatedness": 0},
    "guild raids":       {"competence": 2, "autonomy": 1, "relatedness": 3},
    "combo system":      {"competence": 3, "autonomy": 1, "relatedness": 0},
}
totals = {k: sum(f[k] for f in features.values())
          for k in ("competence", "autonomy", "relatedness")}
print(totals)   # a near-zero need is a design hole worth discussing
```

(The scores are your judgement; the value is the discussion, not the sum.)

**Overjustification in practice.** A game players already love for building
(Minecraft, Factorio) risks diluting that if every build task becomes
"complete 5 builds for 50 coins". Prefer rewards that confirm competence
("informational": you did something skilful) over rewards that control
("controlling": do this or lose the streak). Achievements as optional,
discoverable surprises are safer than mandatory checklists.

## Trade-offs
- **Serve one motivation deeply vs. many shallowly**: a focused game (a
  mastery-driven arcade shooter) keeps identity; a broad one reaches more
  players but risks a shapeless loop.
- **Extrinsic rewards vs. intrinsic play**: rewards help onboarding and
  retention early, but tie them to meaningful play and phase them out as
  intrinsic enjoyment takes over.
- **Social features vs. solo comfort**: relatedness boosts retention for many,
  but forced social play excludes players who want privacy; make it opt-in.
- **Type models vs. data**: types are cheap; own survey or telemetry data is
  better but costs time.

## Gotchas
- Treating Bartle types as exclusive boxes; people shift with mood and
  context, and the model fits MUDs better than modern genres.
- Designing for "Killers" as a license for griefing; guard against abuse in
  [[multiplayer-and-social-play]].
- Streaks and daily rewards that create obligation. Missing a day feels like
  a loss, which erodes autonomy and may breed resentment.
- Over-quoting studies: SDT links need satisfaction to enjoyment, but the
  effect sizes and applicability to your genre need your own testing.
- Using leaderboards as the only relatedness feature; they serve competition
  and can discourage players who rank low.

## Related
- [[what-makes-a-game-fun]] - the kinds of fun these motivations map onto.
- [[reward-schedules-and-loot]] - how extrinsic rewards are scheduled.
- [[progression-systems]] - how competence is made visible over time.
- [[multiplayer-and-social-play]] - building relatedness without toxicity.
- [[meaningful-choices]] - the main lever for autonomy.

## References
- Ryan, Rigby, Przybylski, "The Motivational Pull of Video Games: A
  Self-Determination Theory Approach" (Motivation and Emotion, 2006); SDT
  overview: https://selfdeterminationtheory.org/
- Richard Bartle, "Hearts, Clubs, Diamonds, Spades: Players Who Suit MUDs":
  https://mud.co.uk/richard/hcds.htm
- Nick Yee and Quantic Foundry, Gamer Motivation Model: https://quanticfoundry.com/
- Jesse Schell, *The Art of Game Design* (lenses on player motivation).
