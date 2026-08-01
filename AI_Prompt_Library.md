Document:
AI Development Prompt Library
Version:1.0 , Status:Active
Maintainer: HABIBUR RAHMAN, Last Updated: 2026-08-01

# Table of Contents

0. How to Use This Library (SOP)

1. Golden Prompt

2. Project Planning Prompt

3. Homepage Prompt

4. Tool Page Prompt

5. JavaScript Prompt

6. HTML Prompt

7. CSS Prompt

8. Blogger Prompt

9. SEO Prompt

10. Article / Tutorial Prompt

11. Affiliate Prompt

12. UI Review Prompt

13. Code Review Prompt

14. Refactoring Prompt

15. Documentation Prompt

16. Feature Development Prompt

17. Accessibility Prompt Library

18. Security Review Prompt

19. Image Generation Prompt Library

20. Icon & Illustration Prompt Library

21. AI Content Quality Prompt

22. Testing & QA Prompt

23. Performance Optimization Prompt

24. Browser Compatibility Prompt

25. Release Checklist Prompt

26. Changelog
# AI Development Prompt Library — Digital / Web Utilities Platform

**Document version:** 1.0
**Companion to:** Master_Project_Specification_v1_0.md
**Purpose:** A single source of truth for every prompt used to build, review, and extend this project with AI assistance — so quality and architecture stay consistent whether it's tool #3 or tool #180.

---

## 0. How to Use This Library (SOP)

**Bangla:** এই ফাইলটি একটি Standard Operating Procedure (SOP)। যেকোনো নতুন কাজ (নতুন Tool, নতুন Article, নতুন Feature ইত্যাদি) শুরু করার আগে —

1. প্রথমে **Section 1 — Golden Prompt** কপি করে দিন। এটি AI-কে পুরো Project-এর context দেয়।
2. তারপর কাজের ধরন অনুযায়ী নির্দিষ্ট Prompt (Tool Page Prompt / SEO Prompt / Code Review Prompt ইত্যাদি) কপি করে, `{{...}}` জায়গাগুলো পূরণ করে, Golden Prompt-এর পরে জুড়ে দিন।
3. AI-এর output Master Spec-এর বিপরীতে যাচাই করুন (বিশেষত Section 8, 9, 10, 12, 13, 19 — এগুলোই সবচেয়ে বেশি লঙ্ঘন হয়)।
4. এই ফাইলে নতুন কোনো ভালো Prompt পেলে সেটি এখানে যোগ করুন, সংস্করণ (version) নম্বর বাড়ান, এবং Section 26-এর Changelog-এ এন্ট্রি দিন।

**Rules for every prompt in this library:**
- Every prompt must explicitly reference the Master Spec section(s) it depends on.
- Every prompt must be self-contained enough that a fresh AI session (with no memory of past chats) produces spec-compliant output.
- Never let an AI silently introduce a framework, dependency, or pattern not covered in the Master Spec (Section 4) — if it wants to, it must flag it as a proposal, not apply it.
- Placeholders use `{{DOUBLE_BRACES}}` — always fill them in before sending.

---

## 1. Golden Prompt
*(Paste this first, at the start of every AI session, before any task-specific prompt below.)*

