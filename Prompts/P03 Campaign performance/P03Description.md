# P03 - Description

> This file contains the workflow context, automation potential, risks, and version history for P03.
> The prompt text is in P03.md.

---

## Business Function

Marketing and Promotions

## Trigger

Campaign end date passes and final performance data is available from email platform, Instagram analytics, and sales reporting tools.

## Intended Workflow / Task

P03 is the final step in the Marketing and Promotions workflow chain. Once a campaign concludes and the Marketing Coordinator has pulled the performance data, P03 generates a structured post-campaign summary ready for the Marketing Manager to review and present to leadership.

The prompt collects all campaign metrics interactively, confirms the inputs, then generates a polished performance report with channel analysis, outcomes, and recommendations.

### Position in Workflow Chain

```
Campaign brief confirmed by Marketing Manager
|
v
P01 - Promotional Email Copywriter
|
v
P02 - Instagram Caption Copywriter
|
v
P03 - Campaign Performance Summary  <-- this prompt
```

---

## Problem Being Solved

Marketing coordinators at Foot Locker Australia spend significant time compiling and writing post-campaign reports after each promotion. With multiple campaigns per month, this is a recurring task that often gets deprioritised or delivered inconsistently. Core pain points include:

- Reports written in inconsistent formats across coordinators - making it hard for leadership to compare campaigns over time
- Raw metrics reported without business context - a 3.2% CTR means nothing to a Marketing Manager without a benchmark
- Recommendations section often absent or vague - reports describe what happened but do not advise what to do next
- Report writing delayed by 3-5 days post-campaign while coordinators manage the next brief

Estimated manual time per campaign report: 60-90 minutes.
Estimated time with P03: 10-15 minutes (data input + review).

---

## Automation Potential

| Dimension | Assessment |
|---|---|
| Repetitiveness | Very high - same structure after every campaign |
| Data availability | All metrics exist in email platform, Instagram analytics, and sales reports |
| Human judgment needed | Medium - coordinator must validate benchmark comparisons and recommendations |
| Estimated time saving | ~80% (90 min manual -> ~15 min review per campaign) |

**Human-in-the-loop role:**
Pull data from platforms -> input into prompt -> review generated summary -> approve or adjust recommendations -> share with Marketing Manager.

**Scale potential:**
4 campaigns/month = approximately 30-40 hours saved annually on report writing, with the added benefit of consistent formatting that enables quarter-on-quarter campaign comparison.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Benchmark figures may be outdated or inapplicable | Medium | Coordinator reviews all benchmark comparisons before sharing with leadership; prompt instructs AI to use only provided figures |
| Fabricated metrics if inputs are incomplete | High | Output rules explicitly instruct AI to note "not tracked this campaign" rather than estimate missing data; coordinator validates all figures before input |
| Recommendations not suited to business context | Medium | Recommendations reviewed by Marketing Manager before actioning; P03 is an advisory tool, not a decision-making tool |
| Report used without human review in time-pressured situations | Medium | Report is positioned as a draft for coordinator review, not a final document - sign-off step retained in workflow |
| Consistent format may create over-reliance on template thinking | Low | Marketing Manager retains discretion to request additional analysis or override recommendations |

**Overall risk rating: MEDIUM** - suitable for regular use but requires coordinator validation of all metrics and benchmark references before the report is shared with leadership.

---

## Version History

### v1.0 - Initial draft

**Date:** March 2025
**Prompt:**
> You are a marketing analyst for Foot Locker Australia. Write a post-campaign performance summary for [CAMPAIGN_NAME]. The campaign ran from [START_DATE] to [END_DATE]. Here are the results: [PASTE METRICS HERE].

