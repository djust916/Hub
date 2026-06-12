# CORNER KINGS — Mobile RTS Game Design Document

> *"Run your block. Stack your paper. Earn your respect."*

A touch-first real-time strategy game set in a stylized inner-city neighborhood.
Two crews compete for control of the block — corner by corner — through hustle,
recruitment, and good old-fashioned scraps.

---

## 1. High Concept

**Genre:** RTS-lite (lane-free, territory control)
**Platform:** Mobile (portrait), HTML5 / wrappable for iOS & Android
**Session length:** 3–6 minute matches
**Audience:** Casual-to-mid-core strategy players, 13+

You run a crew on one end of the block. A rival crew runs the other end.
Between you: corners. Whoever holds a corner earns cash from it. Cash recruits
crew members. Crew members take more corners — or march on the rival's
clubhouse and shut them down for good.

### Design pillars

1. **One thumb, full control.** Every action is a tap or a drag. No hotkeys,
   no camera juggling — the whole block fits on one screen.
2. **The block is the economy.** No mining, no farms. Territory IS income.
   Every fight is a fight over money, which keeps matches aggressive.
3. **Style over grit.** The tone is block-party, not crime drama. Scraps are
   cartoon scuffles (dust clouds, stars, "OOF!"). Knocked-out units dust
   themselves off and walk home. No weapons, no drugs, no death.
4. **Respect is the meta-resource.** Cash buys bodies; Respect buys legends.

---

## 2. Setting & Tone

The game takes place on **one city block** rendered like a living mural:
bold colors, chunky outlines, gold-hour lighting, boomboxes, double-dutch
ropes, dominoes tables, ice-cream trucks. Think *Hey Arnold!* meets
*Streets of Rage* character design with a lo-fi hip-hop soundtrack.

The conflict is a **neighborhood rivalry** — two crews competing for who
*runs* the block (who gets the corner-store hookups, who headlines the block
party, whose name is on the wall). It's competitive and trash-talky, never
grim. Writing leans on humor and authentic neighborhood culture: the corner
store, the barbershop, the auntie who sees everything, the OG who's
respected by both sides.

**Content guardrails (intentional):** no firearms, no drugs, no police
encounters, no gang iconography. Crews are distinguished by color and style
(tracksuits vs. throwback jerseys). This keeps the game store-safe (ESRB E10+
/ PEGI 7 target) and keeps the culture celebratory instead of stereotyped.

---

## 3. Core Loop

```
Hold corners → earn Cash → recruit crew → take more corners
     ↑                                          |
     └── win scraps / capture → earn Respect ←──┘
                  ↓
        unlock the OG (hero unit) + powers
                  ↓
      push the rival's Clubhouse → WIN
```

**Victory:** destroy the rival Clubhouse, **or** hold every corner on the
block simultaneously for 15 seconds ("Whole Block Locked").

**Defeat:** your Clubhouse falls.

---

## 4. Resources

| Resource | Earned by | Spent on |
|----------|-----------|----------|
| **Cash 💵** | Passive trickle + per-corner income | Recruiting units |
| **Respect ✊** | Capturing corners, winning scraps | The OG (hero), match powers |

- Base income: $8/sec. Each held corner: +$5/sec.
- Holding more corners than the rival also grants +1 Respect/sec ("running the block").

There is deliberately **no third resource and no tech tree** in v1 — depth
comes from map control timing, not from build orders.

---

## 5. Units (the Crew)

All units auto-scrap when enemies come close. Tap to select, tap to send.

| Unit | Cost | Role | Stats sketch |
|------|------|------|--------------|
| 🧢 **Youngin** | $60 | Runner / capper | Fast, fragile, captures corners 2× faster |
| 💪 **Muscle** | $120 | Bruiser | Solid HP & damage, the line-holder |
| 🏋️ **Big Homie** | $240 | Tank | Slow, huge HP, knockback slap (mini-AoE) |
| 👑 **The OG** | ✊100 Respect | Hero (one at a time) | Strong, fast, nearby crew fight harder (aura) |

**Counter-triangle (soft):** Youngins out-run Big Homies, Muscle beats
Youngins pound-for-pound, massed Youngins swarm Muscle, Big Homie scatters
swarms. The OG breaks stalemates but paints a target on himself — KO'ing the
enemy OG awards a big Respect bounty.

### Roadmap units (v2+)
- 🚲 **Pedal Boy** — scout on a BMX, reveals fog (if fog is added), harasses.
- 🎤 **Hype Man** — support; boombox aura speeds nearby allies.
- 🍦 **Ice Cream Truck** — slow mobile heal station, both teams' kids chase it (neutral aggro magnet).
- 👵 **Auntie** — area denial; nobody scraps on Auntie's stoop. Both teams path around her. Comedy + tactical wall.