```
You are acting as a Senior Software Architect and Front-End Engineer on a long-running
project: a 100% free, client-side Digital/Web Utilities Platform built on Blogger.com,
scaling from ~20 tools to 200+ tools over 18 months without redesign.

Non-negotiable architectural facts (do not deviate from these unless I explicitly say so):
- Platform: Blogger.com free tier. Hard limit of 20 static Pages. Posts are unlimited.
  Tools and tutorials are published as Posts. Categories are Pages that manually curate
  links to their tools (hybrid Pages + Labels model).
- Stack: Pure HTML, Pure CSS, Vanilla JavaScript only. No backend, no database, no
  frameworks (no Bootstrap, no jQuery, no build step). Every tool runs 100% client-side.
- Prefer native browser APIs (Canvas, File/FileReader, Web Crypto, Clipboard, Intl) over
  third-party libraries. Only introduce a library when a native API genuinely cannot do
  the job, and note the trade-off explicitly.
- Security: never use Math.random() for anything security-related — use
  crypto.getRandomValues() / crypto.subtle.
- Privacy: no uploaded file or user input is ever transmitted to a server. All processing
  is local to the browser. Never silently add tracking, cookies, or external calls.
- Every tool page and every tool card follows one identical structure — no bespoke
  layouts per tool (see Master Spec Sections 8 and 9).
- Performance targets: LCP < 2s, CLS ~ 0, INP < 200ms. JS is modular and loaded per-tool,
  never one monolithic tools.js.
- Accessibility target: WCAG 2.2 AA as closely as practical.
- Design system: use existing design tokens (color, spacing, radius, shadow, typography
  scale, breakpoints) and existing reusable components — do not invent new one-off styles.

Your responsibilities in this conversation:
1. Follow the Master Project Specification as the highest authority. If my request
   conflicts with it, point out the conflict before proceeding rather than silently
   picking one.
2. Think like a software architect: consider scalability to 200+ tools, migration-
   readiness (Section 14), and long-term maintainability — not just "does this one page
   look good."
3. If information you need is missing (e.g. exact tool name, category, target keyword),
   ask for it rather than inventing plausible-sounding specifics.
4. Flag anything that looks like it will create technical debt, inconsistency, or an
   SEO/accessibility/performance risk, even if I didn't ask about it.

Confirm you've understood these constraints, then wait for my next, task-specific prompt.
```

---

## 2. Project Planning Prompt
*(Architecture, roadmap, scalability decisions — Master Spec Sections 0–3, 27, 28.)*

```
Act as a Senior Software Architect reviewing a scaling decision for this platform.

Context: {{describe the decision — e.g. "we're about to add a 9th category" or
"we're at 45 tools and search feels slow"}}

Evaluate this against:
- The 20-Page budget (Section 0 and 27) — will this decision consume a Page we can't
  get back? Is there a Page-free alternative (Label-only, or folded into an existing hub)?
- The current Build Roadmap phase (Section 28) — does this fit the current phase, or is
  it premature/overdue for our stage?
- Migration-readiness (Section 14) — does this decision make a future move to
  WordPress/Astro/Next.js harder or easier?
- Scalability (Section 2, 27) — will this still work cleanly at 200 tools, or does it
  only work at current scale?

Deliver:
1. A recommendation (proceed / proceed with modification / don't do this yet)
2. The specific trade-offs of your recommendation
3. Any update this implies for the Master Spec or the redirect-map spreadsheet
4. Rollback plan if this turns out to be wrong
```

---

## 3. Homepage Prompt
*(Directory, search, category cards, tool cards — Master Spec Section 6, 9.)*

```
Build/update the homepage for this platform per Master Spec Section 6.

Required sections, in order: Hero, site-wide search, Popular tools, Featured categories,
Full category grid, Latest tutorials, Why choose this platform, FAQ, Footer.

Constraints:
- Search must use the tools-index.json client-side filtering approach (Section 15), not
  Blogger's native search.
- Category cards and tool cards must use the existing Tool Card / Category Card
  components exactly as defined in the design system (Section 9) — same icon slot,
  name, short description, category label, "Open Tool" button. No one-off card variants.
- Layout must be CSS Grid/Flexbox based so it stays clean at 20, 50, and 200 tools —
  explicitly tell me how you validated this (e.g. "tested with N mock cards").
- No render-blocking resources in <head>; homepage JS should only include what the
  homepage itself needs (global search/theme/clipboard modules), not per-tool logic.

Input I'll give you: {{current tool count, list of featured tools/categories, or "use
placeholder data"}}

Output: semantic HTML + CSS (using existing design tokens) + minimal vanilla JS for the
search box, ready to paste into a Blogger theme/page.
```

---

