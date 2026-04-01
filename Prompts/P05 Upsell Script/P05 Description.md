# P05 - Description

> This file contains the workflow context, automation potential, risks, and version history for P05.
> The prompt text is in P05.md.

---

## Business Function

Retail Operations and Training

## Trigger

New product arrival confirmed in inventory, or a scheduled staff training or briefing event where a product needs to be introduced to the floor team.

## Intended Workflow / Task

P05 is the second step in the In-Store Experience workflow chain. Once P04 has generated the product description for the website and price card, P05 generates a staff upsell talking points script for the same product. The output is used in daily team huddles before store open, giving floor staff the language they need to confidently recommend and upsell the product to customers.

The prompt collects product and customer inputs interactively, confirms the brief, then generates a short, spoken-language talking points script with a product hook, key benefits, FLX mention, objection handling, and a closing line.

### Position in Workflow Chain

```
New product arrival / Stock inventory update
|
v
P04 - Product Description Writer
|
v
P05 - Staff Upsell Script  <-- this prompt
```

P05 can also be triggered independently for any product already on the floor that staff need refreshed talking points for.

---

## Problem Being Solved

Foot Locker Australia floor staff are the primary conversion point in-store. Their ability to communicate product value confidently and naturally directly affects sales per shift. Without prepared talking points, staff default to reciting specs from the box - which rarely converts a browsing customer into a buyer. Core pain points include:

- Staff unprepared at product launch, particularly for new arrivals or collaboration drops that require specific messaging
- Inconsistent upsell language across staff members in the same store
- No structured objection handling, meaning price resistance often ends the conversation
- FLX Rewards not consistently introduced during the sales interaction, reducing loyalty sign-ups and repeat purchase rates
- Store managers spending 20-30 minutes before each shift writing ad-hoc briefing notes that vary in quality

Estimated manual time per staff briefing script: 20-30 minutes per product.
Estimated time with P05: 5-8 minutes (input + review).

Research by McKinsey (2023, cited in PwC 2024) identifies AI-enhanced workforce tools as a key driver of retail productivity, particularly for frontline staff enablement. For Foot Locker Australia, equipping staff with consistent, benefit-led talking points at the start of every shift reduces the performance gap between experienced and new staff, and directly supports conversion rate improvement on new product arrivals.

---

## Automation Potential

| Dimension | Assessment |
|---|---|
| Repetitiveness | Very high - same structure for every new product or briefing event |
| Data availability | All required fields exist in the product inventory record and campaign brief |
| Human judgment needed | Low - tone and relevance check by store manager only |
| Estimated time saving | ~75% (30 min manual -> ~7 min review per product) |

**Human-in-the-loop role:**
Store manager inputs product details -> reviews talking points for accuracy and floor relevance -> reads aloud in team huddle or distributes as a briefing sheet. No rewriting expected once inputs are correctly entered.

**Scale potential:**
At 10 new products per month across the store network, P05 saves approximately 30-40 hours annually per store on briefing script preparation. Across a network of 100+ stores, the aggregate saving is significant - and the consistency benefit is arguably more valuable than the time saving. Morgan Stanley (2024) notes that AI tools deliver the greatest ROI in retail when applied to high-frequency, repetitive tasks that currently vary in quality across locations. Staff briefing scripts are exactly that task. As the prompt library grows, P05 outputs could also feed directly into a centralised training platform accessible to all stores simultaneously.

**Integration potential:**
P05 could be triggered automatically from the same inventory event that triggers P04, with both outputs delivered to the store manager in a single workflow. At that point, a new product arrival generates both customer-facing copy and staff-facing talking points without any manual drafting.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Fabricated product specs in talking points | High | Output rules prohibit generating specs not in the inputs; store manager validates all product claims against the physical product before the huddle |
| Talking points too formal or scripted for floor use | Medium | Prompt explicitly instructs conversational spoken language; store manager reads aloud during review to check natural flow before the huddle |
| Objection response not suited to local customer base | Low | Store manager can adjust the objection response for their specific store context before delivery |
| FLX mention framed as a sales push rather than a customer benefit | Low | Output rules explicitly require FLX to be framed as a customer benefit; manager reviews before delivery |
| Over-reliance replacing genuine product knowledge | Medium | P05 is a floor preparation tool, not a substitute for product training - staff should be encouraged to handle and try products in addition to using the talking points |

