# Meta Specs and Policy Gate

Checked before anything ships. Current for 2026.

## Sizes

| Placement | Ratio | Pixels | Note |
|---|---|---|---|
| Feed (Facebook + Instagram) | **4:5** | **1080 x 1350** | Meta's own recommendation and the default. Take it unless there is a reason not to. |
| Feed, square | 1:1 | 1080 x 1080 | Supported, safe, universally generated. Loses about a third of the mobile screen versus 4:5 and consistently underperforms it. |
| Stories and Reels | 9:16 | 1080 x 1920 | Heavy UI overlay - see safe zones. |
| Landscape | 1.91:1 | 1200 x 628 | Right-column and some placements only. Rarely the right choice for paid social in 2026. |

One creative at 4:5 covers feed placements well. Make a separate 9:16 for Stories and Reels rather than letting Meta crop the 4:5 - automatic crops put copy under the UI.

## Safe zones

Where the platform draws its own interface on top of the creative.

**Stories and Reels (unified since March 2026):**
- Top 14% (about 250px of 1080 x 1920) - profile icon, account name, metadata
- Bottom 35% - caption, CTA button, engagement icons
- 6% each side

Keep headlines, logos, prices, and CTAs out of both. Background imagery may extend through; nothing that must be read may.

**Feed (4:5 and 1:1): no UI over the creative at all.** The profile name renders above the image and the CTA below it. Nothing is covered. Do not reserve margins here - big type running to the edge is normal feed creative. Padding is a design choice, not a requirement.

**One asset across all placements** (Advantage+ / "use for all placements") gets reframed into 9:16, and that crop eats the edges. Either design the 4:5 knowing it will be cropped, or supply a separate 9:16. Separate is better.

## Copy limits

| Field | Limit | Reality |
|---|---|---|
| Primary text | 125 characters | Truncates with "See more" beyond roughly 125 on mobile. Front-load the hook. |
| Headline | about 27 characters | Truncates hard. Short and concrete. |
| Description | about 27 characters | Often not rendered at all depending on placement. Never put anything essential here. |
| Reels overlay text | 72 characters | Shorter than you think. |
| CTA button | fixed list | Chosen from Meta's set, not written. |

## File

- **JPG** for photographic creative, **PNG** for text-heavy or flat-color creative
- Under 30 MB
- The old 20% text rule is gone as a hard limit. Heavy text still tends to underperform, so treat it as a design guideline rather than a rule.

## Policy gate

Check the copy and the image before generating where possible, and again before shipping. These are the common rejections, in rough order of frequency.

**Personal attributes.** Ads may not imply knowledge of a **sensitive** personal characteristic: health and mental health conditions, weight and body, sexual health or orientation, race, ethnicity, religion, financial hardship, criminal history.

- Rejected: "Your acne is caused by this." / "Struggling with your weight?" / "Behind on payments?"
- Fine: "Acne is often caused by this." / "A routine for acne-prone skin."

The fix is to move from asserting to describing.

**This rule does not cover ordinary experience.** "Tired at 3pm?", "Coffee making you jittery?", "Runners:" are not personal attributes - they are experiences and interests, not private information. Live ads run second-person copy of that kind constantly and are approved.

Apply the test before flagging: **would the viewer consider this private information about themselves?** If not, leave the copy alone. Over-flagging produces bland copy, which loses reliably, while a rejection is edited and resubmitted the same day.

**Health and body.** No implication that the viewer's body is inadequate, no idealized body imagery pushed as an outcome, no promises of specific results.

- Rejected: "Lose 10kg in 30 days." / close-up before-and-after of a body.
- Fine: "A programme built around slow, steady change."

**Before and after.** The riskiest format on the platform. Restricted outright for weight loss and heavily scrutinised for skin, hair, and cosmetic categories. Where it is allowed, the before must not be framed as shameful and the after must not be presented as a typical or guaranteed outcome. When in doubt, use process shots rather than outcome shots.

**Unverifiable claims and superlatives.** "#1", "the best", "guaranteed", "clinically proven" without a citable study. Statistics used as the creative hero must be defensible - see the Data/Stat Callout format.

**Named competitors.** Comparison ads must compare against a category, not an identifiable brand. "Ordinary vitamin C serums" is fine; naming the competitor is a legal and platform problem.

**Regulated categories** carry extra rules: financial products, supplements, health services, alcohol, dating, and anything targeting minors. If the brand is in one of these, their own banned-claims list in the brand profile outranks anything here.

## Pre-ship checklist

Run all six. Report as pass or fix, one line each.

1. Correct pixel dimensions for the intended placement
2. Nothing essential inside a safe zone
3. Smallest text still legible at phone size
4. Copy within character limits, hook in the first 125 characters
5. Nothing on the policy list above, nothing on the brand's banned-claims list
6. Brand colors, voice, and logo usage correct
