# Banynova — Tool Registry

**Governed by:** `Documentation_Governance_v1.0.md`
**Purpose:** The single tracking table for every tool's lifecycle — from idea to published to (eventually) deprecated. As the platform scales toward 200+ tools, this is what prevents losing track of what state any given tool is actually in.

---

## 1. Status Definitions

Every tool has **exactly one** status at any time:

| Status | Meaning |
|---|---|
| **Planning** | Tool is scoped (name, category, target keywords identified) but no implementation has started. |
| **In Development** | HTML/CSS/JS is being built, following the Universal Tool Template and Design System. |
| **Testing** | Implementation complete; running through `Testing_Checklist.md` in full. |
| **Published** | Live on the site, passed all testing, added to `tools-index.json` (Master Spec Section 15) and the internal linking plan (Master Spec Section 17). |
| **Deprecated** | No longer maintained/available — replaced by another tool, or removed. Kept in this table (not deleted) with a note on why and what replaced it, per redirect-map practice (Master Spec Section 14). |

**Rule:** a tool only moves to **Published** after passing every item in `Testing_Checklist.md` — no exceptions, regardless of deadline pressure.

---

## 2. Registry

| Tool Name | Slug | Category | Status | Blogger URL | Last Updated | Notes |
|---|---|---|---|---|---|---|
| JSON Formatter | `json-formatter` | Developer Tools | Planning | — | {{date}} | |
| Regex Tester | `regex-tester` | Developer Tools | Planning | — | {{date}} | |
| Base64 Encoder/Decoder | `base64-encoder-decoder` | Developer Tools | Planning | — | {{date}} | |
| UUID Generator | `uuid-generator` | Developer Tools | Planning | — | {{date}} | |
| Meta Tag Generator | `meta-tag-generator` | SEO Tools | Planning | — | {{date}} | |
| Robots.txt Generator | `robots-txt-generator` | SEO Tools | Planning | — | {{date}} | |
| Percentage Calculator | `percentage-calculator` | Calculators | Planning | — | {{date}} | |
| Password Generator | `password-generator` | Security Tools | Planning | — | {{date}} | Must use Web Crypto API per Master Spec Section 4 — never `Math.random()` |
| QR Code Generator | `qr-code-generator` | Security Tools | Planning | — | {{date}} | |
| Image Compressor | `image-compressor` | Image Tools | Planning | — | {{date}} | |
| Word Counter | `word-counter` | Text Tools | Planning | — | {{date}} | Reference tool for Roadmap Step 5 (changed from JSON Formatter) — validates the Universal Tool Template before other tools are built. See `Tool_Category_Architecture_Master_Plan.md`. |

*(This starter list mirrors the homepage's mock data — update statuses as real work begins, and add every additional tool from Master Spec Section 5 as it's scoped, even before development starts, so Planning-stage tools are visible too.)*

---

## 3. How to Use This Registry

- **Adding a tool:** add a row at **Planning** as soon as it's scoped — don't wait until development starts. This gives visibility into the full pipeline, not just what's live.
- **Updating status:** update the row the moment status changes, and update "Last Updated." This table should always reflect reality, not last month's snapshot.
- **Before marking Published:** confirm the Testing Checklist (`Testing_Checklist.md`) was run in full for this tool — link or note the completed checklist if kept separately.
- **Deprecating:** never delete a row. Change status to Deprecated and add a note (what replaced it, and the redirect destination per Master Spec Section 14's redirect-map practice).
- **Cross-reference:** this table's Category column must match a category defined in Master Spec Section 5 exactly — don't introduce ad hoc category names here.

---

## 4. Changelog

| Version | Date | Change |
|---|---|---|
| 1.0 | {{fill in date}} | Initial registry created with status lifecycle (Planning → In Development → Testing → Published → Deprecated) and starter tool list |
