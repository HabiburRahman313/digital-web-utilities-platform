# Banynova — Documentation Governance v1.0

**Project Philosophy:** Build the foundation once. Reuse it everywhere. Never redesign.

---

## 1. Single Source of Truth

Together these documents define the official architecture, design, development workflow, and governance of the Banynova platform.

**Every decision, implementation, and future enhancement must align with this documentation.**

No page, tool, prompt, or process may deviate from what is written here without first updating the relevant document. If reality and documentation ever disagree, that is treated as a bug in the documentation to be fixed immediately — not a discrepancy to quietly work around.

---

## 2. Documentation Hierarchy

```
Master Project Specification
│
├── Design System
│     └── Component Library
│
├── Brand Voice Guide
│
├── AI Prompt Library
│
├── Tool Registry
│
├── SEO Content Map
│
├── Roadmap
│
├── Testing Checklist
│
├── Static Page Creation Standard
│
└── Changelog
```

| Document | File | Status |
|---|---|---|
| Master Project Specification | `Master_Project_Specification_v1_0.md` | ✅ Exists |
| Design System | `Design_System_v1.0.md` | ✅ Exists |
| Component Library | `Component_Library.md` | ⬜ To be created at Roadmap Step 3 |
| Brand Voice Guide | `brand-voice.md` | ✅ Exists |
| AI Prompt Library | `AI_Prompts.md` | ✅ Exists |
| Tool Registry | `Tool_Registry.md` | ✅ Exists (created alongside this document) |
| SEO Content Map | `SEO_Content_Map.md` | ⬜ To be created once tools begin publishing (Roadmap Step 6–7) |
| Roadmap | tracked inside `Design_System_v1.0.md` Section 20 today; may be split into its own file once Step 4+ begins | ⬜ Consider splitting out |
| Testing Checklist | `Testing_Checklist.md` | ✅ Exists (created alongside this document) |
| Static Page Creation Standard | `Static_Page_Creation_Standard.md` | ✅ Exists — created after the Terms of Service blank-page incident, includes the Page Registry |
| Changelog | one Changelog section per document today; a consolidated top-level `CHANGELOG.md` can be added if per-document logs become hard to track | ⬜ Consider consolidating later |

**Reading the hierarchy:** Master Project Specification is the root authority — architecture, platform constraints, categories, and principles all originate there. Everything below it must be consistent with it. Design System governs all visual/structural decisions and itself governs the Component Library beneath it (no component may contradict a Design System token or rule). Brand Voice Guide, AI Prompt Library, Tool Registry, SEO Content Map, Roadmap, Testing Checklist, and Changelog are siblings — each owns one concern and defers to Master Spec + Design System wherever they overlap.

---

## 3. Documentation Rules — Development Order

Every new piece of work — a tool, a feature, a page — follows this fixed order. **Skipping a step, or doing them out of order, is what produces enterprise-grade documentation vs. ad hoc documentation.**

```
1. Master Project Specification
        ↓
2. Design System
        ↓
3. Component Library
        ↓
4. Brand Voice Guide
        ↓
5. AI Prompt Library
        ↓
6. Implementation
        ↓
7. Testing
        ↓
8. Release
```

**What this means in practice:**
1. **Master Project Specification** — confirm the work fits the platform's architecture and constraints (Page/Post budget, stack, categories).
2. **Design System** — confirm every token needed already exists; add it here first if not.
3. **Component Library** — confirm every component needed already exists; enhance it here first if not (per Design System Section 19, Rule 0).
4. **Brand Voice Guide** — confirm any copy needed matches established voice/tone; add new copy patterns here if none fit.
5. **AI Prompt Library** — use (or add) the relevant prompt so the work is produced consistently, whether done by a human or an AI session.
6. **Implementation** — only now is code actually written, using what Steps 1–5 confirmed.
7. **Testing** — run the Testing Checklist in full (`Testing_Checklist.md`) — no exceptions.
8. **Release** — publish, update the Tool Registry's status (see Section on Tool Registry below), update the relevant Changelog.

---

## 4. Governance Rules Summary

*(Consolidated from across the documentation set, so the core non-negotiables are visible in one place.)*

- **No page may redefine an existing component.** Enhancements go into the Component Library first (Design System Section 19).
- **Every design token must be defined only once.** Hard-coded colors, spacing, font sizes, and shadows are prohibited anywhere in component or page CSS (Design System Section 0/1).
- **No tool may be published without passing the complete Testing Checklist** (`Testing_Checklist.md`) — this is a hard gate, not a recommendation.
- **Every tool has exactly one status at a time** in the Tool Registry: Planning → In Development → Testing → Published → Deprecated (`Tool_Registry.md`).
- **Documentation is updated before or immediately after implementation — never left to "later."** A change that only exists in code and not in documentation is considered incomplete.

---

## 5. Changelog

| Version | Date | Change |
|---|---|---|
| 1.0 | {{fill in date}} | Initial governance structure established: Single Source of Truth statement, Documentation Hierarchy, and 8-step Development Order formalized. `Tool_Registry.md` and `Testing_Checklist.md` created as new companion documents. |
