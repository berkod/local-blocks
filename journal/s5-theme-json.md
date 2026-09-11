# S5 — theme.json deep dive

1. In one sentence each: what does `settings` do, and what does `styles` do? What does each one compile into?


2. I wrote `"primary": "#c2410c"` in `settings.color.palette`, and separately wrote
   `"color": { "text": "var(--wp--preset--color--primary)" }` in `styles.elements.link`.
   Why the indirection? Why not just write `#c2410c` in the styles section?


3. We set `defaultPalette: false` and the core colors stayed in the generated CSS anyway.
   What DID that flag change, and what's the practical lesson about what `settings` controls?


4. Core generated `a:where(:not(.wp-element-button)){...}` rather than a plain `a{...}`.
   Why does core wrap its selectors in `:where()`? (Think about specificity and user overrides.)


5. One thing that surprised me.

