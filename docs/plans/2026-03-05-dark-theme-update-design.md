# Dark Theme Update Design
**Date:** 2026-03-05
**Source reference:** kevinohara.com
**Approach:** Near-exact match (Approach A)

## Objective
Update `index.html` to match kevinohara.com's dark aesthetic: color palette, photo treatment (animated gradient ring), and all four social/contact links.

## Color Palette

| Token    | Old value  | New value              |
|----------|------------|------------------------|
| `--bg`   | `#F5F3EE`  | `#0e0f11`              |
| `--card` | `#FFFFFF`  | `#16181c`              |
| `--name` | `#1A1A1A`  | `#e8e6e2`              |
| `--title`| `#888888`  | `#7a7772`              |
| `--body` | `#444444`  | `#e8e6e2`              |
| `--muted`| `#BBBBBB`  | `#7a7772`              |
| `--accent`| `#C96A3A` | `#c8b89a`              |
| `--border`| (none)    | `rgba(255,255,255,0.07)`|

## Typography
- Replace Google Font `Playfair Display` with `DM Serif Display` for `.name`
- Keep `DM Sans` for all other text
- Update `font-weight` on DM Sans import to include `300` weight

## Photo
- Shrink from `120px` → `96px`
- Remove `::after` hover overlay
- Remove 3D tilt mousemove/mouseleave JS
- Add `@keyframes spin` rotating conic-gradient ring using `--accent` color, `8s linear infinite`
- Ring implemented as a pseudo-element or wrapper with `conic-gradient` and `border-radius: 50%`
- Keep existing `assets/kevin-ohara-profile-gemini.PNG` and initials (`KO`) fallback

## Links
Replace single LinkedIn link with four links in a vertical list:

| Label     | URL                                        |
|-----------|--------------------------------------------|
| Instagram | https://www.instagram.com/kevinoh15        |
| Facebook  | https://www.facebook.com/kevin.ohara.15    |
| LinkedIn  | https://www.linkedin.com/in/kevinoh15/     |
| Email     | mailto:kevinoh15@gmail.com                 |

**Link styles:**
- Full-width rows (not pill buttons)
- Icon left + label center + arrow right
- Hover: translateY(-2px), background `rgba(200,184,154,0.07)`, icon background changes
- Staggered fade-in animation with delay per item

## Preserved
- Card layout, `max-width: 420px`, `border-radius: 12px`
- Entry rise animation (0.3s)
- Bio: "I design things people love to use."
- Mantra: "Keeping things simple. And fun."
- Mobile breakpoint (`max-width: 480px`) full-bleed behavior
