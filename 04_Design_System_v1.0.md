# Banynova — Design System v1.0

**Project Philosophy:** Build the foundation once. Reuse it everywhere. Never redesign.

**Companion to:** Master_Project_Specification_v1_0.md, AI_Prompts.md, Brand Voice Guide
**Position in hierarchy:** Governed by `Documentation_Governance_v1.0.md` — this document is the child of Master Project Specification and the parent of Component_Library.md.
**Status:** v1.3 — synced with the live `Base_Layout.xml` (Header, Footer, Hero, Popular Tools, Categories, Latest Articles, New Tools all built). Governs every future page, tool, and component.

---

## 0. How to Use This Document

This is the **single source of truth for every visual and structural decision** on Banynova. Before building anything new — a tool page, a category hub, a form, a card — check here first.

**Rules for using this document:**
- If a value you need (a color, a spacing amount, a shadow) isn't listed here, **do not invent one**. Either reuse the closest existing token, or propose an addition to this document first and get it approved before shipping it in a page.
- Every component built from today forward must be described here **before or immediately after** it ships, so this document never drifts out of sync with the real site (see Section 21 — Changelog).
- When using the AI Prompt Library (`AI_Prompts.md`), the CSS Prompt, UI Review Prompt, and Code Review Prompt all reference this document directly — keep it updated so those prompts stay accurate.

**Non-negotiable token rule:**
- Every design token (color, spacing, font size, radius, shadow) must be defined **only once**, in Section 2–7 below.
- **Hard-coded colors, spacing values, font sizes, or shadows anywhere in component CSS are prohibited.** If a value isn't already a token, it gets added here first — it never gets typed as a raw number directly into a page's CSS. This is what prevents CSS drift once there are 200+ tool pages each potentially touched by a different session or contributor.

---

## 1. Design Principles