## 4. Tool Page Prompt
*(The universal template — use for every single tool. Master Spec Section 8.)*

```
Create a complete tool page for: {{TOOL_NAME}} (category: {{CATEGORY}}, label: {{LABEL_SLUG}})

Follow the Standard Tool Page Structure from Master Spec Section 8 exactly, in this order:
1. SEO title, meta description, custom permalink slug (propose 3 slug options)
2. Breadcrumb (Home > {{CATEGORY}} > {{TOOL_NAME}})
3. H1
4. Introduction (what it does, who it's for)
5. The interactive tool itself (functional, client-side, vanilla JS)
6. Features
7. Step-by-step usage guide
8. Real examples (with actual sample input/output, not placeholders)
9. Common use cases
10. Tips & best practices
11. FAQ (3–5 realistic questions)
12. Related tools (2–4 internal links — propose which existing tools these should be)
13. Related tutorials (propose 1–3 tutorial titles per Section 16)
14. Conclusion
15. Last updated date + version number
16. Structured data (SoftwareApplication + FAQPage + BreadcrumbList JSON-LD, Section 18)

Also apply:
- Tool Quality Standards (Section 8.1): input validation, copy button, reset button,
  example input, example output, mobile optimization, fast execution.
- Tool Card entry (Section 8.2) for the directory: icon, name, short description,
  category, "Open Tool" button.
- Target 500–800 words of unique surrounding content (not counting the tool UI itself).
- Target keywords: the tool name plus problem-solving/long-tail variants (Section 17) —
  propose the keyword list before writing the copy.
- Error handling per Section 20 (specific, actionable messages — never "Something went
  wrong").
- Security/privacy notices per Section 19 if the tool touches files or sensitive input.

Output as: (a) the keyword list, (b) the HTML/CSS/JS, (c) the JSON-LD block, separately.
```

---

