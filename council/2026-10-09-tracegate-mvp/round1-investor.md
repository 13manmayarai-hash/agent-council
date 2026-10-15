## Investor — Round 1

The brief gives no currency, pricing or volumes, so I use USD [Assumption]. The unit is **one paying team per month**, and I assume a typical team of 10 developers who open PRs [Assumption: low 5, likely 10, high 25].

**Unit economics (per team per month, likely case)**
| Item | Value | Tag / source |
|---|---|---|
| Price per seat | $25 (low $15 / high $40) | [Assumption], set against [Fact] CodeRabbit Pro at $24 annual / $30 monthly ([docs](https://docs.coderabbit.ai/management/plans)) and [Fact] Greptile at $30/seat ([Capterra](https://www.capterra.co.uk/software/1105629/Greptile)) |
| Gross revenue | 10 × $25 = **$250** | arithmetic |
| Billing fee | 5% = $12.50 | [Fact] GitHub Marketplace keeps 5% ([InfoWorld](https://www.infoworld.com/article/3606490/github-increases-developers-cut-of-github-marketplace-sales.html)). Stripe is about the same. |
| PRs per team | 400/mo (low 200 / high 1,000) | [Assumption], 40 per dev for agent-heavy teams |
| LLM + CI compute per PR | $0.20 (low $0.05 / high $1.00) | [Assumption]. At [Fact] Sonnet's $3/$15 per M tokens ([aggregator](https://anotherwrapper.com/llm-pricing/claude-sonnet-4-6)), 50K in + 5K out = $0.15 + $0.075 = $0.225 |
| Compute per team | 400 × $0.20 = $80 | arithmetic |
| Hosting + support | $15 | [Assumption] |
| **Contribution margin** | 250 − 12.5 − 80 − 15 = **$142.50 (57%)** | arithmetic |

**Monthly fixed costs**
| Item | Likely | Range | Tag |
|---|---|---|---|
| Two founders (modest pay) | $16,000 | $0 – $30,000 | [Assumption] |
| Infrastructure and tools | $1,000 | $500 – $3,000 | [Assumption] |
| Marketing / dev-rel | $3,000 | $1,000 – $12,000 | [Assumption] |
| **Total** | **$20,000** | **$5,000 – $45,000** | |

**Break-even:** $20,000 / $142.50 = **141 teams (about 1,410 paid seats)**. The range runs from $5,000 / 142.5 = 35 teams (founders unpaid) to $45,000 / 142.5 = 316 teams.

**Cash to break-even:** **about $200K likely (range $25K to over $1M), reached around month 17.**
- Build phase: 3 months with no revenue, so 3 × $20K = $60K [Assumption].
- Ramp: I assume +10 net paying teams per month [Assumption: 5 / 10 / 20]. That takes 141 / 10 ≈ 14 months. The monthly loss shrinks in a straight line from $20K to $0, so the ramp costs about 20K × 14 / 2 = $140K.
- Total: $60K + $140K = $200K, at about month 17.
- Low case: founders unpaid ($5K/mo), 35 teams reached in about 3.5 months, so roughly $15K build + $9K ramp ≈ $25K.
- High case: $45K/mo fixed and only 5 teams/month means a 63-month ramp. That is not fundable.

**The number that breaks the model:** **price per seat, which depends on whether teams will pay for this separately.** With compute and support at about $95 per team, contribution reaches zero when 10 × p × 0.95 = 95, so **p ≈ $10/seat**. If CodeRabbit, Greptile or GitHub add "test-weakening detection" as a feature, the price this can charge separately could fall toward that level. The second risk is compute per PR. Contribution reaches zero at ($250 − 12.5 − 15) / 400 = **$0.56 per PR**, which is plausible if the evidence checks (DB row, telemetry) need real CI or runtime work instead of static diff analysis.

**My investment condition:** I would invest if this is proven:
- **10 teams paying at least $20/seat for 3 months in a row**, with no free extension of the pilot,
- **monthly logo churn under 5%**,
- **measured blended cost of $0.30 or less per PR**,
- **at least 1 flagged real "fake-green" PR per team per month** that the team confirms as a true positive. This shows the problem occurs often enough to justify paying for it.

**Verdict from the numbers:** **Marginal.** A 57% contribution margin and a break-even of about 141 teams are reachable on roughly $200K. But every revenue input is an assumption, and the main risk is that this becomes a free feature inside incumbent review tools. Until teams pay a separate price in a design-partner test, it does not qualify for my money.

Sources:
- https://docs.coderabbit.ai/management/plans
- https://www.coderabbit.ai/pricing
- https://www.capterra.co.uk/software/1105629/Greptile
- https://aicodereview.cc/blog/greptile-pricing
- https://anotherwrapper.com/llm-pricing/claude-sonnet-4-6
- https://www.infoworld.com/article/3606490/github-increases-developers-cut-of-github-marketplace-sales.html

Brief read: /home/user/agent-council/council/2026-10-09-tracegate-mvp/brief.md
