# P10 - Description

> This file contains the workflow context, automation potential, risks, and version history for P10.
> The prompt text is in P10.md.

---

## Business Function

CRM and Loyalty (FLX Rewards)

## Trigger

A CRM data trigger fires when a member has not made a purchase in 90 or more days.

## Intended Workflow / Task

P10 generates a personalised win-back email for a lapsed FLX member. The email leads with the member's point balance or expiry risk and includes a single win-back offer to motivate a return purchase. P10 runs independently of P09 - both are triggered by separate CRM conditions.

### Position in Workflow Chain

```
CRM data trigger (Lapsed 90+ days)
|
v
P10 - Win-Back Email  <-- this prompt
```

---

## Problem Being Solved

Lapsed customers represent a significant revenue recovery opportunity that is currently underutilised at Foot Locker Australia. Re-engaging a customer who has already purchased is substantially cheaper than acquiring a new one, but win-back emails require a different approach to standard promotional sends - generic re-engagement emails accelerate unsubscribes rather than preventing them. Core pain points include:

- Win-back emails sent as generic bulk campaigns ("we miss you") that feel hollow and produce low re-engagement rates
- Point expiry not being communicated proactively, meaning members let points lapse rather than returning to redeem them
- CRM coordinators spending 20-30 minutes per win-back variant writing copy that could be templated
- No consistent single-offer structure - some win-back emails include multiple incentives that create decision fatigue

Estimated manual time per win-back email variant: 20-30 minutes.
Estimated time with P10: 5-8 minutes (input + review).

Harvard Business Review (2014, cited in Salesforce 2024) established that acquiring a new customer costs 5-25 times more than retaining an existing one. For Foot Locker Australia, a well-timed win-back email targeting lapsed FLX members with a relevant, single-offer message is one of the most cost-efficient retention investments available. Salesforce (2024) further notes that personalised re-engagement emails with loss-aversion framing (e.g. points expiry) consistently outperform generic promotional win-back sends.

---

## Automation Potential

| Dimension | Assessment |
|---|---|
| Repetitiveness | Very high - same structure, only member data and offer change |
| Data availability | All required fields exist in the CRM (name, tier, point balance, expiry date, purchase history) |
| Human judgment needed | Low - tone review and offer accuracy check only |
| Estimated time saving | ~75% (30 min manual -> ~7 min review per email variant) |

**Human-in-the-loop role:**
CRM coordinator inputs member data and win-back offer -> reviews email for tone and accuracy -> approves for send. Coordinator confirms points expiry date is accurate before approval.

**Scale potential:**
At any given time, Foot Locker Australia's FLX member base will have a significant cohort of lapsed members. P10 enables the CRM team to send personalised win-back emails at a volume that would be impossible to achieve manually. AllAboutAI (2025) reports that AI-driven personalisation in retail generates measurably higher conversion rates than generic campaigns. As the lapsed member cohort grows with the FLX program, P10 scales proportionally without additional coordinator time.

**Integration potential:**
P10 could be triggered automatically from the CRM when a member crosses the 90-day inactivity threshold, with member data pre-populated and a draft generated for one-click coordinator approval.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Incorrect point balance or expiry date sent to member | High | Coordinator validates all CRM data before inputting; point expiry dates confirmed against the member record before send |
| Win-back offer not aligned with current program terms | Medium | Offer details collected as required input; coordinator confirms against current program before approval |
| Email tone feels pushy despite low-pressure instruction | Low | Specific prohibited phrases built into output rules; coordinator reviews tone before send |
| Sending to a member who has already re-engaged | Low | CRM trigger is based on real-time inactivity data; coordinator checks member activity status before approving send |
| Spam Act non-compliance | Low | Unsubscribe mention mandatory in output rules; coordinator checks footer before send |

**Overall risk rating: LOW to MEDIUM** - the incorrect data risk is the primary concern and is mitigated by coordinator data validation before inputting.

---

## References

- AllAboutAI (2025). *AI in Retail Statistics 2025*. Retrieved from https://www.allaboutai.com/resources/ai-statistics/ai-in-retail/
- Salesforce (2024). *State of the Connected Customer*. Retrieved from https://www.salesforce.com/resources/research-reports/state-of-the-connected-customer/

---

## Version History

### v1.0 - Initial draft

**Date:** March 2025
**Prompt:**
> Write a win-back email for a Foot Locker Australia FLX member who hasn't purchased in 90 days. Their name is [NAME] and they have [POINTS] points. Include an offer to bring them back.

**Output:** Generated an email that opened with "We miss you, [NAME]" and included a generic offer without framing it as exclusive or time-limited. Point balance was mentioned but point expiry was not referenced. No subject line, no preheader, and the tone felt like a standard promotional email rather than a targeted re-engagement.
**Observed effect:** CRM coordinator rewrote the email - the "we miss you" opening and generic offer structure were not aligned with the brand voice or win-back best practice. No time saving.
**Lesson learned:** Win-back emails require specific prohibited phrases ("we miss you"), a loss-aversion framing around points expiry, a single offer only, and a subject line that earns the open on its own. All of these must be explicit prompt requirements, not implied by the persona.

---

### v2.0 - Added loss-aversion framing, prohibited phrases, single offer rule, and full structure

