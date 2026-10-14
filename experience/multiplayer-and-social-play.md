---
title: Multiplayer and social play
category: experience
tags: [multiplayer, matchmaking, elo, glicko, trueskill, toxicity, co-op, asymmetric, guilds, spectating, social]
use_cases:
  - "new players get crushed in matchmaking and quit"
  - "how should I rate and match players by skill"
  - "players are toxic or griefing each other"
  - "should my game be co-op or competitive"
  - "how do I make players feel connected to each other"
  - "designing an asymmetric multiplayer game like one versus many"
  - "I want a multiplayer game that works without both players online at once"
status: draft
last_verified: 2026-10-14
sources:
  - https://en.wikipedia.org/wiki/Elo_rating_system
  - http://www.glicko.net/glicko/glicko.pdf
  - https://www.microsoft.com/en-us/research/project/trueskill-ranking-system/
  - https://www.schellgames.com/art-of-game-design
---

# Multiplayer and social play

## Summary
Multiplayer design shapes how people relate to each other through the game: whether they cooperate or compete, who they are matched with, how bad behaviour is discouraged, and what ties them into a community. Most retention in long-lived multiplayer games comes from relationships and fair matches more than from content. Use this topic when planning modes, matchmaking, social features or fixing a toxic or lopsided player experience.

## Key concepts
- **Cooperation vs competition**: co-op (Left 4 Dead, Deep Rock Galactic) shares a goal and rewards communication; competitive (Dota 2, Street Fighter) rewards mastery and status. Hybrids (team vs team, co-opetition such as Overcooked versus mode) mix both. Choose based on the emotions you want: camaraderie or triumph.
- **Skill rating**: a number estimating strength so matches are close. Elo updates after each game from expected vs actual result. Glicko adds a rating deviation (uncertainty), so new or inactive players move faster. TrueSkill (Microsoft) models each player as a mean and uncertainty and handles teams and free-for-all.
- **Matchmaking goals**: close matches, short queues, low latency. They conflict; tune the trade-off, do not pretend all three are free.
- **Relatedness** (self-determination theory): players stay for people. Features creating social bonds: guilds or clans, friends lists, gifting, trading, shared goals, voice or emotes.
- **Asymmetric multiplayer**: players have different roles and power (Dead by Daylight, Evolve, Mario Party-style one versus three), so balance is about experience and win rate across roles, not identical tools.
- **Spectating and async play**: watching (esports, Twitch) and non-simultaneous play (Words With Friends, Clash Royale replays, Dark Souls messages and bloodstains, Animal Crossing visits) extend multiplayer beyond synchronous sessions.
- **Anti-griefing design**: reduce the tools for harm and the payoff for it, rather than only punishing after the fact.

## When to use / scenarios
- New players churn after repeated losses: separate new players (placement matches, a beginner queue, rating uncertainty) and protect early wins.
- Win rates differ strongly by role in an asymmetric design: rebalance by fun and perceived agency, not only by win percentage.
- Voice chat harassment or sabotage: add mute and report, limit text for strangers, give positive commendations, and design mechanics that cannot be used to harass.
- Players leave once friends stop playing: add reasons to return together (guild goals, gifting, scheduled events).
- NOT everything needs a rating. For party or casual games, loose matching or bots keep queues fast and avoid ranking anxiety.

## How it works / example
**Elo update.** Expected score for player A against B is `1 / (1 + 10 ** ((Rb - Ra) / 400))`. After the match, `Ra += K * (S - E)` where S is 1 for a win, 0.5 for a draw, 0 for a loss. K controls how quickly ratings move (larger for new players).

```python
def expected(ra, rb):
    return 1 / (1 + 10 ** ((rb - ra) / 400))

def update(ra, rb, score_a, k=32):
    """Return new ratings. score_a: 1 win, 0.5 draw, 0 loss."""
    ea = expected(ra, rb)
    return ra + k * (score_a - ea), rb + k * ((1 - score_a) - (1 - ea))

a, b = 1500, 1700
print(round(expected(a, b), 3))      # ~0.24 chance for the underdog
print(update(a, b, 1))               # upset: big gain for A, big loss for B
print(update(a, b, 0))               # expected loss: small change
```

