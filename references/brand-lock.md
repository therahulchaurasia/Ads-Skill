# Brand Profile - `.ad-studio/brand.json`

The source of truth for this project's brand. Written in Stage 1, read by every later stage, verified against in Stage 5.

Written once, then never asked about again. If any of it was guessed or auto-detected rather than confirmed by the user, mark it and confirm before it drives a paid creative.

## Schema

```json
{
  "brand": {
    "name": "",
    "sells": "one sentence: what it is and who it is for",
    "website": ""
  },

  "palette": {
    "background": "<hex or plain description>",
    "surface":    "<hex or plain description>",
    "accent":     "<hex or plain description>",
    "text":       "<hex or plain description>",
    "text_inverse": "<hex or plain description>"
  },

  "type": {
    "headline": "font name or description, e.g. 'bold geometric sans, tight tracking'",
    "body":     "font name or description",
    "case":     "sentence | title | upper"
  },

  "logo": {
    "file": ".ad-studio/products/<logo file>",
    "placement": "top-left | bottom-center | none",
    "rules": "never recolor, never on busy photo, min clear space = logo height"
  },

  "voice": {
    "words": ["direct", "warm", "confident"],
    "avoid": ["hype", "clinical", "salesy"]
  },

  "claims": {
    "allowed": [],
    "banned":  [],
    "notes":   "regulated category? name it here"
  },

  "products": [
    { "name": "", "photo": "", "price": "", "offer": "" }
  ],

  "confirmed": {
    "palette": true,
    "type": false,
    "claims": false
  }
}
```

## Field notes

**palette** - five roles, not a swatch dump. Every generated ad maps the reference's color *structure* onto these five roles. If the user knows only one color, put it in `accent` and choose sensible neutrals for the rest - then say that is what you did rather than presenting invented colors as theirs.

**type** - a description is fine and often better than a name. Image models take fonts as language, not files. "Bold geometric sans, tight tracking" outperforms a font filename.

**claims.banned** - the highest-value field here and the one users skip. Checked before anything ships. Push for it once, especially in supplements, skincare, finance, and weight-related categories. An empty banned list for a regulated brand means it was not asked properly, not that there are no limits.

**products.photo** - a real product photograph beats any generated approximation of the product. Where one exists, the generated ad should be built around it rather than around a model's guess at what the product looks like.

**logo.file and products[].photo** are the only asset paths. Both live in `.ad-studio/products/`. There is no separate assets folder.

**confirmed** - which fields the user actually verified versus which were auto-detected or inferred. Anything unconfirmed gets a quick check before it drives a paid creative. Auto-detected brand colors are usually close and quietly wrong about one value.

## What does NOT belong here

- Anything taken from a competitor's ad. References are read per campaign and never stored as brand truth.
- Prompt text or model names. Those belong with the generation step.
- Campaign or performance data. This file describes the brand, not the work.
