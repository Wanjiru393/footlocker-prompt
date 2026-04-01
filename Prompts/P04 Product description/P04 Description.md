# P04 - Description

> This file contains the workflow context, automation potential, risks, and version history for P04.
> The prompt text is in P04.md.

---

## Business Function

Retail Operations and Training

## Trigger

New product arrival confirmed in the inventory system or stock management platform.

## Intended Workflow / Task

P04 is the first step in the In-Store Experience workflow chain. As soon as new stock is confirmed in inventory, P04 generates a product description ready for the website listing and a condensed version for the digital price card in-store. Both outputs are produced in a single prompt run.

The prompt collects product inputs interactively, confirms the details, then generates two format-specific descriptions with benefit-led language and SEO requirements enforced.

### Position in Workflow Chain

```
New product arrival / Stock inventory update
|
v
P04 - Product Description Writer  <-- this prompt
|
v
P05 - Staff Upsell Script
```

---

## Problem Being Solved

When new stock arrives at Foot Locker Australia, product descriptions for the website and digital price cards must be written before the product can be listed or displayed on the floor. This task currently falls to store managers or marketing coordinators who are simultaneously managing stock intake, staff allocation, and customer floor time. Core pain points include:

- Descriptions written under time pressure that lead with specs rather than benefits, reducing conversion on the website
- Inconsistent language between the website listing and the in-store price card, undermining brand consistency
- Delays in listing new products online because description writing is deprioritised during high-volume intake periods
- Staff spending time writing copy they are not trained for, taking them away from sales floor activity

Estimated manual time per product description set: 30-45 minutes.
Estimated time with P04: 6-10 minutes (input + review).

This addresses a well-documented retail challenge. OpenText (2025) notes that generative AI is actively reducing friction in the retail content pipeline by automating product descriptions and marketing copy, directly improving speed-to-floor and conversion rates. For Foot Locker Australia, faster listings mean less revenue lost to the window between stock arrival and product going live online.

---

## Automation Potential

| Dimension | Assessment |
|---|---|
| Repetitiveness | Very high - same structure for every new product arrival |
| Data availability | All required fields exist in the product inventory record |
| Human judgment needed | Low - benefit translation and tone review only |
| Estimated time saving | ~80% (45 min manual -> ~8 min review per product) |

**Human-in-the-loop role:**
Input confirmed product specs -> review website and price card copy for accuracy and tone -> approve for upload and print. No rewriting expected once specs are correctly entered.

**Scale potential:**
Foot Locker Australia receives new stock across multiple brands and models weekly. At a conservative estimate of 10 new product descriptions per month, P04 saves approximately 50-60 hours annually on description writing alone. Shopify (2025) reports that 94% of retailers using AI have seen reduced operating costs, and AI adoption in marketing automation among eCommerce professionals has reached 48.9% (AllAboutAI, 2025). As catalogue size grows or seasonal drops increase, P04's structured input approach allows consistent, benefit-led copy to be produced at scale without proportional increases in staff time.

**Integration potential:**
P04 could be connected directly to the inventory management system so that when a new SKU is confirmed, the product fields pre-populate the prompt inputs automatically. At that stage the human role shifts entirely to reviewing and approving the generated copy before it goes live.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Fabricated product specs if inputs are incomplete or incorrect | High | Output rules explicitly prohibit generating specs not provided in inputs; staff must validate all product details against the physical product or supplier sheet before running the prompt |
| Benefit language that misrepresents the product | Medium | Human review mandatory before copy goes live; coordinator cross-checks claims against confirmed specs |
| SEO requirements not met for website listing | Low | Output rules require brand name and model name in the first sentence; coordinator checks before uploading |
| Price card copy too long for physical display constraints | Low | Output rules enforce 25-35 word limit; coordinator adjusts if display template requires shorter copy |
| Over-reliance reducing staff copywriting capability | Low | P04 is a drafting tool, not a replacement for product knowledge - staff still need to understand the product to review and approve the output |

**Overall risk rating: LOW to MEDIUM** - the High fabrication risk is mitigated by the input validation step, but staff must treat spec accuracy as a non-negotiable checkpoint before approving copy for publication.

---

## References

- AllAboutAI (2025). *AI in Retail Statistics 2025: The $14.49B Market Transforming Global Commerce*. Retrieved from https://www.allaboutai.com/resources/ai-statistics/ai-in-retail/
- OpenText (2025). *From Experiments to Expected: How AI is Fundamentally Reshaping the Retail Industry in 2025*. Retrieved from https://blogs.opentext.com/from-experiments-to-expected-how-ai-is-fundamentally-reshaping-the-retail-industry-in-2025/
- Shopify (2025). *AI in Retail: Use Cases and Implementation Guide*. Retrieved from https://www.shopify.com/enterprise/blog/ai-in-retail

