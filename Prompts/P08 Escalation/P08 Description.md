# P08 - Description

> This file contains the workflow context, automation potential, risks, and version history for P08.
> The prompt text is in P08.md.

---

## Business Function

Customer Service and Support

## Trigger

P06 triage output assigns urgency level of High. P08 runs only for High-urgency complaints, in parallel with or immediately after P07.

## Intended Workflow / Task

P08 generates an internal escalation summary addressed to the relevant senior manager or department head. The summary gives management the facts, risk assessment, and a recommended action in under 200 words, enabling fast decision-making without requiring them to read the full complaint thread.

### Position in Workflow Chain

```
Customer complaint received
|
v
P06 - Complaint Triage
|
v
P07 - Customer Response Draft
|
v
P08 - Escalation Summary (High urgency only)  <-- this prompt
```

---

## Problem Being Solved

High-urgency complaints at Foot Locker Australia - those involving legal threats, safety issues, or significant reputational risk - require senior management visibility and fast decision-making. Currently, customer service agents forward full email threads to managers, who must read through potentially lengthy back-and-forth exchanges to understand the situation and assess the risk. Core pain points include:

- Managers spending 20-30 minutes reading complaint threads before they can decide on an action
- Risk assessment inconsistent across agents - legal exposure or ACL implications not always flagged clearly
- Escalation summaries written in inconsistent formats, making it hard for managers to compare cases or identify patterns
- Delay between complaint receipt and management visibility, particularly outside business hours

Estimated manual escalation summary time: 20-30 minutes per High-urgency complaint.
Estimated time with P08: 4-6 minutes (input + review).

PwC (2024) identifies AI-assisted management reporting as a key enabler of faster retail decision-making, noting that reducing the time between incident and management awareness is a direct operational risk mitigation. For Foot Locker Australia, a consistent, structured escalation summary ensures that no high-risk complaint goes unreviewed at the appropriate level.

---

## Automation Potential

| Dimension | Assessment |
|---|---|
| Repetitiveness | High - same structure for every High-urgency escalation |
| Data availability | All required fields come from the P06 triage output and agent knowledge |
| Human judgment needed | Medium - agent must validate risk assessment and confirm recommended action |
| Estimated time saving | ~80% (30 min manual -> ~6 min review per escalation) |

**Human-in-the-loop role:**
Agent inputs triage details and any additional case context -> reviews escalation summary for factual accuracy and risk completeness -> forwards to the named addressee. Agent remains responsible for the accuracy of the summary before it reaches management.

**Scale potential:**
P08 applies only to High-urgency complaints, which represent a subset of total complaint volume. Even at 10 High-urgency complaints per month, P08 saves approximately 30-40 hours annually on escalation summary writing. More importantly, the consistent structured format enables management to review escalations faster and build a reliable record of high-risk cases for compliance and legal review purposes. Shopify (2025) notes that AI's greatest retail value often lies in tasks that are both time-sensitive and high-stakes - escalation summaries are exactly that.

**Integration potential:**
P08 could be triggered automatically when P06 assigns High urgency, generating the escalation summary and routing it to the relevant manager's inbox without manual intervention. At that point the agent's role is limited to reviewing the summary before it is forwarded.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| ACL exposure not flagged in risk assessment | High | Output rules require explicit ACL flagging for product defect and quality complaints; agent reviews risk assessment before forwarding |
| Escalation signals omitted from risk assessment | High | Output rules require all escalation signals (legal, media, social media) to appear explicitly in the risk assessment section |
| Summary forwarded to wrong addressee | Medium | Addressee is collected as a required input and confirmed in Step 2; agent verifies before forwarding |
| Summary forwarded without agent review | High | P08 is positioned as a draft requiring agent review - this must be enforced at team management level |
| Recommended action is too vague or lacks a timeframe | Low | Output rules require a specific timeframe in the recommended action; agent adjusts if the suggested timeframe is not operationally achievable |

**Overall risk rating: HIGH** - P08 is an internal management document with direct influence on business decisions and potential legal proceedings. Agent review before forwarding is non-negotiable and must be treated as a hard process requirement, not a guideline.

---

## References

- PwC (2024). *AI-Powered Retail Reinvention: Why Now Is the Time*. Retrieved from https://www.pwc.com/gx/en/services/alliances/microsoft/ai-retail-transformation-future.html
- Shopify (2025). *AI in Retail: Use Cases and Implementation Guide*. Retrieved from https://www.shopify.com/enterprise/blog/ai-in-retail

---

## Version History

### v1.0 - Initial draft

**Date:** March 2025
**Prompt:**
> Summarise this customer complaint for management. The complaint is: [PASTE COMPLAINT]. Urgency is High. Suggest what we should do.

