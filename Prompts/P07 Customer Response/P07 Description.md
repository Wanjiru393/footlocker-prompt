# P07 - Description

> This file contains the workflow context, automation potential, risks, and version history for P07.
> The prompt text is in P07.md.

---

## Business Function

Customer Service and Support

## Trigger

P06 triage output is reviewed and approved by the handling agent. P07 runs immediately after triage for all complaint categories at any urgency level.

## Intended Workflow / Task

P07 drafts a customer response email for the handling agent to review and send. The draft is empathetic, professionally worded, legally safe, and calibrated to the urgency level assigned in P06. The agent reviews the draft, verifies factual accuracy, and approves or adjusts before sending.

### Position in Workflow Chain

```
Customer complaint received
|
v
P06 - Complaint Triage
|
v
P07 - Customer Response Draft  <-- this prompt
|
v
P08 - Escalation Summary (High urgency only)
```

---

## Problem Being Solved

Drafting customer complaint responses is one of the most time-consuming and legally sensitive tasks in a retail customer service operation. At Foot Locker Australia, agents must balance empathy with legal safety - a response that is too apologetic creates liability, while a response that is too formal damages the customer relationship. Core pain points include:

- Agents defaulting to hollow apology templates ("sorry for any inconvenience") that customers find dismissive and that fail to address the specific issue
- Inconsistent tone across agents - some too formal, some too casual - creating an inconsistent brand experience in complaint handling
- Agents inadvertently admitting liability or making promises that cannot be fulfilled, creating downstream legal risk
- High-urgency responses requiring a senior tone that junior agents struggle to achieve under time pressure
- Draft writing taking 15-25 minutes per complaint on top of triage time

Estimated manual response draft time: 15-25 minutes per complaint.
Estimated time with P07: 4-7 minutes (input + review).

According to Salesforce (2024), 72% of customers expect companies to understand their needs and expectations - a generic template response signals the opposite. AI-drafted responses that are personalised to the specific complaint and calibrated by urgency level directly address this expectation gap while protecting the business from legal exposure that can arise from poorly worded manual responses.

---

## Automation Potential

| Dimension | Assessment |
|---|---|
| Repetitiveness | High - same response structure across complaint types, only content changes |
| Data availability | All required fields come from the P06 triage output and agent knowledge |
| Human judgment needed | Medium - agent must verify factual accuracy and confirm proposed resolution before sending |
| Estimated time saving | ~70% (25 min manual -> ~7 min review per response) |

**Human-in-the-loop role:**
Agent inputs triage summary and proposed resolution -> reviews draft for accuracy and tone -> adjusts any factual details -> approves and sends. Agent retains full responsibility for the response before it leaves the team.

**Scale potential:**
At 50 complaints per month, P07 saves approximately 150-200 hours annually on response drafting. The consistency benefit is equally significant - every response follows the same legal-safe structure regardless of which agent handles it, eliminating the risk of a junior agent inadvertently creating liability. PwC (2024) identifies AI-enhanced frontline productivity as a key driver of retail cost reduction, and customer service response drafting is one of the highest-frequency, highest-risk tasks in that category.

**Integration potential:**
P07 could be integrated with the email platform so that the approved draft is populated directly into the reply window against the customer's original complaint, removing the copy-paste step and reducing the chance of sending the wrong draft to the wrong customer.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Draft admits liability or makes unconfirmed promises | High | Output rules explicitly prohibit liability language and unconfirmed promises; agent reviews all factual claims before sending |
| Hollow apology language used despite prohibition | Medium | Specific prohibited phrases listed in output rules; agent flags and replaces before sending |
| Draft tone not matched to urgency level | Medium | Tone calibration rules are explicit in the prompt by urgency level; agent adjusts if default tone is not appropriate |
| Response sent without agent review | High | P07 is explicitly positioned as a draft for review - workflow requires agent approval before send; this must be enforced at the team management level |
| Customer's specific concern not addressed in the draft | Low | Step 2 confirmation requires agent to confirm complaint summary before generating - agent checks draft against the original complaint before sending |

**Overall risk rating: MEDIUM to HIGH** - the two High risks (liability language and sending without review) are process risks as much as prompt risks. Both require team management enforcement of the review step as a non-negotiable workflow requirement.

---

## References

