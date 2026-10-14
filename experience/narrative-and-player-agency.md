---
title: Narrative and player agency
category: experience
tags: [narrative, story, agency, ludonarrative, environmental-storytelling, branching, emergent-narrative, consequences]
use_cases:
  - "players skip all my cutscenes and dialogue"
  - "the story and the gameplay feel disconnected"
  - "should my story branch or stay linear"
  - "how do I make player choices feel like they matter"
  - "how do I tell a story without text or cutscenes"
  - "what is the difference between embedded and emergent narrative"
status: draft
last_verified: 2026-10-14
sources:
  - https://clicknothing.typepad.com/click_nothing/2007/10/ludonarrative-d.html
  - https://www.gamedeveloper.com/design/environmental-storytelling-creating-immersive-3d-worlds-using-lessons-learned-from-the-theme-park-industry
  - https://www.schellgames.com/art-of-game-design
---

# Narrative and player agency

## Summary
Game narrative is the story a player experiences through actions as well as words. The central design tension is authorial control (a crafted story) against player agency (the player's own decisions). Use this topic to decide how much story the game carries, where it lives (cutscenes, space, systems, choices), and how to keep play and story pulling the same way.

## Key concepts
- **Ludonarrative harmony and dissonance**: Clint Hocking coined "ludonarrative dissonance" for a conflict between what the mechanics reward and what the story claims (his example was BioShock's selfish game logic versus its altruistic narrative). Harmony means mechanics and story say the same thing.
- **Embedded vs emergent narrative** (Salen and Zimmerman's terms in Rules of Play, after Marc LeBlanc): embedded stories are pre-authored and delivered (The Last of Us); emergent stories arise from systems and player choices (RimWorld, Dwarf Fortress, The Sims, XCOM's named soldiers). Most games blend them.
- **Environmental storytelling**: telling story through space and objects (Don Carson's theme-park-derived formulation). A skeleton clutching a key by a locked door tells a story with no text. Dark Souls item descriptions and BioShock's audio diaries use this.
- **Agency**: the player's felt ability to make meaningful, effective decisions. Agency is about intention-to-outcome: "I wanted this, I did that, the world responded."
- **Branching vs illusion of choice**: true branching multiplies content cost. Many games use "foldback" structures (branch, then reconverge) and reactive text, which still feels responsive if the game acknowledges the choice.
- **Consequences**: delayed, visible results of earlier choices produce the strongest sense of agency (Undertale's pacifist/genocide routes remember your actions, even across resets; Disco Elysium's skill-voices and failed checks open new story paths instead of dead ends).
- **Skippable by design**: assume many players skip text. Critical information must survive that.

## When to use / scenarios
- Playtest data shows high cutscene-skip rates or unread quest text: restructure delivery.
- Players "do not care" about the protagonist: tie story beats to verbs the player performs, not just watched scenes.
- Planning a branching story: decide the budget first, then pick a structure.
- Systems-heavy sim or strategy game: lean on emergent narrative, add hooks that make events narratable (names, relationships, memorable failures).
- NOT every game needs a story. A pure arcade or puzzle game may be better with minimal framing; tacked-on narrative hurts pacing.

## How it works / example
**Pick a delivery layer by cost and player attention**

```
layer                  cost    skippable?   example
cutscene / dialogue     high    yes          Mass Effect conversations
in-play dialogue        med     partly       Half-Life 2 (never takes control)
environmental detail    med     no           Dark Souls, Fallout, Gone Home
mechanical expression   low*    no           Papers, Please, Return of the Obra Dinn
systemic / emergent     low*    no           RimWorld, Crusader Kings
```
*low content cost, high design cost.

**Writing for players who skip.** Put the actionable information (where to go, what to do) in the UI or in the world; use dialogue for flavour and depth. Keep lines short and give the player something to do while a line plays (Half-Life 2, Portal, Hades, which delivers story in short bursts between runs). Let players interrupt, fast-forward or replay a log.

**Making choices feel real without infinite content.**
1. Name the choice's cost: the player should give something up.
2. Reflect it: NPCs mention it, a location changes, an option closes or opens.
3. Delay some consequences so the player connects cause and effect later.
4. Be honest: do not promise consequences the game will not deliver (a "this will be remembered" banner that does nothing erodes trust).

**Ludonarrative checks.** If the story says "you are a fragile survivor", do mechanics make resources scarce and combat risky (The Last of Us)? If the story says "you hate killing", do the systems penalize or avoid rewarding it (Undertale, Dishonored's chaos system)? Where story and systems disagree, either change the mechanic reward or reframe the story to explain the contradiction (a self-aware protagonist, an unreliable narrator).

**Emergent narrative aids.** RimWorld's storyteller picks events to shape tension, and its colonists have traits and relationships so a mundane death becomes a story. XCOM lets you name soldiers and keeps them alive across missions; a lost veteran stings because of that bookkeeping.

## Trade-offs
- **Control vs freedom**: authored scenes guarantee pacing and emotional beats; open systems create personal stories that feel earned but are not guaranteed to be dramatic.
- **Breadth vs depth of branching**: a few deeply reactive choices beat many shallow ones; players remember the big moments.
- **Illusion vs real choice**: the illusion of choice is cost-effective and often enough; players who replay or compare notes will find the seams, so avoid pretending when the choice is decorative.
- **Story as reward vs story as context**: gating narrative behind skill motivates some players and locks out others; offer an easy mode or story mode.
- **Player-character voice**: a voiced protagonist has personality but may clash with the player's choices; a silent one invites projection but limits depth.

## Gotchas
- Moral choices with an obviously "good" option; tension requires costs on every side.
- Forced cutscene sections that take control at moments the player just earned; interactivity is the medium's strength.
- Mechanics rewarding behaviour the story punishes, undermining emotional beats (dissonance).
- Hidden branching: players cannot appreciate content they never see. Make the paths discoverable, or accept that replay is the audience.
- Over-explaining lore in dialogue boxes instead of surfacing it through objects and places.
- Continuity bugs in branching narratives: track state centrally (flags), and test every combination of major flags.
- Quest logs that substitute for comprehension: if a player must open a menu to know what to do, the in-world signposting failed.

## Related
- [[meaningful-choices]] - choices that matter are the mechanical core of agency.
- [[level-design-and-pacing]] - spaces carry environmental storytelling and set emotional rhythm.
- [[feedback-loops-and-snowballing]] - emergent stories often come from systemic feedback loops.
- [[player-motivation-and-player-types]] - some players are story-driven; others skip it entirely.
- [[onboarding-and-tutorials]] - exposition and teaching compete for the same attention in the first hour.

## References
- Clint Hocking, "Ludonarrative Dissonance in Bioshock": https://clicknothing.typepad.com/click_nothing/2007/10/ludonarrative-d.html
- Don Carson, "Environmental Storytelling: Creating Immersive 3D Worlds Using Lessons Learned from the Theme Park Industry" (Gamasutra/Game Developer): https://www.gamedeveloper.com/design/environmental-storytelling-creating-immersive-3d-worlds-using-lessons-learned-from-the-theme-park-industry
- Jesse Schell, "The Art of Game Design: A Book of Lenses" (story and world chapters): https://www.schellgames.com/art-of-game-design
- Katie Salen and Eric Zimmerman, "Rules of Play: Game Design Fundamentals" (MIT Press, 2003) - embedded vs emergent narrative.
- Lee Sheldon, "Character Development and Storytelling for Games" (2nd ed.).
