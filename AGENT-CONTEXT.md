# Agent Context: Matt April's Personal Homepage

This document is a handoff brief for an AI agent continuing work on Matt April's personal landing page. It contains everything you need: who Matt is, the design vision, technical architecture, CSS variable system, every section's structure, content tone guidelines, and what still needs doing.

---

## Who is Matt

Matt April is a 33-year-old Senior Staff Engineer and physicist living in Columbus, OH with his wife (also 33), their dog, and their cat. His GitHub username is `matt-april`. This site is his main personal landing page, to be hosted on GitHub Pages at `matt-april.github.io`.

### Career Trajectory (chronological)

1. **B.S. Physics & Mathematics** — Perfect 4.0 GPA, top of his class. Always one of the smartest in the room. Built a deep foundation in mathematical reasoning and computational methods.

2. **Senior/Principal Engineer at a startup (5 years)** — His first major career chapter. Mastered the entire stack: .NET, C#, JavaScript, AngularJS, SQL. Was the de facto principal engineer in behavior though not in title. The person everyone came to. The superstar. Architecture decisions, hard problems, the go-to for everything.

3. **Physics graduate program (M.S., Cosmology)** — Left the startup to pursue a Physics PhD. Focused on galaxy clusters and cosmology. Key accomplishments:
   - Published a **first-author peer-reviewed paper** on galaxy cluster analysis
   - Refactored and ran highly complex simulation code on **high-performance computing clusters (HPCs)**
   - Created **reusable pipelines** for cosmological analysis: statistical likelihood analysis, imaging pipelines
   - Led multiple **open source repositories** for the **Rubin Observatory LSST DESC** collaboration:
     - **Firecrown**: Multi-probe cosmological likelihood framework
     - **TJPCov**: Covariance matrix computation pipeline for two-point correlation functions
   - Co-authored multiple additional papers as a non-first author
   - Left with a master's degree **by choice** — the PhD was within reach and he was excelling, but his heart moved on. This was his decision, not a failure.

4. **Senior Staff Engineer at a new software startup (current role)** — Backend-focused. The technical cornerstone of the company. Key details:
   - Top-tier expert in **PostgreSQL, C#, Python**
   - Recognized by the **CEO as the top engineer** in the company
   - Genius-level ability in code design, PR design, code quality, and engineering standards
   - **Product-minded** — thinks about business impact, not just code
   - Sets the engineering **culture and standards** for the dev team
   - IC-determined — leads through individual contribution and excellence, not management hierarchy

### Personal Character & Values

- **Humble and reserved** — naturally bright and confident but not egotistical. Doesn't brag. Lets the work speak.
- **Authentic and genuine** — deeply caring, not superficial
- **Values social justice** — DSA member, anti-fascist, cares about economics and socialism
- **More of a homebody** — less extraverted, prefers depth over breadth in relationships
- **Relentless learner** — constantly discovering new music, solving new problems, picking up new passions

### Hobbies & Interests

- Electronics projects
- 3D printing
- Woodworking
- Music discovery (loves all sorts of music)
- Constant learning and problem-solving

### Side Projects (both have docs hosted on GitHub IO)

- **Vehix** → `https://matt-april.github.io/vehix-docs`
- **Pilled** → `https://matt-april.github.io/pilled-docs`
- We don't have detailed descriptions of what these projects do. The current site uses intentionally vague copy. If Matt provides details, flesh out the descriptions.

---

## Tone & Voice Guidelines

This is critical. The tone of this site is **relaxed professional confidence**. Think: the smartest person in the room who doesn't need to tell you they're the smartest person in the room. Specific guidelines:

- **Not stuffy, not silly** — professional but with warmth and personality
- **Not a resume** — it's a narrative. The "Journey" section is explicitly subtitled "Not a resume. A trajectory."
- **Confident without arrogance** — statements like "I set the standards" rather than "I'm the best"
- **First person** — the site speaks as Matt ("I build software", "I operate across the full stack")
- **Short, punchy section headers** — "Things I'm building." / "The rest of the picture." / "Not a resume. A trajectory."
- **No corporate buzzwords** — no "synergy", no "leverage", no "passionate about". Real language.
- **The cosmology angle is a differentiator** — it's what makes Matt memorable. The hero tagline "I build software and study *the cosmos*" is the hook. Don't dilute it.
- **Understated about the PhD** — the site says "Physics M.S. · Cosmology" and describes the work without dwelling on PhD vs. master's. It frames the departure as a pivot, not a shortcoming.

---

## Technical Architecture

### File Structure

Single file: `homepage/index.html`. Everything is self-contained — HTML, CSS, and JS in one file. No build step, no frameworks, no dependencies beyond Google Fonts.

