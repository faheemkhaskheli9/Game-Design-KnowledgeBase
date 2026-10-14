---
title: Game feel and juice
category: experience
tags: [game-feel, juice, screen-shake, hit-stop, input-latency, coyote-time, jump-buffering, polish, celeste, vlambeer]
use_cases:
  - "the controls feel floaty, stiff or unresponsive even though the numbers look right"
  - "hits and pickups feel weak, like nothing happens when I attack"
  - "the platformer feels unfair because jumps get eaten near ledges"
  - "how much screen shake, particles and sound should I add"
  - "the game works mechanically but is not satisfying to play moment to moment"
status: draft
last_verified: 2026-10-14
sources:
  - http://www.game-feel.com/
  - https://www.youtube.com/watch?v=AJdEqssNZ-U
  - https://www.youtube.com/watch?v=Fy0aCDmgnxg
  - https://github.com/NoelFB/Celeste
---

# Game feel and juice

## Summary
Game feel is the tactile, moment-to-moment quality of controlling something in a game: how fast it answers, how it accelerates, how it collides, how it sounds and looks when you act. Juice is the layer of redundant feedback (shake, particles, sound, squash and stretch, hit-stop) that makes actions feel powerful. Use this topic when a game is mechanically correct but dull to touch, or when a punishing-feeling game turns out to be an input-handling problem rather than a difficulty problem.

## Key concepts
- **Swink's three pillars** (Steve Swink, "Game Feel"): real-time control (the player's input is answered within a perceptible-instant), simulated space (the thing moved has believable mass, collision and momentum), and polish (effects that exaggerate the result without changing the simulation).
- **Input responsiveness**: the delay between press and visible reaction. Anything the player feels is "lag" kills feel faster than any missing effect. Respond on the frame of the input, even if the full animation takes longer (start the jump immediately, play the anticipation frames after).
- **Acceleration curves**: instant top speed feels twitchy and digital; slow ramps feel heavy. Mario-style run acceleration, faster deceleration than acceleration, and variable jump height (release early to jump lower) give "tight" feel.
- **Forgiveness windows**: coyote time (you may still jump a few frames after leaving a ledge) and jump buffering (a jump pressed a few frames before landing fires on landing). Celeste uses both, and its input code is public (see sources). Typical windows are a handful of frames at 60 fps; tune by playtest, do not copy a number blindly.
- **Juice**: screen shake, hit-stop (freezing both attacker and target for a few frames on impact), particles, flashes, squash and stretch, camera kick, controller rumble, layered audio. Redundant feedback on a single event is the point.
- **Feedback for every action**: each input should produce at least a visual and an audio acknowledgment; important events (kill, level-up, pickup) get several.

