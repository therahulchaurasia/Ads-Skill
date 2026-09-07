# Prompt Craft

Turning a filled brief plus a brand profile into a prompt an image model will actually execute.

## Pass the reference as an image, not as a description

Where the model accepts multiple input images, use this convention. It is the single biggest quality lever available.

```
Image 1   the reference ad        - structural template only
Image 2+  the product photos      - what the product must actually look like
```

The prompt then names what each image is for. The model copies the *arrangement* from image 1 and the *product* from images 2+, and takes everything else - color, type, words - from the prompt.

This beats describing the layout in prose, because layout is spatial and prose is not. It also beats describing the product, because a real photograph of the product is always more accurate than a model's guess at it.

More product angles means better product fidelity. Three or four photographs from different angles is a meaningful upgrade over one.

If the model accepts only one input image, pass the product photo, not the reference, and describe the layout in words. The product is the harder thing to fix.

## The prompt template

Write the prompt as labelled slots, not prose. Each line maps to one decision, so any line can be edited and re-run without rewriting the whole thing.

```
Image 1: reference ad layout - structural template only
Background: [brand background colour]
Typography: [brand typeface + weight]
Headline: "[the approved headline]"
Benefits: [the approved benefit rows]
CTA: "[the approved CTA text]"
Product: exact [brand product] from images 2+
[safe zones - 9:16 only, omit for feed]
[aspect ratio] aspect ratio
```

Line by line:

- **Image 1** - structure only. Never brand identity. This line is what keeps the rebuild from becoming a copy.
- **Background / Typography** - always from the brand profile. Never from the reference. These two lines are the whole reason the output looks like the user's brand and not the reference's.
- **Headline / Benefits / CTA** - the copy approved in Stage 3, pasted in exactly. Not paraphrased at generation time.
- **Product** - "exact ... from images 2+" tells the model to match rather than invent.
- **Safe zones** - only for 9:16. Feed has no UI overlay; see below.
- **Aspect ratio** - 4:5 by default.

## The detail layer - two opposite jobs

Section J of the brief records how text attaches to graphics: notches, leader lines, arrows, shape, fill, edge, tilt, dividers. What the prompt does with it depends entirely on whether the reference is being passed as image 1.

### When the reference IS passed as an image

The model copies the detail visually. Notch shapes, shadows, and spacing transfer on their own, and describing them again wastes words the prompt cannot spare.

**The risk inverts here: the model copies too much.** It will carry the reference's colours and typeface across unless told not to. So the prompt's job is *overriding identity*, not describing craft:

```
Image 1: reference ad layout - structural template only.
Match its callout treatment and spacing. Do not carry its colours or typeface.
Background: [brand background]
Typography: [brand typeface + weight]
```

Check the output for identity bleed - a stray accent colour from the reference, a typeface that is not the brand's. That is the failure mode on this path, not blandness.

### When the reference is NOT passed as an image

Some models take one image only, and the product photo should win that slot. Now the detail must be carried in words, because a model given "four labels around the product" draws four plain rectangles floating in space. It is the safest thing it can draw, and it is what makes a rebuild look generic beside its own reference.

Be specific about:

- **attachment** - notched, leader line, arrow, touching, or floating; and what it points at
- **shape and fill** - pill / rounded rect / hard rect / tag; solid / translucent / outline only
- **edge** - flat, drop shadow, stroke
- **tilt and distribution** - evenly spaced or scattered, square or slightly rotated
- **dividers and emphasis** - thin rules between rows, underlines, highlight bars

Compare:

> Bland, what the model gives for free: "Four labels around the product."
>
> Specific: "Four small pill-shaped callouts in [accent colour] with pointed speech-bubble notches, each notch aimed at a different point on the product, solid fill, white uppercase text, soft drop shadow, distributed asymmetrically."

A callout that points at nothing reads as decoration. If the reference's labels aimed at specific points, say so explicitly or the model will float them.

Keep it to one sentence. Worth the words; cut treatment detail elsewhere to pay for it.

## Safe zones - only where they exist

Safe zones are **placement-specific**, not universal. Applying them everywhere costs a fifth of the canvas for nothing.

| Placement | UI over the creative | What to ask for |
|---|---|---|
| Feed 4:5, 1:1 | **None.** Profile name renders above the image, CTA below | Nothing. Design edge to edge if the layout wants it. |
| Stories / Reels 9:16 | **Yes.** Unified across Facebook and Instagram since March 2026 | Top 14%, bottom 35%, 6% each side clear of anything that must be read |

So for a feed ad, do not put a safe-zone line in the prompt. Big type running near the top edge is normal in feed creative and often what makes it stop the scroll.

For a 9:16 asset, put it in:

```
Safe zones: top 14% and bottom 35% clear of text, 6% clear at each side
```

**Reformatting caveat.** If one asset is going to be stretched across placements - Advantage+ or "use for all placements" - it will be reframed into 9:16 and the crop eats whatever sits at the edges. Either design the 4:5 with the 9:16 crop in mind, or make a separate 9:16. A separate asset is better; automatic reframing is where good feed creative goes to die.

**Verify regardless of what the prompt said.** Instruction adherence varies by model - some respect a stated margin, some ignore it. Check the output rather than trusting the request.

