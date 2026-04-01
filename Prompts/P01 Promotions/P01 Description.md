# P01 - Description

> This file contains the workflow context, automation potential, risks, and version history for P01.
> The prompt text is in P01.md.


## Business Function

Marketing and Promotions

## Trigger

A campaign event or promotional period confirmed by a Marketing Manager in the campaign calendar.

## Intended Workflow / Task

P01 is the first step in the Marketing and Promotions workflow chain. Once a campaign brief is confirmed, P01 generates a complete promotional email ready for coordinator review and send via the email platform.

The prompt collects campaign inputs interactively, confirms the brief, then generates a subject line, preheader, and full email body with format constraints enforced.

### Position in Workflow Chain

```
Campaign brief confirmed by Marketing Manager
|
v
P01 - Promotional Email Copywriter  <-- this prompt
|
v
P02 - Instagram Caption Copywriter
|
v
P03 - Campaign Performance Summary
```

## Problem Being Solved

Marketing coordinators at Foot Locker Australia spend significant time manually drafting promotional emails for each campaign. With frequent campaigns across a retail chain (seasonal sales, product launches, FLX exclusives), this compounds quickly. Core pain points include:

- Inconsistent tone and brand voice across campaigns
- Missed compliance notes (e.g. exclusions, unsubscribe language)
- Slow turnaround when campaigns are confirmed at short notice
- Time spent rewriting the same brief into email format from scratch

Estimated manual time per campaign email: 45-60 minutes.
Estimated time with P01: 5-7 minutes (brief input + review).

This aligns with broader industry evidence: in retail and e-commerce, personalised and well-structured emails deliver up to 41% higher click-through rates compared to generic ones (Opensend, 2025), and AI-assisted content consistently improves CTR and message relevance at scale (HubSpot, 2025). 
For a lean marketing team running 4+ campaigns per month, the compounding cost of manual drafting is a direct operational risk.


## Automation Potential

| Dimension | Assessment |
|---|---|
| Repetitiveness | Very high - same structure, only inputs change per campaign |
| Data availability | All required fields exist in the campaign brief |
| Human judgment needed | Low - tone check and compliance review only |
| Estimated time saving | ~80% (60 min manual -> ~10 min review per campaign email) |

**Human-in-the-loop role:**
Fill brief -> review output -> minor edits -> approve for send. No full rewrite expected at this stage.

**Scale potential:**
4 campaigns/month = approximately 15-20 hours saved annually on email drafting alone, before accounting for A/B subject line testing or localisation across states.

 This is consistent with Morgan Stanley's analysis (2024) that AI automation can bring efficiency to up to 70% of routine marketing tasks in retail, and with Shopify's finding (2025) that 94% of retailers using AI have seen measurable reductions in operating costs. 
 As Foot Locker Australia's campaign frequency grows or localisation across states is introduced, the time saving scales proportionally without additional headcount.

## Integration potential:
This prompt could eventually be triggered directly from a campaign management system, with brief fields pre-populated from the campaign calendar, reducing manual input time further. At that stage, the human role shifts entirely to review and approval.


## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Hallucination of product details or offer terms | Medium | Human review mandatory before send; all product and offer details are collected as explicit inputs - the AI does not generate them independently |
| False urgency or unverifiable stock claims | Medium | Output rules explicitly prohibit unverifiable stock claims; compliance notes are collected as a required input field |
| Australian Consumer Law breach (misleading conduct) | Medium | Coordinator reviews all urgency and offer language before approval; exclusion notes captured in Step 1 inputs |
| Tone mismatch during sensitive periods | Low | Campaign type input flags the context; coordinator can override tone before approval |
| Over-reliance reducing in-house copywriting skill | Low | P01 is positioned as a drafting aid, not a replacement; human review is retained at all times |

**Overall risk rating: LOW** - suitable for regular use with lightweight human review before send.

## References
Opensend (2025). Email Click-Through Rate Statistics for eCommerce Stores. Retrieved from https://www.opensend.com/post/email-click-through-rate-ecommerce
Shopify (2025). AI in Retail: Use Cases and Implementation Guide. Retrieved from https://www.shopify.com/enterprise/blog/ai-in-retail

