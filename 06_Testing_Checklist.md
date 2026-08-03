# Banynova — Testing Checklist

**Governed by:** `Documentation_Governance_v1.0.md`

> **No tool may be published without passing the complete testing checklist below.**
> This is a hard release gate, not a recommendation — a tool stays at **Testing** status in `Tool_Registry.md` until every item here passes.

---

## 1. Functional Testing

- [ ] Every input/output path works as intended
- [ ] Edge cases handled: empty input, maximum-length input, invalid/malformed input, special characters
- [ ] Large file/input handling verified (if applicable to the tool)
- [ ] Input validation present and correct (Master Spec Section 8.1)
- [ ] Copy-to-clipboard button present and working
- [ ] Reset button present and working
- [ ] Example input and example output present (Master Spec Section 8.1)

## 2. Error Handling (Master Spec Section 20)

- [ ] Every failure mode shows a clear, specific, actionable message
- [ ] No generic "Something went wrong" messages anywhere
- [ ] Empty-state guidance present where relevant

## 3. Accessibility (Master Spec Section 12 / Design System Section 15)

- [ ] Full keyboard-only pass completed — every control reachable and operable
- [ ] Visible focus indicator on every interactive element (`--bn-focus-ring`)
- [ ] Heading hierarchy correct (one H1, no skipped levels)
- [ ] Color contrast verified in both light and dark mode
- [ ] All images/icons have correct alt text or `aria-hidden`
- [ ] Dynamic content (tool output, errors) announced via `aria-live` where appropriate
- [ ] Screen reader spot-check completed

## 4. Cross-Browser & Responsive (Master Spec Section 11 / Design System Section 8)

- [ ] Chrome (latest) verified
- [ ] Edge (latest) verified
- [ ] Firefox (latest) verified
- [ ] Safari (latest) verified
- [ ] Responsive at mobile, tablet, and desktop breakpoints
- [ ] Touch targets appropriately sized on mobile
- [ ] Graceful degradation confirmed for any unsupported browser API

## 5. Performance (Master Spec Section 13)

- [ ] LCP < 2s
- [ ] CLS ~ 0
- [ ] INP < 200ms
- [ ] No third-party library loads on page load — confirmed lazy-loaded on first interaction only (if the tool uses one)
- [ ] Images optimized (WebP where applicable, explicit width/height set)

## 6. Security & Privacy (Master Spec Section 4, 19)

- [ ] `crypto.getRandomValues()`/`crypto.subtle` used for any security-adjacent randomness — never `Math.random()`
- [ ] Network tab confirms zero requests are made with user data/files during tool use
- [ ] No unnecessary `localStorage`/cookie usage; anything used is disclosed to the user
- [ ] Privacy notice shown if the tool touches files or sensitive input

## 7. Design System & Component Compliance (Design System Sections 2–13, 19)

- [ ] Only existing design tokens used — no hard-coded colors, spacing, font sizes, or shadows
- [ ] Only existing components used (Tool Card, Buttons, Forms) — no page-level component redefinition
- [ ] Verified correct in both Light and Dark mode

## 8. SEO & Structured Data (Master Spec Section 8, 17, 18)

- [ ] SEO title and meta description set
- [ ] Custom permalink slug set
- [ ] 500–800 words of unique supporting content present
- [ ] Internal links present: category hub + 2–4 related tools + related tutorials
- [ ] JSON-LD structured data present and validates (SoftwareApplication/FAQPage/BreadcrumbList as applicable)

## 9. Content Quality (Master Spec Section 25)

- [ ] Content is original, not a reworded rewrite of existing top-ranking pages
- [ ] All technical/factual claims verified accurate
- [ ] No fabricated statistics, user counts, or reviews
- [ ] If AI-drafted, has received human review before publish

## 10. Registry & Housekeeping

- [ ] `Tool_Registry.md` row updated with correct status and Last Updated date
- [ ] `tools-index.json` updated with this tool's entry (Master Spec Section 15)
- [ ] Redirect-map spreadsheet row added (Master Spec Section 14)
- [ ] "Last updated" date and version number set on the page itself

---

## Sign-off

| Field | Value |
|---|---|
| Tool name | |
| Tested by | |
| Date | |
| Result | ☐ Pass — ready for Published status  ☐ Fail — return to In Development |

---

## Changelog

| Version | Date | Change |
|---|---|---|
| 1.0 | {{fill in date}} | Initial checklist created, consolidating testing/release criteria from AI_Prompts.md into a standalone enforced gate document |
