# learning-blocks

Self-study repo for mastering Gutenberg / WordPress block editor.

## Learner profile (read first)

- 10+ years WordPress, strong PHP/WP backend
- Mid-level vanilla JS — comfortable but not strong; prefers vanilla over jQuery
- **Promises / async-await are a known weak spot** — explain carefully when they come up
- Light React exposure
- Goal: understand AI-generated block code on client work, not keep shipping blind

## Local environment

- **ddev** — user manages this themselves; do not suggest wp-env / Local / Studio
- Project root: `/Users/berkod/projects/github/learning-blocks`

## How to use this repo across sessions

1. Read `docs/curriculum.md` — full 18-session plan, deliverables, and structure
2. Read `docs/decisions.md` — sequencing choices, out-of-scope items, and the *why*
3. Read `docs/checkpoints.md` — verification criteria at S6 / S12 / S18
4. Read `journal/sNN-*.md` (if present) — learner's notes from completed sessions; resume from highest N

When asked to "start session N," recap prior session's deliverable from the journal first, then proceed.

## Per-session protocol

- 30–45 min total: 5 min recap → 20–30 min hands-on → 5 min commit + journal note
- Each session ends with a git commit (subject: `sNN: <topic>`) and a `journal/sNN-<slug>.md` note explaining *why*, not just *what*
- Don't skip the journal — articulation is the retention mechanism

## Project site

Recipe / learning library:
- CPT: `recipe`
- Taxonomies: `cuisine`, `diet`
- Custom blocks (built progressively): Cook Time → Ingredient List (InnerBlocks) → Latest Recipes (dynamic) → Recipe Card (composite)

## File layout (built up over sessions)

```
themes/recipe-block-theme/    # block theme (S4+)
  theme.json                  # design tokens (S5)
  templates/                  # front, single-recipe, archive-recipe (S6)
  parts/                      # header, footer (S6)
  patterns/                   # hero, recipe-card-grid, cta (S7)
plugins/recipe-blocks/        # custom blocks plugin (S11+)
  recipe-blocks.php           # bootstrap + CPT registration (S8)
  src/cook-time/              # static block (S14)
  src/ingredient-list/        # InnerBlocks parent (S15)
  src/latest-recipes/         # dynamic block (S16)
  src/recipe-card/            # composite block (S17)
journal/                      # per-session notes
docs/                         # this plan + decisions + checkpoints
```

## Tooling to reuse (do NOT reinvent)

- `@wordpress/create-block` — scaffold custom blocks
- `@wordpress/create-block-theme` — scaffold the block theme
- `@wordpress/scripts` — build (`wp-scripts start` / `build`)
- `@wordpress/components` — `TextControl`, `NumberControl`, `PanelBody`, `InspectorControls`, etc.
- `@wordpress/block-editor` — `useBlockProps`, `InnerBlocks`, `RichText`, `MediaUpload`
- `@wordpress/data` — `useSelect`, `useDispatch`
