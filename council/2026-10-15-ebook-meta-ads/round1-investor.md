## Investor — Round 1

**Unit economics** (one front-end sale, US$, US buyer)

| Item | Value | Tag / source |
|---|---|---|
| E-book price | $17 (low $9 / high $27) | [Assumption]. The brief sets no price. |
| Platform + card fees (Payhip free plan 5% + Stripe 2.9% + $0.30) | $0.85 + $0.49 + $0.30 = $1.64 | [Fact] [fungies.io](https://fungies.io/sellfy-vs-payhip-vs-gumroad-2026) (Gumroad would take more: 10% + $0.50 on top of card fees, [schoolmaker](https://schoolmaker.com/blog/gumroad-pricing)) |
| Delivery / hosting per copy | ~$0 | [Assumption] |
| **Net revenue per sale** | **$15.36** | arithmetic |
| Meta CPC (US, all industries) | $1.24 (fitness ~$1.90) | [Fact] [superads.ai](https://www.superads.ai/facebook-ads-costs/cpc-cost-per-click/united-states), [bestever.ai](https://www.bestever.ai/post/facebook-ads-benchmarks) |
| Landing-page conversion, cold social traffic | 2.5% (low 1.5% / high 4%) | [Assumption], based on the 2–5% cold-DTC band in [clickminded](https://www.clickminded.com/landing-page-conversion-benchmark/) |
| **Ad cost per sale (CAC) = CPC ÷ CVR** | likely 1.24/0.025 = **$49.60**; worst 1.90/0.015 = $126.67; best 0.90/0.04 = $22.50 | arithmetic |
| **Contribution per sale** | 15.36 − 49.60 = **−$34.24** | arithmetic |

Even the best case ($22.50 CAC) is higher than the $15.36 net. A single ebook sold to cold ad traffic loses money on every sale.

Adding an order bump and an upsell helps but does not fix it. Assume a $9 bump taken by 30% of buyers and a $37 upsell taken by 10% [Assumption]. Average order = 17 + 2.70 + 3.70 = $23.40. Net after ~9.7% fees is about $21.13. That is still below the $49.60 CAC.

**Monthly fixed costs** [all Assumption]

| Item | Low / likely / high |
|---|---|
| Store (Payhip free → Plus $29) | $0 / $0 / $29 |
| Email tool, design, AI writing tools | $0 / $50 / $100 |
| Domain, misc | $2 / $10 / $20 |
| New ad creatives (UGC/video) | $0 / $40 / $250 |
| **Total** (founder time unpaid) | **~$2 / $100 / $400** |

One-off cost to create the ebook: $0 if self-written, up to ~$1,000 for a ghostwriter and design [Assumption].

**Break-even:** The likely case never breaks even. Contribution per sale is negative, so selling more loses more.
- The funnel needs CAC ≤ net order value. At a $1.24 CPC and $21.13 net order value, the break-even conversion rate is 1.24 / 21.13 = **5.9%**. For the single $17 book it is 1.24 / 15.36 = **8.1%**.
- Workable scenario: CPC $1.00, conversion 5%, average order $30. CAC = $20, net ≈ $27.30, contribution ≈ $7.30 per sale. Covering $100/month fixed then takes 100 / 7.3 ≈ **14 sales/month**, which is about $280 of ad spend.

**Cash to break-even:** **$2,000–$5,000 (likely ~$3,000)**, over **2–4 months**. Derived as:
- Tools: $100 × 3 months = $300.
- Product creation: $0–1,000.
- Ad testing: enough spend to get about 40–60 purchases across 5–10 creatives. At a $25–50 CAC that is $1,500–3,000, most of which is lost while learning.

If conversion never reaches about 5%, this money is gone and break-even never comes.

**The number that breaks the model:** the **landing-page conversion rate**, or put another way, CAC against net order value.
- Below **~5.9%** (with a funnel) or **~8.1%** (a single $17 book) at US CPCs, every sale loses money.
- A second risk: UK consumer prices include 20% VAT [Fact, [gov.uk](https://www.gov.uk/vat-rates)]. That takes 1/6 off £ revenue unless the platform handles it in the price.

**My investment condition:** "I would invest if a capped $1,000 test spend produces at least 40 purchases at a blended CAC of $20 or less, with front-end ROAS of 1.2 or more (average order value / CAC) in the same campaign, and an email list growing at about 3× buyers for later sales."

**Verdict from the numbers:** **Unattractive as a single cheap ebook. Marginal only as a funnel** (bump + upsell + email backend). At benchmark CPCs and cold-traffic conversion rates, a $17 ebook costs about $50 in ads to sell. It only works if a higher-priced back-end product makes up the difference, and there is no evidence for that yet.

Sources:
- [superads.ai – US Facebook CPC](https://www.superads.ai/facebook-ads-costs/cpc-cost-per-click/united-states)
- [superads.ai – US Facebook CPM](https://www.superads.ai/facebook-ads-costs/cpm-cost-per-mille/united-states)
- [bestever.ai – Facebook ads benchmarks 2025](https://www.bestever.ai/post/facebook-ads-benchmarks)
- [fungies.io – Sellfy vs Payhip vs Gumroad 2026](https://fungies.io/sellfy-vs-payhip-vs-gumroad-2026)
- [schoolmaker.com – Gumroad pricing 2026](https://schoolmaker.com/blog/gumroad-pricing)
- [clickminded.com – Landing page conversion benchmarks 2026](https://www.clickminded.com/landing-page-conversion-benchmark/)
- [gov.uk – VAT rates](https://www.gov.uk/vat-rates)
