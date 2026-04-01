# P09 - Description

> This file contains the workflow context, automation potential, risks, and version history for P09.
> The prompt text is in P09.md.

---

## Business Function

CRM and Loyalty (FLX Rewards)

## Trigger

A CRM data trigger fires when a member reaches a defined point threshold or is within a set distance of their next FLX tier level.

## Intended Workflow / Task

P09 generates a personalised FLX loyalty reward offer email for a member who is close to their next tier. The email is drafted by the CRM coordinator, reviewed, and sent via the email platform. P09 runs independently of P10 - both are triggered by separate CRM conditions.

### Position in Workflow Chain

```
CRM data trigger (Points threshold reached)
|
v
P09 - FLX Loyalty Reward Offer Email  <-- this prompt
```

---

## Problem Being Solved

Foot Locker Australia's FLX Rewards program has a large member base across four tiers. Manually writing personalised tier-progress emails for each member at scale is not feasible - without automation, these emails either do not get sent or are sent as generic bulk communications that lack the personal relevance needed to drive action. Core pain points include:

- Generic loyalty emails ("you're almost at the next level") that do not state the exact points gap, reducing urgency and click-through
- Offer language that feels promotional rather than celebratory, undermining the perceived value of the loyalty program
- CRM coordinators spending 20-30 minutes per email variant writing personalised copy that could be templated
- Inconsistent tone across loyalty communications, making the FLX program feel less premium than it should

Estimated manual time per loyalty email variant: 20-30 minutes.
Estimated time with P09: 5-8 minutes (input + review).

Loyalty program engagement is directly linked to repeat purchase rates. Salesforce (2024) reports that personalised emails deliver significantly higher transaction rates than generic sends, and that customers who engage with loyalty communications spend more per visit. For Foot Locker Australia, a well-executed tier-progress email at the right moment is one of the lowest-cost, highest-return retention tools available.

---

## Automation Potential

| Dimension | Assessment |
|---|---|
| Repetitiveness | Very high - same structure, only member data changes |
| Data availability | All required fields exist in the CRM (name, tier, point balance, purchase history) |
| Human judgment needed | Low - tone review and offer accuracy check only |
| Estimated time saving | ~75% (30 min manual -> ~7 min review per email variant) |

**Human-in-the-loop role:**
CRM coordinator inputs member data -> reviews email for tone and offer accuracy -> approves for send. No rewriting expected.

**Scale potential:**
At scale, P09 could generate personalised tier-progress emails for hundreds of members per week as CRM triggers fire. AllAboutAI (2025) reports that AI adoption in marketing automation has reached 48.9% among eCommerce professionals, with personalisation identified as the highest-value use case. As the FLX member base grows, P09's structured input approach allows the same quality of personalised communication to be maintained at any volume without additional coordinator time.

**Integration potential:**
P09 could be connected directly to the CRM so that when a member crosses a points threshold, the email inputs are pre-populated automatically and a draft is generated for coordinator review and one-click approval.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Incorrect point balance or tier data sent to member | High | Coordinator validates all CRM data against the member record before inputting; output reviewed before send |
| Offer terms not aligned with current FLX program rules | Medium | Offer details collected as a required input; coordinator confirms against current program terms before approval |
| Email tone feels generic despite personalisation placeholders | Low | Specificity rules built into prompt - exact points gap and tier benefit required in inputs; coordinator reviews tone before send |
| Spam Act non-compliance | Low | Unsubscribe mention mandatory in output rules; coordinator checks footer before send |
| Over-communication fatiguing the member | Low | P09 is triggered by CRM data conditions, not sent on a fixed schedule - coordinator reviews send frequency before approval |

**Overall risk rating: LOW to MEDIUM** - the incorrect data risk is the primary concern and is fully mitigated by the coordinator data validation step before inputting.

---

## References

- AllAboutAI (2025). *AI in Retail Statistics 2025*. Retrieved from https://www.allaboutai.com/resources/ai-statistics/ai-in-retail/
- Salesforce (2024). *State of the Connected Customer*. Retrieved from https://www.salesforce.com/resources/research-reports/state-of-the-connected-customer/

---

## Version History

### v1.0 - Initial draft

**Date:** March 2025
**Prompt:**
> Write a loyalty email for a Foot Locker Australia FLX member. They are a [TIER] member with [POINTS] points. Tell them they are close to the next tier and include an offer.

**Output:** Generated a generic loyalty email that referenced the tier and points in passing but did not state the exact gap to the next tier or name the specific benefit they would unlock. The offer was included but not framed as exclusive to their membership status - it read like a standard promotional email with a points mention added. No subject line, no preheader, no compliance footer.
**Observed effect:** CRM coordinator rewrote the email entirely - the output was not usable as a draft. No time saving.
**Lesson learned:** The exact points gap and the specific next-tier benefit must be required inputs, not implied from the tier name. The offer must be explicitly framed as exclusive to the member's status. Subject line, preheader, and compliance footer must all be required output elements from the start.

---

### v2.0 - Added specificity requirements, full email structure, and compliance rules