---

## 6. The Map: One Block

Portrait orientation, single screen, no camera scrolling (pillar #1).

```
┌─────────────────────────┐
│   RIVAL CLUBHOUSE  🏠   │   ← enemy spawn
│  [corner]     [corner]  │
│        [corner]         │   ← center corner: worth double
│  [corner]     [corner]  │
│    YOUR CLUBHOUSE  🏠   │   ← player spawn
└─────────────────────────┘
```

- **5 corners** in v1: four side corners + a **center corner worth 2×
  income**, which becomes the natural mid-fight magnet.
- Corners are captured by standing on them uncontested; capture progress
  shows as a filling ring. Contested corners freeze progress.
- Streets between corners are open ground — flanking is just walking wide.

**Map roadmap:** Block layouts as unlockable maps — "The Projects" (vertical,
chokepoints), "Marketplace" (rich center, poor sides), "Two Bridges" (split
lanes).

---

## 7. Controls (Touch UX)

| Gesture | Action |
|---------|--------|
| Tap own unit | Select it **and its nearby squad** (group-grab radius) |
| Drag on field | Box-select |
| Tap ground | Move selected (attack-move: they scrap anything en route) |
| Tap enemy/building | Focus target |
| Tap 🔊 "SQUAD UP" button | Select entire crew |
| Tap recruit buttons (bottom bar) | Spawn unit at Clubhouse |

Design notes:
- **Fat targets:** units have a generous invisible tap radius (44pt+).
- **Squad-grab select** replaces ctrl-groups: one tap grabs a cluster, which
  is how mobile players naturally think ("send *those* guys").
- All recruit buttons live in one bottom bar with cost + disabled state —
  the only UI chrome on screen besides the resource strip.

---

## 8. Match Powers (Respect sinks, v2)

Castable abilities to give late-game Respect somewhere to go:

- ✊25 **"Posted Up"** — selected units hold ground with +50% defense, 8s.
- ✊40 **"Block Party"** — all corners you hold pay out 5× for 6s.
- ✊60 **"Old Heads Pull Up"** — two veteran Muscles spawn free at any corner you hold.

---

## 9. AI Opponent

Simple utility AI, tuned to feel like a hungry rival, not a chess engine:

1. **Economy first:** always recruits when it can afford its desired comp
   (rotates Youngin → Muscle → Youngin → Big Homie).
2. **Corner pressure:** idle units are sent to the nearest corner not owned
   by the AI, weighted toward the center corner.
3. **Power sense:** if the AI's crew outnumbers the player's by 3+, it
   commits everything to the player's Clubhouse. If outnumbered, it turtles
   on its richest corner.
4. **Rubber-band difficulty (campaign):** income multiplier 0.8×–1.2× by level.

---

## 10. Progression & Modes

- **v1 (this prototype):** single skirmish vs AI. Pure mechanics proof.
- **v2 Campaign — "Take Back the Block":** 20 levels across the
  neighborhood. Story: a slick out-of-town crew is buying up corners and
  pushing folks out; you unite the block's characters (each level recruits a
  new unit type into your roster) to run them off. The campaign's heart is
  community: you win by making the block *yours* again.
- **v3 PvP:** async ghost battles first (fight a recording of another
  player's strategy), live 1v1 later.
- **Cosmetics only monetization:** crew fits (fits = outfits), clubhouse
  murals, victory dances, boombox tracks. No pay-for-power — pillar #3's
  tone dies the moment whales can buy the block.

---

## 11. Art & Audio Direction

- **Art:** flat 2D, thick outlines, graffiti-styled UI numerals, gold-hour
  palette (warm asphalt, teal shadows). Prototype uses emoji as placeholder
  sprites — they read shockingly well at mobile size.
- **Audio:** lo-fi hip-hop loop (90 BPM) for build phase; beat switches when
  a Clubhouse takes damage. SFX: basketball bounce = recruit, spray-can
  rattle = capture, record scratch = defeat, air horn = victory.

---

## 12. Prototype Scope (built in this repo)

`index.html` — a complete, dependency-free, single-file HTML5 prototype:

- Full core loop: income → recruit → capture → win/lose
- 3 recruitable units + the OG hero, with the counter-triangle stats
- 5-corner map with double-value center
- Touch + mouse controls: tap/squad-grab/box-select/move/attack
- The utility AI from §9 (economy, corner pressure, power-sense attacks)
- Cash + Respect economy, both victory conditions, restart flow

Open it on a phone (or serve via GitHub Pages) and play.