### External Dependencies

- **Google Fonts**: `DM Serif Display` (display/headings) and `Outfit` (body text), loaded via `<link>` tags with `preconnect`.
- That's it. No other external resources.

### CSS Architecture

All theming is done through CSS custom properties on `:root`:

```css
--bg-deep: #0d0f14;        /* Deepest background — body, page base */
--bg-surface: #13161d;      /* Card backgrounds, slightly raised surfaces */
--bg-raised: #1a1e28;       /* Tags, nested cards (e.g. repo cards inside research) */
--text-primary: #e8e4df;    /* Main heading/body text — warm off-white */
--text-secondary: #9a958e;  /* Body copy, descriptions — warm gray */
--text-dim: #5e5a54;        /* Footer text, scroll indicator — very muted */
--accent: #c8956c;          /* Primary accent — warm copper/amber. Used for: labels, timeline dots, hover states, CTA button, card icons */
--accent-glow: #c8956c33;   /* Box-shadow glow on primary button hover */
--accent-bright: #e0ad82;   /* Lighter copper for hover states on accent-colored elements */
--accent-alt: #6c9ec8;      /* Secondary accent — cool steel blue. Used for: repo card titles, repo card hover borders. Provides contrast against the warm copper. */
--timeline-line: #2a2e38;   /* Timeline connecting line, ghost button border */
--font-display: 'DM Serif Display', Georgia, serif;  /* Headings — elegant, literary serif */
--font-body: 'Outfit', -apple-system, sans-serif;     /* Body — clean geometric sans */
--max-width: 860px;         /* Content container max width */
--section-gap: clamp(80px, 12vh, 140px);  /* Vertical spacing between sections */
```

### Typography Scale

- Hero h1: `clamp(2.8rem, 6vw, 4.5rem)` — DM Serif Display
- Section titles: `clamp(1.8rem, 3.5vw, 2.4rem)` — DM Serif Display
- Card/timeline h3: `1.15rem–1.3rem` — DM Serif Display
- Section labels (uppercase): `0.75rem–0.8rem` — Outfit, weight 600, letter-spacing 0.15-0.18em
- Body text: `17px` base — Outfit, weight 400
- Tags: `0.72rem` — Outfit, weight 500
- Nav links: `0.82rem` uppercase — Outfit, weight 500

### Background Layers (bottom to top)

1. **`<canvas id="starfield">`** — Fixed position, z-index 0, opacity 0.45. Animated star particles.
2. **`body::before`** — Fixed position, z-index 1. SVG fractal noise texture at opacity 0.022. Creates subtle film-grain feel.
3. **`.page-wrapper`** — z-index 2. All actual page content sits here.

### JavaScript (vanilla, no dependencies)

Three small scripts at the bottom of `<body>`:

1. **Starfield animation** — IIFE. Creates 110 star particles on a `<canvas>`. Each star has position, radius (0.3–1.5px), drift velocity (very slow), base opacity (0.2–0.7), and a pulse phase. On each `requestAnimationFrame`, stars drift and flicker via `sin()`. Canvas resizes on window resize.

2. **Nav scroll effect** — Adds `.scrolled` class to `<nav>` when `window.scrollY > 60`. This triggers: background becomes semi-transparent with blur, padding shrinks, subtle bottom border appears.

3. **Scroll reveal** — `IntersectionObserver` watching all `.reveal` elements. When an element enters viewport (threshold 0.12, rootMargin -40px bottom), adds `.visible` class (which transitions from `opacity: 0; transform: translateY(28px)` to visible). Each element is unobserved after reveal (one-time animation).

### Responsive Behavior

Single breakpoint at `max-width: 680px`:
- All 2-column grids (about, research repos, projects) collapse to single column
- Nav section links (About, Journey, Research, Projects) hide; only GitHub icon remains
- Hero h1 font size reduces: `clamp(2rem, 8vw, 3rem)`
- Timeline padding-left reduces from 36px to 28px (and dot repositions accordingly)
- Footer goes vertical (column direction) with centered text
- Scroll indicator at bottom of hero hides

### Animation System

Two types of animations:

**CSS @keyframes (hero only):**
- `fadeUp`: `opacity 0→1, translateY 20px→0`. Used on hero elements with staggered `animation-delay` (0.3s, 0.5s, 0.7s, 0.9s, 1.2s).
- `scrollPulse`: Opacity oscillates 0.4→1→0.4 over 2s. Used on the scroll indicator line.

**Scroll-triggered reveals (everything else):**
- Base class `.reveal`: `opacity: 0; transform: translateY(28px); transition: opacity 0.7s ease, transform 0.7s ease`
- Active class `.visible`: `opacity: 1; transform: translateY(0)`
- Delay modifiers: `.reveal-delay-1` (0.1s), `.reveal-delay-2` (0.2s), `.reveal-delay-3` (0.3s)