- PwC (2024). *AI-Powered Retail Reinvention: Why Now Is the Time*. Retrieved from https://www.pwc.com/gx/en/services/alliances/microsoft/ai-retail-transformation-future.html
- Salesforce (2024). *State of the Connected Customer*. Retrieved from https://www.salesforce.com/resources/research-reports/state-of-the-connected-customer/

---

## Version History

### v1.0 - Initial draft

**Date:** March 2025
**Prompt:**
> Write a customer service response email for Foot Locker Australia. The customer complained about [ISSUE]. Reply professionally and empathetically.

**Output:** Generated a polite, generic response that opened with "We are sorry for any inconvenience caused" and closed with "Please do not hesitate to contact us." No specific acknowledgement of the customer's issue, no proposed resolution, no next step. Tone was consistent across all complaint types regardless of urgency - a legal threat complaint received the same response structure as a minor delivery query.
**Observed effect:** Agent discarded the draft and wrote their own response - the generic output was less useful than starting from scratch because it still needed to be read and assessed before being rejected.
**Lesson learned:** The prompt needs explicit prohibition of hollow apology phrases, a required next step, tone calibration by urgency level, and a specific resolution as a mandatory input - without a proposed resolution the AI has nothing to work with beyond platitudes.

---

### v2.0 - Added tone calibration, prohibited phrases, and resolution requirement

**Date:** March 2025
**Changes made:**
- Added senior customer service agent role with explicit knowledge of ACL, legal-safe language, and complaint response best practice
- Added explicit prohibition of hollow apology phrases with specific examples
- Added tone calibration by urgency level (Low / Medium / High)
- Added proposed resolution as a required input field
- Added word count range (80-150 words) to prevent over-long responses
- Added interactive input collection replacing single-field prompt

**Output:** Response tone was appropriately calibrated by urgency. Hollow apology phrases absent. However, the output had section labels visible in the draft (e.g. "ACKNOWLEDGEMENT:", "RESOLUTION:") and the closing line defaulted to "Please do not hesitate to contact us" - a phrase explicitly listed in the output rules as overused.
**Observed effect:** Agent editing time reduced to approximately 8 minutes - mostly removing labels and rewriting the closing line.
**Lesson learned:** Label suppression must be explicit. Prohibited phrases must also be prohibited in the closing line specifically - the AI defaulted to the most common closing phrase in customer service writing despite the general prohibition.

---

### v3.0 - Suppressed labels, tightened prohibited phrases, added no-liability rule (current)

**Date:** March 2025
**Changes made:**
- Removed all output labels - prompt instructs the AI to use the structure internally but output a clean email only
- Added explicit prohibition of "Please do not hesitate to contact us" in the closing line specifically
- Added explicit no-liability-admission rule as a standalone output rule, not just implied in the persona
- Added Step 2 brief confirmation before generating
- Added instruction: if urgency is High, the response must include a direct commitment to escalation or senior review

**Observed effect:** Output is a clean, legally safe, empathetic response draft ready for agent review. Tone is correctly calibrated by urgency. No labels, no hollow phrases, no liability language. Agent review time under 5 minutes.
**Lesson learned:** Legal safety rules must be stated as explicit output constraints, not left to the persona description - the AI needs to be told directly what not to say, not just told to be "legally safe"

**Live test - Incorrect order (Medium urgency):**

Output received:

> Hi Jane,
>
> Thank you for reaching out. We understand that you received a Nike Air Force 1 in size 9 instead of the Jordan 1 Retro High OG in Black/White size 11 that you ordered. We appreciate you bringing this to our attention and understand how receiving the wrong item can be frustrating.
>
> Our team is currently reviewing your order and arranging the correct replacement. We will confirm the replacement dispatch within the next 3 business days and provide you with tracking details once it's on its way.
>
> We appreciate your patience while we resolve this matter and are committed to ensuring you receive the correct item promptly.
>
> Kind regards,
> Foot Locker Australia Customer Service team

**Observed effect:** Response is empathetic without admitting fault, contains a specific next step with a 3-business-day timeframe, and closes professionally without hollow phrases. No liability language present. Word count within range. Agent review time under 3 minutes.
**Lesson learned:** Medium urgency tone is correctly calibrated - response feels attentive and efficient without the elevated urgency of a High-level complaint. The proposed resolution input (replacement + prepaid return label) was correctly reflected in the output, confirming that the resolution field is the most important input for generating a useful draft.