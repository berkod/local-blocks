# S6 — Site Editor + templates

1. A template and a template part are both just `.html` files full of block markup.
   In WP's eyes, what is the actual difference between them?


2. `resolve_block_template()` showed a category archive landing on `archive.html`
   and a 404 landing on `index.html`. In your own words: what does it mean to say
   "`index.html` is the fallback"? Where does the list of filenames WP tries come from?


3. `single-recipe.html` does not exist yet, so a recipe would render `single.html`.
   At S8 you'll register the `recipe` CPT. What file would you add to take over, and
   *why* would it beat `single.html`?


4. The Query Loop markup in `index.html` and in `archive.html` is nearly identical, and both
   say `"inherit": true` — yet the home page and a category archive list different posts.
   What is being inherited, and what classic-theme code does that replace?


5. `theme.json` now declares `templateParts` with `"area": "header"`. The part file
   rendered fine before that existed. So what did declaring the area actually buy?


6. One thing that surprised me.