---

## Version History

### v1.0 - Initial draft

**Date:** March 2025
**Prompt:**
> Write a product description for the [BRAND] [MODEL] in [COLOURWAY]. It has [FEATURES]. Price is [PRICE]. Make it sound exciting for a Foot Locker Australia customer.

**Output:** Generated a description that led with the product name and listed features in order, reading more like a spec sheet than a sales tool. The price card version was not generated separately - the coordinator had to manually cut the website copy down. No benefit-led language, no SEO structure in the opening sentence, and the tone was generic retail rather than sneaker-culture specific.
**Observed effect:** Copy required significant rewriting before it could be used - both the website listing and the price card had to be redrafted manually. Approximately 25 minutes of editing per product.
**Lesson learned:** The prompt needs an explicit persona with product copywriting expertise, a clear instruction to lead with customer benefits not features, separate word count targets for each output format, and SEO requirements stated explicitly for the website version

---

### v2.0 - Added role, benefit-led instruction, and dual format outputs

**Date:** March 2025
**Changes made:**
- Added senior retail copywriter role with explicit knowledge of benefit-led language, SEO requirements, and Australian English
- Added instruction to translate features into customer benefits throughout
- Added separate word count targets: 80-120 words for website, 25-35 words for price card
- Added SEO rule: brand name and model name in the first sentence of the website copy
- Added interactive input collection for brand, model, colourway, features, benefit, price, and campaign context

**Output:** Website copy was benefit-led and SEO-structured. Price card was appropriately condensed. However, both outputs were labelled in the response (e.g. "WEBSITE DESCRIPTION:", "PRICE CARD:") meaning the coordinator still had to remove the labels before copying into the upload template.
**Observed effect:** Editing time reduced to approximately 5 minutes - mostly removing output labels and minor tone adjustments
**Lesson learned:** Label suppression must be explicit - the prompt needs to instruct the AI to use the format structure internally but not print section headers in the output

---

### v3.0 - Suppressed output labels and added spec fabrication safeguard (current)

**Date:** March 2025
**Changes made:**
- Removed all output labels - prompt instructs the AI to use the dual-format structure internally but output clean copy only
- Outputs separated with a single `---` line only
- Added explicit output rule prohibiting fabrication of specs or features not provided in the inputs
- Added superlative restriction to prevent unsubstantiated claims
- Added Step 2 brief confirmation before generating to catch input errors before a full output is produced

**Observed effect:** Output is paste-ready for both the website upload template and the price card print template. No labels, no fabricated specs, benefit-led throughout. Coordinator review time under 5 minutes.
**Lesson learned:** The spec fabrication risk is the most serious failure mode for a product description prompt - a single incorrect spec published on the website creates a customer trust issue and potential consumer law exposure. Making this an explicit output rule, not just an implied expectation, is essential

**Live test - Jordan 4 Retro Cactus Jack (University Blue):**

Output received:

> Step up your streetwear game with the Jordan 4 Retro Cactus Jack from Nike, designed for all-day comfort and street-ready style. The premium University Blue Durabuck upper feels soft to the touch, while the mismatched "Cactus Jack" and Jumpman branding on the heels and unique inner tongue graphics make every step a statement. Black lace cages, a red sock liner, and light blue speckled accents bring eye-catching detail to the wings and heel panel, complemented by a black, white, and blue midsole with visible red Air cushioning in the heel. This University Blue colourway is perfect for collectors and style enthusiasts alike, retailing at $279.
>
> ---
>
> Experience street-ready style and comfort with the Jordan 4 Retro Cactus Jack, featuring a premium Durabuck upper and visible Air cushioning in a standout University Blue colourway, retailing at $279.

**Observed effect:** Website description is benefit-led, opens with brand and model name for SEO, includes colourway and price naturally, and closes with a style and collector positioning statement. Price card is clean, standalone, and within the 25-35 word limit. No labels, no fabricated specs beyond what was provided in inputs. Coordinator review time under 3 minutes.
**Lesson learned:** The benefit-led instruction works most effectively when the input provides both the feature and the intended benefit - where only a feature was given, the AI translated it well, but prompting staff to think in "feature -> benefit" terms when filling inputs will further improve output quality in future use