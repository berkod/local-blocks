  1. What's the actual difference between Group/Row/Stack? (Hint: it's layout type, not separate block types — check the markup)

Different is in the layout attributes. The classes assigned to the divs and the block type are the same for each variation (wp:group).

I was confused a bit because the admin toolbar describes each layout differently ( Row, Group, Grid, Stack ), so they seem like different blocks

```
  <!-- wp:group {"layout":{"type":"flow"}} -->        ← Group
  <!-- wp:group {"layout":{"type":"flex"}} -->         ← Row
  <!-- wp:group {"layout":{"type":"flex","orientation":"vertical"}} --> ← Stack
```

  2. Where does alignment (wide, full, contentSize) actually live in the serialized output?

  There's an attibute in the block json called "align" that controls the alignment in addition to a class on the container. I got stuck on considering alignment as left, right or center, not width of the container.


  3. One thing that surprised you about how layout nesting works

How straightforward the nesting and mark up are once I got past the confusion about the terminology differences between the visual editor and the code (group with a layout of flex in the code and it being ROW in the visual)

This seems to be a common pattern:  the editor uses friendly names (Row, Stack, Grid, Cover) but the serialized markup uses fewer, more generic block types.
