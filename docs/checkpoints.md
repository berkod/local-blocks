# Checkpoints

Three checkpoints across the 18-session arc. Don't advance past one until its criteria pass.

---

## Checkpoint 1 — End of S6 (FSE foundation)

**State to verify:**
- ddev site running, fresh latest WP
- Block theme installed and **active** (scaffolded via `@wordpress/create-block-theme` or Twenty Twenty-Five child)
- `theme.json` customized: brand palette, typography, spacing scale all driving the editor + front-end
- Site Editor used to customize: home template, single template, archive template
- Header + footer template parts exist
- Query Loop block in use somewhere

**Pass criteria:**
- Front-end loads with no console errors
- Editor color/font controls reflect `theme.json` settings (not browser defaults)
- Learner can articulate, unprompted: difference between `settings` and `styles` in `theme.json`; difference between a template and a template part; what Query Loop replaces from classic themes
- Six git commits exist (`s1:` … `s6:`) with matching journal entries

**If failing:** re-do S5 + S6 before advancing. theme.json understanding is load-bearing for everything that follows.

---

## Checkpoint 2 — End of S12 (JS + tooling foundation)

**State to verify:**
- `recipe` CPT registered, `'show_in_rest' => true`, archive working
- `cuisine` and `diet` taxonomies registered
- Block patterns registered (hero, recipe-card-grid, CTA)
- One block variation registered + one template-locked block confirmed
- `recipe-blocks` plugin scaffolded via `@wordpress/create-block`
- `wp-scripts start` runs cleanly with HMR
- Learner has run `fetch` + `wp.data.select(...)` from console and got real data back

**Pass criteria:**
- `wp-scripts build` exits 0; build artifacts in `build/`
- Learner can articulate, unprompted: what a Promise is and why every `@wordpress/data` and REST call returns one; what `wp-scripts` does under the hood (webpack + Babel preset for JSX); `useSelect` vs `select`
- Twelve git commits + matching journal entries

**If failing on JS:** add an extra session. Don't try to learn `block.json` (S13) if promises still feel opaque — they'll drown the next phase.

---

## Checkpoint 3 — End of S18 (full arc retrospective)

**State to verify:**
- Recipe site demo'd end-to-end: home → recipe archive → single recipe → all built with knowledge from S1–S17
- Custom blocks all functional in editor + front-end:
  - Cook Time (S14) — static block, two number controls
  - Ingredient List (S15) — InnerBlocks parent + Ingredient child
  - Latest Recipes (S16) — dynamic block w/ PHP `render_callback`
  - Recipe Card (S17) — composite, ties prior three blocks together
- Eighteen git commits + matching journal entries

**Pass criteria — the real test:**
- Learner pulls up an AI-generated block from a past client project, opens it cold, and **narrates what each line does without referring to docs.**
- If they get stuck on a line, they can name the package the symbol comes from (`@wordpress/components`, `@wordpress/block-editor`, `@wordpress/data`, etc.) and what that package's role is.
- If they don't pass this test, do not advance to the classic-theme module — repeat weakest week.

**Decision point (only after passing):**
Choose next module:

1. **Classic theme + blocks bridge** (originally planned next) — PHP enqueue, classic editor compat, hybrid themes, how blocks slot into PHP templates
2. **Deeper custom block topics** — block filters, slot/fill, Block Bindings API (WP 6.5+), Interactivity API (WP 6.5+)

Default: option 1, since it matches client-site reality. But if learner finds custom block work more energizing, option 2 is valid.

**Deliverable:** written self-assessment in `journal/s18-retrospective.md` + chosen next module.
