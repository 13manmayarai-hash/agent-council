## Investor — Rebuttal

**Numbers affected by their points:**

1. **Skeptic's COD RTO/refusal stat (28–35% for Indian COD orders [Fact, shipmozo.com]) materially weakens my margin assumption.** My Round 1 treated ₹7/order as a clean contribution margin, but that assumes every attempted delivery is paid. In reality, a refused/failed delivery still costs ₹18 (rider already traveled) and earns ₹0 revenue. Expected margin per *attempted* order = `s×25 − 18`, where s = success rate:
   - s=95% (refusal 5%, [Assumption] low end — hyperlocal grocery with known local customers plausibly beats generic ecommerce COD) → 0.95×25−18 = **₹5.75/order**
   - s=85% (refusal 15%, [Assumption] likely) → 0.85×25−18 = **₹3.25/order**
   - s=70% (refusal 30%, [Fact-derived] Skeptic's industry ceiling) → 0.70×25−18 = **−₹0.50/order — model loses money on every attempt, no volume fixes it.**
   This is a direct, quantified strengthening of my original "number that breaks the model" — it's not just cost-per-delivery drift, it's *refusal rate interacting with* cost-per-delivery, and the industry ceiling Skeptic cites sits inside the loss zone. I flag that the 28–35% figure is from general ecommerce COD, not confirmed for hyperlocal grocery with repeat local buyers, so I keep my own lower range as [Assumption], but the exposure is real and larger than I modeled in Round 1.

2. **Believer's own citation (Swiggy Instamart launched in Siliguri, Feb 2025) weakens the ramp-speed assumption behind my cash-to-break-even estimate.** A national prepaid, faster incumbent already operating in the exact launch city raises customer-acquisition cost and lengthens the time to reach break-even volume — it doesn't change unit economics per order, but it pushes out my 3–4 month ramp assumption.

3. **Believer's tier-2 cost-advantage point (delivery costs up to 50% lower in non-metro, Zomato-cited) doesn't move my numbers** — it describes scaled fleet economics at Zomato/Swiggy, not a 10-vendor ad-hoc gig-rider pilot, so I don't adopt it without a measured number from QuickCart's own pilot.

4. **Skeptic's vendor-commitment point (only 3/5 interested, need 10) compounds with #2** — fewer vendors means slower volume ramp, which combined with a lower realistic margin (₹3.25, not ₹7) pushes break-even volume and cash need up materially.

**Revised break-even / verdict:**

Using likely margin ₹3.25/order (15% refusal) instead of ₹7: Break-even = ₹30,000 ÷ ₹3.25 ≈ **9,231 orders/month ≈ 308/day ≈ ~31 orders/vendor/day across 10 vendors** — more than double my Round 1 figure and harder to hit given only 3 vendors are confirmed and an incumbent (Instamart) already serves the city.

Revised cash to break-even: longer ramp (5–6 months, not 3.5) × ₹30,000 fixed + ₹50,000 setup ≈ **₹200,000–300,000** [Assumption, widened range].

**Verdict: Unattractive, more firmly than Round 1.** The COD refusal risk Skeptic raised turns a thin ₹7 margin into a ₹3-ish (or negative) one, roughly doubling required volume at a weaker competitive position than assumed — I would not invest until a real pilot measures both cost-per-delivery *and* refusal rate together.