Upsets move ratings more than expected results, which is why the system converges. Elo is simple but treats all ratings as equally certain; Glicko and TrueSkill track uncertainty, which matters for new accounts and for team games where individual contribution is inferred.

**Practical matchmaking recipe**
1. Start with a rating plus uncertainty; place new players with a short placement series.
2. Search a narrow rating band first, then widen the band as queue time grows (state the maximum acceptable gap).
3. Prefer fair-to-close over instant for ranked; prefer instant for casual.
4. Hide or soften the raw number if it creates anxiety (many games show ranks and divisions rather than a raw rating).

**Reducing toxicity by design**
- Remove channels harassers use: no free-text chat for strangers or opt-in only, ping and wheel systems as the main communication (Overwatch, Apex Legends, Rocket League quick chat).
- Make cooperation cheaper than blame: shared objectives, revive mechanics, rewards for assists and support.
- Make reporting easy and visibly acted on; reward good behaviour (endorsements) as well as penalising bad.
- Avoid scoreboards that single out the lowest performer in a team; they invite scapegoating.

**Social glue examples**: guilds with shared chests or raids (World of Warcraft), gifting with a daily cap (Animal Crossing, Clash of Clans donations), trading economies (Path of Exile, Diablo 2 trade culture), shared building (Minecraft servers), and recurring events players schedule together.

## Trade-offs
- **Skill-based vs engagement-based matching**: pure skill matching makes everyone win about half the time, which can feel bland; some games bias to protect new or struggling players, trading fairness for retention. Be transparent where practical.
- **Open chat vs safety**: open communication builds community and also abuse. Default to restricted channels for strangers, open ones for friends.
- **Asymmetric power vs parity**: asymmetric roles add novelty and spectacle but double the balance and onboarding workload and strain queue times if one role is unpopular.
- **Ranked pressure vs casual fun**: ranked gives goals and status but amplifies toxicity; offer a clearly separate casual mode.
- **Real-time vs asynchronous**: async lowers scheduling friction and server needs but weakens immediacy; live modes feel exciting but need critical mass.
- **Trading and gifting**: they build bonds yet open the door to scams, real-money markets and economy distortion; see [[game-economy-sources-and-sinks]].

## Gotchas
- Rating systems fail when teams are small or contributions are unmeasurable; ratings inferred from win/loss only will be noisy in big team games.
- Smurfing and boosting break matchmaking; use uncertainty and fast-rising ratings for suspiciously strong new accounts.
- Queue-dodging when ranked rewards are tied to a lopsided penalty. Penalise leaving, but forgive disconnects caused by network failure.
- Snowballing losses in team games produce "surrender at 20" behaviour; see [[feedback-loops-and-snowballing]] and add comeback mechanics.
- Social features with no content depend on a critical mass. A guild system in a game with 50 concurrent players is a ghost town; seed with bots, NPC guilds or solo-friendly content.
- Over-rewarding top performers publicly (MVP screens) can encourage selfish play in team modes; credit teamwork actions too.
- Anonymous cooperation without any communication tools yields frustration; provide at least pings or emotes.

## Related
- [[player-motivation-and-player-types]] - socializers, achievers and killers want different multiplayer experiences.
- [[feedback-loops-and-snowballing]] - comeback mechanics and snowball control in competitive matches.
- [[game-balance]] - asymmetric roles and competitive balance need ongoing tuning.
- [[retention-and-session-design]] - social ties are among the strongest retention levers.
- [[game-economy-sources-and-sinks]] - trading and gifting affect the economy.

## References
- Elo rating system overview: https://en.wikipedia.org/wiki/Elo_rating_system
- Mark Glickman, "The Glicko system": http://www.glicko.net/glicko/glicko.pdf
- Microsoft Research, TrueSkill ranking system: https://www.microsoft.com/en-us/research/project/trueskill-ranking-system/
- Jesse Schell, "The Art of Game Design: A Book of Lenses" (chapters on players and communities): https://www.schellgames.com/art-of-game-design
- Richard Bartle, "Hearts, Clubs, Diamonds, Spades: Players Who Suit MUDs" (player types in social worlds).
