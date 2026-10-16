# Council Verdict: QuickCart (Siliguri grocery delivery pilot)

**Verdict:** TEST FIRST
**Confidence:** 3
**One-line reason:** The brief's own ₹7/order contribution margin is real but razor-thin, and the two variables that decide whether it survives — actual cost per delivery and COD refusal/RTO rate — are both unmeasured, not unfavorable; a cheap, short pilot answers both before any further commitment.

## What the evidence shows
- Strongest point for: The pilot is cheap and the baseline arithmetic isn't broken before it starts — ₹25 delivery fee − ₹18 cost/delivery = ₹7 positive contribution margin per order (Believer/Investor, [Fact] directly from the brief, undisputed arithmetic). A thin margin is not the same as a negative one, and this is a low-commitment way to find out which it is.
- Strongest point against: The Investor's Round 2 sensitivity analysis — margin = (success rate × ₹25) − ₹18 — shows the model goes to roughly breakeven at ~72% delivery success (≈28% refusal) and goes negative beyond that, which sits inside the refusal-rate range the Skeptic cited for Indian COD orders generally. All three members converged on this as the decisive uncertainty by Round 2 (Investor [Arithmetic, verified independently], Skeptic concession, Believer concession).
- Unsupported claims set aside:
  - Skeptic's "no stated capacity to run daily ops alone" — explicitly tagged [Assumption, not stated in brief]; not evidence against the idea, just an open operational question.
  - Believer's claim that hyperlocal grocery COD refusal behaves like "low single digits" food-delivery no-shows — [Assumption] offered with no source, set against the Skeptic's sourced (if unverified-by-us) industry figure; doesn't earn more weight than the number it's trying to discount.
  - The Zomato/Emkay "50% lower non-metro delivery cost, 800 vs 1,300 orders/store breakeven" figure — flagged by the Believer themselves as a secondary source needing verification, and the Investor correctly declined to adopt it because it describes Zomato/Swiggy's scaled fleets, not a 10-vendor gig-rider pilot. Treated as unverified, not as proof ₹18/delivery is realistic.

## Source spot-check
WebFetch was non-functional for the entirety of this review (DNS resolution failed for every URL attempted, including unrelated control domains like example.com and google.com — an environment issue, not a sign the cited pages don't exist). Per the instructions, these are recorded as **not reachable** and treated as unverified, not false. No claim below is being called wrong — only unconfirmed by this council sitting.

| Claim | Source | Result |
|---|---|---|
| COD orders see ~28–35% RTO/refusal rates vs 4–8% prepaid | shipmozo.com (Skeptic) | not reachable |
| Swiggy Instamart launched in Siliguri Feb 2025 as part of 100-city tier-2/3 push; ~1 in 4 new users from tier-2/3 | swiggy.com/corporate, outlookbusiness.com (Believer) | not reachable |
| Non-metro delivery costs up to 50% lower; Emkay breakeven ~800 orders/store (tier-2) vs ~1,300 (metro) | officechai.com (Believer, self-flagged as needing verification) | not reachable |
| Quick-commerce platforms typically take 15–25% vendor commission | base.com, storyboard18.com/CareEdge (Investor) | not reachable |
| Blinkit/Zepto/Instamart hold ~90% of India's quick-commerce market | (Skeptic) | not reachable |

Because the two most decision-relevant external claims (COD refusal rate, Instamart's presence in Siliguri) could not be verified this sitting, neither should be treated as settled fact when deciding what to do Monday — both need direct, local confirmation (see tests below), which is cheap and faster than re-attempting remote verification.

## The single biggest risk
The ₹7/order margin is a product of two unmeasured variables, not one: real cost per delivery (brief gives ₹18 as a self-reported estimate) and delivery success rate (refusal/no-show/short-cash rate under COD). The Investor's own math shows that if refusal lands anywhere near the industry range the Skeptic cited (~28%+), or if true cost per delivery runs ₹7–10 above ₹18, the model loses money on every attempt — and no volume fixes a per-order loss. Neither input has been measured in this specific context (hyperlocal grocery, COD, Siliguri); both sides agree on this by Round 2. This is a "can't know yet," not a "known bad" — nothing presented proves the margin is already negative — but it is the one fact that, if unfavorable, kills the model outright.

## Three cheapest next tests (≤ 2 weeks each)
| Test | How | Result that means continue | Result that means stop |
|---|---|---|---|
| Real-cost, real-refusal pilot | Run 2 weeks with the 3 already-interested vendors; log every delivery's actual rider cost, every refusal/no-show/short-cash incident, and resulting revenue per attempt | Measured cost/delivery ≤ ₹20 **and** refusal/loss rate ≤ ~10-15%, yielding real margin ≥ ₹4-5/order | Measured refusal rate tracks toward 25-30% or measured cost/delivery ≥ ₹25, pushing margin to ≤ ₹0 |
| Vendor conversion | Get written/verbal commitment with specific terms (commission, restock cadence, exclusivity) from all 10 target vendors, not just the 3 already favorable | ≥ 7-8 of 10 convert to committed within 1-2 weeks | Fewer than 5-6 convert — supply side isn't there yet regardless of demand |
| Incumbent coverage check | Check Blinkit/Zepto/Instamart app pincode coverage for the exact target Siliguri neighborhoods (not the city generally) | None of the three currently deliver to the target neighborhoods, or QuickCart can name a clear underserved niche (cash-preferring, non-app-fluent customers) they don't reach | All three already deliver to the same neighborhoods faster and prepaid, with no identifiable underserved segment |

These map directly onto the Investor's own stated investment condition: "measured cost per delivery ≤ ₹20, ≥10 orders/vendor/day sustained, COD losses under 2% of order value" — adopted here as the bar to clear before any further spend.

## What would flip this verdict
**To GO / GO WITH CONDITIONS:** the pilot above returns a measured (not estimated) contribution margin of roughly ₹4-5+/order after refusals and cash losses, with at least 7 vendors under real commitment, and no major incumbent already covering the specific target neighborhoods with comparable or better service.

**To NO-GO:** the pilot shows refusal/RTO rate sustaining near or above ~25-28% (margin at or below zero at any volume), or confirms Blinkit/Zepto/Instamart already serve the exact target neighborhoods faster and prepaid with no distinguishable underserved niche, or vendor commitment stalls below ~5 signed vendors after real outreach — any one of these, confirmed rather than assumed, is a genuine blocker rather than a "need more data" problem.

## Where the council agreed / disagreed
- Agreed: the Round 1 ₹7/order margin was treated too cleanly by the Believer and was fragile; the Investor's break-even arithmetic (≈4,286 orders/month at ₹7 margin, worse at ₹3.25) is correct and was adopted by both other members without challenge; vendor pipeline (3 of 5 contacted, 10 needed) is currently weak and unconfirmed, not a settled "yes"; none of the three inputs that would resolve the debate — measured delivery cost, measured refusal rate, confirmed vendor count — exist yet.
- Still disputed: whether the Instamart-in-Siliguri fact (itself unverified by this council) is evidence of validated local demand (Believer) or of a funded, faster, prepaid incumbent that makes a thin-margin COD challenger's position worse (Skeptic) — this was raised and countered but never resolved, because it turns on a competitive-differentiation claim ("QuickCart serves a niche Instamart can't") that is itself an unsupported [Assumption] from the Believer, not evidence.
