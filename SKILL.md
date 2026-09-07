---
name: ad-studio
description: Turn reference ads you admire into on-brand Meta static ads. Reads one reference or a whole swipe file to work out why they convert, rebuilds that structure in your brand, writes the on-image and Ads Manager copy, checks sizing and policy, then generates the image with whatever image model is available or hands you a ready-to-paste prompt. Works with any image generator.
when_to_use: Use when the user has competitor or inspiration ads and wants their own version, says "replicate this ad", "make this ad for my brand", "recreate this creative", "make static ads", drops a swipe file and asks what works in the category, or drops an ad screenshot and asks what makes it work.
argument-hint: "[path to reference image or folder] [optional: brand or product name]"
allowed-tools: Read, Write, Edit, Bash, Glob, WebFetch
---

# Ad Studio

Rebuild a reference static ad as an on-brand Meta ad. References in, finished creative plus its copy out - one ad, a batch from a swipe file, or a read of what a category is running.

## Who you are talking to

A marketer, not an engineer. Possibly new to AI tools.

- **One question per turn.** Never a list of questions.
- **No jargon in chat.** Say "a warm orange", not a hex code. Say "your brand profile", not a filename.
- **Never show raw JSON, file paths, or model names** unless asked. Keep the schema internal.
- **End every stage with one line**: what they now have, and what happens next.
- **Never spend money silently.** If generating costs credits, say so before the call.
- If they seem lost, stop the pipeline and ask what they were expecting. Do not push forward.

## The five stages

```
1  Brand   ->  who we are making this for        (skip if already known)
2  Read    ->  what the reference is doing       (the important one)
3  Plan    ->  their version, confirmed by them
4  Make    ->  copy + prompt -> image
5  Check   ->  sizing, policy, brand -> ship or fix
```

Do not run stages in parallel. Do not skip stage 3.

---

## Stage 1 - Brand

If `.ad-studio/brand.json` exists, load it and name the brand in one line - "Making these for <brand>." - then move on. No question. Naming it is enough: if it is the wrong brand the user will say so, and if it is right they have lost nothing.

Should they say it is a different brand, move the old profile to `.ad-studio/archive/` and build the new one from scratch. Do not merge, and do not keep the old colours as a starting point - a stale accent is what survives into the output.

**Check the assets.** If a logo or product image carries placeholder or template content - dummy text, a stock mockup, a name that is not theirs - say so and ask for the real file. A placeholder that reaches the prompt reaches the ad.

Otherwise ask for the minimum, one at a time, and stop as soon as you can work:

1. Brand name and what it sells, in one sentence
2. Their main color - hex, a description, or "pull it from my logo"
3. A product photo or logo, if they have one

Everything else can wait. Write what you learn to the brand profile per `references/brand-lock.md` so it is never asked twice.

**One thing worth pushing for, once:** anything they must never claim. Supplements, skincare, finance, and weight-loss brands get ads rejected over wording, not images. Ask once, record it, do not nag.

---

## Stage 2 - Read the reference

References are screenshots or image files. If given a Meta Ad Library link, ask them to screenshot it - the Ad Library blocks automated fetching, and their screenshot is faster than any workaround.

### More than one reference?

Do not guess how they combine. **Ask what each one is for.** Every ad is assembled from slots, and each slot takes exactly one source:

| Slot | Usual source |
|---|---|
| Layout | one reference - **only ever one** |
| Product | their photo (best), a reference, or generated |
| Copy | a reference's pattern, or written fresh |
| Proof | a reference's device, or the brand's real proof |
| Look | a reference, or brand default |
| Color and type | **always the brand** |

Ask only about slots that are open, one question per turn, in plain language: "Which of these has the layout you want?" / "Do you have your own product photo?" Stop as soon as the ad is specified. Full question script in `references/multi-reference.md`.

**Layout takes exactly one source.** Two layouts cannot merge - a comparison split plus a testimonial quote plus a stat hero is a cluttered ad with no read order, and read order is the only thing a static ad really has. Drop anything that competes with the chosen layout, and say why.

If the pile is a swipe file for several ads, or a category to analyse rather than copy, see the second half of `references/multi-reference.md`.

### Reading one reference

Look at the image and fill in the brief. Full field list in `references/brief-schema.md`. Format identification in `references/ad-formats.md`.

Answer these in order, because each depends on the last:

1. **Which of the 12 formats is this?** See `references/ad-formats.md`.
2. **What does the eye hit first, second, third?** This is the layout's job. Record it.
3. **Where does everything sit?** Product, headline, proof, CTA - as **fractions of frame height** ("headline top 25%, three benefit rows through the middle 35%, CTA at 70% down"). Fractions transfer into a prompt; vague regions do not.
4. **How does text attach to the graphics?** Notched pills pointing at the product, leader lines, arrows, or floating with no connection? Pill or hard rectangle, solid or translucent, shadowed or flat, tilted or square? Dividers between rows? This is the detail layer (`brief-schema.md` section J) and it is what separates a rebuild that looks designed from one that looks generic. Zones transfer the skeleton; this transfers the craft.
5. **What is the copy doing?** Not what it says - its pattern. "Denies a category assumption." "Leads with a number."
6. **Why does it work?** One sentence. This is the thing worth taking.

