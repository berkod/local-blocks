  1. What is a block, in one sentence?

A block is html delineated by html comments in a specific format that informs WP how to render the block.

_The comment + HTML together is the block. But worth tightening: a block is a JS object (name, attributes, edit fn, save fn) registered in JS. The stored HTML is just its output. The comment is the re-hydration contract. When you see code editor view, you're seeing the save output, not the block itself._

  2. Where does block data live in the database? What column?

wp_posts.post_content

  3. What do the <!-- wp:... --> delimiters do? What breaks if you remove them?

the delimiters inform the WP render how to render the block. The delimiter stores custom display info as json. If you remove the delimiter, the block is broken and is rendered as standard html.

_it becomes a Classic block (wraps the orphaned HTML in <!-- wp:freeform -->). Gutenberg is defensive about raw HTML it can't parse. Worth knowing because clients will occasionally paste raw HTML and wonder why their block toolbar is gone._

  4. How is a static block fundamentally different from a shortcode at render time?

static block is rendered at save

_the stored HTML is the front-end output — PHP runs zero render logic for static blocks. That's why static blocks are fast but their output is frozen at save time._

  5. One thing that surprised you, one thing still unclear.

  Surprise: How much my understanding of blocks grew just by grokking the wp:... comments and json attributes.

  Unclear: Shortcodes vs blocks, and how blocks will update if the underlying React changes if they are rendered on save.


_This is block deprecations — one of the trickiest parts of block dev. Short answer:_

  - _WP stores the save output. If you ship a new version of your block with a different save function, old posts have HTML that no longer matches   → block validation error in the editor._
  - _Fix: deprecated array in block registration. You list old save functions so WP can recognize old output and migrate it._
  - _Core handles this all the time — why you occasionally see "block updated" notices._

_This bites custom block developers hard the first time. S14 (Cook Time block) will touch it. Worth bookmarking._
