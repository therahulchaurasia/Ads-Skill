# The Ad Spec

One file per ad. Written at the end of Stage 3, executed in Stage 4, updated in Stage 5.

It exists so an ad is a thing you can re-run, edit one field of, and diff against another. Without it, "change one variable at a time" depends on Claude remembering what it did last turn, which does not survive a new session.

**Never shown to the user.** Like the brand profile, the skill writes it and executes it. Nobody sees JSON in chat.

## Where it lives

```
.ad-studio/
├── brand.json
├── references/     reference ads they supplied
├── products/       their product photos and logo
├── archive/        superseded brand profiles, when the brand changes
└── ads/            specs and finished ads, side by side
    ├── comparison-pain-cold.json
    ├── comparison-pain-cold-prompt-pack.md      only when no generator is connected
    ├── comparison-pain-cold-var-1_4x5.png
    ├── comparison-pain-cold-var-1_9x16.png
    └── comparison-pain-cold-var-2_4x5.png
```

**Two levels deep, never more.** No folder per ad, no folder per variation. The name prefix groups everything and sorts it together, which does the same job without making the user click through a tree to find one PNG.

`<output-name>` describes the ad, not the brand: `<format>-<angle>-<audience>`. It is the filename prefix for the spec and every image that comes from it.

## Schema

```json
{
  "output_name": "<format>-<angle>-<audience>",
  "brand": "<brand-slug>",
  "product_name": "<product name and size>",

  "derived_from": null,
  "reference_image": ".ad-studio/references/<reference-file>.png",

  "brief": {
    "format": "feature-callout",
    "variant_of_format": "problem-inversion - callouts name problems, not features",
    "goal": "first purchase, cold audience",
    "persona": "<one person, what they already believe>",
    "awareness_observed": "<what the reference targets>",
    "awareness_target": "<what this ad targets - wins when they differ>",
    "hook_mechanic": "negative-marketing",
    "mechanism": "<one sentence: why the reference works>",
    "read_order": ["headline", "product", "callouts", "cta"]
  },

  "layout_zones": {
    "headline_zone": { "top": 0.05, "bottom": 0.22 },
    "callout_zone":  { "top": 0.30, "bottom": 0.75 },
    "product_zone":  { "top": 0.25, "bottom": 0.88 },
    "cta_zone":      { "top": 0.88, "bottom": 0.95 }
  },

  "detail": {
    "attachment": "notched",
    "points_at": "<what each connector aims at>",
    "shape": "pill",
    "fill": "solid accent",
    "edge": "soft drop shadow",
    "tilt": "none",
    "distribution": "asymmetric, two per side",
    "dividers": "none",
    "emphasis": "second headline line heavier than the first"
  },

  "copy": {
    "headline": { "text": "<approved headline>", "source": "written" },
    "callouts": [
      { "text": "<callout 1>", "source": "INFERRED" },
      { "text": "<callout 2>", "source": "INFERRED" }
    ],
    "cta": { "text": "<approved cta>", "source": "OBSERVED" },
    "ads_manager": {
      "primary_text": "",
      "headline": "",
      "description": "",
      "cta_button": "Shop Now"
    }
  },

  "slots": {
    "layout": "reference_image",
    "product": "products/<product-photo>",
    "copy": "written",
    "proof": "none",
    "look": "brand default",
    "color": "brand",
    "type": "brand"
  },

  "product_images": [".ad-studio/products/<product-photo>"],
  "offer": "<the offer this ad carries, or none>",
  "aspect_ratio": "4:5",
  "additional_aspect_ratios": ["9:16"],

  "variations": [
    {
      "slug": "var-1",
      "what_changed": "baseline",
      "prompt": "...",
      "result": "<output-name>-var-1_4x5.png",
      "status": "shipped"
    },
    {
      "slug": "var-2",
      "what_changed": "hook_mechanic: negative-marketing -> curiosity-loop",
      "prompt": "...",
      "result": null,
      "status": "planned"
    }
  ]
}
```

## Field notes

**layout_zones** are fractions of frame height, `0.0` at the top edge, `1.0` at the bottom. Add `left` and `right` the same way when horizontal placement matters (a product held at the right edge, a left-aligned text rail).

**Zones may overlap, and usually should.** In the example the product runs 0.25-0.88 while the callouts sit 0.30-0.75 - the labels are over the product, which is the point of that format. Prose cannot express that cleanly; numbers can.

Be honest about what the numbers buy. **Image models do not honour exact geometry** - passing 0.05-0.22 will not place the headline at precisely 5%. The precision is for us: reproducibility, diffing, and variant tracking. Translate zones into prompt language when generating ("headline across the top fifth"), and keep the numbers for the record.

**awareness_observed vs awareness_target.** The reference targets one awareness level; this ad may target another. Record both - the gap between them is the mismatch Stage 3 exists to catch. `awareness_target` is what the copy and angle serve; `awareness_observed` is context for why the layout looks the way it does. When only one is known, fill `awareness_target`.

**variant_of_format** - optional, one line, only when the reference bends its format in a way worth naming ("problem-inversion - callouts name problems, not features"). Leave it out otherwise.

**offer** - what this ad is actually offering, or `none`. Asked in Stage 3 and a variation axis in Stage 5, so it needs somewhere to live.

**detail** is section J of the brief. Carry it into the prompt only when the reference is *not* being passed as an image - see `prompt-craft.md`.

**copy.source** on every factual element: `OBSERVED` (read from a real source), `INFERRED` (reasoned from something real), `ASSUMED` (invented to fill the layout), or `written` for creative lines carrying no factual claim. Anything `ASSUMED` is resolved before the ad ships.

**slots** records which reference or asset filled each role. It is what lets a variant change one input without rebuilding the reasoning - and what tells you, a week later, where a layout came from.

**variations[].what_changed** is the most valuable field in the file. One variable per variation, named. `"hook_mechanic: negative-marketing -> curiosity-loop"` is readable in a month; `"var-3"` is not.

## Using it

**Writing.** At the end of Stage 3, once the user has approved the plan - brief, zones, detail and slots. The `copy` block stays empty until Stage 4 approves wording, then gets filled in. The spec is the approved plan in machine form: if it contains something they did not agree to, the gate was skipped.

**Executing.** Stage 4 builds the prompt from the spec plus the reference image on disk, not from the conversation. The spec carries the decisions; the reference image carries the visual detail that would be wasteful to transcribe.

**Re-running.** Same spec, same prompt, new seed. This is the cheapest fix for a garbled or badly composed output and should be the first thing tried.

**Varying, or starting a new ad.** The filename decides which.

`output_name` is `<format>-<angle>-<audience>`. Change any of those three and it is a **new spec** - the name no longer describes the file. Change anything else and it is a **variation appended to this one**.

| Changed | Result |
|---|---|
| format, angle, or audience | new spec file, `derived_from` set to the old one |
| hook mechanic, copy, detail, look, product photo, ratio, seed | append to `variations` |

Appending: change exactly one field, name it in `what_changed`, re-run. Never edit an existing variation in place - the record of what was tried is the point.

Starting a new spec: copy the old one, change the field, set `"derived_from": "<old-output-name>"`, and reset `variations` to a single baseline. Do not re-interview the user - everything needed is already in the spec they approved.

**Recording.** Stage 5 writes `result` and `status` back. A spec with three shipped variations is a working history of what the brand has tried, and the input to deciding what to try next.