**Output:** Generated a 3-4 sentence paragraph summarising the complaint in neutral language. No risk assessment, no ACL flagging, no escalation signal identification, no timeframe on the recommended action. The summary read like a complaint description rather than a management briefing - it told management what happened but not why it mattered or what to do about it.
**Observed effect:** Manager read the summary and immediately asked the agent for more context - the summary created an additional back-and-forth rather than enabling a decision.
**Lesson learned:** A management escalation summary is not a complaint description - it is a risk and action document. The prompt needs an explicit risk assessment section, ACL flagging, escalation signal identification, a specific recommended action with a timeframe, and a defined word count that forces brevity.

---

### v2.0 - Added risk assessment, ACL flagging, and structured format

**Date:** March 2025
**Changes made:**
- Added senior customer service specialist role with explicit knowledge of ACL, management communication, and escalation requirements
- Added risk assessment as a required section with ACL flagging instruction
- Added explicit requirement to identify escalation signals in the risk assessment
- Added recommended action with required timeframe
- Added 150-200 word count range to enforce management-appropriate brevity
- Added interactive input collection replacing single paste field

**Output:** Risk assessment was present and correctly identified ACL exposure for a product defect case. Escalation signal was flagged. However, section labels were visible in the output (e.g. "INCIDENT SUMMARY:", "RISK ASSESSMENT:") making it look like a form rather than a professional briefing document. Recommended action timeframe was present but vague ("as soon as possible").
**Observed effect:** Manager was able to make a decision from the summary without requesting additional context. Agent editing time approximately 10 minutes - mostly removing labels and specifying the timeframe.
**Lesson learned:** Label suppression must be applied from the start. "As soon as possible" is not an acceptable timeframe - the output rules must require a specific timeframe (e.g. "within 24 hours") not a relative one.

---

### v3.0 - Suppressed labels, required specific timeframe, added forwarding safeguard (current)

**Date:** March 2025
**Changes made:**
- Removed all output labels - summary reads as a professional briefing document from first line to last
- Required specific timeframe in recommended action (e.g. "within 24 hours", "by end of business today") - relative timeframes prohibited
- Added explicit positioning: P08 is an internal document only - output rules prohibit customer-facing language or tone
- Added Step 2 brief confirmation before generating
- Reinforced that ACL exposure and escalation signals must appear explicitly in the risk assessment, not implied

**Observed effect:** Output is a clean, management-ready escalation brief that enables a decision without additional context. Risk assessment correctly flags ACL exposure and escalation signals. Recommended action includes a specific timeframe. Agent review time under 5 minutes.
**Lesson learned:** Management documents require a different writing discipline to customer-facing documents - the output rules must explicitly prohibit empathetic or customer-facing language, not just assume the persona will enforce the right tone. Internal and external documents need separate output rule sets.

**Live test - Delayed express delivery with legal and social media escalation (High urgency):**

Output received:

> To: Head of Logistics - Escalation: Delayed Express Delivery of Nike Air Max 270s - Ref 27659786
>
> Maverick Samuels placed an order for Nike Air Max 270s on 24 March with express delivery, which was expected within 2 business days. As of 1 April, the order has not been received. The customer contacted Foot Locker Australia twice by phone regarding the delay and was promised follow-up on both occasions, which has not occurred.
>
> The complaint presents reputational risk due to the customer's intention to escalate to Consumer Affairs Victoria, post publicly on social media, and leave a negative Google review. There is potential ACL exposure as the consumer paid for express delivery and has not received the product or a timely remedy, which may constitute a failure to deliver goods within the agreed timeframe.
>
> Customer service has initiated follow-ups with delivery channels to determine the cause of the delay.
>
> It is recommended that logistics urgently confirm the status of the shipment and provide an update to the customer, including arranging immediate delivery or refund where appropriate, by end of business today to mitigate legal and reputational risk.
>
> Customer Service Team - 1 April 2026

**Observed effect:** Output is a clean, management-ready escalation brief. Addressee line correctly formatted. Incident summary is factual and neutral. Risk assessment explicitly flags ACL exposure and all three escalation signals (Consumer Affairs, social media, Google review). Actions taken section reflects the follow-up initiated. Recommended action includes a specific timeframe (end of business today). No customer-facing language or tone present. Agent review time under 4 minutes.
**Lesson learned:** The ACL flagging instruction is the most valuable addition in this prompt - without it, a generic escalation summary would describe the complaint without identifying the legal exposure, leaving management to make that assessment themselves. Making ACL flagging a required output element ensures it is never missed regardless of which agent runs the prompt.