# Dark Theme Update Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Update `index.html` to match kevinohara.com — dark color palette, animated gradient ring on photo, and four social/contact links.

**Architecture:** Single `index.html` file with inline CSS and JS. No build system. All changes are to CSS custom properties, font imports, photo wrapper styles, link section HTML/CSS, and removal of the 3D tilt script.

**Tech Stack:** Vanilla HTML/CSS/JS, Google Fonts (DM Sans + DM Serif Display)

---

### Task 1: Update CSS color tokens

**Files:**
- Modify: `index.html` (`:root` block, approx lines 18–28)

**Step 1: Replace the `:root` block**

Find and replace the existing `:root` block:

```css
:root {
  --bg: #0e0f11;
  --card: #16181c;
  --name: #e8e6e2;
  --title: #7a7772;
  --body: #e8e6e2;
  --muted: #7a7772;
  --accent: #c8b89a;
  --border: rgba(255,255,255,0.07);
  --shadow: 0 8px 40px rgba(0,0,0,0.4);
  --radius: 12px;
}
```

**Step 2: Verify visually**

Open `index.html` in a browser. Background should be near-black (`#0e0f11`), card should be dark (`#16181c`), text should be off-white.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: switch to dark color palette from kevinohara.com"
```

---

### Task 2: Update font import

**Files:**
- Modify: `index.html` (Google Fonts `<link>` tag, line 10)

**Step 1: Replace the Google Fonts link**

Find:
```html
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,400;0,500;1,400&family=Playfair+Display:wght@700&display=swap" rel="stylesheet" />
```

Replace with:
```html
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500&family=DM+Serif+Display&display=swap" rel="stylesheet" />
```

**Step 2: Update `.name` font-family**

Find in CSS:
```css
.name {
  font-family: 'Playfair Display', serif;
```

Replace with:
```css
.name {
  font-family: 'DM Serif Display', serif;
```

**Step 3: Update `.initials-text` font-family**

Find:
```css
.initials-text {
  display: none;
  font-family: 'Playfair Display', serif;
```

Replace with:
```css
.initials-text {
  display: none;
  font-family: 'DM Serif Display', serif;
```

**Step 4: Verify visually**

Open in browser. Name "Kevin O'Hara" should render in DM Serif Display (a clean serif, slightly different from Playfair Display).

**Step 5: Commit**

```bash
git add index.html
git commit -m "feat: swap Playfair Display for DM Serif Display"
```

---

### Task 3: Update photo to animated gradient ring

**Files:**
- Modify: `index.html` (`.photo-wrap` CSS block and surrounding rules)

**Step 1: Replace `.photo-wrap` and related CSS**

Remove these CSS rules entirely:
- `.photo-wrap::after` (hover overlay)
- `.photo-wrap:hover::after`

Replace `.photo-wrap` with:
```css
.photo-wrap {
  position: relative;
  width: 96px;
  height: 96px;
  border-radius: 50%;
  padding: 3px;
  background: conic-gradient(var(--accent), transparent 60%, var(--accent));
  animation: spin 8s linear infinite;
  margin-bottom: 24px;
  flex-shrink: 0;
}
```

**Step 2: Update `.photo-inner`**

Replace `.photo-inner` with:
```css
.photo-inner {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  overflow: hidden;
  background: var(--card);
}
```

**Step 3: Add `@keyframes spin`**

Add after the existing `@keyframes rise` block:
```css
@keyframes spin {
  to { transform: rotate(360deg); }
}
```

**Step 4: Verify visually**

Open in browser. Photo should be 96px circle with a slow-rotating tan gradient ring. No tilt on hover.

**Step 5: Commit**

```bash
git add index.html
git commit -m "feat: replace 3D tilt with animated gradient ring on photo"
```

---

### Task 4: Update link styles to vertical list

**Files:**
- Modify: `index.html` (`.links` and `.link` CSS blocks)

**Step 1: Replace `.links` CSS**

Find `.links` block and replace with:
```css
.links {
  display: flex;
  flex-direction: column;
  gap: 8px;
  width: 100%;
  margin-bottom: 32px;
}
```

**Step 2: Replace `.link` CSS**

Find the `.link` block and all its pseudo-element rules (`.link::after`, `.link:hover`, `.link:hover::after`) and replace with:
```css
.link {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 14px 16px;
  border: 1px solid var(--border);
  border-radius: 10px;
  font-size: 14px;
  font-weight: 400;
  color: var(--name);
  text-decoration: none;
  transition: transform 0.2s ease, background 0.2s ease;
}

.link:hover {
  transform: translateY(-2px);
  background: rgba(200, 184, 154, 0.07);
  color: var(--accent);
}

.link-icon {
  width: 36px;
  height: 36px;
  border-radius: 8px;
  background: var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  transition: background 0.2s ease;
}

.link:hover .link-icon {
  background: rgba(200, 184, 154, 0.15);
}

.link-label {
  flex: 1;
  text-align: left;
}

.link-arrow {
  color: var(--muted);
  transition: transform 0.2s ease, color 0.2s ease;
}

.link:hover .link-arrow {
  transform: translateX(3px);
  color: var(--accent);
}

.link:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 3px;
}
```

**Step 3: Add staggered fade-in for links**

Add after the `@keyframes spin` block:
```css
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(8px); }
  to   { opacity: 1; transform: translateY(0); }
}

.link {
  opacity: 0;
  animation: fadeUp 0.4s ease forwards;
}

.link:nth-child(1) { animation-delay: 0.15s; }
.link:nth-child(2) { animation-delay: 0.25s; }
.link:nth-child(3) { animation-delay: 0.35s; }
.link:nth-child(4) { animation-delay: 0.45s; }
```

Note: the `opacity: 0` and `animation` on `.link` should be merged into the `.link` block from Step 2 above (not duplicated). Merge them together so `.link` has one combined rule.

**Step 4: Verify visually**

Open in browser. Links area should show a vertical column of rounded-rectangle rows with icon on left, label, and arrow on right.

**Step 5: Commit**

```bash
git add index.html
git commit -m "feat: update link styles to vertical list rows"
```

---

### Task 5: Update HTML — four links with icons

**Files:**
- Modify: `index.html` (`<nav class="links">` block)

**Step 1: Replace the `<nav class="links">` block**

Replace the existing `<nav>` with:
```html
<nav class="links">
  <a class="link" href="https://www.instagram.com/kevinoh15" target="_blank" rel="noopener">
    <span class="link-icon">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"/></svg>
    </span>
    <span class="link-label">Instagram</span>
    <svg class="link-arrow" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
  </a>
  <a class="link" href="https://www.facebook.com/kevin.ohara.15" target="_blank" rel="noopener">
    <span class="link-icon">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/></svg>
    </span>
    <span class="link-label">Facebook</span>
    <svg class="link-arrow" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
  </a>
  <a class="link" href="https://www.linkedin.com/in/kevinoh15/" target="_blank" rel="noopener">
    <span class="link-icon">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
    </span>
    <span class="link-label">LinkedIn</span>
    <svg class="link-arrow" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
  </a>
  <a class="link" href="mailto:kevinoh15@gmail.com">
    <span class="link-icon">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4-8 5-8-5V6l8 5 8-5v2z"/></svg>
    </span>
    <span class="link-label">Email</span>
    <svg class="link-arrow" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
  </a>
</nav>
```

**Step 2: Verify visually**

Open in browser. Should show four vertical link rows: Instagram, Facebook, LinkedIn, Email — each with icon box, label, and right-pointing arrow. Hover should lift the row and tint it.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add four social/contact links with icons"
```

---

### Task 6: Remove 3D tilt JavaScript

**Files:**
- Modify: `index.html` (`<script>` block at bottom)

**Step 1: Delete the entire `<script>` block**

Remove:
```html
<script>
  const wrap = document.getElementById('photoWrap');

wrap.addEventListener('mousemove', (e) => {
  ...
});

wrap.addEventListener('mouseleave', () => {
  ...
});
</script>
```

The page now has no JavaScript — the animated ring is pure CSS.

**Step 2: Remove `id="photoWrap"` and `id="card"` attributes** (no longer needed)

**Step 3: Remove `perspective: 600px` from `.card` CSS** (was only for 3D tilt)

**Step 4: Remove `cursor: default` and `transition: transform 0.15s ease` from `.photo-wrap`** (no longer needed)

**Step 5: Verify visually**

Open in browser. Page should fully render with no JS. No console errors.

**Step 6: Commit**

```bash
git add index.html
git commit -m "feat: remove 3D tilt JS, page is now JS-free"
```

---

### Task 7: Final polish and card border

**Files:**
- Modify: `index.html`

**Step 1: Add a subtle border to the card**

In the `.card` CSS rule, add:
```css
border: 1px solid var(--border);
```

**Step 2: Adjust card padding to match kevinohara.com**

Update `.card` padding:
```css
padding: 48px 32px 40px;
```

**Step 3: Verify full page visually**

Check in both desktop (420px card centered) and mobile (full-bleed). Confirm:
- [ ] Dark background, dark card with subtle border
- [ ] Rotating gradient ring on photo
- [ ] Name in DM Serif Display
- [ ] Four link rows with icons, hover effects, staggered fade-in
- [ ] Mantra visible at bottom in muted color

**Step 4: Final commit**

```bash
git add index.html
git commit -m "feat: final polish — card border, padding, dark theme complete"
```