### Hover States & Micro-interactions

- **About cards**: translateY(-3px) + border brightens on hover
- **Timeline dots**: Fill with accent color on hover (border stays, background transitions from transparent to copper)
- **Repo cards**: translateY(-2px) + border turns blue accent on hover
- **Project cards**: translateY(-3px) + border brightens; arrow in "View Documentation" link translates 4px right
- **Interest pills**: Border turns copper, text brightens to primary on hover
- **Buttons**: Primary button lifts (-2px) with copper glow shadow; ghost button border and text brighten
- **Nav links**: Color transitions from secondary to primary
- **Footer icons**: Color transitions from dim to primary

---

## Detailed Section Breakdown

### 1. Hero Section

```
class="hero" — min-height: 100vh, flexbox centered
├── .container.hero-content
│   ├── .hero-label — "ENGINEER · PHYSICIST · BUILDER" (uppercase, copper, animated in)
│   ├── h1 — "I build software\nand study the cosmos." ("the cosmos." is <em> = italic + copper)
│   ├── p.hero-description — elevator pitch paragraph
│   └── .hero-cta
│       ├── a.btn.btn-primary → #journey — "See My Journey"
│       └── a.btn.btn-ghost → #projects — "View Projects"
└── .scroll-indicator — "SCROLL" text + animated vertical line
```

### 2. About Section (`id="about"`)

```
section#about
└── .container
    ├── .reveal — section header (label, title, subtitle)
    └── .about-grid (2×2 grid)
        ├── .about-card — Σ icon, "Physics & Math", description
        ├── .about-card — >_ icon, "Full Stack Engineering", description
        ├── .about-card — ◊ icon, "Technical Leadership", description
        └── .about-card — ⊕ icon, "Open Source", description
```

Card icons use HTML entities: `&Sigma;`, `&gt;_`, `&loz;`, `&oplus;`. They're styled in the accent color at 1.5rem.

### 3. Journey Section (`id="journey"`)

```
section#journey
└── .container
    ├── .reveal — section header
    └── .timeline (left-bordered with gradient line)
        ├── .timeline-item — "FOUNDATION" / "B.S. in Physics & Mathematics" / description / tags: Physics, Mathematics, 4.0 GPA
        ├── .timeline-item — "5 YEARS · STARTUP" / "Senior / Principal Engineer" / description / tags: .NET/C#, JavaScript, AngularJS, SQL, Full Stack
        ├── .timeline-item — "GRADUATE RESEARCH" / "Physics M.S. · Cosmology" / description / tags: Cosmology, Galaxy Clusters, HPC, Published Research, LSST DESC
        └── .timeline-item — "NOW" / "Senior Staff Engineer" / description / tags: PostgreSQL, C#, Python, Architecture, Product Strategy
```

The timeline line is a `::before` pseudo-element: 1px wide, gradient from copper at top to timeline-line color to transparent at bottom. Each item has a `::before` dot (9px circle, copper border, fills on hover).

### 4. Research Section (`id="research"`)

```
section#research
└── .container
    ├── .reveal — section header
    ├── .research-highlight (elevated card with gradient top border)
    │   ├── h3 — "Galaxy Clusters & Cosmological Analysis"
    │   ├── p — first-author paper, pipelines, HPC work
    │   └── p — co-authored additional publications
    └── .research-repos (2-column grid)
        ├── .repo-card — "Firecrown" (blue accent title) + description
        └── .repo-card — "TJPCov" (blue accent title) + description
```

The `.research-highlight` card has a 3px gradient top border: copper → blue → transparent (via `::before`). This is the only place both accent colors appear together, creating a visual bridge between the engineering (warm) and science (cool) sides.

### 5. Projects Section (`id="projects"`)

```
section#projects
└── .container
    ├── .reveal — section header
    └── .projects-grid (2-column)
        ├── .project-card — "Vehix" + description + link to vehix-docs
        └── .project-card — "Pilled" + description + link to pilled-docs
```

Each card has a "View Documentation →" link where the arrow animates right on card hover.

### 6. Personal Section (`id="personal"`)

```
section#personal
└── .container
    ├── .reveal — section header ("Beyond the Code" / "The rest of the picture.")
    ├── .interests-list (flex-wrap pill layout)
    │   └── .interest-pill × 6 — Electronics, 3D Printing, Woodworking, Music Discovery, Constant Learning, Columbus OH
    └── p.personal-note — warm paragraph about life outside work
```

### 7. Footer

```
footer
└── .container.footer-inner (flex, space-between)
    ├── .footer-left — "Matt April"
    └── .footer-links
        └── a → GitHub (SVG icon)
```

