# Personal Web Page Design — Kevin O'Hara
**Date:** 2026-03-05
**Mantra:** "Keeping things simple. And fun."

---

## Brief

A single-page personal landing page for Kevin O'Hara, UX & Product Designer. The page is a personality-first introduction — not a portfolio. The primary goal is to connect visitors to Kevin's social profiles. No case studies, no project grid.

---

## Design Direction: "The Card"

A centered card on a warm off-white background. Minimal, confident, and quietly fun. The restraint is the statement. A single hover interaction on the photo adds delight without clutter.

---

## Layout

Single centered card, max-width 420px, centered vertically and horizontally in the viewport. Mobile-first — the card fills the screen on small devices with appropriate padding.

Card contents (top to bottom):
1. Circular photo — 120px diameter, subtle border
2. Name — Kevin O'Hara
3. Title — UX & Product Designer
4. One-liner — short, warm bio line
5. Social link pills — LinkedIn, and any other relevant profiles
6. Mantra footnote — "Keeping things simple. And fun."

---

## Typography

| Role | Font | Weight | Size |
|---|---|---|---|
| Name | Playfair Display | Bold (700) | ~32px |
| Title | DM Sans | Regular | 14px |
| One-liner | DM Sans | Italic | 15px |
| Links | DM Sans | Medium | 14px |
| Mantra | DM Sans | Italic | 11px |

Both fonts loaded from Google Fonts.

---

## Color Palette

| Element | Color |
|---|---|
| Page background | `#F5F3EE` (warm off-white) |
| Card background | `#FFFFFF` |
| Name | `#1A1A1A` |
| Title | `#888888` |
| One-liner | `#444444` |
| Link default | `#1A1A1A` |
| Link hover | `#C96A3A` (warm terracotta accent) |
| Mantra | `#BBBBBB` |

---

## Interactions

- **Page load:** Card fades up 12px with opacity 0→1 over 300ms. Subtle, not flashy.
- **Photo hover:** Gentle 3deg tilt (CSS transform rotate) + warm sepia/color overlay. Feels alive.
- **Link hover:** Underline slides in from left using a CSS pseudo-element transition.
- **No other animations.** Every interaction earns its place.

---

## Tech Stack

- Single `index.html` file
- Inline `<style>` block (no external CSS file needed)
- Vanilla JS for the photo tilt on hover (mousemove delta)
- Google Fonts via `<link>` in `<head>`
- No frameworks, no build tools, no dependencies
- Deployable to GitHub Pages, Vercel, or Netlify with zero config

---

## File Structure

```
kevin-ohara-v002/
├── index.html        (entire site — HTML + CSS + JS)
└── photo.jpg         (Kevin's headshot — to be provided)
```

---

## Placeholder Content

Until a real photo is provided, use a CSS-generated placeholder (initials "KO" on a warm gray circle).

One-liner placeholder: *"I design things people love to use."*

Social links placeholder: LinkedIn (href to be filled in).

---

## Success Criteria

- Loads instantly (no dependencies beyond Google Fonts)
- Looks great on mobile and desktop
- Photo hover interaction feels delightful, not gimmicky
- The mantra reads as a wry, confident signature — not a tagline
- A stranger can understand who Kevin is within 3 seconds of landing
