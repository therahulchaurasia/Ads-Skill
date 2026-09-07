# Regression Tests

Run after any meaningful edit to the skill. Each case is a fresh session, a real reference ad, and one thing being checked.

These are the behaviours that were broken at some point and got fixed. If one regresses, it will regress silently - the ad will still come out, it will just be worse in a way that is easy to miss.

**Stop each case at Stage 3 unless the case says otherwise.** No generation needed to check most of this, and it costs nothing.

Not in `references/` deliberately: this file names brands and carries example copy, and anything the skill loads can leak into a prompt.

---

## 1. Detail layer

**Setup.** A reference whose callouts attach to the product with a visible device - notched pills, curved arrows, leader lines. Supplement and skincare ads are full of these.

**Ask.** "Make an ad like this for my brand."

**Pass.** By Stage 2 it has named the attachment type and what it points at. Not just "four callouts around the product" but "notched pills, each aimed at a different point on the bottle."

**Fail.** Describes only position. The output will come back as plain rectangles floating in space, which is what a model draws when nothing tells it otherwise. This was broken once and is the single most likely thing to regress.

---

## 2. Invented numbers

**Setup.** A reference containing a stat or review count. A brand profile with no rating recorded.

**Pass.** It asks for the real number, or leaves the row out and says so.

**Fail.** Any specific figure appears that you did not supply. A reference ad has a stat-shaped hole in it and rebuilding the layout creates real pull to fill it.

---

## 3. Awareness mismatch

**Setup.** An offer-led reference - "25% OFF, ENDS TONIGHT". Tell it the goal is cold acquisition.

**Pass.** It says the layout is usable but the offer angle is not, and leads with a problem instead.

**Fail.** Rebuilds the discount headline faithfully for an audience that has never heard of the brand.

---

## 4. Policy calibration - both directions

**Setup A.** Copy along the lines of "Tired at 3pm?" or "Coffee making you jittery?"
**Pass A.** Left alone. Ordinary experience, not a personal attribute. Live ads run this constantly.
**Fail A.** Flagged and rewritten into something limp. Over-flagging is the failure mode here - a skill that cries wolf twice gets ignored.

**Setup B.** Copy along the lines of "Struggling with your weight?" or "Behind on payments?"
**Pass B.** Flagged, with a describing-not-asserting rewrite offered.
**Fail B.** Passes it through.

Both halves must pass. Either one alone means the rule is miscalibrated rather than working.

---

## 5. Slot assignment

**Setup.** Two references with clearly different layouts.

**Pass.** Asks which one gives the layout. Names what it is taking from the other. Explicitly drops anything that would fight the chosen layout, and says why.

**Fail.** Merges both, or picks silently.

---

## 6. Product fidelity

**Setup.** Two or three photos of a real product. Run this one through generation.

**Pass.** The output product matches the photos - label, proportions, colours.

**Fail.** A plausible generic version of the product. Means the photos were not passed as images 2+.

---

## 7. Spec file

**Setup.** Any run, taken through Stage 3 approval.

**Pass.** `.ad-studio/ads/<name>.json` exists. Two levels deep, no folder per ad.

Then ask for a second version:

- **different hook or offer** -> appends to `variations` in the same file, `what_changed` filled in
- **different angle or format** -> new file, `derived_from` pointing back

**Fail.** Re-interviews you about brand or layout. Everything it needs is in the spec it already wrote.

---

## 8. Stale brand

**Setup.** A folder with an existing `brand.json` from a different brand.

**Pass.** Names the brand it loaded in one line, so a wrong one is obvious immediately.

**Fail.** Silently inherits the old name and palette. Produces an ad that looks right and is for the wrong company.

---

## 9. No generator

**Setup.** A session with no image tool connected.

**Pass.** Runs end to end and writes a prompt pack next to where the image would have gone.

**Fail.** Stops, or leaves you with nothing.

---

## 10. Example leakage

**Setup.** Any completed run.

**Check.** Does any colour, number, headline or product detail in the output appear verbatim in the skill's own files?

```bash
grep -rE "#[0-9A-Fa-f]{6}" SKILL.md references/*.md
```

Should return nothing. This has happened before: an example palette in `prompt-craft.md` and a second one in `brand-lock.md` both reached real generated ads. Any concrete value added to those files is a candidate to leak, so illustrate the shape and never a fillable value.

---

## When `plugin eval` becomes available

These cases map straight onto it. `claude plugin eval init --bare <name>` scaffolds the format, and the ablation arm gives you a with-versus-without score rather than a judgement call.

Watch the cost: `--runs` defaults to 3 per case and ablation doubles it, so an unqualified run is 6 executions per case. Start with `--runs 1` and `--max-cost-usd`.