1. **One system, infinite tools.** Whether it's tool #3 or tool #180, it must look, behave, and feel like it belongs to the same family. No page gets a "special" layout or one-off styling.
2. **Function before decoration.** Every visual choice (color, shadow, spacing) must help the user understand or use the tool faster — never decoration for its own sake.
3. **Quiet by default, deliberate when it matters.** The UI stays calm and understated; the few places we allow a bolder visual (e.g. the homepage hero's "stays in your browser" diagram) are chosen deliberately, not scattered everywhere.
4. **Accessible and fast are not optional.** Every component in this system is designed to meet WCAG 2.2 AA and the Core Web Vitals targets in the Master Spec (Section 12, 13) by default — not as a later pass.
5. **Native HTML first.** Reach for semantic elements (`<details>`, `<button>`, proper form elements) before reaching for custom JS-built widgets — they're more accessible and cheaper to maintain, by construction.
6. **Never redesign, only extend.** New categories, new tool types, and new content formats should be solvable by *combining existing components*, not by inventing new visual language. If a real gap appears, it gets added here formally (Section 21), not improvised on one page.

---

## 2. Color System

All colors are defined as **HSL-based CSS custom properties**, prefixed `--bn-`. Never hard-code a hex/rgb value in component CSS — always reference a token.

### 2.1 Core palette

| Token | Light mode value | Role |
|---|---|---|
| `--bn-primary` | `hsl(220, 90%, 56%)` | Brand blue — primary actions, links, active states, focus |
| `--bn-primary-hover` | `hsl(220, 90%, 48%)` | Primary hover state |
| `--bn-primary-active` | `hsl(220, 90%, 40%)` | Primary pressed/active state |
| `--bn-primary-subtle` | `hsl(220, 90%, 96%)` | Tinted backgrounds behind primary-colored content (badges, icon chips) |
| `--bn-secondary` | `hsl(215, 16%, 47%)` | Secondary UI accents, muted actions |
| `--bn-accent` | `hsl(262, 83%, 58%)` | Purple accent — used for category cards and secondary emphasis, never for primary CTAs |
| `--bn-success` | `hsl(142, 71%, 45%)` | Confirmations, valid states, trust checkmarks |
| `--bn-warning` | `hsl(38, 92%, 50%)` | Non-blocking warnings |
| `--bn-danger` | `hsl(354, 70%, 54%)` | Errors, destructive actions, invalid form states |
| `--bn-info` | `hsl(199, 89%, 48%)` | Neutral informational callouts |

Each of the above (except `--bn-accent`) also has a `-subtle` background variant for use behind badges/alerts, and primary/secondary/danger additionally have `-hover`/`-active` states. Never approximate these — always use the token.

### 2.2 Surface & text

| Token | Light | Dark | Role |
|---|---|---|---|
| `--bn-bg` | `hsl(220, 20%, 98%)` | `hsl(222, 47%, 11%)` | Page background |
| `--bn-surface` | `hsl(0, 0%, 100%)` | `hsl(217, 33%, 17%)` | Card/component background |
| `--bn-surface-raised` | `hsl(0, 0%, 100%)` | `hsl(217, 33%, 22%)` | Elevated surfaces (modals, dropdowns) |
| `--bn-border` | `hsl(220, 13%, 88%)` | `hsl(215, 25%, 27%)` | Default borders/dividers |
| `--bn-border-strong` | `hsl(220, 13%, 72%)` | `hsl(215, 20%, 45%)` | Emphasized borders (hover states) |
| `--bn-text-primary` | `hsl(220, 24%, 12%)` | `hsl(210, 40%, 98%)` | Headings, body copy |
| `--bn-text-secondary` | `hsl(220, 12%, 42%)` | `hsl(215, 20%, 75%)` | Supporting text, descriptions |
| `--bn-text-tertiary` | `hsl(220, 9%, 60%)` | `hsl(215, 16%, 55%)` | Metadata, timestamps, placeholders |
| `--bn-text-on-primary` | `hsl(0, 0%, 100%)` | (same) | Text placed on top of `--bn-primary` |

### 2.4 Gradient & Glass Tokens (v1.1 addition)

Added to support premium, SaaS-grade surface treatments (sticky glass header, hero accents) without introducing hard-coded values. Used sparingly — see usage rules below.

| Token | Light | Dark |
|---|---|---|
| `--bn-gradient-primary` | `linear-gradient(135deg, hsl(220,90%,56%), hsl(262,83%,58%))` | (same — works on both) |
| `--bn-gradient-subtle` | `linear-gradient(135deg, hsl(220,90%,97%), hsl(262,83%,97%))` | `linear-gradient(135deg, hsla(220,90%,56%,0.12), hsla(262,83%,58%,0.12))` |
| `--bn-glass-bg` | `hsla(0,0%,100%,0.72)` | `hsla(217,33%,17%,0.72)` |
| `--bn-blur-md` | `12px` | (same) |

**Usage rules:**
- `--bn-gradient-primary` is reserved for **one deliberate accent per page at most** — e.g. a hero headline highlight or a single CTA glow. It is never used as a general background or repeated across multiple elements; overuse defeats the "quiet by default" principle (Section 1).
- `--bn-glass-bg` + `backdrop-filter: blur(var(--bn-blur-md))` is reserved for the sticky header only, so the effect stays a distinctive, recognizable signature rather than a generic texture applied everywhere.

---

### 2.3 Usage rules

- **Primary** is reserved for the single main action on a page (e.g. "Open tool," "Browse all tools"). Never use it decoratively.
- **Accent (purple)** is reserved for category-level branding — category card icons, category badges — so it visually reads as "this represents a category," distinct from primary actions.
- **Danger/Warning/Success** are reserved for actual state communication (form validation, error messages) — never for decoration or emphasis unrelated to status.
- Text contrast must be checked against whichever `--bn-surface`/`--bn-bg` it sits on, in **both** light and dark mode, before shipping (see Section 15).

---

## 3. Typography

### 3.1 Font stacks

| Token | Stack | Use |
|---|---|---|
| `--bn-font-sans` | `system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif` | All UI text, headings, body copy |
| `--bn-font-mono` | `ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace` | Code snippets, tool input/output areas (JSON, regex, hashes, etc.) |

Using the system font stack is deliberate: zero font-loading time (helps Section 13's performance targets), and it renders natively/correctly on every OS without a webfont dependency to maintain across 200+ pages.

### 3.2 Type scale

| Token | Size | Typical use |
|---|---|---|
| `--bn-fs-xs` | 12px | Metadata, tags, timestamps |
| `--bn-fs-sm` | 14px | Secondary text, nav links, form labels |
| `--bn-fs-base` | 16px | Body copy (default) |
| `--bn-fs-lg` | 18px | Card titles, lead paragraphs |
| `--bn-fs-xl` | 20px | Sub-headings |
| `--bn-fs-2xl` | 24px | H2 in dense contexts |
| `--bn-fs-3xl` | 30px | Section titles (H2, standard) |
| `--bn-fs-4xl` | 36px | H1 on mobile / secondary hero |
| `--bn-fs-5xl` | 48px | H1 on desktop hero |

### 3.3 Weights & line-heights

- Weights: `--bn-fw-normal` (400) for body, `--bn-fw-medium` (500) for labels/nav, `--bn-fw-semibold` (600) for card titles/buttons, `--bn-fw-bold` (700) for H1/H2 only.
- Line-heights: `--bn-lh-tight` (1.2) for headings, `--bn-lh-snug` (1.375) for card titles, `--bn-lh-base` (1.5) for body copy, `--bn-lh-relaxed` (1.625) for long-form article/tutorial content.

### 3.4 Rules

- **Exactly one `<h1>` per page.** Tool pages: the tool name. Category hubs: the category name. Homepage: the hero headline.
- Never skip heading levels (no H2 → H4).
- Never set font sizes, weights, or line-heights with raw values — always the token.
- **Headings are mobile-first with a distinct scale at each breakpoint** — this was a real bug (h1 and h2 both rendered at the same size on mobile) caught and fixed after initial launch, so treat the exact values below as load-bearing, not approximate:

| Heading | Mobile base (default) | Desktop (`min-width: 640px`) |
|---|---|---|
| h1 | `--bn-fs-3xl` | `--bn-fs-4xl` |
| h2 | `--bn-fs-2xl` | `--bn-fs-3xl` |
| h3 | `--bn-fs-xl` | `--bn-fs-2xl` |
| h4 | `--bn-fs-lg` | `--bn-fs-xl` |

All four bump together in the same `min-width: 640px` media query — never split across separate breakpoints, or the hierarchy can desync again.

---

## 4. Spacing Scale (8pt Grid)

| Token | Value | Token | Value |
|---|---|---|---|
| `--bn-space-1` | 4px | `--bn-space-8` | 32px |
| `--bn-space-2` | 8px | `--bn-space-10` | 40px |
| `--bn-space-3` | 12px | `--bn-space-12` | 48px |
| `--bn-space-4` | 16px | `--bn-space-16` | 64px |
| `--bn-space-5` | 20px | `--bn-space-20` | 80px |
| `--bn-space-6` | 24px | `--bn-space-24` | 96px |

**Usage patterns already established:**
- Component internal padding (cards, buttons): `--bn-space-4` to `--bn-space-6`
- Gap between grid items: `--bn-space-5`
- Section vertical padding: `--bn-space-16` (standard), `--bn-space-12` (tight, used for stacked sections below the hero)
- Section-to-section heading margin: `--bn-space-10`

Never use a spacing value outside this scale — if a layout seems to need "18px," round to the nearest token instead of introducing a new number.

---

## 5. Border Radius

| Token | Value | Use |
|---|---|---|
| `--bn-radius-sm` | 4px | Focus ring corners, small chips |
| `--bn-radius-md` | 8px | Buttons, inputs, icon containers |
| `--bn-radius-lg` | 12px | Cards (tool/category/tutorial), search box |
| `--bn-radius-xl` | 16px | Larger feature panels (e.g. hero signature diagram) |
| `--bn-radius-full` | 9999px | Pills/badges, circular avatars |

---

## 6. Shadows (Elevation)

| Token | Use |
|---|---|
| `--bn-shadow-1` | Barely-there separation (rarely used directly) |
| `--bn-shadow-2` | Default hover elevation for cards |
| `--bn-shadow-3` | Elevated panels at rest (e.g. hero signature diagram, search results dropdown in some contexts) |
| `--bn-shadow-4` | Highest elevation — dropdowns, modals, popovers (e.g. live search results panel) |

Dark mode uses the **same tokens** with higher-opacity shadow values already baked into the `[data-theme="dark"]` override — never define separate shadow logic per theme in component CSS.

---

## 7. Grid System & Containers

| Token | Value | Use |
|---|---|---|
| `--bn-container-max` | 1280px | Outer page container (`.bn-container`) |
| `--bn-content-max` | 800px | Long-form/reading content width (FAQ, article body) |
| `--bn-sidebar-width` | 320px | Reserved for future sidebar layouts (e.g. filters) |
| `--bn-header-height` | 65px | Sticky header height — drives `.bn-header-inner` min-height and the mobile nav panel's `top` offset, so they can never drift out of sync |

### 7.1 Z-Index Scale

Never use an arbitrary `z-index` number in component CSS — always one of these four tokens:

| Token | Value | Use |
|---|---|---|
| `--bn-z-dropdown` | 100 | Mobile nav panel, nav overlay backdrop |
| `--bn-z-sticky` | 200 | Sticky header |
| `--bn-z-modal` | 500 | Reserved for future modal/dialog components |
| `--bn-z-tooltip` | 600 | Skip link (needs to sit above literally everything when keyboard-focused) |

**Standard grid pattern:** `display: grid; grid-template-columns: repeat(auto-fill, minmax(Xpx, 1fr)); gap: var(--bn-space-5);`

| Grid context | `minmax()` floor |
|---|---|
| Tool cards | 260px |
| Category cards | 220px |
| Article cards | 280px |
| Stat blocks | `auto-fit, minmax(160px, 1fr)` |

This auto-fill pattern is what makes the directory scale from 20 to 200+ tools without any layout change — verified visually at low and high item counts before shipping any new grid context.

---

## 8. Breakpoints

Mobile-first. Base styles target the smallest screen; breakpoints add layout complexity upward.

| Breakpoint | Value | Used for |
|---|---|---|
| Default (no query) | — | Single column, stacked nav |
| `min-width: 640px` | Small tablet | Minor spacing/type scale bump |
| `min-width: 760px` | Tablet | Footer grid goes from 2 to 4 columns |
| `min-width: 860px` | Small desktop | Primary nav becomes visible (mobile nav pattern TBD — see Section 21 open item) |
| `min-width: 960px` | Desktop | Hero switches from stacked to 2-column layout |

---

## 9. Buttons

| Class | Look | Use |
|---|---|---|
| `.bn-btn--primary` | Solid `--bn-primary` fill, white text | The single primary action per view |
| `.bn-btn--ghost` | Transparent fill, bordered | Secondary actions |
| `.bn-btn--sm` | Reduced padding/font-size modifier | Compact contexts (inline actions, toolbars) |

**States (all buttons):**
- Hover: background shifts to `-hover` token (primary) or subtle background tint (ghost)
- Focus: `--bn-focus-ring` box-shadow, always visible — never suppressed
- Disabled: `--bn-disabled-bg` / `--bn-disabled-text`, and `cursor: not-allowed`
- All buttons use `--bn-radius-md`, `--bn-fw-semibold`, and `--bn-transition-fast` for state changes

**Rule:** never introduce a third button color/style without adding it here first — every button on the site must be one of the above.

---

## 10. Forms

- Inputs share the same base treatment as `.bn-search-input`: `--bn-radius-lg` (or `-md` for compact inline forms), `--bn-border` default, `--bn-primary` + `--bn-focus-ring` on focus.
- Validation states use the semantic tokens directly: `--bn-danger`/`--bn-danger-subtle` for invalid fields and error text, `--bn-success` for confirmed/valid state. Never use red/green outside these tokens.
- Every input requires a associated `<label>` (visually hidden via `.bn-visually-hidden` where a placeholder alone would otherwise be the only label — see the homepage search input for the reference pattern).
- Error messages must be specific and actionable (Master Spec Section 20) — displayed inline below the field, not just a color change, since color alone isn't accessible.

---

## 11. Cards

Three card types exist, all built and live (not just planned). **No new card variant may be created without adding it to this table first.**

| Card | Component class | Contains | Reference build |
|---|---|---|---|
| **Tool Card** | `.bn-tool-card` | Icon chip (`--bn-primary-subtle` bg), category label, name, description, "Open tool →" link. Optional `.bn-new-badge` in the top-right corner for recently-added tools. | Homepage `#bn-popular-grid`, `#bn-new-tools-grid` |
| **Category Card** | `.bn-cat-card` | Icon chip (`--bn-accent` solid bg), name, tool count, one-line description | Homepage `#bn-categories-grid` |
| **Article Card** | `.bn-article-card` | Image placeholder (16:9 gradient, `--bn-radius-md`), category tag, title, description, meta row (read time) | Homepage `#bn-articles-grid` |

Shared card rules: `--bn-radius-lg`, `--bn-surface` background, `--bn-border` default border, hover state = border color shift + `translateY(-3px)` + `--bn-shadow-3`. All transitions use `--bn-transition-fast`.

**New Badge:** `.bn-new-badge` — absolutely positioned top-right on a Tool Card, `--bn-accent` background, `--bn-fs-xs`/`--bn-fw-semibold`, `--bn-radius-full`. Reuses the Tool Card unchanged; never a separate card variant just to show "New."

### 11a. Section Heading (shared pattern)

Every homepage content section (Popular Tools, Categories, Latest Articles, New Tools, and any future section) opens with the same three-part heading, never a one-off:

| Element | Class | Contains |
|---|---|---|
| Eyebrow | `.bn-section-eyebrow` | Short label above the title, `--bn-primary` colored, `--bn-fs-sm`/`--bn-fw-semibold` (e.g. "Most used," "Explore," "Learn," "Just shipped") |
| Title | `.bn-section-title` | `<h2>`, `--bn-fs-3xl` |
| Subtitle | `.bn-section-sub` | One-line description, `--bn-text-secondary`, `--bn-fs-lg` |

All three sit inside `.bn-section-head` (max-width 640px, `margin-bottom: var(--bn-space-10)`).

### 11b. Stat Block & Newsletter

| Component | Class | Contains | Rule |
|---|---|---|---|
| **Stat Block** | `.bn-stat` | Large number/value, label | Values must be verifiable/honest counts (e.g. "100+ Planned Tools," "7 Categories") — never a fabricated or vague metric (Master Spec Section 25, Brand Voice "never fabricate statistics"). Uses `--bn-fs-4xl`/`--bn-fw-bold` for the number, `--bn-text-secondary` for the label. |
| **Newsletter** | `.bn-newsletter` | Heading, one-line benefit copy, email input + submit button (reuses `.bn-search-input` and `.bn-btn--primary` styles — no new input/button style) | No fabricated subscriber counts. Copy must match Brand Voice Guide's Newsletter CTA exactly. |

**Status:** Stat Block and Newsletter are designed and tokenized here, but **not yet built into `Base_Layout.xml`** — they're part of the still-pending Why Choose/Stats/FAQ/Newsletter homepage sections (see Section 20).

---

## 12. Navigation

**Header** (`.bn-header`): sticky top, `--bn-z-sticky`. At rest, `--bn-surface` background; once scrolled past 8px, switches to `--bn-glass-bg` + `backdrop-filter: blur(var(--bn-blur-md))` (the one approved use of the glass token, per Section 2.4). Bottom border throughout. Height driven by `--bn-header-height` (65px). Contains logo (left, links to homepage — this doubles as the "Home" link, so no separate "Home" nav item exists), primary nav links (center/right, visible from 860px up), and header actions (theme toggle, mobile hamburger) on the far right.

**Header nav — deliberately minimal, 3 items only:** Resources, Blog, About. This is a real, considered decision, not an oversight — two items that used to be here were removed:
- **"Tools"** was removed because the logo already links home; a second link to the same destination was pure redundancy.
- **"Categories"** was removed because it's tool-discovery, not global site navigation — it now lives in the Hero's Quick Actions instead (see 12a below), scoped to the homepage where tool discovery actually happens. **Trade-off worth knowing:** this means a reader on a Blog post or Resources page can no longer reach category browsing in one click — they have to go home first. Accepted as reasonable since Footer still carries a Categories link for anyone who wants it, but revisit if usage data ever suggests otherwise.

**Mobile navigation** (below 860px): nav links collapse behind a hamburger button, opening a full-width slide-down panel (`--bn-surface`, `--bn-shadow-3`, `--bn-z-dropdown`, `top: var(--bn-header-height)`) with the same links stacked vertically. A `.bn-nav-overlay` dims the rest of the page behind it. Closes on: outside click, Escape key, or clicking the overlay itself — all three wired, all three tested. Opening the menu adds `.bn-scroll-locked` to `<body>` (`overflow: hidden`) so the page behind the panel can't scroll.

**Active link:** `aria-current="page"` is set via JS (`Banynova.navigation.initActiveLink`) by comparing normalized URLs (hash, query string, and trailing slash all stripped before comparing) — not just a raw string match, which was a real bug caught and fixed (Blogger's `?m=1` mobile parameter and inconsistent trailing slashes both broke a naive comparison).

**Footer** (`.bn-footer`): four-column grid — Brand+tagline, Quick Links, Legal, Contact — collapsing to two columns under 760px (mobile-first: 2 columns is the base, 4 columns is the `min-width: 760px` addition, not the other way around).

| Column | Links |
|---|---|
| Brand | Logo (via the shared `#bn-logo-icon` symbol, Section 13), tagline |
| Quick Links | Categories, Blog, Resources, Sitemap, RSS Feed |
| Legal | Privacy Policy, Terms of Service, Cookies, Accessibility |
| Contact | Contact Us, GitHub (`rel='noopener' target='_blank'` — required on every external link) |

Bottom bar (below the grid): copyright line + **Disclaimer** link + the "Your files never leave your browser" trust line. Disclaimer is deliberately here, not in the main Legal column — it's a legal footnote, not a primary policy page, so it doesn't compete for attention with Privacy/Terms/Cookies/Accessibility.

**Sitemap** links to Blogger's real, native `sitemap.xml` endpoint — never build a custom sitemap page, Blogger already serves a working one.

**Breadcrumbs** (used on tool/category pages per Master Spec Section 7, 8): not yet built in a dedicated component — required before the Universal Tool Template ships (Section 21 open item).

### 12a. Hero & Search (Homepage only)

The Hero is the one component that deliberately breaks the "reusable across every page" rule — it's homepage-exclusive by design, gated behind the same `data:blog.url == data:blog.homepageUrl` conditional that already exists in the Main widget's includable. See `Base_Layout.xml`'s own "HERO SECTION — INTEGRATION MAP" comment for exactly where its HTML/CSS/JS each live.

**Structure:** headline + subhead, a real search form (`role="search"`, `aria-labelledby`) posting to Blogger's native `/search?q=` endpoint — so search works even with JavaScript disabled — enhanced with a JS-driven combobox: live suggestion list, keyboard navigation (arrow keys, Enter, Escape), a `/` keyboard shortcut to focus the input from anywhere on the page, and an `<noscript>` fallback that keeps the plain form fully functional for crawlers and no-JS users.

**Quick Actions** (below the search box): four shortcuts — Popular Tools, Browse Categories, Latest Articles, New Tools — that link to **sections on the homepage itself** (`#popular-tools`, `#categories`, `#latest-articles`, `#new-tools`), not separate pages. This is the other half of the Header-nav trade-off above: tool-discovery shortcuts live here, scoped to where discovery actually happens, while Header carries only genuine distinct pages.

**Rule:** any future homepage-only section follows this same pattern — HTML inside the same `b:if` branch, CSS positioned in Section 5 (Components) matching render order, JS as its own `Banynova.register()`'d module (Section 12b) called unconditionally at the bottom of the init sequence. Never build a homepage section as a one-off outside this pattern.

### 12b. JavaScript Module Architecture

All JS lives in one script at the end of `<body>`, organized as named modules under a single global namespace — never scattered inline scripts, never a monolithic unstructured file.

**The pattern:**
```js
Banynova.register('moduleName', {
  // properties and methods
  init: function () { /* ... */ }
});
```

`Banynova.register()` is the **only** sanctioned way to add a module — never `Banynova.x = {...}` directly. It does two things: refuses to silently overwrite an existing module (warns via `console.warn` instead), and **freezes the module object immediately** upon registration.

**Live modules today:** `storage`, `theme`, `a11y`, `utils`, `perf`, `support`, `navigation`, `search`, `directory`. Each is called unconditionally in the init sequence at the bottom of the script (`Banynova.theme.init()`, `Banynova.navigation.init()`, etc.) — every module's own `init()` is responsible for checking whether its DOM elements actually exist and safely no-op'ing if not, so it's always safe to call every module on every page.

**The top-level `Banynova` object is deliberately never frozen**, only each individual module is. This is intentional, not an oversight: freezing the top level would make it impossible for a future tool page to add its own module (`Banynova.register('clipboard', {...})`, per Master Spec Section 10's planned Global Modules) without throwing a `TypeError` in this script's strict mode.

**A real gotcha, worth knowing before writing a new module:** because `register()` freezes the module the instant it's added, a module's own `init()` (which runs later) **cannot assign new properties to `this`** — `this.someValue = x` inside `init()` will throw. This exact bug was caught once already (a module tried `this.home = ...` to cache a computed URL). The fix: use a local variable inside `init()` and pass it as a parameter to any helper method that needs it, never store computed state back onto the frozen module object.

---

## 13. Icons

- **Style:** line icons only, 2px stroke width, `stroke="currentColor"` (never a hard-coded fill color) so icons automatically match text color and adapt to light/dark mode with zero extra code.
- **Format:** inline SVG, `viewBox="0 0 24 24"`, no external icon font/library dependency (keeps the site framework-free per Master Spec Section 4, and avoids an extra network request).
- **Logo specifically uses a `<symbol>`/`<use>` sprite**, not a repeated inline SVG: one `<symbol id="bn-logo-icon">` defined once (visually hidden) near the top of `<body>`, referenced everywhere the logo appears (`<svg><use href="#bn-logo-icon"></use></svg>`) — currently the header and footer. Any icon repeated 2+ times verbatim across the page should follow this same sprite pattern rather than duplicating markup.
- **Card/content icons render per-instance from JS**, not the sprite — each `Banynova.register()`'d module with a render function (e.g. `directory`) keeps its own small `ICONS` map of path data and an `icon(name, size)` helper. This is deliberate: these icons vary by size/context per card and are generated dynamically from mock/future-real data, so a static sprite doesn't fit; the logo is static markup repeated verbatim, so it does.
- **Sizing:** 14–16px for inline/metadata icons, 18–20px for buttons/search, 22–24px for card icon chips, 28px for "Why Choose" feature icons (pending, Section 20).
- **Decorative icons** get `aria-hidden="true"`; any icon that is the *only* content of an interactive control (e.g. the theme toggle button) must have an `aria-label` on the parent control instead, and that label must update dynamically if the icon's meaning changes (the theme toggle swaps between sun/moon icons and updates its `aria-label` between "Switch to light mode"/"Switch to dark mode" in lockstep — never let the icon and the label disagree).
- New icons should visually match the existing set's stroke weight and corner rounding — don't mix in a different icon style (e.g. filled/solid icons) without updating this section first.

---

## 14. Motion

| Token | Duration | Use |
|---|---|---|
| `--bn-transition-fast` | 150ms | Hover/focus state changes (buttons, cards, links) |
| `--bn-transition-base` | 250ms | Larger UI transitions (dropdowns opening, accordion expand) |
| `--bn-transition-slow` | 350ms | Reserved for deliberate, larger moments only (used sparingly) |

All use the same easing curve: `cubic-bezier(0.4, 0, 0.2, 1)`.

**Rule:** `@media (prefers-reduced-motion: reduce)` must collapse all transition/animation durations near-instant — already implemented globally in the base stylesheet and must be preserved in any new component CSS.

**Philosophy:** motion should confirm an interaction happened (hover lift, chevron rotation on FAQ expand), never decorate. No auto-playing animations, no gratuitous entrance effects.

---

## 15. Accessibility

- **Contrast:** all text/background pairings from Section 2.2 are intended to meet WCAG 2.2 AA; re-verify manually whenever a new color pairing is introduced, in both themes.
- **Focus:** every interactive element must show `--bn-focus-ring` on keyboard focus — never `outline: none` without replacing it with this token.
- **Keyboard:** all interactive components must be fully operable via keyboard alone. The FAQ accordion deliberately uses native `<details>/<summary>` specifically so this comes for free, without custom JS key-handling.
- **Semantics:** use the correct native element before reaching for ARIA. ARIA attributes are added only to fill a genuine semantic gap (e.g. `aria-pressed` on the theme toggle, `aria-live` for dynamic tool output regions — required on every tool page, per the Tool Page Prompt in `AI_Prompts.md`).
- **Images/icons:** every meaningful image needs alt text; every decorative icon needs `aria-hidden="true"`.
- **Reduced motion:** respected globally (see Section 14).

---

## 16. Dark Mode

- **Mechanism:** a single `data-theme="light"|"dark"` attribute on the root wrapper (`#bn-app` on the homepage; the same pattern should wrap every future page). All color tokens are redefined inside `[data-theme="dark"] { ... }` — component CSS never checks the theme directly, it only ever references tokens.
- **Initial state:** detected via `prefers-color-scheme` on load.
- **Persistence:** the homepage reference build keeps the toggle in-memory only. **On the live Blogger site, add `localStorage` persistence** (save/read the chosen mode) — this was intentionally left out of the demo file only because in-chat previews don't support browser storage; it's expected and required in production.
- **Rule:** any new component must be checked in both themes before shipping — a component that "only looks right in light mode" is not done.

---

## 17. CSS Architecture

All CSS lives in a single sectioned stylesheet (Blogger has one theme stylesheet), organized in this fixed order — **never add a rule out of its section**:

```
1. Variables   → :root tokens + [data-theme="dark"] overrides
2. Base        → resets, base element styles, global focus/motion rules
3. Layout      → .bn-container, .bn-section, .bn-grid and grid variants
4. Components  → header, buttons, hero, search, cards, faq, footer, etc.
5. Utilities   → .bn-visually-hidden, .bn-text-center, small single-purpose helpers
6. Tool-specific → styles unique to one tool's interactive UI (kept minimal — reuse Components wherever possible)
7. Responsive  → any global breakpoint override not already handled inline per-component
```

Component-level responsive overrides (e.g. a card grid's `minmax()` at different sizes) live inline within that component's own block in Section 4, not duplicated into Section 7 — Section 7 is only for page-wide adjustments.

---

## 17a. XML Compliance (Blogger Publishing)

Blogger's theme/template editor parses all pasted markup as **strict XML**, not lenient HTML. Every page built for this platform must satisfy the following before it's considered done — these are hard requirements, not style preferences, because a violation blocks publishing entirely rather than just looking wrong:

1. **One root element only.** A pasted snippet may have exactly one top-level element. Comments may sit outside it, but if a page needs multiple sibling blocks (JSON-LD `<script>` tags, `<style>`, content `<div>`, logic `<script>`), wrap all of them in a single containing element.
2. **No `--` inside comments.** XML comments (`<!-- -->`) forbid the two-character sequence `--` anywhere in their body — including CSS token names like `--bn-primary` written in prose. Refer to tokens without the leading double-dash inside comments (e.g. "the bn-primary token").
3. **Self-close every void element.** `<input>`, `<br>`, `<img>`, `<meta>`, `<link>`, `<hr>` must be written as `<input .../>`, `<br/>`, etc. — HTML's "unclosed void element" convention is not valid XML.
4. **No bare boolean attributes.** `hidden`, `required`, `disabled`, `checked`, `readonly`, `open`, `selected` must be written with an explicit value: `hidden="hidden"`, `required="required"`.
5. **Escape every raw `&`.** In ordinary markup/text content, `&` must be written `&amp;`. **Exception — inline `<script>` blocks:** escaping `&`/`&&` there would corrupt real JavaScript (`&&` the logical operator), so instead wrap the entire script body in a CDATA section: `<script>//<![CDATA[ ... real, unescaped JS ... //]]></script>`. The `//` comment markers keep the CDATA delimiters harmless to the JS engine while the CDATA itself keeps the XML parser from trying to interpret the script's content as markup.
6. **Never self-close a non-void HTML element** — `<span>`, `<div>`, `<a>`, etc. written as `<span id="x"/>` are valid XML but a **real, live Blogger rendering bug**: Blogger's XML-to-HTML output doesn't reliably preserve the self-closing convention for non-void elements the way it does for true void elements, and a browser's HTML parser can then treat the unclosed tag as swallowing all following markup until the next matching closing tag appears anywhere later in the page — corrupting the entire rest of the render. Always write a real closing tag: `<span id="x"></span>`. This is stricter than plain XML validity requires, specifically because of this Blogger-specific behavior.

**Verification before shipping any page:** parse the final snippet as XML (single well-formed root, no artificial wrapper needed to pass), and separately scan for any self-closed element outside the true void-element list (`area, base, br, col, embed, hr, img, input, link, meta, param, source, track, wbr` — plus SVG child elements like `path`/`circle`/`rect`, which are fine self-closed) and outside Blogger's own `b:`/`data:` template tags. Both checks are cheap and catch the overwhelming majority of real Blogger publish failures before they ever reach the editor.

---

## 18. Naming Convention

- **CSS custom properties:** `--bn-{category}-{variant?}-{state?}`, e.g. `--bn-primary-hover`, `--bn-fs-2xl`, `--bn-space-6`. Always prefixed `bn-` to avoid collision with Blogger's own theme variables.
- **CSS classes:** `.bn-{component}` for the root of a component, `.bn-{component}-{part}` for a sub-part, `.bn-{component}--{variant}` for a modifier (double-hyphen, BEM-style), e.g. `.bn-tool-card`, `.bn-tool-card-icon`, `.bn-btn--primary`.
- **IDs:** reserved for JS hooks and single-instance landmarks only (`#bn-search-input`, `#bn-app`) — never used for styling.
- **File/slug naming** (ties to Master Spec Section 14/17): lowercase, hyphen-separated, matching the tool/category name exactly (`json-formatter`, `developer-tools`) — no abbreviations that don't match the visible title.
- **JS:** camelCase functions/variables, one IIFE per page/tool to avoid global scope pollution (Master Spec Section 10).

---

## 19. Component Rules

0. **No page may redefine an existing component.** If a component requires enhancement (a new state, a new size, a new variant), the change is made **in the Component Library first** (`Component_Library.md` — see `Documentation_Governance_v1.0.md`), then adopted by pages. A page-level override of a component's styling is never acceptable, even "just this once."
0a. **No script may add a JS module outside `Banynova.register()`.** Every module — this file's or a future tool page's — goes through the registration function documented in Section 12b, never a direct `Banynova.x = {...}` assignment. This is the JS-side equivalent of Rule 0 above.
1. **Before building any new UI, check Sections 9–13 first.** If what's needed already exists as a Button, Card, Nav pattern, or Icon style, reuse it exactly — don't restyle it "just for this page."
2. **A genuinely new component** (something not covered by Buttons/Forms/Cards/Navigation) must be proposed and added to this document — with its states, tokens used, and accessibility behavior documented — before or immediately after it ships. This keeps the "never redesign" philosophy real rather than aspirational.
3. **Every component must be theme-safe** (Section 16), **keyboard-accessible** (Section 15), and **built only from tokens** (Sections 2–7) — no exceptions for "just this once."
4. **Deprecating a component:** if a pattern is replaced, mark it deprecated here with a note on what replaced it, rather than silently deleting the row — future contributors (or an AI session with no memory) need the history.

---

## 20. Appendix — Adopted Build Order (Development Roadmap)

Agreed sequence for building out the platform, so each stage has a solid foundation before the next depends on it:

| Step | Stage | Status |
|---|---|---|
| 1 | **Design System** (this document) | ✅ Complete |
| 2 | Global Components — Header, Footer, Navigation | ✅ Built directly into `Base_Layout.xml` (Header/Footer/Nav are sitewide, not per-page copies — the goal of this step was achieved, just not via separate standalone include files as originally envisioned) |
| 3 | Homepage Directory | 🟡 In progress — Hero (with real search), Popular Tools, Categories, Latest Articles, and New Tools are live in `Base_Layout.xml`. Why Choose, Platform Stats, FAQ, and Newsletter are designed (Section 11b) but not yet built. |
| 4 | Universal Tool Template | ⬜ Pending |
| 5 | JSON Formatter (reference tool, validates the Universal Tool Template) | ⬜ Pending |
| 6 | Remaining categories & tools | ⬜ Pending |
| 7 | Articles, SEO & affiliate integration | ⬜ Pending |

Note: Step 2 turned out not to need separate standalone include files — Blogger's `<b:section>`/`<b:widget>` model already makes Header/Footer genuinely sitewide from a single definition in `Base_Layout.xml`, so "extracting" them into something else would have been redundant. All homepage sections built so far use mock data (Section 11's `TOOLS`/`CATEGORIES`/`ARTICLES` arrays) explicitly designed to be swapped for a real `tools-index.json` fetch (Master Spec Section 15) once Steps 4–6 produce real tools — nothing about the render logic needs to change when that swap happens.

---

## 21. Open Items / Known Gaps

*(Tracked honestly rather than glossed over — resolve before the relevant build step.)*

- ~~Mobile navigation pattern~~ — resolved, see Section 12 (hamburger + slide-down panel + overlay + focus trap + scroll lock).
- ~~Dark mode persistence~~ — resolved. `Banynova.theme` uses real `localStorage`, plus a no-flash-of-wrong-theme inline script that runs before first paint.
- ~~Header search-icon-opens-a-modal pattern~~ — superseded. The Hero has its own real, always-visible search (Section 12a); a separate header search trigger was never built and is no longer planned.
- Breadcrumb component not yet built — required before Step 4 (Universal Tool Template), per Master Spec Section 8.
- Alert/Toast/Modal/Tabs components (listed in Master Spec Section 9's original component list) not yet designed — `--bn-z-modal` is reserved and ready when this happens.
- **Why Choose, Platform Stats, FAQ, and Newsletter** homepage sections designed (Section 11b) but not yet built into `Base_Layout.xml` — the remaining piece of Roadmap Step 3.
- **Real `tools-index.json`** doesn't exist yet — every homepage section currently renders from hardcoded mock arrays inside the `directory` module (Section 12b). Swapping to real data is a Step 4–6 dependency, not a Design System change.
- Category hub pages (`/p/developer-tools.html`, etc.) that the Category Cards already link to don't exist yet — same dependency as above.

---

## 22. Changelog

| Version | Date | Change |
|---|---|---|
| 1.0 | {{fill in date}} | Initial Design System formalized from the homepage reference build and supplied design tokens |
| 1.1 | {{fill in date}} | Added Section 2.4 (Gradient & Glass tokens) to support the premium homepage refresh — sticky glass header, single-accent gradient use. Added Tutorial Card optional `image` + `publishedDate` fields (Section 11) and Header mobile-nav + search-trigger pattern (Section 12). |
| 1.2 | {{fill in date}} | Added Section 17a (XML Compliance) after two real Blogger publish failures on the homepage — single-root-element rule, comment `--` restriction, void-element self-closing, boolean attribute values, and the CDATA pattern for inline scripts. |
| 1.3 | {{fill in date}} | Major sync with the now-live `Base_Layout.xml`, after Roadmap Step 3 (Homepage Directory) reached Hero + Popular Tools + Categories + Latest Articles + New Tools. Fixed Section 3.4's heading scale to match a real mobile h1/h2 collision bug found and fixed live. Section 7 gained header-height and the z-index token scale. Section 11 rewritten: Tool/Category/Article Card finalized (Tutorial Card renamed Article Card), New Badge documented, Section Heading pattern added as 11a, Stat Block/Newsletter moved to 11b and marked not-yet-built. Section 12 rewritten: final 3-item header nav (Tools and Categories removed, with the trade-off explicitly documented), real footer structure, active-link URL normalization, and a new 12a (Hero & Search) and 12b (JavaScript Module Architecture — the `Banynova.register()` pattern, the frozen-module `this.x =` gotcha). Section 13 gained the SVG symbol/use sprite pattern for the logo. Section 17a gained Rule 6 (never self-close non-void elements) after a second real Blogger rendering bug. Section 19 gained a JS-module parallel to the existing CSS component rule. Sections 20–21 updated to reflect actual build status. |
