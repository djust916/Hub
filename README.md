# 👑 CORNER KINGS

*A mobile-playable RTS about running your block.*

Two crews. Five corners. One block. Hold corners to earn cash, recruit your
crew, build Respect, and either shut down the rival clubhouse or lock the
whole block down. Matches run 3–6 minutes, one thumb, one screen.

**📐 Full game design document:** [DESIGN.md](DESIGN.md)
**🕹️ Playable prototype:** [`index.html`](index.html) — single file, zero
dependencies, works in any modern mobile or desktop browser.

## Play it

**On your phone (easiest):** enable GitHub Pages for this repo
(Settings → Pages → deploy from branch), then open the page URL on your phone.

**Locally:**

```bash
python3 -m http.server 8080
# then open http://localhost:8080 (or your computer's LAN IP from a phone)
```

Or just double-click `index.html` — no build step, no server required.

## How to play

| Action | Control |
|--------|---------|
| Select a squad | Tap one of your units (grabs nearby crew too) |
| Box select | Drag across the street |
| Select everyone | 🔊 **SQUAD UP** button |
| Move / attack | With a squad selected, tap anywhere (tap an enemy to focus them) |
| Recruit | Bottom-bar buttons (spawn at your clubhouse) |

**The crew:**

- 🧢 **Youngin** ($60) — fast, fragile, captures corners 2× faster
- 💪 **Muscle** ($120) — your line-holder
- 🏋️ **Big Homie** ($240) — slow-rolling tank
- 👑 **The OG** (✊100 Respect) — hero unit; nearby crew fight 25% harder

**The block:**

- Stand on a corner uncontested to capture it. Each corner pays **+$5/sec**;
  the center 🏀 court pays double.
- Out-hold the rival and you earn **Respect ✊** over time; captures and
  knockouts pay Respect too. Respect buys the OG.
- Clubhouses fight back — don't rush a porch without numbers.

**Win** by demolishing the rival clubhouse, or by holding **all five corners
for 15 seconds** (🔒 Block Locked).

## Status

v1 prototype: full core loop (economy → recruit → capture → victory), three
unit types + hero, utility AI rival, touch + mouse controls. See
[DESIGN.md](DESIGN.md) §12 for what's in scope and the roadmap (campaign,
new units like Auntie and the Ice Cream Truck, match powers, async PvP).