---

## Links & URLs Currently in the Page

| Element | URL | Status |
|---------|-----|--------|
| Nav GitHub icon | `https://github.com/matt-april` | Confirmed |
| Nav section links | `#about`, `#journey`, `#research`, `#projects` | Internal anchors, working |
| Hero CTA buttons | `#journey`, `#projects` | Internal anchors, working |
| Vehix docs link | `https://matt-april.github.io/vehix-docs` | Assumed correct |
| Pilled docs link | `https://matt-april.github.io/pilled-docs` | Assumed correct |
| Footer GitHub icon | `https://github.com/matt-april` | Confirmed |

### Missing Links (add when Matt provides them)

- **LinkedIn URL** — there's no LinkedIn link anywhere currently. The nav had one in an earlier draft but it was removed since we didn't have the real URL. If added, put it next to the GitHub icon in both nav and footer.
- **Email address** — no email link currently. An earlier draft had one in the footer. If added, use a `mailto:` link with an envelope SVG icon.

---

## What's Complete & Working

- All HTML structure and content written from Matt's real profile
- Full CSS styling with custom properties, responsive design
- Starfield canvas animation (drift + flicker)
- Noise texture overlay
- Nav frosted glass scroll effect
- Scroll-triggered fade-up reveals with staggered delays
- Hero entrance animations
- All hover micro-interactions (cards, timeline, pills, buttons, links)
- Mobile responsive (680px breakpoint)
- Semantic HTML with proper `aria-label`s on icon links
- Google Fonts loaded with `preconnect` for performance
- `::selection` styled (copper background)
- `smooth-scroll` enabled on `html`

## What Could Be Improved or Added

### High Priority
- **Favicon** — no favicon currently. A simple one matching the copper/charcoal palette would be good.
- **Open Graph meta tags** — `og:title`, `og:description`, `og:image`, `og:url`, `twitter:card` etc. Critical for when the link is shared on social media or Slack.
- **More specific Vehix/Pilled descriptions** — current copy is generic placeholder. Flesh out when Matt provides details about what these projects actually do.

### Medium Priority
- **LinkedIn and email links** — add to nav and footer when URLs are provided
- **Profile photo** — could add to the hero or about section. Would need to decide on placement and ensure it fits the aesthetic (maybe a subtle circular image with a border, or a more editorial rectangular crop).
- **Dynamic footer year** — currently no year shown, just "Matt April". Could add `new Date().getFullYear()` if desired.
- **Accessibility audit** — color contrast ratios on the dim/secondary text against dark backgrounds should be verified. The `--text-secondary` (#9a958e) on `--bg-deep` (#0d0f14) may be borderline for WCAG AA.

### Low Priority / Nice-to-Have
- **Analytics** — Google Analytics, Plausible, or similar
- **Contact section** — a dedicated section with email, LinkedIn, GitHub, maybe a contact form
- **Blog or writing section** — if Matt ever writes
- **Dark/light mode toggle** — the site is dark-only currently, which fits the aesthetic, but some users prefer light
- **Page transitions** — more elaborate entrance animations or parallax effects
- **Performance** — the starfield runs `requestAnimationFrame` continuously. Could add a visibility check to pause when tab is not active (via `document.hidden`). Minor optimization.
- **Print stylesheet** — for people who might want to print the page as a resume-like document

---

## Design Philosophy Notes for the Agent

If you modify or extend this site, keep these principles in mind:

1. **Less is more** — the current design works because of restraint. Resist the urge to add gradients, shadows, or effects. The starfield is the one "wow" element. Everything else is typography, spacing, and subtle interaction.

2. **Warm over cold** — the palette is intentionally warm for a dark site. The copper accent, warm off-white text, and warm grays create intimacy. Don't introduce cool grays or pure whites.

3. **The two-accent system is deliberate** — copper (`--accent`) = engineering/personal/warm. Blue (`--accent-alt`) = science/research/cool. They only overlap in the research section's gradient border. Don't mix them elsewhere.

4. **Content hierarchy matters** — section labels (small, uppercase, copper) → section titles (large serif) → section subtitles (medium, muted) → body content. This three-tier header pattern repeats consistently. Keep it.

5. **Cards don't have visible borders in their resting state** — they use `border: 1px solid #ffffff06` which is nearly invisible. The border only becomes apparent on hover. This creates a clean look at rest with satisfying interaction on hover.

6. **The narrative framing is intentional** — "Not a resume. A trajectory." This isn't a list of accomplishments. Each section tells part of a story. New sections should follow this pattern.

7. **Matt's profile.md source file** is also in the repo root at `profile.md` for reference.
