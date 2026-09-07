# Reference Brief Schema

Filled in Stage 2. Drives the prompt and the copy in Stage 4.
Design constraints: extractable by vision from one image; compressible to a prompt under 200 words; sufficient to rebuild in a different brand.

## A. Classification
- `archetype` - one of 12: product-hero | testimonial | before-after | feature-callout |
  us-vs-them | ugc-native | grid-collage | offer-promo | lo-fi | stat-callout | meme | listicle
- `awareness_stage` - unaware | problem-aware | solution-aware | product-aware | most-aware
  This is what the REFERENCE targets. What YOUR ad targets is decided in Stage 3 and may differ -
  the gap between them is the mismatch worth catching.
- `variant_of_format` - optional. Only when the reference bends its format in a way worth naming,
  e.g. "problem-inversion - callouts name problems, not features".
- `angle` - pain | aspiration | social-proof | curiosity | humor | education | authority
- `mechanism` - one sentence: WHY this ad works. The thing worth stealing.

## B. Canvas
- `ratio` - as shipped (1:1 / 4:5 / 9:16)
- `density` - sparse | balanced | dense  (approx % of canvas covered by text/graphic overlay)

## C. Layout (the transferable part)
- `zones` - ordered list, each: {band, contains, weight}
  band = fraction of frame height, e.g. "top 25%", "35%-70%", "bottom 15%"
         plus horizontal placement where it matters: left-aligned / centered / right third
  contains = product | headline | subhead | proof | badge | cta | person | background
  weight = dominant | supporting | minor

  Fractions, not vague regions. "Headline top 25%, three benefit rows through the
  middle 35%, CTA at 70% down, product held at the right edge" is executable by an
  image model. "Headline at the top" is not.
- `read_order` - sequence of `contains` values, 1->n. What the eye hits first, second, third.
- `focal` - what dominates and how much of the frame it holds
- `alignment` - centered | left-rail | split | diagonal | radial

## D. Treatment
- `photo_style` - studio | lifestyle | flat-lay | selfie/UGC | screenshot-mimic | illustration | none
- `lighting` - soft | hard | high-key | moody | flat
- `background` - solid | gradient | environment | texture | cutout-on-color
- `ui_mimicry` - none | imessage | comment-thread | notes-app | review-widget | search-result

## E. Color (ROLES, not the reference's hexes)
- `roles` - {background, surface, accent, text-primary, text-inverse}
  Record the ROLE STRUCTURE and contrast relationships only.
  Never carry the reference's actual palette. Brand lock supplies the hexes.
- `contrast_pattern` - where the highest contrast sits (usually = focal)

## F. Typography (structure, not the reference's fonts)
- `blocks` - count of distinct text blocks
- `per_block` - {role, approx_words, case, weight_relative, size_relative}
  role = hook | support | proof | offer | disclaimer | cta
- `type_contrast` - ratio between largest and smallest block

## G. Copy slots
For each: the FUNCTION, plus the reference's structural pattern (not its words).
- `hook` - pattern e.g. "negation of category assumption", "number + noun", "direct question"
- `support` - pattern
- `proof` - device: stars | quote | stat | badge | chart | checklist | logo-row | none
- `offer` - present/absent, type
- `cta` - verb pattern, placement

## H. Transfer control (IP boundary)
- `keep` - structure, hierarchy, read order, archetype, copy patterns, contrast logic
- `discard` - logo, wordmark, product shape, palette, typeface, mascot, tagline wording,
  any distinctive graphic device unique to that brand
- `risk_flags` - anything that would trigger ip_detected or read as trade dress

## I. Meta compliance pre-check
- `safe_zone_conflicts` - copy sitting where platform UI will land
- `policy_flags` - before/after claims, health/financial claims, body-image framing,
  personal attributes ("your acne"), unverifiable superlatives

## J. Detail layer - how text attaches to graphics

The difference between a rebuild that reads as designed and one that reads as generic. Zones and read order transfer the skeleton; this transfers the craft. Skipping it produces a technically correct ad that looks bland next to its own reference.

Capture per text element that sits over or beside artwork:

- `attachment` - how the label relates to the thing it describes:
  `notched` (speech-bubble tail pointing at a spot) | `leader-line` | `arrow` |
  `bracket` | `touching` (abuts the subject) | `floating` (no connection)
- `points_at` - if attached, the specific point on the subject. Callouts that point
  at nothing read as decoration.
- `shape` - pill (fully rounded) | rounded rect | hard rect | circle | tag | hand-drawn
- `fill` - solid | translucent | outline only | none
- `edge` - flat | drop shadow | stroke | glow
- `tilt` - any deliberate rotation off-axis
- `distribution` - evenly spaced | organic/scattered | aligned to a grid

Also capture, where present:

- `dividers` - thin rules between benefit rows, or none
- `emphasis` - underline, highlight bar, colour shift, weight change on key words
- `text_align` inside each element
- `overlap` - do labels overlap the product, abut it, or clear it entirely

### What transfers and what does not

**Generic devices transfer.** A notch, a leader line, an arrow, a pill shape, a
drop shadow, a divider rule - these are common visual grammar, not identity.
Take them. They are most of what makes a reference feel considered.

**Brand-distinctive devices do not.** A signature badge shape, a custom frame,
a proprietary swoosh or mascot, a recognisable graphic motif - these belong to
the brand that made them. Describe the *function* they served and rebuild it
with a generic device instead.

The test: would a designer call this a technique, or would they call it
"that brand's thing"? Techniques transfer.