### The rule that governs everything

**Take the structure. Leave the identity.**

| Take | Leave |
|---|---|
| Layout, zones, read order | Their logo, wordmark, colors, fonts |
| Which format it is | Their product's shape and packaging |
| Copy patterns and slot order | Their actual sentences and tagline |
| Where contrast sits | Any graphic device unique to them |
| Generic devices - notches, leader lines, arrows, pills, shadows, dividers | Signature devices - a custom badge, frame, swoosh, or mascot |

The last row matters more than it looks. Generic devices are common visual grammar and they are most of what makes a reference feel considered - take them. The test: would a designer call it a technique, or "that brand's thing"? Techniques transfer.

This is not only a legal boundary. Image models reject prompts containing trademarks, and a near-copy is worthless in the auction anyway - it competes against an ad that already owns that look. The structure is the transferable asset; the skin never was.

If the user asks for a closer copy, say once, plainly, that it will likely be rejected by the model and will not perform, offer the structural version, and follow their decision.

---

## Stage 3 - Plan (never skip)

### First, four decisions the reference cannot make for you

A reference carries somebody else's goal, persona and awareness level baked into it. Decide yours, then check the reference against them. Full detail in `references/creative-strategy.md`.

1. **Goal** - not "more sales". First purchase from cold, reactivating lapsed buyers, moving one SKU.
2. **Persona** - one person, not a bracket. What they already believe and have already tried.
3. **Format** - one of the 12.
4. **Awareness level** - and whether the format matches it.

Ask only what you cannot infer. If the brand profile and the reference already imply an answer, state it and move on rather than making them choose.

**The mismatch to catch:** a product-aware format aimed at a cold audience. A clean product hero shown to someone who has never heard of the category is invisible. If the reference is a most-aware offer ad and the goal is cold acquisition, say so - the layout is still usable, the angle is not.

Then pick the **hook mechanic** deliberately (`creative-strategy.md`, layer 3). It is also the cheapest variant axis: hold layout and product fixed, change only the hook.

### Then show the brief back

In plain English, and get a yes. Roughly:

> "Here is what that ad is doing:
>  It is a **comparison ad**. Your eye lands on the split down the middle, then the headline above it, then the price at the bottom.
>  The headline works by denying something people assume about the category.
>  For you, that would be: **<their version>**
>  Sound right, or want a different angle?"

Never generate before they have said yes to this. It is the cheapest place to be wrong.

Ask here, and only here, anything Stage 2 did not already settle: aspect ratio and the offer. Do not re-ask about the product photo - the slot questions covered it.

### Then write the spec

Once they have said yes, write the approved plan to `.ad-studio/ads/<output-name>.json` per `references/ad-spec.md`: brief, zones, detail, and which reference filled which slot. The copy fields stay empty until Stage 4 approves them, then get written in.

The spec is the approved plan in machine form - if it contains something the user did not agree to, the gate was skipped. Everything after this stage reads the spec plus the reference image on disk, not the conversation - which is what makes an ad re-runnable in a new session.

---

## Stage 4 - Make

### Copy first, approved before any pixels

Write the copy before the prompt. The image is built around the words, not decorated with them afterwards.

Ground the copy in real material, and prefer the sources that are hardest to fake:

```
customer voice (reviews, Reddit, comments)   strongest - their words, already validated
observed creative (what the category runs)
third-party coverage
the brand's own marketing copy               weakest - aspirational, not proven
```

A product page is the brand talking about itself. Read it for facts - ingredients, specs, review counts - but take the *language* from reviews wherever they exist. Customers describe the benefit in the words other customers search for.

**Tag every factual claim in the copy with where it came from.** These are internal working notes, never shown in chat:

| Tag | Means |
|---|---|
| `[OBSERVED]` | read from a real source - their page, their reviews |
| `[INFERRED]` | reasoned from something real, e.g. "popular with runners" because reviews mention running |
| `[ASSUMED]` | filled in to complete the layout, with nothing behind it |

Anything `[ASSUMED]` is removed or asked about before it ships. Never invent a number, a review count, or a certification. If a figure cannot be found, ask for it or leave the row out - an approximate stat is worse than no stat.

The risk this guards against: a reference ad has a stat-shaped hole in it, and rebuilding the layout creates strong pull to fill that hole with a plausible number. A fake stat gets ads rejected, and gets found out later.

Draft **three complete sets of copy**, not one, and get one approved. (These are drafts to choose between, not spec `variations` - nothing is written to the spec until they pick.)

- **On-image copy** - headline, benefit rows, CTA. Six words or fewer per block. Models garble long strings.
- **Ads Manager copy** - primary text (125 characters), headline (about 27), description, CTA button.

Show all three, let them pick or edit, then write the chosen one into the spec's `copy` block with its source tags. Copy is free to change now and expensive to change after generation, because a regenerated image is a different image.

### Then the prompt

Build it **from the spec**, not from the conversation - everything needed is in the file. Translate the numeric zones into prompt language ("headline across the top fifth") and keep the numbers for the record; image models do not honour exact geometry.

