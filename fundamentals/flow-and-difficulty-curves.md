---
title: Flow and difficulty curves
category: fundamentals
tags: [flow, difficulty, DDA, sawtooth, assist-mode, Celeste, Left-4-Dead, Resident-Evil-4]
use_cases:
  - "Players say the game is too hard in one section and too easy in another"
  - "Beginners quit while veterans are bored; how do I serve both?"
  - "Should I add difficulty settings or dynamic difficulty?"
  - "How punishing should death or failure be?"
status: draft
last_verified: 2026-10-14
sources:
  - https://www.harpercollins.com/products/flow-mihaly-csikszentmihalyi
  - https://www.theoryoffun.com/
  - https://www.gdcvault.com/
  - https://www.gamedeveloper.com/
---

# Flow and difficulty curves

## Summary
Flow is the state of absorbed engagement that occurs when a challenge matches
the player's skill and the goals are clear. Difficulty design is the craft of
keeping challenge inside that channel while skill changes through play. The
main tools are a rising-and-resting (sawtooth) curve, adaptive systems such as
dynamic difficulty adjustment, player-selected options, and a failure cost that
keeps trying worthwhile.

## Key concepts
- **Flow channel** (Csikszentmihalyi): too much challenge over skill causes
  anxiety; too little causes boredom; the channel runs diagonally between.
  Clear goals and immediate feedback are also conditions for flow.
- **Skill moves**: players get better, so a flat difficulty drifts into
  boredom. The curve must climb, or the game must introduce new challenges.
- **Sawtooth curve**: tension builds through a level or encounter chain, then
  drops at a rest or reward before rising slightly higher. Pacing matters more
  than the average level.
- **Dynamic difficulty adjustment (DDA)**: the game adapts to measured
  performance. *Resident Evil 4* quietly shifts enemy aggression and drops
  based on how the player is doing. *Left 4 Dead*'s AI Director modulates
  threat and pacing, with relaxed periods after peaks.
- **Player-chosen difficulty**: selectable modes and assist options let players
  place themselves in the channel. *Celeste*'s Assist Mode offers adjustable
  game speed, extra dashes and invincibility without shaming the player.
- **Failure cost**: the price of dying (lost time, items, progress) shapes
  how bold players are willing to be.

## When to use / scenarios
- Playtest data shows a drop-off spike at one level or boss: a difficulty
  spike or missing teaching step ([[onboarding-and-tutorials]]).
- A wide audience: combine a well-tuned default curve with options.
- Roguelikes and run-based games: failure is part of the loop, so keep the
  cost of failure small relative to the length of a run.
- Competitive multiplayer: do not use DDA; matchmaking handles skill matching.
- Not a fix for repetitiveness caused by mastered patterns; add variety
  instead ([[what-makes-a-game-fun]]).

## How it works / example
**Sawtooth by hand.** A level with 5 encounters might use difficulty values
3, 4, 5, rest (2), 6, boss 8. The rest gives recovery and a feeling of
progress, and the next peak is a bit higher than the last. Many action games
(*Resident Evil 4* village sections, *Doom (2016)* arenas followed by calm
exploration) alternate in this manner.

**Simple DDA**: nudge a difficulty multiplier from rolling performance, with
caps and slow movement so the player does not notice or exploit it.

```python
def update_difficulty(diff, deaths_recent, clears_recent,
                      step=0.05, lo=0.7, hi=1.3):
    """Raise on streaks of success, lower on streaks of failure."""
    if deaths_recent >= 3:
        diff -= step
    elif clears_recent >= 3:
        diff += step
    return max(lo, min(hi, diff))

def sawtooth(level, period=5, base=1.0, slope=0.1, rest=0.6):
    """Base difficulty rising with a rest at the end of each period."""
    peak = base + slope * level
    return peak * (rest if level % period == period - 1 else 1.0)

diff = 1.0
for outcome in ["die", "die", "die", "win", "win", "win", "win"]:
    d = 1 if outcome == "die" else 0
    c = 1 - d
    diff = update_difficulty(diff, d * 3, c * 3)
    print(outcome, round(diff, 2))

print([round(sawtooth(i), 2) for i in range(10)])
```

**Difficulty options** that work in practice:
- Few, labelled by experience ("Story", "Standard") rather than by player
  worth. Avoid "Easy: for babies" style copy.
- Granular assists (*Celeste*): invincibility, speed, infinite stamina;
  these let players tailor rather than pick a bucket.
- Safe changes mid-game, with no penalty for lowering difficulty.

**Failure cost**: *Super Meat Boy* and *Celeste* use instant respawn; deaths
are cheap, so players try bold lines. *Dark Souls* uses soul-loss with a
retrieval run; failure carries weight and makes progress feel earned. Match
failure cost to the aesthetic you want.

## Trade-offs
- **DDA vs. authored difficulty**: adaptation keeps more players in flow but
  can feel patronising or erode the sense that a win was earned. Hidden,
  small adjustments tend to be accepted; visible rubber-banding is not.
- **One tuned experience vs. options**: options widen the audience but you
  must test each setting; a hard mode may reveal broken balance.
- **Cheap vs. expensive failure**: cheap failure encourages experimenting;
  expensive failure raises stakes and the satisfaction of success.
- **Fixed vs. adaptive ramps**: authored curves are predictable and
  tuneable; adaptive ones respond to skill spread but are harder to QA.

## Gotchas
- Difficulty spikes that come from missing information rather than real
  challenge (an unfair first-time death with no signal).
- Tuning for yourself: developers are far more skilled than their audience.
  Test with new players.
- DDA that punishes good play, such as dropping resources because you were
  doing well, or players that deliberately fail to farm an easier state.
- Constant peaks with no rest; fatigue turns challenge into frustration.
- Locking players into their first difficulty choice.
- Rewarding failure too generously so that stakes disappear.

## Related
- [[onboarding-and-tutorials]] - teaching skills so the early curve does not need to be flat.
- [[level-design-and-pacing]] - the sawtooth applied to spaces and encounters.
- [[combat-and-encounter-design]] - tuning the individual encounters on the curve.
- [[game-balance]] - numerical tuning behind the curve.
- [[playtesting-and-metrics]] - finding drop-off spikes in real data.

## References
- Mihaly Csikszentmihalyi, *Flow: The Psychology of Optimal Experience*:
  https://www.harpercollins.com/products/flow-mihaly-csikszentmihalyi
- Raph Koster, *A Theory of Fun for Game Design*: https://www.theoryoffun.com/
- Michael Booth, "The AI Systems of Left 4 Dead" (Valve, AIIDE/Artificial
  Intelligence in the Game Industry material; search https://www.gdcvault.com/).
- Game Developer, difficulty and dynamic difficulty articles:
  https://www.gamedeveloper.com/
- Celeste Assist Mode design notes by Maddy Thorson and team (devlog and
  GDC-related talks via https://www.gdcvault.com/).
