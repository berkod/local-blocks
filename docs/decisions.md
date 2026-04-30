# Decisions & Scope

## Sequencing: block theme (FSE) first, classic-theme + blocks second

**Decision:** start with FSE block theme, pivot to classic-theme + blocks module after S18 checkpoint.

**Why:**
- Pure block mental model — FSE makes everything blocks (templates, parts, patterns, global styles). Classic+blocks mixes paradigms (PHP template hierarchy + block content), confusing while learning.
- Forward investment — new WP installs since 6.0 default block themes (Twenty Twenty-Two onward). Core dev energy goes here. Classic theme work is increasingly maintenance.
- theme.json centralizes design — one file for colors, typography, spacing, layout. Classic themes scatter across `functions.php` enqueues, `add_theme_support`, CSS files, separately registered patterns.
- Custom block dev is identical in both — that skill transfers cleanly.

**Counter considered (and noted):** classic+blocks matches current client-site reality. Addressed by making classic-theme module the *next* phase — not skipped, just sequenced.

## Project: Recipe / learning library

**Decision:** recipe site over portfolio / agency / pick-for-me options.

**Why:** strongest custom-block territory (Cook Time, Ingredient List, Step block, Recipe Card, taxonomies for cuisine/diet). Maximizes coverage of curriculum topics — InnerBlocks, dynamic blocks, REST integration, CPT registration.

## Local dev: ddev

**Decision:** ddev. User self-managing.

**Why:** user explicit preference. Do not suggest wp-env / Local / Studio.

## JS ramp: included, scheduled S10–S12

**Decision:** brief explicit JS ramp before custom block dev.

**Why:** learner is mid-level vanilla JS, called out **promises / async-await as confusing**. Every `@wordpress/data` and REST call returns a promise — fixing this confusion early prevents compounding misunderstanding when custom blocks start.

## Cadence: 18 sessions / 6 weeks before first major checkpoint

**Decision:** 18 sessions over 6 weeks (vs 12 / 30).

**Why:** 12 too tight for a full FSE + custom block arc. 30 over-plans before testing the cadence. 18 covers core blocks → FSE → JS ramp → static + dynamic custom blocks with room for the recipe project. Re-plan after S18 with real data on what stuck.

---

## Out of Scope (explicit non-goals for sessions S1–S18)

These are deliberately deferred. Do **not** introduce them mid-curriculum unless the user explicitly asks.

- **Classic theme + blocks bridge** — deferred to post-S18 module (sequencing decision above)
- **Block Bindings API (WP 6.5+)** — powerful, but adds surface area. Revisit after fundamentals.
- **Interactivity API (WP 6.5+)** — newer; introduces directives + alpinejs-like patterns. Out of scope for fundamentals pass.
- **Block filters** — `blocks.registerBlockType` JS filter, `render_block` PHP filter. Advanced; post-S18.
- **Multi-block plugins, Slot/Fill** — internal extensibility patterns. Post-S18.
- **Headless WP w/ blocks** — separate concern; not in this curriculum.
- **TypeScript** — keep block dev in plain JS for now to match learner's JS comfort level.
- **Custom webpack config** — `@wordpress/scripts` only. No ejecting.
- **Gutenberg plugin (vs core blocks)** — stick with what's bundled in WP core for predictability.

## Per-session protocol (binding)

- 30–45 min total
- Structure: 5 min recap → 20–30 min hands-on → 5 min commit + journal
- Every session ends with a git commit, subject `sNN: <topic>`
- Every session ends with `journal/sNN-<slug>.md` explaining *why*, not *what*
- Skipping the journal breaks the retention mechanism — do not skip it

## What to reuse, not reinvent

- `@wordpress/create-block` — scaffold custom blocks (do not hand-write boilerplate)
- `@wordpress/create-block-theme` — scaffold the block theme
- `@wordpress/scripts` — build (`wp-scripts start` / `build`)
- `@wordpress/components` — UI primitives (`TextControl`, `NumberControl`, `PanelBody`, `InspectorControls`)
- `@wordpress/block-editor` — `useBlockProps`, `InnerBlocks`, `RichText`, `MediaUpload`
- `@wordpress/data` — `useSelect`, `useDispatch`
