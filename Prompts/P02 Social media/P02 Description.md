# P02 - Description

> This file contains the workflow context, automation potential, risks, and version history for P02.
> The prompt text is in P02.md.

---

## Business Function

Marketing and Promotions

## Trigger

A campaign event or promotional period confirmed by a Marketing Manager in the campaign calendar. P02 can run independently or follow P01 in the workflow chain using the same campaign brief.

## Intended Workflow / Task

P02 generates 2 Instagram caption variants for a Foot Locker Australia campaign post. The captions are ready to paste into the Instagram scheduling tool or post directly, requiring only a coordinator review before publishing.

The prompt collects campaign inputs interactively, confirms the brief, then generates 2 distinct caption variants with platform-specific format rules enforced.

### Position in Workflow Chain

```
Campaign brief confirmed by Marketing Manager
|
v
P01 - Promotional Email Copywriter
|
v
P02 - Instagram Caption Copywriter  <-- this prompt
|
v
P03 - Campaign Performance Summary
```

P02 can also be triggered independently without running P01 first.

---

## Problem Being Solved

Social media coordinators at Foot Locker Australia manually write Instagram captions for each campaign post. With multiple campaigns per month across product launches, seasonal sales, and FLX exclusives, caption writing is a frequent, repetitive task. Core pain points include:

- Captions that open too slowly and get cut off before the "more" button - losing the audience before the offer lands
- Inconsistent tone and hashtag usage across posts
- Time spent rewriting the same campaign message into social format from scratch
- Missed disclosure requirements (e.g. promotion end dates, T&Cs) on paid or promotional posts

Estimated manual time per campaign caption set: 20-30 minutes including revisions.
Estimated time with P02: 5-8 minutes (brief input + review).

---

## Automation Potential

| Dimension | Assessment |
|---|---|
| Repetitiveness | Very high - same structure, only campaign inputs change |
| Data availability | All required fields exist in the campaign brief |
| Human judgment needed | Low - tone check and disclosure review only |
| Estimated time saving | ~75% (30 min manual -> ~7 min review per campaign) |

**Human-in-the-loop role:**
Fill brief -> review 2 variants -> select preferred or blend elements -> approve for scheduling. No full rewrite expected.

**Scale potential:**
4 campaigns/month x 2 caption variants = approximately 8-10 hours saved annually on Instagram copy alone, before accounting for A/B testing or additional post formats (Stories, Reels).

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Opening line exceeds 125-character cut-off | Medium | Output rules enforce hook-first structure; coordinator checks first line length before publishing |
| Missing or incorrect disclosure language | Medium | Disclosure requirements collected as a required input field; coordinator reviews before publishing |
| Hashtags used inline rather than at end | Low | Output rules explicitly place hashtags on their own line at the end of each caption |
| Tone mismatch for the paired visual | Low | Visual type collected as an input - coordinator can override tone before approval |
| Over-reliance reducing in-house social media skill | Low | P02 is positioned as a drafting aid, not a replacement; human review retained at all times |

**Overall risk rating: LOW** - suitable for regular use with lightweight human review before publishing.

---

## Version History

### v1.0 - Initial draft

**Date:** March 2025
**Prompt:**
> You are a senior social media copywriter for Foot Locker Australia. Write 2 Instagram captions for a campaign promoting [CAMPAIGN_NAME]. The hero product is [PRODUCT]. The offer is [OFFER]. Use an energetic sneaker culture tone and include relevant hashtags.

**Output:** Two captions generated with decent brand tone and hashtags included. However, both captions opened with long sentences that exceeded the 125-character feed cut-off, meaning the hook was buried behind the "more" button. No CTA, no disclosure line, and both variants used the same opening angle - they read like rewrites of each other rather than genuinely distinct options.
**Observed effect:** Coordinator had to rewrite the opening lines of both captions and add a CTA manually - edit time approximately 20 minutes
**Lesson learned:** The prompt needs to specify the 125-character hook constraint, require a CTA, require a disclosure line, and force the two variants to use different opening angles

---

### v2.0 - Added platform constraints, CTA, disclosure, and variant angle rules

**Date:** March 2025
**Changes made:**
- Added 125-character hook constraint with instruction to land the key message before the feed cut-off
- Added CTA as a required output element
- Added disclosure line requirement for promotional campaigns
- Added rule requiring the two variants to use different opening angles
- Added interactive input collection for campaign details, visual type, tone, and hashtags

**Output:** Both variants had strong opening hooks within the character limit and used distinct angles. CTA and disclosure line present. However, no word count guidance was given for the body copy - one variant ran to 6 sentences and felt too long for a social post. Hashtags also appeared inline mid-caption rather than at the end.
**Observed effect:** Coordinator edit time reduced to approximately 8 minutes - mostly trimming body copy and moving hashtags
**Lesson learned:** Body copy needs a sentence limit and hashtags need an explicit placement rule - inline hashtags break reading flow and look unprofessional

---

### v3.0 - Added body copy limit, hashtag placement rule, and label suppression (current)

**Date:** March 2025
**Changes made:**
- Added body copy limit of 2-4 sentences per caption
- Added explicit hashtag placement rule - hashtags on their own line at the end, never inline
- Applied label suppression from the start (learned from P01) - output labels do not appear in the generated captions
- Variants separated with a single `---` line only

**Live test - Grid Street FLX Exclusive campaign:**

Output received:

> First look, first cop
> Exclusive Adidas, Skechers & Jordans are live for FLX members only. Don't wait - these Grid Street styles are built to move fast. Shop now and secure your pair before they vanish.
> T&Cs apply.
> #FootLockerAU #FLXExclusive #GridStreetDrop #SneakerHeads #StreetStyle
>
> ---
>
> Your FLX early access just dropped
> Adidas, Skechers & Jordans in Grid Street exclusives are calling your name. Tap in and grab yours before the clock runs out!
> T&Cs apply.
> #FootLockerAU #FLXExclusive #GridStreetDrop #SneakerHeads #StreetStyle

**Observed effect:** Output is paste-ready with no cleanup required. Two distinct variants with different opening angles, body copy within range, hashtags on their own line, compliance line included. The prompt also ran independently with a different campaign brief to P01, confirming P02 works standalone. Coordinator review time under 3 minutes.
**Lesson learned:** Specifying sentence limits and placement rules removes the last manual editing steps - the more precisely the output format is described, the less the coordinator has to do before publishing