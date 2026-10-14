---
title: Retention and session design
category: progression
tags: [retention, sessions, streaks, daily-goals, live-ops, one-more-turn, dark-patterns, fomo]
use_cases:
  - "players churn after the first week"
  - "design daily or weekly goals without nagging players"
  - "decide how long a play session should be on mobile versus PC"
  - "add a streak or login reward ethically"
  - "plan a live-ops content cadence"
status: draft
last_verified: 2026-10-14
sources:
  - https://www.gamesbrief.com/
  - https://celiahodent.com/
  - https://en.wikipedia.org/wiki/Civilization_(series)
  - https://en.wikipedia.org/wiki/Zeigarnik_effect
  - https://www.artofgamedesign.com/
---

# Retention and session design

## Summary
Retention is whether players come back; session design is how a single visit is shaped. Healthy retention comes from a game that is worth returning to: clear goals, satisfying stopping points and fresh content. Unhealthy retention comes from pressure and fear of missing out. This file covers the tools and where the ethical line sits.

## Key concepts
- **Session length target**: choose it from the context of play. Mobile on a commute might be two to five minutes; console sessions often one to two hours. Design the loop to complete inside that window.
- **Natural stopping points**: moments where the player can leave feeling finished (end of a level, a save, a completed run). Games that hide them risk resentful players; games that offer them with an open hook ("next time...") are more likely to be resumed.
- **Open loops**: the Zeigarnik effect, a tendency to remember unfinished tasks, is why a visible next goal draws people back. Civilization's "one more turn" works because every turn finishes something and starts something else.
- **Appointment mechanics**: events tied to time (daily quests, energy refills, crop growth in farming games). Effective, but they train players to schedule the game, which can feel like a chore.
- **Streaks**: rewards for consecutive days. Strong habit formers (Duolingo is the well-known example) and strong sources of anxiety when broken.
- **Return incentives**: welcome-back rewards, catch-up mechanics, push notifications.
- **Live-ops cadence**: a regular rhythm of new events, seasons and content updates that gives lapsed players a reason to return.

## When to use / scenarios
- Day-1 retention is fine but day-7 collapses: the first week lacks a mid-term goal. Add a short-term goal ladder, an unlockable system after a few sessions, and a visible long-term target.
- Players say "I never know when to stop": add a clear milestone and a summary screen.
- A live service has quiet periods: plan a cadence (weekly small event, seasonal large one) before the content runs out, not after.
- Do NOT use retention tools to cover up a weak core loop; push notifications bring people back once, a good loop brings them back repeatedly.

## How it works / example
Layer goals by time horizon, as in most successful live games:
- **Within a session (minutes)**: the core loop, with a reward every cycle.
- **Within a day**: two to three optional goals that fit a short visit (Destiny's daily activities, Genshin's dailies).
- **Within a week**: a larger goal that rewards players who play a few times, not daily (weekly caps instead of daily deadlines).
- **Within a season (weeks)**: a track with cosmetic and convenience rewards, plus a story or meta goal.

Respectful streak design: reward the streak but include a grace mechanism (a free freeze, a weekly instead of daily target, or partial credit) so a missed day or a sick week does not erase months of progress. Banking systems like "rested XP" in World of Warcraft invert the pressure: time away makes the next session more rewarding, rather than punishing the absence. A weekly cap on a reward track gives the same total value to a player who logs in three times as one who logs in seven.

Test your retention design with a simple question: if the player stopped playing tomorrow, would they feel they got their value? If the design only works by making stopping feel like a loss, it is a pressure mechanism, not a good game.

## Trade-offs
- **Daily vs weekly goals**: dailies maximize logins and exhaust players; weeklies respect schedules and shift the burden from "must log in" to "can plan".
- **Time-limited events vs permanent content**: limited events create urgency; permanent catch-up routes (rerun events, a store for old rewards) remove the unfair loss.
- **Notifications**: useful when opt-in and relevant (your crops are ready); harmful when they guilt or spam. Default to few, and let players configure them.
- **Energy systems**: they limit sessions deliberately and can feel considerate or exploitative depending on whether refills are sold at the moment of frustration.

## Gotchas
- FOMO design (limited-time exclusive rewards that disappear forever, streak loss, "your friends are waiting") produces short-term engagement and long-term resentment. Ethical alternative: make events rerunnable, make rewards cosmetic, and cap penalties.
- Loss aversion tricks, such as showing the exact value the player will lose by leaving, are a recognized dark pattern.
- Measure retention alongside satisfaction. A game can have excellent day-30 retention among a minority who feel trapped; surveys and sentiment reveal it.
- Session length creep: each added daily task adds minutes; check the total against the time players actually have.
- Live ops burnout, for the team and the players: a cadence you cannot sustain produces rushed content and bugs; slower and better beats faster and thinner.
- Do not tie progress to real-time waits and then sell the skip to the person the wait was designed to frustrate, especially children.

## Related
- [[core-gameplay-loop]] - retention starts with a loop worth repeating.
- [[progression-systems]] - the long-term ladder that gives sessions a direction.
- [[reward-schedules-and-loot]] - reward timing and the ethics of variable rewards.
- [[playtesting-and-metrics]] - how to measure retention and read what the numbers mean.
- [[player-motivation-and-player-types]] - different players return for different reasons.

## References
- Nicholas Lovell, "The Curve" and GamesBrief on retention and long-term engagement: https://www.gamesbrief.com/
- Celia Hodent, "The Gamer's Brain" (motivation, habits and ethics in UX): https://celiahodent.com/
- Sid Meier's Civilization series ("one more turn" design): https://en.wikipedia.org/wiki/Civilization_(series)
- The Zeigarnik effect: https://en.wikipedia.org/wiki/Zeigarnik_effect
- Jesse Schell, "The Art of Game Design" (interest curves and player goals): https://www.artofgamedesign.com/
