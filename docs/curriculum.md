# Curriculum — 18 Sessions, 6 Weeks

Format: 30–45 min × 3 per week. Hands-on every session.

Each session: 5 min recap → 20–30 min hands-on → 5 min commit + journal note.

---

## Setup (Session 0 — pre-work)

- ddev project: `ddev config --project-type=wordpress`, spin up fresh latest WP
- Init git in repo root, commit each session
- VS Code extensions: **WordPress Hooks IntelliSense**, **PHP Intelephense**
- Browser: **React Developer Tools** + **Redux DevTools** (inspect `@wordpress/data` stores)

Theme decision deferred to S4: scaffold via `npx @wordpress/create-block-theme` OR start from Twenty Twenty-Five child.

---

## Week 1 — Foundations + Core Blocks

### S1. What is Gutenberg, really.
- Block = JS object: `name`, `attributes`, `edit`, `save`. Not a shortcode.
- `post_content` stores HTML + HTML-comment delimiters (`<!-- wp:paragraph -->`)
- Open DB, view raw `post_content`. See serialized block markup
- Browser DevTools: inspect editor iframe, run `wp.blocks.getBlockTypes()` in console
- **Deliverable:** `journal/s1-block-anatomy.md`

### S2. Core blocks tour — text + media.
- Paragraph, Heading, List, Image, Gallery, Cover, Media&Text, Quote
- Each: insert, inspect attributes panel, toggle block-style variations, view block markup (`Ctrl+Shift+Alt+M`)
- **Deliverable:** demo post using all 8. Save and inspect serialized output.

### S3. Core blocks tour — layout + design.
- Group, Row, Stack, Columns, Spacer, Separator, Buttons, Cover
- Layout types: flow / flex / constrained. Where width/alignment lives.
- **Deliverable:** rebuild simple 3-column "featured recipes" layout. Note hierarchy in journal.

---

## Week 2 — FSE + theme.json

### S4. Block theme anatomy.
- Scaffold theme: `npx @wordpress/create-block-theme`. Walk file tree.
- `templates/`, `parts/`, `patterns/`, `theme.json`, `style.css`, `functions.php` (slim)
- Compare: classic theme tree vs block theme tree
- **Deliverable:** theme installed, activated on ddev site.

### S5. theme.json deep dive.
- `settings` (what editors *can* do) vs `styles` (what theme *does* by default)
- Color palette, font families, spacing scale, block-level overrides
- Live edit: change palette, see in editor immediately
- Reference: https://developer.wordpress.org/themes/global-settings-and-styles/
- **Deliverable:** customize palette, typography, spacing for recipe brand.

### S6. Site Editor + templates.
- Site Editor (`/wp-admin/site-editor.php`). Templates vs template parts.
- Edit `single.php` equivalent → `templates/single.html`. Header/footer parts.
- Query Loop block: how it replaces `WP_Query` in template land.
- **Deliverable:** customize home, single, archive templates for recipes.

---

## Week 3 — Patterns, CPTs, Block Variations

### S7. Block patterns.
- Pattern = pre-composed block markup. Register via `patterns/*.php` w/ header comment.
- Build 3 patterns: hero, recipe card grid, CTA
- Pattern categories. Synced vs unsynced (formerly "reusable blocks")
- **Deliverable:** 3 patterns in theme, inserted into pages.

### S8. Custom Post Type for Recipes.
- Register `recipe` CPT in PHP (`functions.php`). Must have `'show_in_rest' => true` (required for editor)
- Custom taxonomies: `cuisine`, `diet`
- Block templates per CPT: lock down what blocks editors can use
- **Deliverable:** Recipe CPT live, archive working, test post created.

### S9. Block variations + locking.
- Variation: same block, different default attributes (e.g. Group → "Recipe Section")
- `register_block_variation` (JS) vs `block.json` variation
- Block locking: `lock: { move: true, remove: true }`. Template lock at template level.
- **Deliverable:** register one variation. Lock recipe template structure.

---

## Week 4 — JS Ramp + Block Tooling

### S10. JS ramp 1: promises + async/await.
- Promise = "value later." `.then`/`.catch` vs `await`/`try/catch`
- Why: every WP REST + `@wordpress/data` call returns one
- Hands-on: `fetch('/wp-json/wp/v2/posts').then(r => r.json()).then(console.log)`. Rewrite with async/await.
- **Deliverable:** `journal/s10-promises.md` with 3 working examples.

### S11. JS ramp 2: modules, npm, build tools.
- ES modules (`import`/`export`). Why bundlers exist (browsers + JSX)
- `@wordpress/scripts`: `wp-scripts start` / `build`. What it does (webpack + Babel preset)
- `package.json` walkthrough
- **Deliverable:** scaffold blank plugin via `npx @wordpress/create-block`, run dev server, see HMR.

### S12. WP data layer — `@wordpress/data`.
- Redux-style stores. `select` (read), `dispatch` (write), `useSelect` / `useDispatch` hooks
- Core stores: `core`, `core/editor`, `core/block-editor`
- Console exercise: `wp.data.select('core').getEntityRecords('postType', 'recipe')`
- **Deliverable:** console-fetch all recipes, log titles.

---

## Week 5 — Custom Blocks: Static

### S13. block.json anatomy.
- Modern way: `block.json` is source of truth. Replaces most `register_block_type` args.
- Fields: `name`, `title`, `category`, `attributes`, `supports`, `editorScript`, `style`
- `attributes` types + `source` (where attribute reads from on re-load: `attribute`, `text`, `html`, `meta`)
- **Deliverable:** read block.json reference top-to-bottom, annotate in journal.

### S14. Build "Cook Time" static block.
- Attributes: `hours` (number), `minutes` (number)
- `edit`: two NumberControls + `useBlockProps`
- `save`: serialized HTML output
- Why static: simple, fast, no PHP render needed
- **Deliverable:** working Cook Time block in recipe plugin.

### S15. InnerBlocks + "Ingredient List" block.
- `InnerBlocks` lets a block contain other blocks
- Build Ingredient List: parent block, child Ingredient block w/ qty + unit + name
- `allowedBlocks`, `template`, `templateLock`
- **Deliverable:** working Ingredient List w/ Ingredient children.

---

## Week 6 — Custom Blocks: Dynamic + Polish

### S16. Dynamic blocks ("Latest Recipes").
- `save: () => null` + PHP `render_callback`
- When to use: data changes after publish (queries, current-user-aware)
- ServerSideRender component for editor preview
- **Deliverable:** Latest Recipes block, query-loop-style, configurable count.

### S17. "Recipe Card" composite block.
- Pull together: Image, Heading, Cook Time (custom), Ingredient List (custom)
- Use as block-pattern OR as parent block w/ locked InnerBlocks template
- Discuss: when is it a pattern vs a custom parent block?
- **Deliverable:** Recipe Card usable on Recipe CPT.

### S18. Checkpoint + retrospective.
- Audit recipe site: every page built with knowledge from S1–S17
- Read AI-generated block code from past projects — narrate what each line does
- Decide next module: classic-theme + blocks deep dive, OR deeper custom block topics (filters, slot/fill, block bindings, interactivity API)
- **Deliverable:** written self-assessment + chosen next module.

---

## External References

- Block Editor Handbook: https://developer.wordpress.org/block-editor/
- Theme Handbook (block themes): https://developer.wordpress.org/themes/
- `@wordpress/scripts` docs: https://developer.wordpress.org/block-editor/reference-guides/packages/packages-scripts/
- Learn WordPress: https://learn.wordpress.org/