**Output:** Generated a readable summary with the metrics restated in paragraph form. However, the report listed raw numbers without translating them into business meaning - it read like a data dump rather than an analysis. No benchmarks referenced, no "what worked / what to improve" structure, no recommended next step. Leadership would not be able to act on it without significant rewriting.
**Observed effect:** Marketing Manager had to rewrite the analysis and recommendations sections entirely - no meaningful time saving on the highest-value parts of the report
**Lesson learned:** Pasting metrics in bulk produces a summary, not an analysis. The prompt needs to collect metrics by channel, instruct the AI to contextualise figures against benchmarks, require a structured what worked / what to improve section, and end with a single clear recommendation

---

### v2.0 - Added channel structure, benchmark framing, and recommendations (current)

**Date:** March 2025
**Changes made:**
- Replaced bulk metric paste with structured per-channel input collection (email, Instagram, overall)
- Added explicit instruction to translate raw metrics into business language with benchmark comparisons
- Added "what worked" and "what to improve" sections with requirement for evidence-based, actionable observations
- Added "recommended next step" as a required output element
- Added word count range (250-350 words) to keep the report concise for leadership
- Applied label suppression from the start - output reads as a polished document with no visible section headers
- Added explicit rule: if a metric was not provided, note it as "not tracked" rather than estimate or omit

**Observed effect:** Output reads as a professional post-campaign report ready for leadership review. Coordinator edit time reduced to under 10 minutes, primarily to validate benchmark references and adjust any recommendations that do not reflect internal strategic priorities.
**Lesson learned:** Structuring the input collection by channel mirrors how the coordinator actually pulls data - one platform at a time - which reduces input errors and produces more accurate channel-level analysis in the output

**Live test - Sole Position collaboration drop (April 3 - July 29):**

Output received:

> The Sole Position collaboration drop ran from April 3rd to July 29th across email, Instagram, and in-store channels, aiming to drive sales and increase FLX sign-ups for future promotional engagement. The campaign leveraged direct email communication, social media visibility, and physical retail presence to maximise reach and conversions.
>
> Email performance was exceptionally strong, with a 62% open rate and a 75% click-through rate, both well above industry benchmarks, demonstrating highly relevant messaging to our audience. The 58% conversion rate indicates that email drove meaningful purchases, directly contributing to the campaign's sales objectives. A mid-campaign dip in open rates highlights an opportunity to test timing and subject lines for sustained engagement.
>
> On Instagram, the campaign reached 400,000 users with 330,000 impressions and generated 350,000 profile visits. While engagement rate was not tracked, the high volume of profile visits indicates strong audience interest and effective content resonance. Notably, the second caption outperformed the first, suggesting message optimisation can enhance future social media performance.
>
> In-store activity contributed to overall campaign outcomes, helping achieve 500 units sold. Combined with 250 new FLX sign-ups, the campaign successfully advanced both revenue and loyalty program growth, meeting the primary objectives.
>
## What worked:
> - Email content and targeting drove exceptional open, click, and conversion rates.
> - Second Instagram caption resonated more strongly, showing value in iterative testing.
> - Multi-channel approach effectively converted interest into both sales and new FLX sign-ups.
>
## What to improve:
> - Monitor email open-rate trends and optimise subject lines and send times mid-campaign.
> - Track Instagram engagement rate consistently to better quantify social impact.
> - Consider additional in-store promotions to further support FLX sign-ups.
>
## Recommended next step: 
Leverage the insights from the high-performing email content and Instagram caption to plan upcoming campaigns, ensuring sustained multi-channel engagement and maximising both sales and loyalty growth.

**Observed effect:** Output is a complete, leadership-ready report with no labels, no raw data dumps, and benchmark-contextualised analysis across all three channels. The untracked engagement rate was correctly flagged as "not tracked" rather than fabricated. Coordinator review time under 10 minutes, primarily to validate benchmark references. Report is ready to present upward with minimal editing.
**Lesson learned:** Collecting metrics per channel rather than as a bulk paste produces genuinely structured analysis - the AI mirrors the input structure in the output, so well-organised inputs produce well-organised reports.