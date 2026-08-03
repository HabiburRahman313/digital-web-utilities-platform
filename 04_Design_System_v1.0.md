# Banynova — Design System v1.0

**Project Philosophy:** Build the foundation once. Reuse it everywhere. Never redesign.

**Companion to:** Master_Project_Specification_v1_0.md, AI_Prompts.md, Brand Voice Guide
**Position in hierarchy:** Governed by `Documentation_Governance_v1.0.md` — this document is the child of Master Project Specification and the parent of Component_Library.md.
**Status:** Locked as of the Homepage build — this document now governs every future page, tool, and component.

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

**Standard grid pattern:** `display: grid; grid-template-columns: repeat(auto-fill, minmax(Xpx, 1fr)); gap: var(--bn-space-5);`

| Grid context | `minmax()` floor |
|---|---|
| Tool cards | 260px |
| Category cards | 220px |
| Tutorial cards | 280px |

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

Three card types exist. **No new card variant may be created without adding it to this table first.**

| Card | Component class | Contains | Reference build |
|---|---|---|---|
| **Tool Card** | `.bn-tool-card` | Icon chip (`--bn-primary-subtle` bg), category label, name, description, "Open tool →" link | Homepage `#bn-popular-grid` |
| **Category Card** | `.bn-cat-card` | Icon chip (`--bn-accent` solid bg), name, tool count | Homepage `#bn-featured-categories` / `#bn-all-categories` |
| **Tutorial Card** | `.bn-tut-card` | Category tag, title, description, meta (read time) | Homepage `#bn-tutorials-grid` |

Shared card rules: `--bn-radius-lg`, `--bn-surface` background, `--bn-border` default border, hover state = border color shift + `translateY(-2px)` + (Tool Card only) `--bn-shadow-2`. All transitions use `--bn-transition-fast`.

---

## 12. Navigation

**Header** (`.bn-header`): sticky top, `--bn-surface` background, bottom border. Contains logo (left), primary nav links (center/right, hidden below 860px — mobile menu pattern is an open item, see Section 21), and header actions (theme toggle, future: search icon trigger) on the far right.

**Footer** (`.bn-footer`): four-column grid (brand+tagline, Categories, Company, Legal) collapsing to two columns under 760px, with a bottom bar (copyright + privacy trust line) separated by a top border.

**Breadcrumbs** (used on tool/category pages per Master Spec Section 7, 8): not yet built in a dedicated component — required before the Universal Tool Template ships (Section 21 open item).

---

## 13. Icons

- **Style:** line icons only, 2px stroke width, `stroke="currentColor"` (never a hard-coded fill color) so icons automatically match text color and adapt to light/dark mode with zero extra code.
- **Format:** inline SVG, `viewBox="0 0 24 24"`, no external icon font/library dependency (keeps the site framework-free per Master Spec Section 4, and avoids an extra network request).
- **Sizing:** 14–16px for inline/metadata icons, 18–20px for buttons/search, 22–24px for card icon chips, 28px for the "Why Choose" feature icons.
- **Decorative icons** get `aria-hidden="true"`; any icon that is the *only* content of an interactive control (e.g. the theme toggle button) must have an `aria-label` on the parent control instead.
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

## 18. Naming Convention

- **CSS custom properties:** `--bn-{category}-{variant?}-{state?}`, e.g. `--bn-primary-hover`, `--bn-fs-2xl`, `--bn-space-6`. Always prefixed `bn-` to avoid collision with Blogger's own theme variables.
- **CSS classes:** `.bn-{component}` for the root of a component, `.bn-{component}-{part}` for a sub-part, `.bn-{component}--{variant}` for a modifier (double-hyphen, BEM-style), e.g. `.bn-tool-card`, `.bn-tool-card-icon`, `.bn-btn--primary`.
- **IDs:** reserved for JS hooks and single-instance landmarks only (`#bn-search-input`, `#bn-app`) — never used for styling.
- **File/slug naming** (ties to Master Spec Section 14/17): lowercase, hyphen-separated, matching the tool/category name exactly (`json-formatter`, `developer-tools`) — no abbreviations that don't match the visible title.
- **JS:** camelCase functions/variables, one IIFE per page/tool to avoid global scope pollution (Master Spec Section 10).

---

## 19. Component Rules

0. **No page may redefine an existing component.** If a component requires enhancement (a new state, a new size, a new variant), the change is made **in the Component Library first** (`Component_Library.md` — see `Documentation_Governance_v1.0.md`), then adopted by pages. A page-level override of a component's styling is never acceptable, even "just this once."
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
| 2 | Global Components — Header, Footer, Navigation (extracted as standalone reusable includes) | ⬜ Next |
| 3 | Homepage Directory | ✅ Built (reference implementation — will be revisited once Global Components are formalized in Step 2) |
| 4 | Universal Tool Template | ⬜ Pending |
| 5 | JSON Formatter (reference tool, validates the Universal Tool Template) | ⬜ Pending |
| 6 | Remaining categories & tools | ⬜ Pending |
| 7 | Articles, SEO & affiliate integration | ⬜ Pending |

Note: the homepage was built (previous session) before this Design System document was formalized — it already follows these tokens correctly since it was the source these values were extracted from, but Step 2 (Global Components) should formally extract its Header/Footer into standalone reusable snippets before the Universal Tool Template (Step 4) is built, so tool pages inherit the exact same header/footer rather than copy-pasting them per page.

---

## 21. Open Items / Known Gaps

*(Tracked honestly rather than glossed over — resolve before the relevant build step.)*

- Mobile navigation pattern (hamburger menu / off-canvas) not yet designed — needed before Step 2.
- Breadcrumb component not yet built — required before Step 4 (Universal Tool Template), per Master Spec Section 8.
- Dark mode persistence (`localStorage`) intentionally omitted from the homepage demo file — must be added when deployed live on Blogger.
- Alert/Toast/Modal/Tabs components (listed in Master Spec Section 9's original component list) not yet designed — add here when first needed, likely during Step 4 or 6.

---

## 22. Changelog

| Version | Date | Change |
|---|---|---|
| 1.0 | {{fill in date}} | Initial Design System formalized from the homepage reference build and supplied design tokens |
