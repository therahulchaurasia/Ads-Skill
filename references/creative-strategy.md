# Creative Strategy - Three Layers

What to decide before touching a reference, and what makes the result land. Three layers, in order. Skipping layer 1 is how you end up with a well-made ad nobody needed.

---

## Layer 1 - Decide, in this order

Four decisions. Each constrains the next, so order matters.

**1. Pick a specific goal.** Not "more sales". First purchase from a cold audience, reactivating lapsed buyers, moving a specific SKU, defending against a competitor's launch. The goal decides everything downstream, and a vague goal produces a vague ad.

**2. Pick your persona.** One person, not a demographic bracket. What they already believe, what they have already tried, what they would object to. Each distinct persona gets its own creative - one ad addressed to everyone is addressed to no one.

**3. Pick a format.** One of the 12 in `ad-formats.md`.

**4. Match it to an awareness level.**

| Awareness | They know | Formats that fit |
|---|---|---|
| Unaware | nothing, not even the problem | stat callout, meme, grid, lo-fi |
| Problem-aware | the pain, not the solution | before/after, lo-fi, UGC-native, listicle |
| Solution-aware | the category, not you | comparison, listicle, feature callout, testimonial |
| Product-aware | you, not yet convinced | testimonial, feature callout, product hero |
| Most-aware | everything, need a reason now | offer/promo, product hero |

The mismatch to watch for: **a product-aware format sent to a cold audience.** A clean product hero to someone who has never heard of the category is invisible. Cold traffic needs the problem named before the product appears.

### Where this meets the reference

A reference ad carries its own goal, persona and awareness level baked in. Those were somebody else's decisions, for somebody else's brand.

So run layer 1 **first**, then check the reference against it. If the reference is a most-aware offer ad and the goal is cold acquisition, the layout is still usable but the copy and angle are not. Say so rather than rebuilding a mismatch faithfully.

---

## Layer 2 - Design

Two rules, and the second one settles most arguments.

**1. Visual hierarchy.** One dominant element, then a deliberate second and third. The eye should have an order to follow. Two elements competing for first place means neither wins, and the ad reads as noise at thumb size.

**2. Clarity beats creativity.** When a clever execution and a legible one conflict, the legible one wins. An ad is looked at for well under a second, at phone size, next to content the viewer actually chose to see. Cleverness that costs a beat of comprehension costs the whole ad.

This is the tiebreaker whenever an idea is defended on the grounds that it is interesting.

---

## Layer 3 - Hook mechanics

Eight ways to make the first line work. Pick one deliberately - and note that several sit near Meta's policy edges, so the safe phrasing matters as much as the mechanic.

**1. Be specific.** `be-specific` Concrete beats impressive. "[their real review count] five-star reviews" over "loved by thousands"; "[their real shipping time]" over "fast shipping". Specificity reads as true because vagueness is what people say when they have nothing. Every figure must be the brand's own and verified - a specific number that is invented is the worst of both worlds.

**2. Lead with a number.** `lead-with-number` Put the figure first, where the eye lands. Works because a number is processed faster than a sentence. Pairs with the stat-callout format. The number must be defensible - unverifiable stats get rejected and disbelieved.

**3. Call out the audience by name.** `call-out-audience` Powerful, and worth getting precise about, because the usual advice here is wrong in both directions.

Meta's personal attributes rule bites on **sensitive** characteristics, not on any use of "you":

| Risk | Territory | Example |
|---|---|---|
| **Real** | health conditions, mental health, weight and body, sexual health or orientation, race, religion, financial hardship, criminal record | "Struggling with depression?" / "Your hair is thinning" / "Behind on payments?" |
| **Low** | ordinary experiences, habits, interests, activities | "Runners:" / "Tired at 3pm?" / "Coffee making you jittery?" |

The test: **would the viewer consider this private information about themselves?** An afternoon energy crash is not private - everybody has one and nobody hides it. A skin condition is.

Live ads run second-person copy about mundane experiences constantly and are approved. Do not sanitize those. Over-cautious copy is reliably weak, and weak copy costs more than an occasional rejection - a rejection is editable and resubmitted, a bland ad just quietly loses.

Where the territory really is sensitive, the fix is to move from asserting to describing: "Are you depressed?" becomes "Depression counselling - learn more." Same audience reached, no claim about the viewer.

**4. Lean into the taboo.** `taboo` Say the thing the category avoids saying. Works because everyone else is being polite and polite is invisible. Constrained in health, body, and financial categories - the taboo can be named without implying it applies to the viewer.

**5. Tap a primal desire.** `primal-desire` Status, belonging, safety, attraction, ease, control. Underneath a feature there is usually one of these, and naming it directly outperforms naming the feature.

**6. Open a curiosity loop.** `curiosity-loop` Withhold the resolution so the click is the only way to close it. One rule: **it must actually pay off on the landing page.** An unpaid loop converts once and poisons the account.

**7. Lean into negative marketing.** `negative-marketing` What it is not, what to stop doing, the mistake being made. Reliably outperforms positive framing because a problem is more urgent than an aspiration. Compare against the **category**, never a named competitor - "ordinary vitamin C serums", not the brand.

**8. Show the transformation.** `transformation` The end state made concrete. Strongest mechanic and the riskiest format on the platform - restricted outright for weight loss, heavily scrutinised for skin, hair and cosmetics. Where allowed: the before is treated with empathy, never shame, and the after is never framed as typical or guaranteed. Process shots are the safer version of the same idea.

### Slugs

The backticked slug after each name is the canonical value for `hook_mechanic` in the spec. Use it verbatim - invented variants break the diffability the spec exists for.

### As a variant axis

The eight mechanics are the cheapest way to generate readable variants. Hold the layout, product and brand fixed, change only the hook. Eight ads, one variable, and the result tells you something about the audience rather than about the design.

---

## The order in one line

Goal, persona, format, awareness - then hierarchy and clarity - then the hook. Decisions first, design second, words last, and never the reverse.
