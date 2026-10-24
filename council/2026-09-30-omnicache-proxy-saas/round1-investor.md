## Investor — Round 1

No price, user count, revenue or cost figures were supplied [from the brief]. Every revenue line below is therefore an [Assumption]. Currency is USD because the tool prices savings in USD.

**Unit economics** (one paid solo seat per month)
| Item | Value | Tag/source |
|---|---|---|
| What a heavy API user spends today | $150–250/dev/month, about $13 per active day | [Fact] [Claude Code docs](https://code.claude.com/docs/en/costs) |
| Share of that spend already on cache discount | In Anthropic's sample session, 940k of about 991k input tokens were cache reads, billed at 0.1x | [Fact] same doc; [prompt caching docs](https://platform.claude.com/docs/en/build-with-claude/prompt-caching) |
| Realistic share of the bill OmniCache removes | 5% / **15%** / 30% | [Assumption]. The README's 40–70% is unverified. Tool replay skips local execution, but the tool output still goes into the prompt sent upstream. |
| Value per API dev per month | $200 × 15% = **$30** (low $7.50, high $75) | derived |
| Value per Pro/Max subscriber | **$0 in dollars**. They pay a flat fee, so the only gain is more headroom before hitting usage limits. | [Fact] docs say session cost "isn't relevant for billing" for subscribers |
| Price (about 1/2 of value) | $8 / **$15** / $29 per seat per month | [Assumption] |
| Stripe fees | 2.9% + $0.30 + 0.7% Billing = $0.84 | [Fact] [Stripe fees 2026](https://checkoutpage.com/blog/stripe-processing-fees), [Billing 0.7%](https://usagebox.com/articles/stripe-billing-fees-2026-the-07-percent-math) |
| Hosting per user | About $0 (runs on the user's own machine) | [Fact] from the README |
| Support and license server | $0.20 / **$0.50** / $2 | [Assumption] |
| **Contribution margin** | 15 − 0.84 − 0.50 = **$13.66** (about 91%) | derived |

**Monthly fixed costs**
| Item | Likely (range) | Tag |
|---|---|---|
| Tools: domain, docs, license server, email | $150 ($100–300) | [Assumption] |
| Marketing | $500 ($0–2,000) | [Assumption] |
| Founder salary | $5,000 ($0–8,000) | [Assumption] |
| **Total** | **$5,650** (ramen version, no salary: $650) | |

**Break-even**
- With salary: 5,650 / 13.66 ≈ **414 paid seats**.
- Ramen version: 650 / 13.66 ≈ 48 paid seats.
- Free-to-paid conversion is probably 1–3% [Assumption], so 414 paid seats means about **14k–41k active free installs**.

**Cash to break-even:** about **$34k–$68k**. I assumed revenue grows in a straight line from zero to break-even over T months, so the money lost along the way is roughly fixed costs × T / 2:
- T = 12 months: 5,650 × 12 / 2 ≈ $34k
- T = 24 months: ≈ $68k
- Ramen version over 12 months: ≈ $4k

**The number that breaks the model:** the real reduction in the monthly provider bill, measured on the provider's invoice rather than the tool's own counter.
- Below about **7%**, an average API user gets about $14 a month of value, so a $15 price is worth nothing to them.
- Anthropic's docs show the big fixed parts of the prompt are already billed at the 0.1x cache rate, so a 7% ceiling is plausible.
- Close behind: the share of target users on flat Pro/Max plans, where the dollar savings are zero.

Two structural problems sit on top of that:
1. **Nothing is set up to charge for.** The license (FSL, a source-available license that turns into MIT after two years) makes it free for developers and internal company use. It runs 100% on localhost, has no telemetry, and the code has no billing or license-key logic (I searched the repo). Any paid tier would have to be new features, such as hosted team sync, SSO or audit dashboards.
2. **The savings evidence comes from the project itself.** The only numbers are its own benchmarks and audit report. The README's sample session "saved" $0.0554.

**My investment condition:** "I would invest if **20+ external teams paying per token show at least a 15% drop in their Anthropic or OpenAI invoice over 30 days, measured in the provider's billing console, and 50+ customers pay at least $15/seat/month with under 5% monthly churn for 3 consecutive months.**"

**Verdict from the numbers:** **Unattractive as a SaaS today.** Serving each user costs almost nothing and the ramen break-even is only about 50 seats. But there is no way to charge yet, the core product is free under its own license, and the claimed savings are unproven and probably much smaller than advertised because provider caching already discounts most input tokens. It is a cheap experiment, not yet an investable business.

Sources:
- [Claude Code docs – Manage costs](https://code.claude.com/docs/en/costs)
- [Anthropic prompt caching docs](https://platform.claude.com/docs/en/build-with-claude/prompt-caching)
- [Stripe fees 2026 – checkoutpage.com](https://checkoutpage.com/blog/stripe-processing-fees)
- [Stripe Billing 0.7% – usagebox.com](https://usagebox.com/articles/stripe-billing-fees-2026-the-07-percent-math)
- Brief and README: /home/user/agent-council/council/2026-09-30-omnicache-proxy-saas/brief.md
- Repo's own audit report: /home/user/13manmayarai-hash/omnicache-proxy/docs/EMPIRICAL_AUDIT_REPORT.md
