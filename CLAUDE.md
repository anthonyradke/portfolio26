# Portfolio — Anthony Radke

Static HTML/CSS/JS mechanical engineering portfolio. No build system, no framework.

## Structure

```
index.html          — main page (About / Projects / Contact)
projects/           — project1–4.html (individual detail pages)
css/styles.css      — single stylesheet, dark-mode CSS custom properties
js/sidebar.js       — <app-sidebar> web component (single source for all sidebar HTML)
js/main.js          — section switching, mobile sidebar, cert modal, contact form
images/             — profile.jpg, about.jpg, cu-logo.png, solidworks-icon.png,
                      linkedin-icon.png, projects/project1–4.jpg
files/              — resume.pdf, cswp-cert.png (documents only)
```

## Architecture

- **Sidebar**: defined once in `js/sidebar.js` as an `<app-sidebar>` web component. Each page just drops `<app-sidebar></app-sidebar>` — the component auto-detects project pages via URL and adjusts paths/nav links. `app-sidebar { display: contents }` keeps it transparent to the flex layout.
- **SPA-style section switching**: JS toggles `.active` on `.page-section` elements; only one visible at a time. `history.pushState` keeps hash URLs in sync.
- **index.html nav** uses `data-section="about|projects|contact"` — JS-driven.
- **Project pages nav** uses plain `href="../index.html#section"` links — no JS switching, no `data-section` attributes.
- **Cert modal**: clicking `.cert-item[data-cert]` opens `#pdfModal` as an `<img>` popup (not iframe — avoids browser PDF toolbar).
- **Contact form**: has `data-static="true"` — blocks real submission. Remove that attribute and set `action="https://formspree.io/f/YOUR_ID"` to go live.

## CSS Tokens (dark mode)

```
--bg: #0d1117  |  --sidebar-bg: #161b22  |  --card-bg: #1c2128
--text: #c9d1d9  |  --text-secondary: #8b949e  |  --text-muted: #6e7681
--accent: #58a6ff  |  --border: #21262d  |  --sidebar-width: 292px
```

## Path Convention

| Context | Prefix |
|---|---|
| `index.html` | `images/`, `files/`, `css/`, `js/` |
| `projects/*.html` | `../images/`, `../files/`, `../css/`, `../js/` |

## Animations in use

| Element | Animation |
|---|---|
| Active nav item | `navActivePulse` — background breathing loop |
| Nav/cert hover | `translateX(3px)` nudge |
| Section enter | `sectionIn` — fade + slide up (0.22s) |
| `h2` accent bar | `accentSlide` — width 0→40px on section activate |
| Timeline dots | `timelinePulse` — staggered glow cascade (About page) |
| Avatar (always) | Blue accent border + 4px glow ring |
| Avatar hover | `avatarBreath` — expanding glow ring, JS-controlled so cycle completes on mouse-out |

## Pending / Outstanding

- **Project images missing**: `images/projects/` is empty — need `project1.jpg` through `project4.jpg`
- **Project page content**: All 4 project pages have placeholder text — user hasn't filled in real project details yet
- **Contact form not live**: Remove `data-static="true"` and add Formspree ID when ready to deploy