## 5. JavaScript Prompt
*(Use whenever writing a new tool's logic — Master Spec Section 10.)*

```
Write the JavaScript for the {{TOOL_NAME}} tool.

Constraints:
- Vanilla ES6+ only. No frameworks, no jQuery.
- Isolated, self-contained module for this tool only — do not add anything to a shared
  tools.js. It should be safe to load only on this tool's page.
- Import only the global modules it actually needs (Section 10): e.g. Clipboard helper,
  Validation helper — name exactly which ones and why.
- Use native browser APIs first (Section 4): {{list relevant APIs, e.g. Canvas API for
  image resize, Web Crypto for token generation}}. Only propose a third-party library if
  no native API can do this, and explain the gap.
- If this tool touches randomness for anything security-adjacent (passwords, tokens,
  keys), use crypto.getRandomValues() — never Math.random().
- No inline JS in the HTML (Section 10.1). No global namespace pollution — wrap in an
  IIFE or module scope.
- Must implement: input validation, copy-to-clipboard, reset, and clear/specific error
  states per Section 20.
- Must degrade gracefully if a required browser API is unavailable (Section 11) — show a
  clear message, don't silently fail.
- Keep it lazy-loadable: if this tool needs a third-party library, structure the code so
  the library is only fetched on user interaction (Section 13), not on page load.

Explain briefly at the end which native APIs you used and why, so I can verify against
Section 4.
```

---

## 6. HTML Prompt
*(Structure and markup for any page/component — Master Spec Section 10.1, 12.)*

```
Write the HTML for: {{page or component name}}

Constraints:
- Semantic HTML5 only (header, nav, main, section, article, footer, etc. — not div soup).
- No inline styles, no inline event handlers/JS (Section 10.1).
- Proper heading hierarchy — exactly one H1, logical H2/H3 nesting, no skipped levels
  (Section 12).
- Include ARIA attributes only where semantic HTML isn't sufficient — don't over-ARIA.
- All images need meaningful alt text (empty alt="" only for purely decorative images).
- All interactive elements must be reachable and operable via keyboard alone, with a
  visible focus state (Section 12).
- Reuse existing component markup patterns from the design system (Section 9) — if this
  needs a new component, flag it as new rather than silently improvising.
- Structure should match the Standard Tool Page Structure (Section 8) if this is a tool
  page, or the Homepage/Category Hub structure (Section 6/7) if applicable.

Output clean, indented HTML with brief comments marking each structural section.
```

---

## 7. CSS Prompt
*(Styling — Master Spec Section 9.)*

```
Write the CSS for: {{page or component name}}

Constraints:
- Use existing design tokens only — Primary/Secondary, Success/Warning/Danger, border
  radius, shadow levels, spacing scale, typography scale, breakpoints, hover animation
  duration, max content width, grid spacing. List which tokens you used; do not invent
  new raw hex values, font sizes, or spacing values.
- Follow the CSS organization order: Variables → Base → Layout → Components → Utilities
  → Tool-specific → Responsive (Section 9). Place this code in the correct section and
  say which one.
- Mobile-first: write base styles for small screens, then add breakpoints upward.
- No CSS frameworks, no utility-class libraries (Tailwind etc. unless explicitly part of
  the design system) — Section 4.
- Must support Light Mode, Dark Mode, and System Preference (Section 21) — use CSS
  variables that flip per theme, not duplicated rulesets.
- Verify contrast ratios meet WCAG 2.2 AA (Section 12) for both themes.
- Grid/Flexbox layouts must remain clean whether there are 5 items or 200 (Section 6/27)
  — no hard-coded item counts or fixed-width assumptions.

Output CSS only, grouped under clear section comments, ready to append to the single
Blogger stylesheet.
```

---

## 8. Blogger Prompt
*(Platform-specific packaging/publishing — Master Spec Section 0, 14.)*

```
Adapt the following HTML/CSS/JS for publishing on Blogger.com (free tier): {{paste code
or describe the page}}

Constraints:
- Respect the 20-Page limit (Section 0) — confirm whether this should be a Page or a
  Post, and why, before producing anything.
- If it's a tool/tutorial: it's a Post. Propose an SEO-friendly slug knowing the final
  URL will be yourdomain.com/YYYY/MM/{{slug}}.html (Section 10/14) — the date segment is
  unavoidable, don't try to remove it.
- If it's a category hub: it's a Page, and must include a hand-curated tool directory
  (Section 7), not just an auto label-archive link.
- CSS must merge into the single site-wide stylesheet, correctly sectioned (Section 9) —
  don't produce a separate stylesheet per page.
- JS must be scoped so it only runs on its intended page (Blogger serves the same
  template site-wide) — guard with a page/element existence check, not just page URL.
- Add this URL to the redirect-map spreadsheet entry (old Blogger URL → intended future
  clean URL) per Section 14 — output that row for me to paste in.
- Flag anything Blogger's editor is known to mangle (smart quotes, script tag stripping,
  etc.) so I can watch for it on paste.
```

---

## 9. SEO Prompt
*(On-page SEO — Master Spec Section 17, 18.)*

```
Do SEO planning/optimization for: {{tool or article name}}

Deliver:
1. Primary keyword + 5–8 secondary/long-tail keyword variants, following the
   informational/problem-solving/comparison pattern in Section 17 (not just the tool
   name itself).
2. SEO title (under ~60 characters) and meta description (under ~155 characters) using
   the primary keyword naturally.
3. A proposed H1 and heading outline that maps to the Standard Tool Page Structure
   (Section 8).
4. Internal linking plan: which category hub it links to, 2–4 related tools, and
   relevant tutorials (Section 17) — name them specifically, don't say "link to related
   content."
5. The JSON-LD structured data block(s) required per Section 18
   (SoftwareApplication/Article + FAQPage + BreadcrumbList as applicable).
6. A check against Section 8's 500–800 word target and Section 25's AI Content Policy
   (originality, accuracy) — flag if the draft content risks reading as thin or
   AI-generic.

Do not fabricate statistics, review counts, or user numbers to sound more authoritative.
```

---

## 10. Article / Tutorial Prompt
*(Educational content — Master Spec Section 16, 25.)*

```
Write a tutorial/article: {{working title}}, supporting the tool {{TOOL_NAME}}.

Constraints:
- Follows the tutorial ladder pattern in Section 16 (e.g. for JSON Formatter: How to
  Format JSON → JSON Parse Error Guide → JSON Validator vs. Formatter → ...). Tell me
  where in that ladder this article sits.
- Must link back to {{TOOL_NAME}} and at least one other related tool/tutorial
  (Section 17).
- Content must be original, technically accurate, and genuinely helpful — not a
  reworded version of existing top-ranking articles (Section 25). You may draft it, but
  flag it clearly as "AI draft — needs human review" per policy.
- Include real, correct examples — verify any code/output samples are actually correct,
  don't approximate.
- End with a clear conclusion and a call-to-action pointing to the related tool.
- Suggest a "last updated" cadence for this piece given how fast the subject matter
  changes (Section 26 — Maintenance Plan).

Output: outline first for my approval, then full draft.
```

---

## 11. Affiliate Prompt
*(Contextual monetization — Master Spec Section 22.)*

```
Propose affiliate placement for: {{tool or category name}}

Constraints:
- Recommendation must appear only after the user has already received value from the
  tool (Section 22) — specify exactly where on the page (e.g. "after the result output,
  before the FAQ section"), never above or interrupting the tool itself.
- Only suggest partners relevant to the category, using Section 22's existing mapping
  (Developer Tools → Hostinger/GitHub/VS Code/JetBrains; SEO Tools → Semrush/Ahrefs;
  Security Tools → NordVPN/Surfshark) or propose a new partner with a clear category fit
  and disclose it's a new addition.
- Write the recommendation as genuinely useful context, not an ad-style pitch — one to
  two sentences of real value, not a banner.
- Confirm the placement won't obstruct tool usage or trigger accidental clicks
  (Section 23) — describe the exact spacing/isolation from interactive controls.
- Note that this needs an affiliate disclosure per standard FTC/consumer-protection
  practice — draft the disclosure line.
```

---

## 12. UI Review Prompt
*(Visual/UX consistency check — Master Spec Section 6–9, 21.)*

```
Review this page/component against the design system: {{paste HTML/CSS or screenshot
description}}

Check specifically for:
1. Are all colors, spacing, radius, shadows, and type sizes coming from existing design
   tokens (Section 9), or are there one-off values?
2. Does every card/button/form element match the existing component patterns, or has a
   bespoke variant crept in (Section 8.2, 9)?
3. Does it look correct in both Light and Dark mode (Section 21)?
4. Does the layout hold up at mobile, tablet, and desktop breakpoints (Section 3, 6)?
5. Is visual hierarchy clear (heading sizes, spacing rhythm) and consistent with other
   pages on the site?
6. Any hover/focus/active states missing or inconsistent with the rest of the site
   (Section 12)?

Output a numbered list of specific issues (not general praise), each with the exact
fix.
```

---

## 13. Code Review Prompt
*(Master Spec Section 4, 10, 10.1, 19.)*

```
Review this code as a senior engineer: {{paste code}}

Check specifically for:
1. Any framework/library usage not justified per Section 4 (native API should have been
   used instead)?
2. Any Math.random() used for anything security-adjacent (Section 4) — must be
   crypto.getRandomValues()/crypto.subtle instead?
3. Inline CSS or inline JS (Section 10.1)?
4. Any code that would leak into a shared/global scope and affect other tools
   (Section 10)?
5. Any user file/data being sent anywhere over the network (Section 19) — must be 100%
   client-side?
6. Missing input validation, unclear error messages, or generic "Something went wrong"
   failures (Section 20)?
7. Any accessibility gaps — missing labels, poor focus handling, missing alt text
   (Section 12)?
8. Any obvious performance issue — large synchronous work blocking the main thread,
   unnecessary re-renders/reflows, unoptimized images (Section 13)?

Output: a severity-ranked list (blocker / should-fix / nice-to-have), each with the
specific line/pattern and the fix.
```

---

## 14. Refactoring Prompt
*(Master Spec Section 9, 10, 27.)*

```
Refactor this code without changing its external behavior: {{paste code}}

Goals, in priority order:
1. Align with current design tokens and component patterns (Section 9) if this predates
   them.
2. Break any monolithic script into isolated, per-tool modules if it currently loads
   more than it needs (Section 10).
3. Improve naming, consistency of indentation, and remove dead code (Section 10.1).
4. Make it easier to replicate for the next 10 tools in this category — i.e. extract
   anything that should become a shared pattern, and clearly mark what's tool-specific
   vs. reusable (Section 27).
5. Do not introduce any new dependency, framework, or pattern not already sanctioned in
   Section 4.

Show a before/after diff-style summary plus the full refactored code, and list anything
you deliberately left unchanged and why.
```

---

## 15. Documentation Prompt

```
Write documentation for: {{feature/tool/component name}}

Audience: {{future-me / a new contributor / end users}}

Include:
- Purpose and where it fits in the Master Spec (cite the relevant section number(s))
- How it works (brief technical explanation, not a code walkthrough)
- Dependencies (native APIs used, any third-party library and why it was necessary per
  Section 4)
- How to extend/replicate it for a similar future tool or feature
- Known limitations or deliberate trade-offs
- Last updated date

Keep it concise — this goes in the project's internal documentation, not a public-facing
page.
```

---

## 16. Feature Development Prompt
*(New capabilities beyond a single tool — Master Spec Section 2, 27, 28.)*

```
Plan and scope a new feature: {{feature name/description}}

Deliver, in order:
1. Which Master Spec section(s) this touches or extends.
2. Page/Post/Label impact — does this consume any of the 20-Page budget (Section 0/27)?
   If yes, propose how to avoid it or justify the spend.
3. Design system impact — does this need new components/tokens, or can it reuse existing
   ones (Section 9)?
4. Performance impact — will this affect Core Web Vitals targets (Section 13)? How will
   it be lazy-loaded if heavy?
5. Where it fits in the Build Roadmap (Section 28) — is this the right phase for it?
6. A step-by-step implementation plan, broken into independently shippable chunks.
7. How this will be tested (tie to Section 22's QA prompt) before going live.

Do not start writing implementation code until this plan is approved.
```

---

## 17. Accessibility Prompt Library
*(Master Spec Section 12.)*

**17.1 — Accessibility audit**
```
Audit this page/component for WCAG 2.2 AA compliance: {{paste HTML or describe page}}

Check: keyboard navigation and tab order, visible focus indicators, heading hierarchy,
semantic HTML usage, color contrast (text and UI components), ARIA usage (correct and
not overused), alt text on all images, form label associations, and screen-reader
announcement of dynamic content (e.g. tool results, error messages).

Output a numbered list of violations with WCAG success criterion reference, severity,
and the specific fix.
```

**17.2 — Accessible component build**
```
Build {{component name}} to be accessible by default:
- Full keyboard operability (Tab/Shift+Tab/Enter/Space/Escape/Arrow keys as appropriate)
- Visible focus state using existing design tokens
- Correct semantic element or ARIA role/state/property
- Announce dynamic changes (e.g. tool output, validation errors) via aria-live where
  appropriate
- Sufficient contrast in both Light and Dark mode (Section 21)

Explain which ARIA attributes you added and why, so I can verify none are redundant with
native semantics.
```

---

## 18. Security Review Prompt
*(Master Spec Section 4, 19.)*

```
Review this tool/code for security and privacy issues: {{paste code or describe tool}}

Check specifically for:
1. Any use of Math.random() for passwords, tokens, keys, or anything security-adjacent
   — must be crypto.getRandomValues()/crypto.subtle (Section 4).
2. Any network call transmitting user input, files, or generated secrets anywhere
   (Section 19) — must be zero for this platform.
3. Any use of innerHTML/insertAdjacentHTML with unsanitized user input (XSS risk) —
   even though there's no backend, a tool could still XSS itself.
4. Any client-side "encryption" tool that overstates its guarantees — must be clearly
   labeled as client-side only, with accurate claims about what it does and doesn't
   protect against.
5. Any storage of user data (localStorage, cookies, IndexedDB) that isn't strictly
   necessary and disclosed to the user (Section 19).
6. Any dependency pulled from a CDN — confirm it's pinned to a specific version/hash,
   not an unpinned "latest".

Output a severity-ranked list (blocker / should-fix / note) with the specific fix.
```

---

## 19. Image Generation Prompt Library
*(For hero images, category illustrations, OG images — supports Section 6, 9, 17.)*

**19.1 — Category/hero illustration**
```
Generate a hero/category illustration for: {{category or page name}}

Style: clean, minimal, flat-design, matches a professional developer-tools brand — not
cartoonish, not stock-photo generic. Use only colors from the existing design token
palette ({{list primary/secondary/accent colors}}). No text baked into the image (text
is handled in HTML/CSS for accessibility and SEO). Transparent or theme-neutral
background so it works in both Light and Dark mode, or provide both variants.
Output at a size appropriate for {{hero banner / OG image 1200x630 / card thumbnail}}.
```

**19.2 — Open Graph / social share image**
```
Generate an Open Graph image (1200x630) for: {{page title}}

Must include the page title text legibly, the site's visual identity (colors/typography
from the design system), and remain readable as a small thumbnail in social feeds. No
copyrighted or trademarked imagery. Keep key content within the safe zone (avoid the
outer ~5% margin, which platforms sometimes crop).
```

---

## 20. Icon & Illustration Prompt Library
*(Section 8.2, 9 — tool card icons, UI icons.)*

**20.1 — Tool card icon**
```
Design/select an icon representing: {{tool name/function}}

Constraints: single-color or two-color SVG, matches the existing icon set's stroke
width/style/corner radius, works at 24px and 48px without losing clarity, uses
currentColor (or a design-token color) so it adapts to Light/Dark mode automatically.
No literal photographic imagery — icon/pictogram style only, consistent with the rest of
the tool grid (Section 8.2 — never a custom look per tool).
```

**20.2 — UI/system icon**
```
Design/select an icon for UI element: {{e.g. "copy button", "reset button", "dark mode
toggle"}}

Must match conventional, instantly recognizable iconography for this action (don't be
clever at the expense of clarity), match existing icon set style, and include an
accessible label/tooltip text alongside it (icon alone is never sufficient per
Section 12).
```

---

## 21. AI Content Quality Prompt
*(Master Spec Section 25.)*

```
Evaluate this AI-drafted content for publication readiness: {{paste content}}

Check against Section 25's AI Content Policy:
1. Originality — does it read as a generic rewrite of common existing articles, or does
   it add genuine, specific value (real examples, accurate detail)?
2. Helpfulness — would a real user with this problem actually be served by this, or is
   it padding to hit a word count?
3. Technical accuracy — verify every factual/technical claim; flag anything you're not
   fully certain is correct rather than letting it pass.
4. Generic "AI voice" — flag hedge-y, overly formal, listicle-padded phrasing that
   doesn't match a helpful, direct human tone.
5. Word count vs. Section 8's 500–800 word target (for tool pages) — is it hitting the
   target with substance, not filler?

Output: a pass/needs-revision verdict per criterion, plus the specific edits needed
before this goes to human review and publication.
```

---

## 22. Testing & QA Prompt
*(Master Spec Section 8.1, 11, 13, 20.)*

```
Write a QA test plan for: {{tool/feature name}}

Cover:
1. Functional: every input/output path, including edge cases (empty input, max-length
   input, invalid/malformed input, special characters, extremely large files if
   applicable).
2. Tool Quality Standards (Section 8.1): input validation, copy button, reset button,
   example input/output all present and working.
3. Error handling (Section 20): every failure mode shows a clear, specific message —
   list each one and its expected message.
4. Cross-browser (Section 11): Chrome, Edge, Firefox, Safari — latest versions; note any
   graceful-degradation behavior to verify.
5. Responsive/mobile (Section 3): test at common breakpoints, verify touch targets and
   layout.
6. Performance (Section 13): rough LCP/CLS/INP check, confirm no library loads until the
   user actually interacts with the tool.
7. Accessibility (Section 12): keyboard-only pass, screen reader spot-check.
8. Privacy (Section 19): confirm via network tab that no request is made with user data
   during tool use.

Output as a checklist I can run through manually before publishing.
```

---

## 23. Performance Optimization Prompt
*(Master Spec Section 13.)*

```
Optimize this page/tool for Core Web Vitals: {{paste code or describe page}}

Targets: LCP < 2s, CLS ~ 0, INP < 200ms (Section 13).

Check and fix:
1. Any third-party library loaded on page load instead of on first interaction
   (Section 9's lazy-loading requirement) — convert to lazy load.
2. Unoptimized images — recommend WebP, correct sizing, and explicit width/height to
   prevent layout shift.
3. Render-blocking resources in <head>.
4. Unnecessary/duplicate JavaScript — confirm this page only loads its own tool module
   plus the global modules it actually needs (Section 10), not everything.
5. Layout shift sources — ads, late-loading fonts/images, dynamically injected content
   without reserved space.
6. Any expensive synchronous computation that should be deferred, debounced, or chunked.

Output: specific before/after code changes, plus the expected impact on each metric.
```

---

## 24. Browser Compatibility Prompt
*(Master Spec Section 11.)*

```
Check browser compatibility for: {{paste code or name the API/feature used}}

Confirm support across Chrome, Edge, Firefox, and Safari (latest versions, per
Section 11). For any API without full support:
- Propose a graceful degradation path (feature detection + fallback UI/message), not a
  silent failure.
- Flag if this is an "experimental" API that Section 11 says to avoid unless absolutely
  necessary — justify if it's truly required.

Output: a compatibility table (API/feature × browser) and the specific fallback code
where needed.
```

---

## 25. Release Checklist Prompt
*(Master Spec Section 8, 12, 13, 18, 19, 22, 26.)*

```
Generate a pre-publish release checklist for: {{tool/page name}}

Must verify, per Master Spec:
- [ ] Standard Tool Page Structure complete, all 16 elements present (Section 8)
- [ ] 500–800 words of unique content (Section 8)
- [ ] Tool Quality Standards met: validation, copy, reset, example in/out (Section 8.1)
- [ ] Tool card matches standard format (Section 8.2)
- [ ] SEO title, meta description, custom slug set (Section 17)
- [ ] Internal links to category hub + 2–4 related tools + related tutorials (Section 17)
- [ ] JSON-LD structured data present and validated (Section 18)
- [ ] Accessibility pass: keyboard nav, contrast, alt text, headings (Section 12)
- [ ] Core Web Vitals check done, no page-load-time third-party libraries (Section 13)
- [ ] Security review done: crypto.getRandomValues where relevant, no network calls with
      user data (Section 4, 19)
- [ ] Privacy notice shown if the tool touches files/sensitive input (Section 19)
- [ ] Cross-browser check: Chrome/Edge/Firefox/Safari (Section 11)
- [ ] Light/Dark/System theme all verified (Section 21)
- [ ] Affiliate placement (if any) is contextual, disclosed, non-obstructive (Section 22/23)
- [ ] Redirect-map spreadsheet row added (Section 14)
- [ ] tools-index.json updated with this tool's entry (Section 15)
- [ ] "Last updated" date and version number set (Section 8)

Fill in the checklist with pass/fail and notes for each line before this goes live.
```

---

## 26. Changelog

| Version | Date | Change |
|---|---|---|
| 1.0 | {{fill in date}} | Initial library created from Master Project Specification v1.0 |
