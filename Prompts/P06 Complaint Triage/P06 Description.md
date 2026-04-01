# P06 - Description

> This file contains the workflow context, automation potential, risks, and version history for P06.
> The prompt text is in P06.md.

---

## Business Function

Customer Service and Support

## Trigger

A customer complaint or inquiry is received via email, web form, or social media.

## Intended Workflow / Task

P06 is the first step in the Customer Service and Complaints workflow chain. Every incoming complaint passes through P06 before any response is drafted. It categorises the complaint, assigns urgency, identifies the responsible team, and outputs a structured JSON triage record ready to log in the customer service platform.

### Position in Workflow Chain

```
Customer complaint received
|
v
P06 - Complaint Triage  <-- this prompt
|
v
P07 - Customer Response Draft
|
v
P08 - Escalation Summary (High urgency only)
```

---

## Problem Being Solved

Without a consistent triage process, complaints are routed inconsistently, urgency is assessed subjectively, and high-risk cases can be missed until they escalate. Core pain points include:

- Agents spending 10-15 minutes per complaint categorising and routing before any response work begins
- High-urgency complaints involving legal threats or safety issues not identified and escalated promptly
- Triage data logged in inconsistent formats, making complaint trend analysis impossible
- Junior agents lacking experience to correctly assess urgency for complaints with legal or reputational implications

Estimated manual triage time: 10-15 minutes per complaint.
Estimated time with P06: 2-4 minutes (input + review).

IBM (cited in AllAboutAI, 2025) reports a 30% reduction in customer service costs for retailers using AI-assisted triage tools. For a team handling high complaint volumes across multiple channels, reducing triage time by 80% per complaint directly improves response speed and agent capacity.

---

## Automation Potential

| Dimension | Assessment |
|---|---|
| Repetitiveness | Very high - same triage structure for every complaint |
| Data availability | All fields come directly from the complaint text and intake form |
| Human judgment needed | Low to Medium - agent reviews urgency before logging |
| Estimated time saving | ~75% (15 min manual -> ~4 min review per complaint) |

**Human-in-the-loop role:**
Agent pastes complaint -> reviews JSON output -> confirms urgency -> logs to platform. Agent retains override authority on urgency if additional context is known.

**Scale potential:**
At 50 complaints per month, P06 saves approximately 100-125 hours annually on triage. Beyond time saving, consistent JSON output enables complaint trend analysis - identifying which categories are growing and whether urgency levels are tracking upward. Morgan Stanley (2024) identifies data-driven operational intelligence as one of the highest-value outputs of AI adoption in retail.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Incorrect urgency on high-risk complaints | High | Explicit priority-ordered urgency rules in prompt; agent reviews and retains override authority |
| Complaint category misclassification | Medium | Three clearly defined categories with routing specified; agent confirms before logging |
| Sensitive customer data included beyond what is needed | Medium | Output rules restrict PII to reference number or name only |
| Agent skips reading the full complaint | Medium | Step 2 confirmation requires agent to review summary before generating |

**Overall risk rating: MEDIUM** - urgency misclassification is the critical failure mode and requires agent review as a non-negotiable step before any triage output is logged.

---

## References

- AllAboutAI (2025). *AI in Retail Statistics 2025*. Retrieved from https://www.allaboutai.com/resources/ai-statistics/ai-in-retail/
- Morgan Stanley (2024). *Retail Technology Trends: AI & Automation Lead Industry Growth*. Retrieved from https://www.morganstanley.com/ideas/retail-technology-trends-2024

---

## Version History

### v1.0 - Initial draft

**Date:** March 2025
**Prompt:**
> Read this customer complaint and tell me: what is the issue, how urgent is it, and who should handle it? Complaint: [PASTE COMPLAINT HERE]

**Output:** A paragraph summarising the complaint with a vague urgency suggestion. No defined categories, no JSON structure, no routing logic, no urgency criteria. Output format varied significantly depending on the complaint text.
**Observed effect:** Agent still had to manually categorise, assign urgency, and create the case record - no time saving.
**Lesson learned:** Triage output must be structured data, not prose. The prompt needs defined categories, explicit urgency rules, a JSON schema, and routing logic.

---

### v2.0 - Added JSON schema, categories, urgency rules, and routing

**Date:** March 2025
**Changes made:**
- Defined three complaint categories with responsible team routing
- Added explicit urgency assignment rules with priority ordering
- Added JSON output schema with all required fields
- Added urgency_reason field requiring the AI to cite the specific signal used
- Added interactive input collection

**Output:** JSON correctly structured and consistently formatted. However, a complaint mentioning "posting this on Instagram" was assigned Medium rather than High - social media escalation was not explicitly covered in the urgency rules.
**Observed effect:** One urgency misclassification identified during agent review - caught before logging.
**Lesson learned:** Urgency rules must explicitly cover social media escalation signals, not just legal threats.

---

### v3.0 - Added social media escalation signal and repeat contact flag (current)

**Date:** March 2025
**Changes made:**
- Added social media escalation explicitly to the High urgency rule
- Added repeat_contact field to the JSON schema
- Added Step 2 brief confirmation before generating
- Clarified that urgency rules apply in strict priority order

**Live test - Delivery failure with legal and social media escalation (1 April 2025):**

Output received:

> {
>   "reference": "Johnson Sakaja, ref no. 10003456",
>   "received": "24th March",
>   "channel": "web form",
>   "category": "Delivery Failure",
>   "urgency": "High",
>   "urgency_reason": "Complaint mentions social media and legal escalation, and involves a missed time-sensitive event.",
>   "responsible_team": "Logistics",
>   "repeat_contact": "no",
>   "complaint_summary": "Customer ordered Nike Air Max 270s with express delivery for 24 March, expected within 2 business days, but has not received the order 8 days later. Customer needed the shoes for a birthday on 29 March, contacted support twice without resolution, and threatens to escalate via Consumer Affairs Victoria, Google review, and Instagram. Seeks full refund including delivery fee.",
>   "recommended_action": "Escalate immediately to the Logistics team for urgent resolution and process full refund including delivery fee."
> }

**Observed effect:** JSON clean and correctly formatted. Urgency correctly assigned as High with all three escalation signals identified. Two input entry errors caught during agent review: received date showed the order date instead of the complaint date, and repeat_contact showed "no" despite the complaint mentioning two prior calls.
**Lesson learned:** Input field labels need clarifying examples to prevent agents entering the wrong value under time pressure - e.g. "date you received the complaint, not the order date." The repeat_contact question should prompt the agent to check the complaint text before answering.