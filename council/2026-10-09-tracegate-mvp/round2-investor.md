## Investor — Rebuttal

**Numbers affected by their points:**

- **Price per seat ($25 likely), weakened by the Skeptic.** Free open-source tools already do the diff-only checks: tampercheck and tamperguard [Fact, Skeptic's PyPI links]. The incumbent AI reviewers already run on every PR. If the product is only diff checks, teams can get the same thing for $0, so $25 per seat cannot hold. That pushes my main breaking point (about $10 per seat) from a risk to the likely case.
- **Compute per PR ($0.20 likely), strengthened for diff checks by the Believer, weakened for evidence checks.** Deterministic diffing needs no LLM. I put that at about $0.03 per PR [Assumption: $0.01 / $0.03 / $0.10]. The YAML evidence checks are the only part buyers have no free option for, and they need a running environment plus access to the database and telemetry (Skeptic's risk 2). I put those at about $0.50 per PR [Assumption: $0.30 / $0.50 / $1.50]. That is close to my $0.56 break point.
- **Support and hosting ($15 per team), weakened.** Writing and maintaining policies per flow means onboarding work. I raise this to $40 per team per month for the evidence product [Assumption: $25 / $40 / $80].
- **Ramp (+10 teams per month), weakened.** Teams have to write YAML before they see value, so the sales cycle is longer. Likely case is now 5–10 teams per month [Assumption].
- **PRs per team (400), pushed up by the Believer.** AI-attributed PRs went from 2% to 10% in about 7 months [Fact, arXiv 2607.04697]. My cost is per PR but my price is per seat, so faster agent PR growth eats the margin. This is a pricing-design flaw in my own Round 1.
- **The Believer's "50–200 paying teams in 12 months"** is a [Guess] with no conversion data. It does not change any of my inputs.

**Revised break-even / verdict:**

The product splits into two cases with different economics. Fixed costs stay at $20K per month.

*A. Diff-only (competes with free tools).* Price $10 per seat [Assumption: $5 / $10 / $15].
- Per team: revenue 10 × $10 = $100. Costs: billing fee $5, compute 400 × $0.03 = $12, support $15.
- Contribution = 100 − 5 − 12 − 15 = **$68**.
- Break-even = 20,000 / 68 = **295 teams**.
- At 15 teams per month (self-serve), the ramp takes 20 months: 20K × 20 / 2 = $200K, plus $60K to build = **about $260K, with a 23-month runway**. That means more cash, a lower price and a free competitor. **Unattractive.**

*B. Evidence-led (the differentiated part).* Price $35 per seat [Assumption: $25 / $35 / $50].
- Per team: revenue 10 × $35 = $350. Costs: billing fee $17.50, compute 400 × $0.50 = $200, support $40.
- Contribution = 350 − 17.5 − 200 − 40 = **$92.50 (26%)**.
- Break-even = 20,000 / 92.5 = **217 teams**.
- At 10 teams per month: 22 months × 20K / 2 = $220K, plus 4 months of build at $80K = **about $300K**.
- At 5 teams per month: 43 months, about $510K. That is not fundable.
- Compute breaks the model at (350 − 17.5 − 40) / 400 = **$0.73 per PR**. If the team has 1,000 PRs instead of 400, the break point drops to $0.29 per PR, so contribution is already negative at my likely $0.50.
- **Marginal, and only with usage-based pricing**, for example per evidence-checked PR or per flow, not per seat.

**Verdict: Marginal, leaning Unattractive** (down from Marginal). The part that costs little to run is a commodity. The part that can command a price costs more to run and is slower to sell.

The good news is that the tests that decide this are cheap to run. The Skeptic's free scan (5 teams × 100 PRs × about $0.20) costs about $100 in compute plus a few weeks of founder time. Nobody should spend the $260K–$510K before running it.

**Updated investment condition.** I would invest if all of these are proven:
1. TraceGate catches at least 30% more confirmed tampering than tamperguard or CodeRabbit on the Skeptic's 30-PR benchmark.
2. At least 5 of 10 paying pilot teams have at least one YAML evidence policy live. They must be paying for evidence, not for diff checks.
3. Measured cost is at or below $0.40 per evidence-checked PR, under pricing that grows with PR volume.
4. My Round 1 thresholds still hold: at least 10 teams paying at least $20 per seat for 3 months, and monthly churn under 5%.

Files read:
- /home/user/agent-council/council/2026-10-09-tracegate-mvp/brief.md
- /home/user/agent-council/council/2026-10-09-tracegate-mvp/round1-investor.md
- /home/user/agent-council/council/2026-10-09-tracegate-mvp/round1-believer.md
- /home/user/agent-council/council/2026-10-09-tracegate-mvp/round1-skeptic.md

Sources (cited by the other members, used above):
- https://pypi.org/project/tampercheck/
- https://pypi.org/project/tamperguard/
- https://arxiv.org/abs/2607.04697
- https://dev.to/moonrunnerkc/ai-agents-cheat-on-pull-requests-i-mined-327-of-them-to-prove-it-43ij/comments
