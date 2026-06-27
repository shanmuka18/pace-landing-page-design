# Pace — Landing Page Design Rationale

**Product:** Pace, a focus-time visibility tool for remote teams
**Goal:** Free trial signups
**Style direction:** Clean, minimal, conversion-focused

---

## 1. Why this product framing

The brief left the product open ("any product or service"), so to make real design decisions rather than generic ones, I grounded it in a specific concrete product: **a shared focus-timer/status tool for distributed teams** ("Pace"). This gives the page an actual subject — a live timer, a real interruption problem, a believable metric set — instead of placeholder SaaS copy. The structure and components transfer cleanly to most B2B SaaS products if you swap the copy and demo widget.

## 2. Hero strategy

Per the brief, the hero needed to convert. Rather than a generic headline + gradient blob (the most common AI-generated default), **the hero's visual is the product itself**: a live, animated timer widget showing an active focus session with teammates' avatars. This works harder than a stock illustration because it shows the actual mechanism a visitor would get on day one — it answers "what is this, exactly?" before they finish reading the headline.

## 3. Color palette

| Token | Hex | Use |
|---|---|---|
| `--bg` | `#0E0E10` | Page background (near-black, not pure black — softer on screen) |
| `--surface` | `#1C1C1F` | Cards, demo widget, footer divid--ers |
| `--surface-raised` | `#232326` | Hover/raised states |
| `--paper` / `--ink` | `#FAFAF7` | Primary text on dark |
| `--ink-dim` | `#9A9AA0` | Secondary text |
| `--ink-faint` | `#6B6B70` | Tertiary/caption text |
| `--accent` | `#FF5A36` | CTAs, links, the one signal color |
| `--border` | `#2C2C30` | Hairline dividers, card borders |

**Why dark + orange, not the expected blue SaaS palette:** blue reads as generic enterprise software. Orange/red signals urgency and energy, which matches a product about *protecting focused time* — it's the color of a "do not disturb" light, not a calm dashboard. Used sparingly (CTAs, the timer ring, the pulse dot) so it stays a signal rather than noise.

## 4. Typography

| Role | Typeface | Notes |
|---|---|---|
| Display (H1, H2, H3) | **Fraunces** | A warm, slightly idiosyncratic serif with optical sizing. Avoids the "every AI SaaS page uses the same grotesk for everything" look. Used with restraint — only headlines. |
| Body / UI | **Inter** | Neutral, highly legible workhorse for paragraph text, nav, buttons. |
| Data / stats / timer | **JetBrains Mono** | Used specifically for the countdown timer and stat numbers, so numbers read as *data* — reinforces the product's time-tracking nature. |

System-font fallback stacks (`Georgia`, `Segoe UI`, `Consolas`, etc.) are included so the layout degrades gracefully if the Google Fonts CDN is slow or blocked for a given visitor.

## 5. Layout & components

- **Nav:** Sticky, blurred-glass background, logo + 4 links + sign-in + primary CTA. Collapses to logo + CTA only on mobile (full nav menu omitted by design at this fidelity — flag for a hamburger menu in dev handoff).
- **Hero:** Eyebrow badge → H1 → subhead → CTA pair → microcopy (risk reducer: "no credit card required") → live demo widget. This ordering follows a standard high-converting hierarchy: hook → promise → proof-of-low-friction → action → show, don't tell.
- **Logo strip:** Social proof immediately under the fold, low-opacity wordmarks (swap for real logos in production).
- **Features (3-up):** Icon + heading + 2-line description. Kept to 3 — more dilutes attention at this stage of the page.
- **How it works (3 numbered steps):** Numbering is justified here — this content is a literal sequence (start → visible → logged), which is exactly the case the frontend-design guidance flags as legitimate for numbered markers.
- **Stats band:** 4 metrics in monospace, high-contrast against dark background, placed after features as proof reinforcement before testimonials.
- **Testimonials (3-up):** Star rating, quote, avatar + name + role + company. Real testimonials should replace these placeholders before launch.
- **Final CTA:** Mirrors the hero CTA pair with a closing headline, positioned with its own radial accent glow to feel like a distinct closing moment, not a repeated block.
- **Footer:** Brand recap + 3 link columns + legal row.

## 6. Responsive behavior (mobile)

- Single-column stacking for all grids (features, testimonials, steps, stats)
- Full-width buttons in all CTA rows
- Demo widget switches from horizontal (ring + text side-by-side) to vertical/centered
- Nav links hidden behind the implied menu icon (logo + CTA retained)
- Type scale steps down (H1: 64px → 36px) to avoid awkward wrapping

## 7. A note on the exported PNGs

The attached PNG screenshots were rendered with a sandboxed tool (`wkhtmltoimage`) that uses an older WebKit engine with limited CSS Grid support (no `repeat()` track sizing) and no internet access to fetch the Google Fonts. As a result, the PNGs show:
- System-font fallbacks instead of Fraunces/Inter/JetBrains Mono
- The 3-column "How it works" and 4-column stats band collapsing to single-column

**This is a limitation of the screenshot tool, not the actual file.** The `index.html` file itself uses standard, well-supported CSS Grid and a normal Google Fonts `<link>` tag — it will render correctly with proper multi-column layouts and the intended typefaces in any modern browser (Chrome, Safari, Firefox, Edge) or in a real design tool import. Open `index.html` directly in a browser to see the design as intended.

## 8. Handoff notes / what's simplified at this fidelity

- Testimonial and logo content is placeholder — swap for real customer data
- No hamburger menu interaction built for mobile nav (links are simply hidden — add a menu icon + drawer in dev)
- No dark/light mode toggle — page is dark-mode-only by design
- Demo timer animation is a CSS keyframe loop, not wired to real data — illustrative only
- Recommend A/B testing the hero CTA copy ("Start free trial" vs. "Try it free") once live

## 9. Files delivered

| File | Description |
|---|---|
| `wireframe.html` / `wireframe.png` | Low-fidelity structural wireframe, desktop |
| `index.html` | High-fidelity responsive build (desktop + mobile in one file) |
| `desktop-mockup.png` | Rendered desktop screenshot, 1440px width |
| `mobile-mockup.png` | Rendered mobile screenshot, 390px width (iPhone-class viewport) |
| `design-rationale.md` | This document |