**Overall risk rating: LOW to MEDIUM** - the spec fabrication risk is the primary concern and is mitigated by the manager validation step. The over-reliance risk is structural and requires a management culture of product knowledge alongside prompt use.

---

## Version History

### v1.0 - Initial draft

**Date:** March 2025
**Prompt:**
> Write a sales script for Foot Locker Australia staff to use when selling the [BRAND] [MODEL]. The key features are [FEATURES]. Price is [PRICE].

**Output:** Generated a full dialogue-style script with staff lines and anticipated customer responses. The format was too long and too rigid for a team huddle - staff would need to memorise multiple exchanges rather than working from flexible talking points. The language was formal and scripted, not natural for a casual in-store conversation. No FLX mention, no objection handling, and no closing line.
**Observed effect:** Store manager discarded the script and wrote their own briefing notes from scratch - no time saving
**Lesson learned:** A sales script format does not work for retail floor staff. The output needs to be short talking points, not a dialogue. Language must be conversational and spoken-word appropriate. FLX, objection handling, and a closing line must all be required output elements.

---

### v2.0 - Switched to talking points format, added FLX and objection handling

**Date:** March 2025
**Changes made:**
- Changed output format from dialogue script to short talking points list
- Added explicit instruction for conversational spoken language
- Added FLX Rewards mention as a required output element, framed as a customer benefit
- Added objection handling as a required output element
- Added closing line as a required output element
- Added 120-word total output limit to keep the briefing sheet huddle-ready
- Added interactive input collection for product, benefit, price, campaign, and target customer

**Output:** Talking points were well-structured and naturally worded. FLX mention and objection response included. However, the output had section labels printed (e.g. "KEY TALKING POINTS:", "OBJECTION RESPONSE:") making it look like a form rather than a briefing sheet. Store manager spent time reformatting before the huddle.
**Observed effect:** Content quality was high - manager used the talking points with minimal changes. Editing time approximately 8 minutes, mostly removing labels.
**Lesson learned:** Label suppression must be applied - output should read as a natural briefing sheet, not a labelled form. Applied from v3.0 onwards as standard practice across the library.

---

### v3.0 - Suppressed output labels and added spec fabrication safeguard (current)

**Date:** March 2025
**Changes made:**
- Removed all output labels - prompt instructs the AI to use the structure internally but output clean copy only
- Added explicit output rule prohibiting fabrication of specs or features not provided in inputs
- Added Step 2 brief confirmation before generating to catch input errors early
- Bullet points retained for the 3 key talking points only - all other elements output as plain prose sentences

**Observed effect:** Output reads as a clean, professional briefing sheet ready to use in a huddle or distribute to staff. No formatting cleanup required. Store manager review time under 5 minutes.
**Lesson learned:** The 120-word limit is the most important constraint in this prompt - without it, the AI generates content that is too long to be absorbed in a 5-minute huddle. Word limits and spoken-language requirements together define what makes a floor tool actually usable.

**Live test - Nike SB Dunk Low x Otomo Katsuhiro (Steamboy/Akira collaboration):**

Output received:

> Catch the hype with the Nike SB Dunk Low x Otomo Katsuhiro - a standout for any sneaker or anime fan.
>
> - Inspired by Steamboy and Akira, the unique colourways and detailing make this sneaker instantly recognisable and perfect for expressing your style.
> - Premium suede, leather, and textile overlays give all-day comfort while keeping the look luxe and street-ready.
> - Raw-edged tongue and custom Hiragana branding make it a true collector's piece for anime and sneaker lovers alike.
>
> With FLX Rewards, you earn bonus points on this drop, adding extra value to your purchase. If you're thinking about it, grab it now - these collabs move fast. Want to try them on and see how they feel?

**Observed effect:** Output is clean, paste-ready, and under the 120-word limit. Product hook is strong and audience-specific. All three talking points are benefit-led and naturally worded. FLX is framed as a customer benefit, not a sales push. Objection response addresses the "I'll think about it" hesitation with urgency that feels authentic for a collaboration drop. Closing line invites action without pressure. Store manager review time under 3 minutes.
**Lesson learned:** The 120-word limit and spoken-language instruction work together effectively - the output reads exactly as it would sound in a team huddle. Providing a specific target customer type (sneaker collectors and anime fans) in the inputs significantly improves how the AI frames the talking points, making them feel relevant rather than generic.