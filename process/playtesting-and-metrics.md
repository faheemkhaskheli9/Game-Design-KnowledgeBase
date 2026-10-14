---
title: Playtesting and metrics
category: process
tags: [playtest, think-aloud, telemetry, funnel, retention, heatmap, analytics]
use_cases:
  - "How do I run a playtest and get useful feedback?"
  - "Players drop off somewhere and I do not know why"
  - "What should I measure in my game?"
  - "Playtesters keep suggesting features; what do I do with that?"
status: draft
last_verified: 2026-10-14
sources:
  - https://www.routledge.com/Game-Design-Workshop-A-Playcentric-Approach-to-Creating-Innovative-Games/Fullerton/p/book/9781138098770
  - https://www.gdcvault.com/
  - https://www.gamedeveloper.com/
---

# Playtesting and metrics

## Summary
Playtesting is observing real players with your game to learn what they do,
where they get stuck and what they feel. Metrics (telemetry) show what
happens at scale but not why. Use qualitative sessions to find problems and
telemetry to size them, and treat player-suggested solutions as symptoms to
investigate, not instructions to follow.

## Key concepts
- **Observe, do not explain**: the designer's job during a test is silence.
  If you help, you hide the problem every real player will hit alone.
- **Think-aloud**: asking players to narrate what they see, expect and feel.
  It reveals expectations; do not ask leading questions.
- **Diagnosis vs. prescription**: players are reliable about their
  experience ("I did not know what to do") and unreliable about fixes ("add
  a minimap"). Record the first, treat the second as a hint.
- **Funnel**: an ordered sequence of steps (install, tutorial start,
  tutorial finish, first level, first session end); the share who reach each
  step shows where players leave.
- **Drop-off point**: the step with an unusually large loss. Locate it first
  and then investigate cause with observation.
- **Retention**: the share of players who return after a day or a week
  (often written D1, D7, D30, measured from first play). Compare against
  genre norms from reliable sources rather than remembered numbers.
- **Telemetry and heatmaps**: logged events with positions (deaths, pauses,
  purchases) aggregated on level maps show hotspots.

## When to use / scenarios
- Every prototype and milestone: test early and often with fresh players.
- A drop-off spike in funnel data: watch new players do that step.
- Balancing ([[game-balance]]): use telemetry on win rates, item picks and
  time-to-complete to find outliers.
- Do not rely on metrics alone for a small audience: with few players,
  numbers are noisy; watch people instead.
- Do not chase metrics that reward manipulation (session length padded with
  friction) at the cost of enjoyment.

## How it works / example
**Running a session (30-45 minutes).**
1. Recruit players matching the target audience; not friends and not
   teammates. Five fresh testers often expose the major problems, which is
   why repeat small rounds beat one large study (a common usability heuristic
   from Jakob Nielsen's research).
2. Brief: "We are testing the game, not you. Please think aloud. I will not be
   able to answer questions during play."
3. Do not help. Note where they hesitate, misread, or sigh. Resist saying
   "try the door on the left".
4. Record screen and face if consent is given; log timestamps.
5. Debrief with open questions: "What was the goal?", "What was the best
   moment?", "What would you tell a friend?"
6. Sort notes into problems (observed), causes (your hypothesis) and fixes
   (yours, not the player's).

**Metrics to log from day one.** Session start/end, tutorial steps,
level start/complete, deaths with position, quits with position, key
actions (purchase, upgrade), and time per segment.

**A tiny funnel analysis:**

```python
steps = ["install", "tutorial_start", "tutorial_end", "level1_end", "return_d1"]
users = {
    "install": 1000, "tutorial_start": 900, "tutorial_end": 520,
    "level1_end": 430, "return_d1": 210,
}
prev = None
for s in steps:
    n = users[s]
    if prev:
        print(f"{s:15s} {n:5d}  step conv {n / prev:.0%}")
    else:
        print(f"{s:15s} {n:5d}")
    prev = n
# The tutorial_start -> tutorial_end step loses the most: watch players there.
```

(The numbers are illustrative; use your own telemetry.)

**Heatmap use**: plot death or quit positions on a level map. A cluster
at one jump means a difficulty spike or an unreadable hazard; a cold region
may be unused content or a place players cannot find. *Halo* and other
Bungie titles and many Valve games have discussed using telemetry like this to
tune levels and weapons (see GDC Vault talks).

**Diagnosis vs. prescription example.** A tester says "the boss needs more
health". Dig: they died eight times, did not notice the dodge window, and
gave up. The diagnosis is a readability problem, and more health makes it worse.

## Trade-offs
- **Qualitative vs. quantitative**: observation explains but does not scale;
  telemetry scales but does not explain. Use both in sequence.
- **Early rough vs. late polished tests**: rough tests find core issues
  cheaply; polished ones validate feel, but changes are costlier.
- **Moderated vs. remote unmoderated**: moderated gets depth; remote gets
  numbers and natural settings but you cannot probe.
- **Logging more vs. privacy and cost**: more events give flexibility but
  need storage, consent and care with personal data.

## Gotchas
- Leading questions ("Did you like the cool new crafting?"); ask what they
  did and felt.
- Testing only with developers, friends or the same few players, who learn
  the game and stop being fresh.
- Acting on one loud tester; look for patterns across several.
- Over-reading small samples or early retention swings; check variance.
- Optimizing a metric (time in game) that is not the goal (enjoyment).
- Forgetting to test the first five minutes with truly new players; most
  quit decisions happen there ([[onboarding-and-tutorials]]).
- Skipping consent and privacy notices when recording or logging players.

## Related
- [[prototyping-and-finding-the-fun]] - what to test and when to kill.
- [[retention-and-session-design]] - turning retention numbers into design.
- [[onboarding-and-tutorials]] - the funnel step that most often leaks players.
- [[game-balance]] - telemetry as input for balance tuning.
- [[design-review-checklist]] - a review pass to run before and after tests.

## References
- Tracy Fullerton, *Game Design Workshop* (chapters on playtesting methods):
  https://www.routledge.com/Game-Design-Workshop-A-Playcentric-Approach-to-Creating-Innovative-Games/Fullerton/p/book/9781138098770
- Jesse Schell, *The Art of Game Design* (playtesting lenses).
- GDC Vault: talks on playtesting, user research and telemetry
  (e.g., Halo and Valve analyses): https://www.gdcvault.com/
- Game Developer articles on analytics and playtesting: https://www.gamedeveloper.com/
