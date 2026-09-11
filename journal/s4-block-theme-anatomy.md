# S4 — Block theme anatomy

1. What single thing makes WordPress treat a directory as a block theme rather than a classic theme? What did I get wrong the first time, and why was that a natural mistake coming from classic themes?

I created an index.php in the templates directory, which is the standard PHP main template. For block themes, the template name should be index.html. This difference is what tells WordPress to treat this is a block theme.


2. `style.css` in a block theme contains no CSS. So where does the theme's CSS actually come from, and who generates it?

Block theme css mostly comes from the blocks themselves and are produced on the page based on the blocks that are needed. Theme.json generally contains design tokens and some style rules. WP Core generates the CSS from the block styles and the theme.json rules.


3. The theme only has `templates/index.html`, yet every page on the site renders. Explain why, in terms of the template hierarchy I already know from classic themes.

templates/index.* is the default template that is used to render pages for both block and classic thems, index.html for block and index.php for classic. If there aren't any more specific templates, WP will default to the index.html one. If we were rendering a category archive, WP would look first for category.html first and then fallback to index.html if it doesn't exist.


4. One thing that surprised me about the block theme file tree.

That the template hierarchy is the same as classic, just looking for html templates instead of php templates. Also, that the CSS is produced by WP Core using the styles from the blocks used on the page and additional information from theme.json.


│                Classic theme                │                 Block theme                  │            What changed            │
├─────────────────────────────────────────────┼──────────────────────────────────────────────┼────────────────────────────────────┤
│ index.php, single.php, archive.php          │ templates/index.html, single.html,           │ PHP → serialized block markup. No  │
│                                             │ archive.html                                 │ PHP executes.                      │
├─────────────────────────────────────────────┼──────────────────────────────────────────────┼────────────────────────────────────┤
│ header.php / footer.php + get_header()      │ parts/header.html + <!-- wp:template-part    │ Include → a block that resolves a  │
│                                             │ {"slug":"header"} /-->                       │ part                               │
├─────────────────────────────────────────────┼──────────────────────────────────────────────┼────────────────────────────────────┤
│ functions.php — enqueue, add_theme_support, │ theme.json                                   │ Config moved from imperative PHP    │
│  nav menus, sidebars                        │                                              │ to declarative JSON                │
├─────────────────────────────────────────────┼──────────────────────────────────────────────┼────────────────────────────────────┤
│ The Loop: while (have_posts())              │ <!-- wp:query --> + <!-- wp:post-template    │ Loop is a block with a query       │
│                                             │ -->                                          │ attribute                          │
├─────────────────────────────────────────────┼──────────────────────────────────────────────┼────────────────────────────────────┤
│ style.css — the actual stylesheet           │ style.css — header comment only              │ Styles come from theme.json; core  │
│                                             │                                              │ generates the CSS                  │
├─────────────────────────────────────────────┼──────────────────────────────────────────────┼────────────────────────────────────┤
│ Template hierarchy in template-loader.php   │ Same hierarchy, resolved against             │ Hierarchy logic is unchanged —     │
│                                             │ templates/*.html                             │ only the file extension             │
└─────────────────────────────────────────────┴──────────────────────────────────────────────┴────────────────────────────────────┘
---

## Reference — classic tree vs block tree

| Classic theme | Block theme | What changed |
|---|---|---|
| `index.php`, `single.php`, `archive.php` | `templates/index.html`, `single.html`, `archive.html` | PHP → serialized block markup. **No PHP executes.** |
| `header.php` / `footer.php` + `get_header()` | `parts/header.html` + `<!-- wp:template-part {"slug":"header"} /-->` | Include → a block that resolves a part |
| `functions.php` — enqueue, `add_theme_support`, nav menus, sidebars | `theme.json` | Config moved from imperative PHP to declarative JSON |
| The Loop: `while (have_posts())` | `<!-- wp:query -->` + `<!-- wp:post-template -->` | Loop is a block with a `query` attribute |
| `style.css` — the actual stylesheet | `style.css` — **header comment only** | Styles come from `theme.json`; core generates the CSS |
| Template hierarchy in `template-loader.php` | Same hierarchy, resolved against `templates/*.html` | Hierarchy logic is unchanged — only the file extension |

The template hierarchy did not change. `single-recipe` still beats `single` still beats
`index` — core just looks for `.html` in `templates/` first, and falls back to the classic
PHP lookup if it finds nothing. That is why a theme with only `index.html` renders every
page type on the site.
