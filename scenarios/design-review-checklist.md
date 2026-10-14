---
title: Design review checklist
category: scenarios
tags: [checklist, review, critique, lenses, design-doc]
use_cases:
  - "review this game design or feature before we build it"
  - "critique my game idea and find what will make it boring"
  - "check a new mechanic, reward system or monetization plan for problems"
status: stable
last_verified: 2026-10-14
sources:
  - https://schellgames.com/art-of-game-design
  - https://users.cs.northwestern.edu/~hunicke/MDA.pdf
  - https://www.gamedeveloper.com/design/gdc-2012-sid-meier-on-how-to-see-games-as-sets-of-interesting-decisions
---

# Design review checklist

## Summary
A question list for reviewing a game design, feature or mechanic before building it, in the spirit of Schell's lenses. Each question names the topic that explains how to fix a "no". Use it on design docs, feature proposals, and when an AI agent is asked to add or change gameplay, so changes are checked against what makes games engaging rather than only against whether they work.

## Key concepts
- Review from the player's experience backwards (aesthetics, then dynamics, then mechanics), as in the MDA framework.
- A "no" or "unsure" is a prompt to read the linked topic, not a verdict; some games deliberately break a rule.
- Answer with evidence where possible: a prototype, a playtest note, a spreadsheet, a simulation.

## When to use / scenarios
- Before implementing a new mechanic, mode, reward or economy change.
- When reviewing a game design document or a pull request that changes gameplay numbers.
- After a playtest, to structure what to change.
- Not a substitute for playtesting: it finds likely problems; only players confirm them ([[playtesting-and-metrics]]).

## How it works / example

**Experience and fun**
1. Can you state in one sentence what the player should feel? ([[what-makes-a-game-fun]])
2. What does the player do every few seconds, and is it satisfying on its own? ([[core-gameplay-loop]], [[game-feel-and-juice]])
3. Does every action give immediate, readable feedback? ([[game-feel-and-juice]])

**Choices and challenge**
4. Does the player make a real decision at least every minute, with trade-offs and no single best answer? ([[meaningful-choices]])
5. Is there a dominant strategy, unit or build? How would you find out? ([[game-balance]])
6. Does difficulty rise with skill, with rests between peaks? Can a stuck player get unstuck? ([[flow-and-difficulty-curves]])
7. Is randomness creating stories and variety, or deciding outcomes the player cannot influence? ([[randomness-and-luck]])
8. Can a losing player come back, and does the game still end decisively? ([[feedback-loops-and-snowballing]])

**Motivation and progression**
9. Which needs does it serve: competence, autonomy, relatedness? ([[player-motivation-and-player-types]])
10. Does progression add options, not only bigger numbers? ([[progression-systems]])
11. Are rewards tied to play the player enjoys, or paid for doing chores? ([[reward-schedules-and-loot]])
12. Does every currency have sinks as well as sources? ([[game-economy-sources-and-sinks]])
13. Does the session have natural stopping points, and would the player feel fine stopping? ([[retention-and-session-design]])

**Learning and structure**
14. Can a new player learn it by doing, within the first minutes, without reading? ([[onboarding-and-tutorials]])
15. Does each level/area introduce, develop and twist one idea? ([[level-design-and-pacing]])
16. Do the story and the mechanics say the same thing? ([[narrative-and-player-agency]])
17. With other players: is losing still fun, and can bad actors ruin it for others? ([[multiplayer-and-social-play]])

**Ethics**
18. Would you be comfortable explaining every engagement or monetization mechanic to the players, including parents of child players? ([[retention-and-session-design]], [[reward-schedules-and-loot]])

**Process**
19. What is the cheapest prototype that tests the riskiest assumption? ([[prototyping-and-finding-the-fun]])
20. What will you measure or watch in the next playtest to know it worked? ([[playtesting-and-metrics]])

Example: a proposal adds "daily login rewards that escalate for 30 days and reset on a missed day". Q11 and Q13 flag it (rewards for logging in, not playing; reset punishes absence), and Q18 flags the loss-aversion pressure. Revision: rewards for a daily play goal, no reset, catch-up allowed.

## Trade-offs
- Thoroughness vs speed: for a small tweak, answer only the questions the change touches. Run the full list on new systems.
- Rules vs vision: an intentionally punishing game (Dark Souls, roguelikes) answers Q6 and Q8 differently. Note the deliberate exception rather than "fixing" it.

## Gotchas
- Answering every question "yes" from the designer's chair is easy. Back the answers with a prototype or playtest, or mark them unverified.
- Checklists favour the familiar. A novel design can fail a convention and still be right; that is a reason to prototype it, not to cut it.
- Numbers changes (damage, prices, drop rates) look small in a diff but change the whole economy and balance; give them a full review.

## Related
- [[scenario-chooser]] - start from a symptom instead of a design.
- [[what-makes-a-game-fun]] - the MDA lens this list is ordered by.
- [[playtesting-and-metrics]] - how to verify the answers.

## References
- Jesse Schell, The Art of Game Design: A Book of Lenses.
- Hunicke, LeBlanc, Zubek, "MDA: A Formal Approach to Game Design and Game Research" (2004).
- Sid Meier, "Interesting Decisions", GDC 2012.