Write it per `references/prompt-craft.md` as labelled slots, not prose, so any single line can be edited and re-run:

```
Image 1: reference ad layout - structural template only
Background: [brand background colour]
Typography: [brand typeface + weight]
Headline: "[approved headline]"
Benefits: [approved benefit rows]
CTA: "[approved CTA text]"
Product: exact [brand product] from images 2+
[safe zones line - 9:16 only, omit for feed]
4:5 aspect ratio
```

**Pass the reference as image 1 and the product photos as images 2+** wherever the model accepts multiple images. The model takes arrangement from image 1 and the product from images 2+; everything else comes from the prompt. This is the single biggest quality lever, and more product angles means better product fidelity.

**Safe zones are placement-specific.** Feed (4:5, 1:1) has no UI over the creative - do not reserve margins there, it wastes a fifth of the canvas. Stories/Reels (9:16) does: top 14%, bottom 35%, 6% each side. Put the line in the prompt only for 9:16.

### Then render

Check what is available, in this order:

1. **An image generation tool is connected** - use it. Say what it will cost first. If more than one is available, prefer the one that handles on-image text best (see the model table in `references/prompt-craft.md`). If the call fails, say what failed in one line, then fall back to the prompt pack rather than retrying silently or leaving them with nothing.
2. **Nothing connected** - hand over a **prompt pack**: the prompt, the copy, the size, and one line on where to paste it. Never leave them empty-handed because a tool is missing. Write it to `.ad-studio/ads/<output-name>-prompt-pack.md` as well as showing it.

**Everything this skill produces goes under `.ad-studio/`.** Nothing is written to the project root or anywhere outside it, and generated images are saved into `.ad-studio/ads/` under the ad's name prefix rather than left wherever a tool dropped them. If a generator returns a URL or writes elsewhere, move the file in and record the path in the spec. Do not invent additional files beyond the spec, the prompt pack, and the images - the spec already holds the brief and the copy.

If the model handles on-image text badly (most do, outside GPT-Image-class models), generate a clean plate with space reserved and say the text gets set in Canva or Figma. `references/prompt-craft.md` covers the two-pass method.

### Output

Generate the primary at 4:5, then reformat to any other ratios needed from it.

Spec and images sit side by side in `.ad-studio/ads/`, sharing a name prefix:

```
<output-name>.json                 the spec
<output-name>-var-1_4x5.png        the primary
<output-name>-var-1_9x16.png       reformatted
<output-name>-var-2_4x5.png        next variation
```

**Keep the tree two levels deep at most.** No folder per ad, no folder per variation - the name prefix groups and sorts them already, and a deep tree just makes the user hunt for a PNG.

Write the prompt and the result path back into the spec's `variations` entry.

---

## Stage 5 - Check

Before it ships, verify against `references/meta-specs.md`:

- **Size** - 1080x1350 (4:5) for feed unless there is a reason otherwise. 1:1 is acceptable; 4:5 performs better.
- **Safe zones** - 9:16 only: top 14%, bottom 35%, 6% each side clear. Feed has no overlay, so nothing to check there.
- **Legible on a phone** - look at the image. If the smallest text would be unreadable at thumb size, it is too small. Say so.
- **Policy** - check the copy against their banned-claims list and against the policy section of `references/meta-specs.md`. Before/after framing, health outcomes, personal attributes ("your acne"), and unverifiable superlatives are the usual rejections.
- **Brand** - right colors, right voice, logo used per their rules.

Report as a short pass/fix list, not a paragraph. Fix what is fixable and regenerate; flag what needs their decision.

### Then offer the next one

Winning accounts run 6-8 formats and 12-15 new statics a week. One ad is a start, not a campaign.

Record the outcome in the spec - `result` and `status` on the variation - then offer the next one.

**Variation or new ad?** The filename decides. `output_name` is `<format>-<angle>-<audience>` - change one of those three and it is a new spec with `derived_from` pointing back. Change anything else and it appends to `variations`, one field at a time, named in `what_changed`. Never edit an existing variation in place; the record of what was tried is the point.

Either way, do not re-interview the user. Everything needed is in the spec they already approved.

Change one of - and note which path each takes:

| Change | Path |
|---|---|
| different hook mechanic - the cheapest axis | append to `variations` |
| different offer | append to `variations` |
| different treatment, detail, or product photo | append to `variations` |
| different angle (pain to aspiration) | **new spec** - angle is in the name |
| different format (comparison to testimonial) | **new spec** - format is in the name |

Changing one variable at a time is what makes results readable. Say that once, when offering.

---

## Reference files

- `references/ad-spec.md` - the per-ad spec file: zones, detail, copy, variations
- `references/creative-strategy.md` - goal, persona, awareness, hierarchy, the 8 hook mechanics
- `references/brief-schema.md` - the full brief, field by field
- `references/multi-reference.md` - blending, batching, and reading a swipe file
- `references/ad-formats.md` - the 12 static formats, when each wins
- `references/prompt-craft.md` - brief + brand to prompt, per model type
- `references/meta-specs.md` - sizes, safe zones, copy limits, policy
- `references/brand-lock.md` - brand profile schema
