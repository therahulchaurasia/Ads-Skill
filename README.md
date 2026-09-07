# Ad Studio

Turn a reference ad you admire into an on-brand Meta static ad.

You give it a competitor's ad. It works out *why* that ad converts - the layout, the read order, what the copy is doing - then rebuilds that structure in your brand, writes the copy, checks Meta's specs and policy, and generates the image.

Works with any image generator. If none is connected, you get a ready-to-paste prompt instead.

---

## What it actually does

```
1  Brand   who this is for               asked once, remembered
2  Read    what the reference is doing   format, read order, zones, detail
3  Plan    your version, confirmed       nothing generates before you say yes
4  Make    copy, then prompt, then image
5  Check   size, policy, brand           pass/fix list, then the next variant
```

The rule underneath all of it: **take the structure, leave the identity.**

Layout, read order, format, copy patterns and generic devices - notches, arrows, dividers - transfer. Their logo, colours, typeface, product shape and actual sentences do not. That is not only a legal line: image models reject prompts carrying trademarks, and a near-copy loses in the auction to the ad that already owns that look.

## Why it isn't just a prompt

Most "make me an ad like this" prompts produce something plausible and generic. The parts that stop that:

- **The reference goes in as an image, the product photos alongside it.** Layout is spatial; describing it in prose loses it. A real product photo beats any model's guess at your product.
- **The detail layer.** Not just *where* the callouts sit but *how they attach* - notched pills pointing at the product, leader lines, arrows, or floating. Skip it and you get four grey rectangles hovering in space, which is what a model draws when it isn't told otherwise.
- **A policy gate that knows where the line actually is.** Meta rejects on sensitive attributes - health conditions, weight, finances. It does not reject "tired at 3pm". Over-cautious copy loses more money than the occasional rejection.
- **Source tags on every claim.** `[OBSERVED]`, `[INFERRED]`, `[ASSUMED]`. A reference ad has a stat-shaped hole in it, and rebuilding the layout creates real pull to fill that hole with a plausible number. Invented review counts get ads rejected and get found out.
- **A spec file per ad.** The ad becomes a thing you can re-run, change one field of, and diff against the last one - so "test one variable at a time" survives into next week instead of depending on what the model remembers.

## Requirements

An image generation tool connected to Claude Code - any of them. Without one the skill still runs end to end and hands you the prompt, the copy and the exact size to paste wherever you generate.

Nothing else. No API keys, no accounts, no install beyond the skill folder.

## Install

```bash
git clone https://github.com/therahulchaurasia/Ads-Skill.git ~/.claude/skills/ad-studio
```

Restart Claude Code. Other surfaces and troubleshooting in [INSTALL.md](INSTALL.md).

## Use it

Put a screenshot of an ad you like in your working folder. Two ways to start:

```
/ad-studio
```

or just say what you want, and it triggers on its own:

```
I want to make an ad like this for my brand
```

Drag the screenshot in either way. Answer its questions - one at a time, plain language, no jargon. It writes everything to `.ad-studio/` in your working folder:

```
.ad-studio/
├── brand.json      your brand, asked once
├── references/     the ads you fed it
├── products/       your product photos and logo
└── ads/            specs and finished creative, side by side
```

## Reference ads

The Meta Ad Library (`facebook.com/ads/library`) is the source. Search a brand in your category, screenshot a static ad you like. The library blocks automated fetching, so a screenshot is faster than any workaround.

Pick detail-dense references over airy ones. A product-plus-headline ad is what image models do natively - the skill adds nothing. Callouts, comparisons and annotated layouts are where it earns its keep.

## What's in the box

| File | What it holds |
|---|---|
| `SKILL.md` | the five stages, decision points, UX rules |
| `references/ad-formats.md` | the 12 static formats, when each wins, how each fails |
| `references/creative-strategy.md` | goal/persona/awareness, the 8 hook mechanics |
| `references/brief-schema.md` | what to extract from a reference, field by field |
| `references/prompt-craft.md` | brief + brand into a prompt that executes |
| `references/meta-specs.md` | sizes, safe zones, copy limits, the policy gate |
| `references/multi-reference.md` | slot assignment, swipe files, category reads |
| `references/ad-spec.md` | the per-ad spec file |
| `references/brand-lock.md` | the brand profile |

## Known limits

- **On-image text** is only reliable on GPT-Image-class models. Elsewhere the skill generates a clean plate with space reserved and hands you the copy to set in Canva or Figma.
- **4:5 (1080x1350)** is Meta's best feed size and several generators do not offer it. The skill asks for the closest available and tells you.
- **Brands with a palette per product** - a different colour per flavour or SKU - do not fit the single-palette brand profile cleanly. Give it the brand system and one SKU.
- **It cannot tell whether your reference actually performed.** Picking a good reference is your job.
