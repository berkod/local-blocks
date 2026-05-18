1. wp:paragraph

```
<!-- wp:paragraph {"style":{"border":{"radius":{"topLeft":"17px","topRight":"17px","bottomLeft":"17px","bottomRight":"17px"}},"elements":{"link":{"color":{"text":"var:preset|color|accent-3"}}}},"textColor":"accent-3"} -->
<p class="has-accent-3-color has-text-color has-link-color" style="border-top-left-radius:17px;border-top-right-radius:17px;border-bottom-left-radius:17px;border-bottom-right-radius:17px">
```

The comment includes the style configuration, but it's also in the class and style declarations of the p tag. I would have expected this not to be duplicated, that the comment config would  be the single source of truth. However, it makes sense that it's duplicated so that the visual editor gets the styling as well, not just the published page.

```
<!-- wp:heading {"textAlign":"center","className":"is-style-text-display"} -->
<h2 class="wp-block-heading has-text-align-center is-style-text-display">
```

in the heading, there is a textAlign attribute that is converted to a class name, but also a classname attribute. i wonder what the point of this is, since I doubt it's just an inconsistency. There probably is a reason for this.

I added a second heading. This one includes a level:3 attribute since it's an h3. Again, odd inconsistency with the h2.

```
<!-- wp:list {"className":"pork-list","fontSize":"small"} -->
<ul id="pork-list" class="wp-block-list pork-list has-small-font-size"><!-- wp:list-item -->```

I like the simplicity of the plain list. it's not far removed from an html list. Again, a seeming inconsistency: the extra class name i assigned the list shows up in both the json attributes and the ul, but the custom anchor/id i added in the visual editor doesn't appear  in the json.

```
<!-- wp:image {"id":15,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://berkod.local/wp-content/uploads/2026/05/Screenshot-2026-03-20-at-4.13.36-PM-1024x92.png" alt="" class="wp-image-15"/></figure>
<!-- /wp:image -->
```

Since WP is big on a11y and performance, I expected this to include a srcset. would be nice if the visual editor flagged missing alt text. why is the custom wp-image-15 class only on the image not the figure?

```<!-- wp:cover ...```

We discussed the cover block already. Interesting that this is a default block.


```
<!-- wp:gallery {"linkTo":"none"} -->
<!-- wp:image {"id":26,"sizeSlug":"large","linkDestination":"none"} -->
```

Gallery is interesting. Very much shows the nature of block composition from smaller component blocks. Surpised the default doesn't produce a link to a larger image in a letterbox (same with regular image. blocks).

But coming from the publishing world, I wonder if commercial publishers use this as is or customize it to include ad blocks or a slider?

Media and Text block: this one is interesting because the visual editor seems to allow one to both add different blocks, and also limit which blocks are allowed. This seems like it would be the easiest way to add a photo+credit+caption, but still would need some custom work to make all those fields. defaults.

Blockquote, i would like to see a way of adding a citation in the visual editor