**Date:** March 2025
**Changes made:**
- Added senior CRM copywriter role with explicit win-back psychology knowledge and FLX program context
- Added prohibition of "we miss you", "it's been a while", and "we haven't seen you" as opening lines
- Added loss-aversion framing: if points are close to expiry, lead with that in both subject line and email body
- Added single offer rule - one incentive only, no multiple options
- Added full email structure: subject line, preheader, body sections, CTA, compliance footer
- Added word count range (100-150 words)
- Added points expiry as a key input field with explicit instruction to reference it if applicable
- Applied label suppression from the start

**Observed effect:** Output is a low-pressure, value-led win-back email that leads with the member's points status and a single clear offer. Subject line and preheader generated. Compliance footer included. Coordinator review time under 5 minutes.
**Lesson learned:** Loss aversion is more powerful than promotion in a win-back context - telling a member their points are about to expire consistently outperforms telling them about a discount. Making point expiry a primary input field and leading the email structure with it is the single most important improvement from v1.0 to v2.0.

**Live test - Lapsed member with expiring points (6 months inactive, 1,400 points expiring in 1 month):**

Output received:

> Subject line: [FIRST_NAME], 1,400 points expiring soon
> Preheader: Don't lose your points - grab 20% off your next purchase today.
>
> Hi [FIRST_NAME],
>
> You've got 1,400 FLX points waiting, and they're set to expire in just a month. Here's a simple way to put them to good use.
>
> As an FLX Member, you can enjoy 20% off your next purchase - exclusively for you. Just use your code at checkout and treat yourself to the latest drops.
>
> Check out the newest Jordan releases and New Balance styles that just landed online - your points make it even better.
>
> Hurry, your points expire in a month, and your discount code is only valid for 3 months.
>
> Redeem Your 20% Off
>
> You're receiving this email as part of Foot Locker Australia FLX Rewards. To unsubscribe, click here.

**Observed effect:** Loss-aversion framing lands correctly - points expiry leads in both the subject line and the opening body line before the offer is introduced. Single offer only (20% off), low-pressure tone throughout, product nudge references known purchase interests (Jordan, New Balance), compliance footer present. Coordinator review time under 3 minutes. Two minor issues: "Hurry" in the urgency line is a cliché phrase that should be added to the prohibited list alongside "Don't miss out" from P09. The preheader also uses "Don't lose your points" which, while effective, borders on pressure language - a future version could soften this.
**Lesson learned:** The loss-aversion framing works exactly as intended - leading with points expiry in the subject line and opening sentence creates urgency without any promotional language. The single offer rule is equally important - having one clear action (redeem 20% off) removes decision fatigue and makes the CTA unambiguous. Both "Hurry" and "Don't miss out" should be added to the prohibited phrases list across P09 and P10 in a future iteration.

---

### v3.0 - Replaced placeholders with actual input values and added cliché prohibition (current)

**Date:** March 2025
**Changes made:**
- Output rule updated: the AI now uses the actual first name and point balance from the inputs directly in the generated email - [FIRST_NAME] and [POINT_BALANCE] no longer appear as literal text in the output
- Added prohibition of urgency clichés: "Hurry", "Don't miss out", "Act now", "Limited time" as standalone phrases - urgency must be integrated naturally into the copy
- Both changes identified from the v2.0 live test output

**Observed effect:** Email output is now fully personalised with real member data and free of cliché urgency language - coordinator receives a complete, send-ready draft requiring no placeholder cleanup before send.
**Lesson learned:** The preheader "Don't lose your points" from the v2.0 test borders on pressure language despite the low-pressure instruction. A future v4.0 improvement would add a preheader tone rule: frame the loss-aversion message around the value of the points, not the fear of losing them - e.g. "Your 1,400 points are worth more than you think" rather than "Don't lose your points."

**Live test v3.0 - Silver member with expiring points (Juma, 1,600 points expiring in 2 months):**

Output received:

> Subject: Juma, your 1600 points are expiring
> Preheader: Use your points before they're gone + 20% off your next order
>
> Hi Juma,
>
> You've got 1600 FLX points ready to use, and some of them are due to expire in the next 2 months. It's a good moment to put them towards something new.
>
> As a Silver FLX member, you've also got a one-time 20% discount waiting for you. Use it on your next purchase and stack the value with your points while they're still active.
>
> Fresh apparel has just landed, with new fits and everyday staples that make it easy to update your rotation.
>
> Your 20% offer is valid until May 30, and your points won't be around much longer.
>
> Shop Now
>
> You're receiving this as part of your Foot Locker Australia FLX Rewards membership. You can unsubscribe at any time.

**Observed effect:** Real member name and point balance used directly in output - no placeholder text. Loss-aversion framing leads correctly in both subject line and opening body line before the offer is introduced. Single offer only (20% off). Low-pressure tone throughout with no cliché urgency phrases. Product nudge references a relevant category. Offer expiry date stated specifically (May 30). Compliance footer present and naturally worded. Coordinator review time under 3 minutes.
**Lesson learned:** The subject line "Juma, your 1600 points are expiring" is more effective than any promotional subject line because it is both personal and loss-aversion framed. Using the actual member name and balance in the subject line - rather than placeholders - is the single most important improvement from v2.0 to v3.0.