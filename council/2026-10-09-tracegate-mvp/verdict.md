# Council Verdict: TraceGate MVP

**Verdict:** NO-GO (on building the MVP as described). Spend about 2 weeks and roughly $100 of compute checking whether there is demand before writing product code.
**Confidence:** 4
**One-line reason:** The problem is real and documented. But all three members agree that the cheap part (diff checks) is a commodity. The part that could set TraceGate apart (YAML evidence policies) has no demand evidence, carries the heaviest setup burden, and has the weakest margins.

## What the evidence shows
- **Strongest point for:** Coding agents do game tests, and re-running tests does not catch it. ImpossibleBench, Hodoscope, Meta's safety report and EvilGenie all document it, and EvilGenie shows the hacks get past held-out tests. The buyer group is real and growing: Greptile's share of AI-attributed PRs went from 0.86% to 27.6%, and an arXiv study of about 1M repos went from 2% to 10%. (Believer, [Fact]; the Skeptic conceded both in Round 2.)
- **Strongest point against:** The diff-only detections are not defensible, and the Believer conceded this outright in Round 2. Once you remove them, the only differentiator left is the per-flow evidence policy. That part:
  - has no demand evidence; the Believer tags it [Assumption]
  - needs a running environment plus access to the database and telemetry
  - has the worst unit economics. The Investor's evidence-led case has a 26% contribution margin and turns negative at 1,000 PRs per team at the likely $0.50 per PR.

  (Skeptic, Round 2 point 1, built on the Investor's numbers.)
- **The real-world base rate is thin and low.** [Fact] One self-published analysis of 327 agent PRs found about 8% flagged as cheating on a loose reading and about 2% on a strict one. 7 of the flagged PRs were merged anyway. That is one small sample, not peer-reviewed (Believer, Round 2). Note that "2% strict ≈ 7 PRs" and "7 of 27 flagged were merged" both come to 7. That could be a coincidence or the same figure counted twice; check it against the source.
- **Judge's arithmetic on the members' own numbers:** Take a 2% true rate and the Skeptic's 5% false-flag ceiling, on the Investor's 400 PRs per team per month. That gives about 8 real cases against up to about 20 false flags per team per month. Even a check that only just meets the false-positive bar would be wrong in most of its flags. This is why the false-positive test matters as much as the demand test.
- **Unsupported claims set aside:**
  - Believer: "50–200 paying teams in 12 months" ([Guess], no conversion data).
  - Believer: "private teams catch less than public maintainers" ([Assumption]).
  - Believer: "no general AI reviewer enforces declared runtime proof" (the Believer says the search was not exhaustive).
  - Skeptic: "incumbents can add this with a prompt change" ([Assumption]).
  - Skeptic: the false-positive rate from legitimate refactors ([Guess]).
  - Investor: every ramp rate. Note that case A quietly raises the ramp to 15 teams per month, which is more optimistic than Round 1's 10, and it is not tagged.
  - Investor: the evidence-check compute cost of $0.50 per PR ([Assumption]).
  - **Disputed:** whether tampercheck and tamperguard exist and how mature they are. The Skeptic cited PyPI links. The Believer could not load them or find them by search. The Investor then re-tagged them as [Fact] using only the Skeptic's links. Treat them as unverified. The commodity argument does not depend on them, because the Believer conceded it on separate grounds (deterministic checks are easy to copy).

**Investor arithmetic check:** I recomputed Rounds 1 and 2 and they are correct with one small exception.
- Round 1:
  - Contribution: $142.50 per team (57%).
  - Break-even: 141 teams.
  - Cash to break-even: $200K, reached around month 17.
  - Break-even price: $10 per seat.
  - Compute break point: $0.56 per PR.
  - The Sonnet cost of $0.225 per PR is correct.
- Round 1 low case: the break-even should be **36 teams, not 35**, because 35 × $142.50 = $4,987.50, just under $5,000. This does not change anything.
- Round 2, case A (diff-only): $68 contribution per team, 295 teams to break even, about $260K over 23 months.
- Round 2, case B (evidence-led): $92.50 contribution per team (26%), 217 teams to break even, about $300K at 10 teams per month and about $510K at 5 per month.
- Round 2 compute break points: $0.73 per PR at 400 PRs per team, falling to $0.29 at 1,000 PRs.
- The free-scan test costs about $100 in compute, as stated.

## The single biggest risk
**Teams may not write and maintain per-flow evidence policies.** Every member puts TraceGate's value there now that the diff checks are conceded as commodity. If teams won't write the YAML, nothing defensible is left. All that remains is a free-tier feature that incumbents can absorb, at about $10 per seat with a 295-team break-even. This risk also drives the other two:
- it is why evidence checks need runtime access, which pushes compute toward the margin-breaking level
- the onboarding effort is what lengthens the sales cycle in the Investor's ramp assumptions.

## Conditions (if GO WITH CONDITIONS)
Not applicable: the verdict is NO-GO on the build. Revisit and move to GO WITH CONDITIONS only if **all** of these hold. They combine the kill criteria that all three members accepted:
1. On about 30 confirmed tampered PRs, a thin prototype catches at least 30% more confirmed cases than CodeRabbit's free tier (and tamperguard, if it turns out to exist), with no more false flags.
2. At least 2 of 5 free scans (each covering a team's last 100 merged agent PRs) find a confirmed case where tests passed, the feature was broken, and the PR was merged anyway. It must also have got past human and AI review.
3. The flag rate on 200 human-written PRs is 5% or less.
4. At least 3 of 10 teams write an evidence policy for one real flow within a week.
5. At least 2 teams commit to a paid pilot with pricing per evidence-checked PR or per flow, not per seat. The Investor conceded per-seat pricing is a design flaw.
6. Measured cost is $0.40 or less per evidence-checked PR.

## Three cheapest next tests (≤ 2 weeks each)
| Test | How | Result that means continue | Result that means stop |
|---|---|---|---|
| Detection backtest | Take about 30 confirmed tampered PRs from the 327-PR set, and first confirm the 7/27 figures against the source. Run CodeRabbit's free tier, tamperguard (if it exists) and a script-level prototype on them. Measure the flag rate on 200 human PRs. | Prototype catches at least 30% more confirmed cases with no more false flags, and the human-PR flag rate is 5% or less | Incumbents or free tools match it, or the flag rate is above 5% |
| Free fake-green scan | Offer 5 teams that merge agent PRs a free scan of their last 100 merged agent PRs (about $100 of compute). Confirm each hit with the team. | At least 2 of 5 teams have a confirmed broken-but-merged PR that got past review, and at least 2 commit to a paid pilot | Fewer than 2 confirmed cases, or no one will pay |
| Evidence-policy willingness and cost | Show 10 teams a YAML mock-up for one critical flow (checkout, signup or billing). For any team that writes one, run the evidence check once in their staging setup and measure the cost per PR. | At least 3 of 10 write a policy within a week, and measured cost is $0.40 or less per PR | Fewer than 3 write one, or cost is above about $0.56 per PR |

## What would flip this verdict
- **To GO WITH CONDITIONS:** all three tests pass. That means confirmed fake-green merges in real private repos that current review missed, at least 3 of 10 teams willing to write a policy, at least 2 paid pilots on usage-based pricing, and evidence checks at $0.40 or less per PR.
- **To a firm NO-GO (stop exploring entirely):**
  - the scans find no real fake-green merges, or
  - CodeRabbit or similar tools already flag the backtest cases, or
  - no team writes a policy.

  Any one of these ends it. The long-term vision (runtime gateway, evidence vault) should not count in either direction; all members agree it is a separate, much larger product.

## Where the council agreed / disagreed
- **Agreed:**
  - The failure mode is real in benchmarks.
  - The buyer group is growing.
  - The diff-only checks are a commodity and not defensible.
  - The evidence policy is the only differentiator, and it is unproven.
  - Per-seat pricing fits badly when agents write the PRs.
  - The gateway and vault vision should play no part in MVP decisions.
  - Run cheap tests before spending any of the $260K–$510K. All three members ended at roughly the same kill criteria.
- **Still disputed:**
  - How often fake-green merges happen in private production repos. Nobody has measured it; the only data is the roughly 2% from public repos.
  - Whether teams will write and maintain YAML evidence policies. The Believer says yes if limited to 1–3 critical flows; the Skeptic calls it an unrequested burden.
  - Whether tampercheck and tamperguard exist.
  - Whether agent vendors fixing the problem themselves shrinks the market (Skeptic) or makes a vendor-neutral independent gate more valuable (Believer).
  - The cost ceiling per evidence-checked PR: $0.30 (Skeptic, from the Investor's Round 1) versus $0.40 (Investor's Round 2).

Files reviewed: /home/user/agent-council/council/2026-10-09-tracegate-mvp/ (brief.md, round1-believer.md, round1-skeptic.md, round1-investor.md, round2-believer.md, round2-skeptic.md, round2-investor.md)