**Date:** March 2025
**Changes made:**
- Added senior CRM copywriter role with explicit FLX program knowledge and loyalty email best practice
- Added points-to-next-tier as a required input with instruction to state the exact gap in the email body
- Added next-tier benefit as a required input so the email names what the member will unlock
- Added offer framing instruction: exclusive to membership status, not generic promotional language
- Added full email structure: subject line, preheader, body sections, CTA, compliance footer
- Added word count range (100-150 words) to keep the email focused
- Added prohibition of generic loyalty phrases
- Applied label suppression from the start

**Observed effect:** Output is a personalised, specificity-led loyalty email ready for coordinator review. Subject line and preheader generated. Compliance footer included. Coordinator review time under 5 minutes.
**Lesson learned:** Loyalty emails require a different writing philosophy to promotional emails - the member is being recognised, not sold to. Making this distinction explicit in the persona and output rules is what separates a useful loyalty email from a promotional email with a points mention bolted on.

**Live test - Gold member approaching VIP tier (Norah, 1,200 points to VIP):**

Output received:

> Subject: Just 1,200 points to VIP, Norah!
> Preheader: Earn double points on your next purchase and reach VIP faster.
>
> Hi Norah,
>
> You're only 1,200 points away from reaching VIP - the tier that unlocks exclusive early access to drops, bonus points events, and more. Every purchase now brings you closer to these top-tier perks.
>
> As a Gold member, you can earn double points on your next purchase - a reward designed to get you to VIP faster. This offer is yours for the next three months, so there's plenty of time to make it count.
>
> Check out our latest running shoes, handpicked to help you rack up points while stepping up your game.
>
> Don't miss out - this double points offer expires in 3 months.
>
> Shop now to earn more points
>
> You're receiving this email because you're a member of Foot Locker Australia FLX Rewards. If you'd like to unsubscribe, click here.

**Observed effect:** Output is personalised, specificity-led, and framed correctly as a member recognition email rather than a promotional send. Exact points gap stated in the opening line, next tier benefit named, offer framed as exclusive to Gold status, product nudge references the member's known interest in running shoes, compliance footer present. Coordinator review time under 3 minutes. One minor issue: the urgency line opened with "Don't miss out" - a cliché phrase the output rules should explicitly prohibit in a future version alongside the existing generic loyalty phrase restrictions.
**Lesson learned:** The specificity rule is the most impactful instruction in this prompt - stating the exact points gap (1,200) and naming the specific VIP benefit (early access to drops, bonus points events) in the opening line makes the email feel genuinely personal rather than templated. Adding "Don't miss out" to the prohibited phrases list in v3.0 would complete the tone refinement.

---

### v3.0 - Replaced placeholders with actual input values and added cliché prohibition (current)

**Date:** March 2025
**Changes made:**
- Output rule updated: the AI now uses the actual first name and point balance from the inputs directly in the generated email - [FIRST_NAME] and [POINT_BALANCE] no longer appear as literal text in the output
- Added prohibition of urgency clichés: "Don't miss out", "Hurry", "Act now", "Limited time" as standalone phrases - urgency must be integrated naturally into the copy
- Both changes identified from the v2.0 live test output

**Observed effect:** Email output is now fully personalised with real member data and free of cliché urgency language - coordinator receives a complete, send-ready draft with no placeholder cleanup required.
**Lesson learned:** Collecting inputs and then outputting placeholders defeats the purpose of interactive input collection. If the AI has the value, it should use it. This applies across the entire library - any prompt that collects a name, number, or date should use that value directly in the output, not defer to a placeholder.

**Live test v3.0 - Silver member approaching Gold tier (Jim, 1,500 points to Gold):**

Output received:

> Subject: Jim, just 1,500 points to Gold!
> Preheader: Earn double points on your next purchase and step up to Gold
>
> Hi Jim,
>
> You're only 1,500 points away from reaching Gold and unlocking exclusive early access to new drops and bonus points events. Your next level is within reach!
>
> To celebrate your progress, we're giving you double points on your next purchase. This reward is just for you as a Silver member, so every step brings you closer to those Gold perks.
>
> Check out the latest Jordans and see which pair can help you rack up points faster.
>
> This offer expires in 2 months, so make sure to take advantage while it lasts.
>
> Claim Your Offer
>
> You're receiving this email as a member of Foot Locker Australia FLX Rewards. If you'd like to unsubscribe, click here.

**Observed effect:** Real member name used throughout, exact points gap stated in opening line, Gold tier benefit named specifically, offer framed as exclusive to Silver status. No [FIRST_NAME] or [POINT_BALANCE] placeholder text in output. No cliché urgency phrases. Urgency integrated naturally into the copy ("make sure to take advantage while it lasts"). Product nudge references known interest in Jordan. Compliance footer present. Coordinator review time under 3 minutes.
**Lesson learned:** Using actual input values instead of placeholders makes the email feel genuinely personalised rather than templated. The coordinator receives a send-ready draft with no cleanup required - this is the most significant usability improvement across the entire v1.0 to v3.0 progression.