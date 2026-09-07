# Reference Roles

When there is more than one reference, do not guess how they combine. Ask what each one is for.

Every ad is assembled from a fixed set of slots. Each slot is filled by exactly one source: a reference, the brand profile, the user's own asset, or generation. Once the slots are assigned, the ad is fully specified and there is nothing left to interpret.

## The slots

| Slot | What it decides | Usual sources |
|---|---|---|
| **Layout** | composition, where everything sits, read order | one reference, **only ever one** |
| **Format** | which of the 12 ad formats this is | follows layout unless told otherwise |
| **Product** | the thing being sold, as it appears | user's photo (best), a reference, or generated |
| **Copy** | hook pattern, slot order, what the words do | a reference, or written fresh |
| **Proof** | stars, quote, badge, stat, chart, none | a reference, or the brand's real proof |
| **Look** | lighting, background, texture, mood | a reference, or brand default |
| **Color** | palette | **always the brand profile** |
| **Type** | fonts, weight, case | **always the brand profile** |
| **Person** | model, face, hands | a reference's style, user's asset, or none |

Two are never up for assignment. **Color and type always come from the brand.** Taking those from a reference is what turns a rebuild into a knockoff - it fails on brand fidelity, and image models reject prompts carrying another brand's identity.

**Layout takes exactly one source.** Two layouts cannot merge. A comparison split plus a testimonial quote plus a stat hero is not a better ad, it is a cluttered one with no read order - and read order is the only thing a static ad really has.

## The question script

Ask only about slots that are actually open. One question per turn. Plain language - never say "slot" or "assign" to the user.

With the references on screen, in this order:

1. **Layout** - "Which of these has the layout you want? I'll build on that one's structure."
2. **Product** - "Do you have your own product photo, or should I generate the product?"
3. **Copy** - "Should the headline work like <ref 1>'s, or do you want a different angle?"
4. **Proof** - "Any reviews, ratings, or numbers you can actually back up?" (skip if no reference uses proof)
5. **Look** - "Should it feel like <ref 2>'s lighting and setting, or keep your usual style?"

Stop as soon as the ad is specified. If they say "you pick", pick and tell them what you picked in one line - do not hand the decision back twice.

Skip any slot no reference contributes to. A single reference plus a product photo needs one question, not five.

## Show the assignment before generating

Repeat it back as part of the Stage 3 plan, so a wrong assumption gets caught before anything is spent:

> "So: **layout** from the second ad - the vertical split. **Your** product photo. Headline works like the third one, denying something people assume. **Star rating** from your real reviews. Your brand's colors and type throughout.
>  Anything you want to move?"

If a slot came from a reference but conflicts with the layout's read order, say so and drop it:

> "The first ad's collage background would fight the split layout - two things competing to be looked at first. Leaving it out."

## Recording it

Keep the assignment with the output so a variant can change one slot without rebuilding:

```
layout   <- ref-02        (comparison split)
product  <- user photo    (<their product photo>)
copy     <- ref-03        (<copy pattern>)
proof    <- brand         (<verified rating and review count>)
look     <- ref-02        (<lighting and setting>)
color    <- brand
type     <- brand
```

This is also the variant mechanism: change one line, regenerate, and the result stays readable against the last one.

---

## When the set is not for one ad

Two other things a pile of references can be. Confirm which before reading anything.

### A swipe file, becoming several ads

One reference in, one ad out, repeated. This is the volume path - healthy accounts ship 12-15 statics a week across 6-8 formats.

Read all of them for format and angle first, then show one table. **Flag duplication before generating**: if five of eight are the same format, producing five near-identical ads wastes their money. Recommend the strongest one or two of that format.

Brand stays constant across the batch; only the format and angle vary. Name outputs `<format>-<angle>-v1` so results stay readable later.

### A category read, becoming no ads yet

Many ads from one category, and the question is what actually works there. Read only for format, angle, and layout convention - full briefs are wasted at this stage.

Report what recurs and what is missing:

- which formats dominate, which are absent
- what the category leads with: pain, proof, aspiration, price
- what nearly all of them do - product placement, where price sits, whether faces appear
- **the gap** - a format that performs elsewhere and nobody here runs

Convention exists because it works; the gap is where cheap attention lives. Recommend one ad on each, and say which you would spend on first.

Above roughly 20 references, read for pattern only. Nobody needs 20 briefs.