## Version History

### v1.0 - Initial draft

**Date:** 27th/March 2025
**Prompt:**
> Draft a promotional email for Foot Locker Australia, to attract customers and convince them to buy products. We'll be running a promotion with Formula One 2026 for a chance to win tickets for the Monaco Grand Prix which will be happening on June 7th. The promotion will be valid for all Jordans and Nikes.

**Output:** Generated a single one-off email for the F1 campaign. No structure, no subject line, no compliance language, no reusable format. Output was campaign-specific and could not be reused for other promotions.
**Observed effect:** Required a full rewrite by the marketing coordinator - no meaningful time saving
**Lesson learned:** A one-off campaign brief is not a reusable prompt. Need a role, input structure, format constraints, and output template to work across all campaigns


### v2.0 - Added role, input collection, and output structure

**Date:** 27th/March 2025
**Changes made:**
- Added senior copywriter role with Foot Locker Australia brand context, FLX loyalty knowledge, and compliance awareness
- Added 12-question interactive input collection (one at a time) to capture all campaign variables
- Added Step 2 brief confirmation before generating
- Added 7-part email body structure (headline, opening, product/offer, FLX callout, urgency, CTA, footer)
- Added 3 subject line options with distinct angle instructions
- Email body word count capped at 120-180 words
- Australian English and compliance exclusions added to output rules

**Live test - F1 x Foot Locker Australia (Monaco Grand Prix campaign):**
- Campaign type: Collaboration drop
- Hero products: Jordan, Nike, New Balance
- Offer: Purchase entry for chance to win Monaco Grand Prix tickets (June 7)
- Campaign dates: April 3 - July 29

**Output sample:**
> Subject line option 1: Step into the Monaco Grand Prix
> Headline: Your chance to hit the F1 track in style
> CTA: Claim Your Monaco Entry

**Observed effect:** All 7 email sections generated correctly. Estimated coordinator edit time: 3-5 minutes.
**Lesson learned:** Output section labels (e.g. "SUBJECT LINE", "PREHEADER", "HEADLINE") were printing in the output - coordinator still needed to manually remove them before the email was paste-ready


### v3.0 - Suppressed output labels for paste-ready email (current)

**Date:** 31st/March 2025
**Changes made:**
- Removed all output section labels from the generated email - prompt now instructs the AI to use the structure internally but not print labels in the output
- Output now reads as a real email from top to bottom, ready to paste into an email platform with no cleanup required
- CTA and footer appear as natural copy, not labelled fields

**Live test - F1 x Foot Locker Australia (Monaco Grand Prix campaign):**

Output received:

> Sole Position: your VIP pass awaits
> Score exclusive Jordan, Nike & New Balance drops
> Win big with your kicks
>
> Get ready to own the streets and the track. Foot Locker Australia is bringing the heat with our Sole Position collab, merging sneaker culture with the thrill of Formula 1. This is your chance to stand out with the latest drops from Jordan, Nike, and New Balance, curated for true fans.
>
> Every pair you cop gives you a shot at scoring Formula 1 Grand Prix Monaco tickets. Rock the latest colourways, flex your style, and maybe even catch the race live - this isn't just a drop, it's an experience. Only purchases of eligible shoes count, so make your move on the sneakers you've been eyeing.
>
> FLX members, your early access gives you the first chance to claim these exclusive kicks and step closer to the Monaco weekend.
>
> Campaign runs until July 29th, so your window to enter won't last forever.
>
> Limited tickets
>
> Offer valid on purchases of Jordan, Nike, and New Balance shoes only. Exclusions apply. Foot Locker Australia reserves the right to modify or cancel the promotion. Unsubscribe anytime.

**Observed effect:** Output is a complete, paste-ready email with no labels, no cleanup required. Brand voice is on point, FLX callout included, compliance footer present. Coordinator edit time under 2 minutes.
**Lesson learned:** Telling the AI what structure to follow and telling it not to label that structure are two separate instructions - both are needed for production-ready output