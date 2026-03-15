# Personal Web Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a single `index.html` personal landing page for Kevin O'Hara, UX & Product Designer.

**Architecture:** One self-contained HTML file with inline `<style>` and `<script>` blocks. No build tools, no frameworks, no dependencies beyond Google Fonts. The card layout centers a photo, name, title, one-liner, social links, and mantra on a warm off-white background.

**Tech Stack:** HTML5, CSS3 (custom properties, transitions, transforms), vanilla JS (mousemove tilt), Google Fonts (Playfair Display + DM Sans)

---

### Task 1: Scaffold the HTML skeleton

**Files:**
- Create: `index.html`

**Step 1: Create the file with boilerplate**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Kevin O'Hara — UX & Product Designer</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,400;0,500;1,400&family=Playfair+Display:wght@700&display=swap" rel="stylesheet" />
  <style>
    /* styles go here */
  </style>
</head>
<body>
  <main class="page">
    <div class="card" id="card">
      <!-- content goes here -->
    </div>
  </main>
  <script>
    // js goes here
  </script>
</body>
</html>
```

**Step 2: Open in browser to verify it loads (blank white page is correct)**

Open `index.html` in any browser. No errors in console.

**Step 3: Commit**

```bash
git init
git add index.html
git commit -m "feat: scaffold html skeleton"
```

---

### Task 2: Add page and card styles

**Files:**
- Modify: `index.html` — fill in the `<style>` block

**Step 1: Add CSS custom properties and reset**

```css
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

:root {
  --bg: #F5F3EE;
  --card: #FFFFFF;
  --name: #1A1A1A;
  --title: #888888;
  --body: #444444;
  --muted: #BBBBBB;
  --accent: #C96A3A;
  --shadow: 0 8px 40px rgba(0,0,0,0.08);
  --radius: 12px;
}

html, body {
  height: 100%;
}

body {
  background: var(--bg);
  font-family: 'DM Sans', sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 24px;
}
```

**Step 2: Add card styles**

```css
.page {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  min-height: 100vh;
}

.card {
  background: var(--card);
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  padding: 48px 40px 36px;
  max-width: 420px;
  width: 100%;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0;

  /* entry animation */
  opacity: 0;
  transform: translateY(12px);
  animation: rise 0.3s ease forwards;
}