## When to use / scenarios
- Playtesters say "it feels cheap / floaty / sluggish" but cannot name why: audit input latency, acceleration, then feedback.
- A platformer or action game feels "unfair" at ledges and landings: add coyote time and buffering before touching difficulty.
- A weapon or ability is balanced but nobody enjoys it: add hit-stop, shake and a punchy sound before buffing damage.
- Prototype stage: cheap juice sells the core loop in a pitch or early playtest (Vlambeer's "The art of screenshake" talk turns a flat shooter into a satisfying one purely by adding effects).
- NOT the fix when the underlying verb is uninteresting; juice amplifies a good action, it cannot rescue a dull one. See [[prototyping-and-finding-the-fun]].
- NOT for turn-based or UI-heavy games in the same way: there, juice means timing, animation snappiness and clear sound cues for state changes, not camera shake.

## How it works / example
The Vlambeer / Jonasson-Purho recipe, applied in order to one "shoot" action:

```
press fire
  -> fire on the same frame (no input delay)
  -> muzzle flash + shell casing particle
  -> recoil kick on the player sprite and camera
  -> screen shake (small, short)
  -> bullet impact: enemy flashes white, knockback, hit-stop 2-4 frames
  -> enemy death: bigger shake, debris particles, louder layered sound
```

A common shake model is "trauma": events add to a 0-1 trauma value that decays over time, and the shake magnitude is trauma squared, so small hits are subtle and stacked hits are violent. (Squirrel Eiserloh's GDC talk on camera maths popularized this.)

```python
import math, random

def shake_offset(trauma, t, max_px=12.0):
    """Camera offset for this frame. trauma in [0,1]; t is time in seconds."""
    mag = max_px * trauma * trauma
    # smooth-ish noise from sines; swap for Perlin noise if available
    x = math.sin(t * 47.0 + 1.3) * math.sin(t * 13.0)
    y = math.sin(t * 53.0 + 2.1) * math.sin(t * 11.0)
    return mag * x, mag * y

def decay(trauma, dt, rate=1.5):
    return max(0.0, trauma - rate * dt)

trauma = 0.0
trauma = min(1.0, trauma + 0.3)   # a hit lands
for frame in range(5):
    print(shake_offset(trauma, frame / 60))
    trauma = decay(trauma, 1 / 60)
```

Coyote time and buffering in pseudo-logic (counters in seconds or frames):

```
if on_ground: coyote = COYOTE_TIME else: coyote -= dt
if jump_pressed: buffer = BUFFER_TIME else: buffer -= dt
if buffer > 0 and coyote > 0: jump(); buffer = 0; coyote = 0
```

Real examples: Celeste (forgiveness windows plus tiny corner-correction so you slide past ledge corners), Super Meat Boy (instant response, tiny respawn), Hades and God of War (hit-stop on every strike), Vlambeer's Nuclear Throne and Luftrausers (shake, recoil, flash on everything).

## Trade-offs
- **Realism vs responsiveness**: physically plausible momentum feels weighty but slow; most successful action games cheat toward the player (instant turn, generous hitboxes in the player's favor).
- **Forgiveness vs precision**: wider windows reduce frustration but blunt skill expression in hardcore precision games; Celeste exposes assist options rather than forcing one setting.
- **Juice vs readability**: every effect competes for attention. In dense combat, clarity of enemy telegraphs beats spectacle.
- **Hit-stop vs flow**: longer freezes sell heavy hits but interrupt rhythm in fast combat; scale by attack weight.
- **Authored vs procedural effects**: hand-tuned shake per weapon feels best; a global trauma system is faster and consistent.

## Gotchas
- Layering juice before fixing latency: the game then feels "loud but laggy". Measure input-to-photon first (display, vsync, buffered frames all add delay).
- Shake that never stops or cannot be disabled causes motion sickness; always ship an intensity slider and reduced-motion option (accessibility).
- Frame-rate dependent tuning: coyote windows, acceleration and decay written per frame change with refresh rate; use delta time.
- Juice on everything equals juice on nothing; reserve the biggest effects for the rarest, most important events so they stay meaningful.
- Screen shake that moves the HUD or the aim reticle hurts accuracy; shake the world camera, not the UI.
- Audio is half of feel. A silent hit-stop feels like a bug; add pitch and volume variation so repeated sounds do not fatigue.
- Hit-stop applied to the player on getting hit can feel like lag; use it for the attacker's successful hits and keep input live where possible.

## Related
- [[core-gameplay-loop]] - the verb you are polishing is repeated thousands of times, so its feel dominates the loop.
- [[prototyping-and-finding-the-fun]] - add juice early in prototypes to judge the verb fairly.
- [[combat-and-encounter-design]] - hit feedback and telegraphs are the core of combat readability.
- [[flow-and-difficulty-curves]] - input forgiveness changes perceived difficulty more than numeric tuning does.
- [[playtesting-and-metrics]] - feel is tested by watching hands and faces, not by dashboards.

## References
- Steve Swink, "Game Feel: A Game Designer's Guide to Virtual Sensation" (2008); companion site http://www.game-feel.com/
- Jan Willem Nijman (Vlambeer), "The art of screenshake" talk: https://www.youtube.com/watch?v=AJdEqssNZ-U
- Martin Jonasson and Petri Purho, "Juice it or lose it" talk: https://www.youtube.com/watch?v=Fy0aCDmgnxg
- Celeste source code (player movement, coyote and buffer handling): https://github.com/NoelFB/Celeste
- Squirrel Eiserloh, GDC "Math for Game Programmers: Juicing Your Cameras with Maths" (trauma-based shake).