## When there is no reference image to pass

Falling back to describing the layout. Record and describe zones as **fractions of frame height**, not as vague regions - it is what a model can act on:

> "Headline occupies the top 25% of the frame, left aligned. Three benefit rows fill the middle 35%, each separated by a thin rule. CTA button sits at 70% down, left aligned. Product held in frame at the right edge, occupying the right third."

Assemble in this order - models weight early tokens more heavily:

```
1  MEDIUM        what kind of image this is
2  COMPOSITION   where things sit, as fractions of the frame
3  SUBJECT       the product or person, described concretely
4  TREATMENT     lighting, background, surface, mood
5  COLOR         brand colours, mapped onto the reference's colour roles
6  TEXT          exact strings, quoted, with placement
7  TECHNICAL     safe zones, aspect ratio, resolution
```

## Hard rules

**Under 200 words.** Models degrade past that - they drop instructions rather than compressing them. Cut treatment detail first, never composition.

**Phrase positively.** Most models have no negative prompt. "Tack sharp" not "no blur". "Clean single-colour background" not "no clutter".

**Never name a brand, a real person, or a trademarked character.** Image models terminate these prompts outright. Describe the thing: "a rounded amber glass dropper bottle", never the brand name.

**Quote on-image text exactly, and keep it short.** Six words or fewer per block.

**Describe fonts as language, not files.** "Bold condensed sans, tight letter spacing, all caps" works. A font filename does nothing.

**Colours: give the role and the value**, taken from the brand profile - "[background colour] background, [accent colour] accents, [text colour] type". GPT-Image-class models also respect hex; give both when in doubt. Never let an example palette from this file reach a prompt: every colour comes from the brand.

## Mapping colour without copying it

The brief records the reference's colour *roles* - background, surface, accent, text - and where the highest contrast sits. Never carry its actual palette.

```
reference role structure          brand profile        prompt
--------------------------------  -------------------  --------------------------
dark background                   [background]         "[background] background,
bright accent                     [accent]             [accent] accents,
light text                        [text]               [text] type,
highest contrast at the product   ---                  strongest contrast at
                                                        the product"
```

The left column is read off the reference. The middle column is read off the brand
profile. The right column is the two combined. No colour ever travels from the
reference to the prompt, and no colour in this file is a default.

Same structure, different skin. That is the whole method in one table.

## On-image text: know your model's ceiling

| Model class | Text ability | Approach |
|---|---|---|
| GPT-Image class, Nano Banana Pro, Ideogram | Strong | Text in the prompt, quoted. Verify letterforms in the output. |
| Flux, Recraft, Seedream | Moderate | Short strings only. Expect a retry or two. |
| Midjourney, most diffusion models | Weak | No text in the prompt. Use the two-pass method. |
| Unknown | Assume weak | Two-pass. |

**Garbled text on a strong model is usually seed variance, not a limit.** Regenerate once before changing anything - a clean run often fixes it. If it persists across runs, shorten the string; if it still persists, go two-pass.

### The two-pass method

When the model cannot be trusted with letters:

**Pass 1 - the plate.** Generate with deliberate empty space where text belongs: "upper third is a clean uncluttered [background colour] field with no objects, reserved for text". Composition, product, lighting and colour all still come from the prompt.

**Pass 2 - the text.** Hand over the exact copy, placement, and type direction to set in Canva or Figma - two minutes of work.

Not a downgrade. It is how most performance creative is actually made, and it keeps the copy editable for variants, which baked-in pixels never are.

## Aspect ratio

Generate the primary at **4:5**, then reformat to any additional ratios from it. The 10% safe-zone margins are what make that crop lossless.

| Target | Ask for | Note |
|---|---|---|
| 1080x1350 (4:5 feed) | 4:5, else 3:4 | Best-performing feed size. Many generators do not offer it; from 3:4, crop the height. |
| 1080x1080 (1:1 feed) | 1:1 | Universally supported. Safe fallback. |
| 1080x1920 (9:16 story) | 9:16 | Reformat from the 4:5 primary. |

If 4:5 is unreachable and no resizing is available, use 1:1 and say so once. Do not block on it.

Generate at the highest resolution offered. Downscaling is free; upscaling is not.

## Iterating

**Regenerate freely.** Copy and layout are locked in the prompt, so every run re-executes the same specification - only the seed changes. A second run is the cheapest fix available and should be the first thing tried.

**Change one line at a time.** If the composition is right and the colour is wrong, edit only the colour line. A rewritten prompt gives a different image, not a corrected one.

| Symptom | Fix |
|---|---|
| Text garbled | Regenerate once. Then shorten. Then two-pass. |
| Product wrong | Add more product photos, from more angles |
| Brand colours ignored | Check the brand profile is current; state colours as role plus value |
| Composition ignored | Move the composition line earlier; cut treatment detail |
| Product looks generic | Add material and finish - "matte recycled kraft", "brushed aluminium" |
| Too busy | Cut adjectives, name one light source, specify which regions stay empty |
| Reference not translating | A busy-background reference often will not. Find a cleaner one in the same format. |
| Prompt rejected | A trademark, real person, or policy term slipped in. Describe rather than name. |