@keyframes rise {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

**Step 3: Open in browser — you should see a white rounded card centered on warm off-white**

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add page and card base styles"
```

---

### Task 3: Add the photo

**Files:**
- Modify: `index.html` — add photo markup and styles

**Step 1: Add photo HTML inside `.card`**

```html
<div class="photo-wrap" id="photoWrap">
  <img
    class="photo"
    src="photo.jpg"
    alt="Kevin O'Hara"
    onerror="this.style.display='none'; document.getElementById('photoWrap').classList.add('initials')"
  />
  <span class="initials-text">KO</span>
</div>
```

**Step 2: Add photo styles**

```css
.photo-wrap {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  overflow: hidden;
  border: 3px solid var(--bg);
  box-shadow: 0 0 0 1px rgba(0,0,0,0.07);
  margin-bottom: 24px;
  position: relative;
  transition: transform 0.15s ease;
  cursor: default;
  flex-shrink: 0;
  background: #E8E4DC;
  display: flex;
  align-items: center;
  justify-content: center;
}

.photo-wrap::after {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: 50%;
  background: rgba(201, 106, 58, 0);
  transition: background 0.2s ease;
  pointer-events: none;
}

.photo-wrap:hover::after {
  background: rgba(201, 106, 58, 0.18);
}

.photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

/* Fallback initials when photo.jpg not found */
.initials-text {
  display: none;
  font-family: 'Playfair Display', serif;
  font-size: 32px;
  color: var(--title);
  position: absolute;
}

.photo-wrap.initials .photo {
  display: none;
}

.photo-wrap.initials .initials-text {
  display: block;
}
```

**Step 3: Open in browser — see the photo circle. If no photo.jpg exists, it shows "KO" initials on a warm gray circle.**

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add photo with initials fallback"
```

---

### Task 4: Add name, title, and one-liner

**Files:**
- Modify: `index.html` — add text content and styles

**Step 1: Add text HTML below `.photo-wrap`**

```html
<h1 class="name">Kevin O'Hara</h1>
<p class="title">UX &amp; Product Designer</p>
<p class="bio">I design things people love to use.</p>
```

**Step 2: Add text styles**

```css
.name {
  font-family: 'Playfair Display', serif;
  font-size: 32px;
  font-weight: 700;
  color: var(--name);
  letter-spacing: -0.5px;
  line-height: 1.15;
  margin-bottom: 6px;
}

.title {
  font-size: 14px;
  font-weight: 400;
  color: var(--title);
  letter-spacing: 0.02em;
  margin-bottom: 16px;
}

.bio {
  font-size: 15px;
  font-style: italic;
  color: var(--body);
  line-height: 1.5;
  margin-bottom: 28px;
}
```

**Step 3: Open in browser — card now shows photo, name in bold serif, muted title, italic bio.**

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add name, title, and bio"
```

---

### Task 5: Add social links

**Files:**
- Modify: `index.html` — add links and styles

**Step 1: Add links HTML below `.bio`**

```html
<nav class="links">
  <a class="link" href="https://linkedin.com/in/kevinohara" target="_blank" rel="noopener">
    <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
    LinkedIn
  </a>
</nav>
```

> Note: Add more `<a>` tags here for Dribbble, Twitter/X, etc. as needed. Replace the `href` with Kevin's actual URL.

**Step 2: Add link styles**

```css
.links {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
  margin-bottom: 32px;
}

.link {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  padding: 9px 18px;
  border: 1.5px solid #E8E4DC;
  border-radius: 100px;
  font-size: 14px;
  font-weight: 500;
  color: var(--name);
  text-decoration: none;
  transition: color 0.15s ease, border-color 0.15s ease;
  position: relative;
}

.link::after {
  content: '';
  position: absolute;
  bottom: 8px;
  left: 18px;
  right: 18px;
  height: 1px;
  background: var(--accent);
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.2s ease;
}

.link:hover {
  color: var(--accent);
  border-color: var(--accent);
}

.link:hover::after {
  transform: scaleX(1);
}
```

**Step 3: Open in browser — see pill link buttons. Hover to see accent color and underline animation.**

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add social links with hover animation"
```

---

### Task 6: Add mantra footnote

**Files:**
- Modify: `index.html` — add mantra and styles

**Step 1: Add mantra HTML as last element inside `.card`**

```html
<p class="mantra">Keeping things simple. And fun.</p>
```

**Step 2: Add mantra style**

```css
.mantra {
  font-size: 11px;
  font-style: italic;
  color: var(--muted);
  letter-spacing: 0.03em;
}
```

**Step 3: Open in browser — small muted italic footnote at the bottom of the card.**

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add mantra footnote"
```

---

### Task 7: Add photo tilt interaction (vanilla JS)

**Files:**
- Modify: `index.html` — fill in the `<script>` block

**Step 1: Add JS for mousemove tilt on the photo**

```javascript
const wrap = document.getElementById('photoWrap');

wrap.addEventListener('mousemove', (e) => {
  const rect = wrap.getBoundingClientRect();
  const cx = rect.left + rect.width / 2;
  const cy = rect.top + rect.height / 2;
  const dx = (e.clientX - cx) / (rect.width / 2);
  const dy = (e.clientY - cy) / (rect.height / 2);
  const tiltX = dy * -8;   // max 8deg vertical
  const tiltY = dx * 8;    // max 8deg horizontal
  wrap.style.transform = `rotateX(${tiltX}deg) rotateY(${tiltY}deg) scale(1.04)`;
});

wrap.addEventListener('mouseleave', () => {
  wrap.style.transform = 'rotateX(0deg) rotateY(0deg) scale(1)';
});
```

**Step 2: Add perspective to `.photo-wrap` parent so the 3D transform renders correctly**

In the CSS, add to `.card`:
```css
perspective: 600px;
```

And to `.photo-wrap`, add:
```css
transform-style: preserve-3d;
```

**Step 3: Open in browser — hover over the photo and move the mouse. It should tilt in 3D with a warm color wash.**

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add 3D tilt hover interaction on photo"
```

---

### Task 8: Mobile polish and final QA

**Files:**
- Modify: `index.html` — add responsive styles

**Step 1: Add mobile media query**

```css
@media (max-width: 480px) {
  .card {
    padding: 40px 28px 28px;
    border-radius: 0;
    box-shadow: none;
    min-height: 100vh;
    justify-content: center;
  }

  body {
    padding: 0;
    align-items: stretch;
  }

  .name {
    font-size: 28px;
  }
}
```

**Step 2: QA checklist**

- [ ] Opens in Chrome — card centered, no layout breaks
- [ ] Opens in Safari — fonts load correctly
- [ ] Resize to 375px width — card fills screen, text readable
- [ ] Hover photo — 3D tilt + warm overlay works
- [ ] Hover link — accent color + underline slide-in works
- [ ] No photo.jpg → "KO" initials show cleanly
- [ ] Console: zero errors

**Step 3: Final commit**

```bash
git add index.html
git commit -m "feat: mobile polish and QA — personal web page complete"
```

---

### Task 9: Add your real photo and links

**Step 1: Drop your headshot into the project root**

Name it `photo.jpg`. Recommended: square crop, at least 300x300px.

**Step 2: Update social link hrefs in `index.html`**

Find the `<nav class="links">` section and update each `href` to your real URLs. Add or remove `<a>` tags as needed.

**Step 3: Final commit**

```bash
git add photo.jpg index.html
git commit -m "chore: add real photo and social links"
```

---

### Task 10: Deploy

**Option A — GitHub Pages (free, recommended)**

```bash
# Push to GitHub repo, then enable Pages in repo settings (root of main branch)
git remote add origin https://github.com/yourusername/yourusername.github.io.git
git push -u origin main
```

Your site will be live at `https://yourusername.github.io`.

**Option B — Netlify (free, drag-and-drop)**

1. Go to netlify.com → "Add new site" → "Deploy manually"
2. Drag your project folder into the drop zone
3. Done — live URL in seconds

**Option C — Vercel (free)**

```bash
npx vercel
# Follow prompts — no config needed for a static HTML file
```
