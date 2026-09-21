# Diya Yatra — Project Handoff Summary

This document summarizes the full conversation that produced `index.html`, a
single self-contained HTML/Canvas/JS game, so it can be handed to another
AI assistant for continued work.

## Original context

The project started from a hackathon/contest brief for a game called
**"Ekarekha — One Line, One Rangoli"**: a single-stroke Eulerian-circuit
puzzle where the player traces a rangoli pattern without lifting their
finger, built with a hard deadline (same-day submission), React+TS+Vite
shell over raw Canvas 2D, no backend, no accounts, localStorage only, one
game mode, procedural art only, and a strict cultural-respect rule: rangoli
and kolam patterns are the gameplay object, and if Ganesha appears at all
it must be as a **still background murti silhouette — never traced, never
a gameplay target, never touched by gameplay, never harmed or mocked.**

## What was actually built, in order

1. **Ekarekha (rangoli puzzle)** — first build. Single HTML file (not
   React/Vite, to save time under deadline pressure), vanilla JS + Canvas,
   5 hand-crafted Eulerian-circuit patterns (guaranteed solvable by
   construction — loops chained at shared vertices, never by trial and
   error), 90-second timer, combo scoring, localStorage best score.
   Published as a live Claude Artifact link for instant testing/sharing.

2. **Pivot to a Hill Climb Racing–style game.** The user didn't like the
   puzzle and asked for something like Hill Climb Racing instead, but
   still tied to the same contest (so the cultural-respect rules still
   apply). Rebuilt from scratch as **"Diya Yatra — Hills of Light"**:
   - Side-scrolling 2-wheel arcade physics (not a full rigid-body engine):
     terrain height is a layered-sine function, wheel contact points set
     the cart's target angle/height, gravity component from slope affects
     speed, simple drag/friction, throttle via a large on-screen GAS
     button (also Space/ArrowUp/ArrowRight on desktop).
   - Fuel drains with distance; collecting glowing diya pickups refuels.
   - Crash conditions: fuel hits zero, or the cart tips past ~70°.
   - Score = distance in meters; personal best saved in localStorage.
   - The rangoli theme was folded into the *visuals* instead of the core
     mechanic: the rear wheel leaves a fading powder trail in the palette
     colors, the terrain surface has a kolam-dot texture, temple-dome
     silhouettes parallax in the background.

3. **Added a Ganesha murti silhouette**, per the brief's own cultural-
   respect exception: a still, glowing background shrine silhouette that
   warms in color as distance increases. Purely decorative, never
   interactive.

4. **Vehicle + task system pass:**
   - Vehicle got a ground shadow, canopy arch, small flag, marigold
     garland trim, gold hubcaps, and a squash/stretch suspension effect
     on landing.
   - Added a rolling **task/quest system**: 3 active objectives shown as
     a HUD checklist (distance milestones, diya-collection counts, etc.),
     each rewarding a fuel refill on completion and auto-replaced with a
     new randomized task shortly after (instead of a static list you
     complete once).

5. **Sky pass:** replaced the flat 3-stop gradient with a richer
   multi-stop night gradient, two-layer twinkling star field, drifting
   low-opacity clouds, a haloed moon, a warm horizon glow, and a string
   of flickering festival lantern lights along the top edge — all
   procedural canvas drawing, no image assets.

6. **Murti redesign.** The user flagged (with a screenshot) that the
   Ganesha silhouette read as a blurry glowing blob rather than a
   figure. Fixed by drawing it as a solid silhouette fill with a thin
   gold rim-light stroke per body part (ears drawn behind the head, a
   small crown added for clarity) instead of one large blurred glow.

7. **Content expansion (most recent changes):**
   - **Modak pickups**: a second collectible type (Ganesha's favorite
     sweet) mixed in with diyas (~35% spawn chance), worth a larger fuel
     refill, tracked in its own counter, shown in the HUD as
     `🪔 diyas  🍡 modaks`.
   - **Mooshika (the mouse/rat, Ganesha's vehicle)**: added as a small,
     purely decorative animal silhouette that idles beside each roadside
     shrine. Not collectible, not interactive — consistent with the
     "never touched by gameplay" rule applied to the murti.
   - **New "modaks" task type**, added to the same rolling task-rotation
     system.
   - **"Tales of Ganesh"**: a short collection of five respectful,
     public-domain-style story summaries (the elephant head origin, the
     broken tusk and the Mahabharata, the race around the world, the
     meaning of Mooshika, and Ganesha as remover of obstacles), written
     in original wording. Accessible two ways:
     - A collapsible panel on the title screen (like the existing
       "How to Play" box), listing all five.
     - An in-game "lore toast" that reveals one story snippet each time
       the player passes a roadside shrine, cycling through the list.

## Known open items / things worth double-checking next

- Physics constants (`THROTTLE_ACCEL`, `GRAVITY_FACTOR`, `DRAG`,
  `FUEL_RATE`, `MAX_TILT`) are tuned by feel, not measurement — worth
  testing on a real phone and adjusting.
- Shrine/pickup spacing constants (`SHRINE_SPACING`, `PICKUP_SPACING`)
  are similarly estimated.
- No audio was implemented (explicitly cut early for time).
- No dedicated Pause screen beyond a simple pause/resume toggle button.
- The submission's non-code requirements (demo video, GitHub repo push,
  README, team details, final live-link verification) were discussed but
  are the user's responsibility to finish outside this tool.
- The live, currently-published version of this file is hosted at a
  Claude Artifact link; that hosting is specific to Claude.ai and won't
  carry over elsewhere — `index.html` in this zip is the same file and
  can be opened directly in a browser or deployed anywhere static HTML
  is servable (GitHub Pages, Netlify, etc.).

## File in this archive

- `index.html` — the complete, current, self-contained game. No build
  step required; open directly in a browser, or deploy as a static file.
