# Council Verdict: omnicache-proxy as a paid SaaS

**Verdict:** NO-GO. Don't charge for it or build a SaaS yet. Run one billing test first.
**Confidence:** 4
**One-line reason:** There is no measured saving on any real provider bill, and the one feature that could save money may raise bills by breaking Anthropic's own caching. The paywall can also be bypassed, and the people who can pay are a minority of users.

## What the evidence shows
- **Strongest point for:** The history-trimming feature is real and runs on every Anthropic request (`server/tool_replayer.py:972`, `server/gateway.py:1387`). Anthropic's native caching makes repeated text cheaper but never removes it, so this is a genuine mechanism that could save input tokens. Each user costs almost nothing to serve, so a failed experiment costs time, not money. (Believer, [Fact, verified in code]. The Skeptic conceded this in Round 2.)
- **Strongest point against:** Anthropic's own caching already bills most input at 0.1x. In Anthropic's sample session, about 95% of input tokens were cache reads (Investor, [Fact, Claude Code docs]). Claude Code reportedly hits the cache about 92% of the time (Skeptic, [Fact, sourced]). OmniCache trims copies deep in the history, and those sit inside the part Anthropic has already cached (Believer, Round 2, [Fact, code, lines 1139-1169]). Changing that part is expected to break Anthropic's cache from that point on, so tokens billed at 0.1x get billed again at 1.25x as cache writes. That step is still an [Assumption]: nobody has measured it. But it follows directly from Anthropic's published pricing, and all three members now expect it. The Believer, whose case rested on this feature, conceded it in Round 2 and dropped to 2/5.
- **Second point against:** You can't enforce payment today. The upgrade handler defaults to `payment_method="sandbox"`, which upgrades the tier with no payment. The Razorpay signature check is also skipped if any one of three values is missing (`gateway.py:2675-2700`). Tiers only change the user's own spending cap and rate limit, on a machine where the user holds the admin key. (Skeptic and Investor, Round 2, [Fact, verified in code].) The Investor's Round 1 claim that the code had "no billing logic" was wrong, and the Investor corrected it. The conclusion still holds: money collected is $0 and nothing stops anyone from upgrading for free.
- **Unsupported claims set aside:**
  - The README's "40–70%" and "60–80% of token burn" figures. They are the project's own claims, with no measurement on a real bill behind them. The README's sample session saved $0.0554.
  - The Believer's $2k–$25k monthly revenue within 12–18 months [Guess].
  - The Believer's claim that fixing the cache problem is "a change of maybe a few days" [Assumption].
  - The Believer's point that subscribers gain headroom before hitting usage limits [Guess, which the Believer marked as low-weight].
  - The Skeptic's claim that LiteLLM, Helicone and Portkey already do response caching [Guess, and the Skeptic says it wasn't checked].
  - Every savings percentage used in the Investor's model: 5/15/30%, then −5/5/15% [Assumption]. The 1–3% free-to-paid conversion rate [Assumption].

**Can't know yet vs. known bad**
- *Can't know yet (a test will settle it):* whether the net saving on a real bill is positive; what share of users pay per token; how often cached `bash` output is stale.
- *Known bad (real blockers today):*
  - The paywall can be bypassed.
  - Flat-rate Pro/Max subscribers save $0 (Claude Code docs, [Fact]).
  - Cursor sends model calls through its own backend (api2.cursor.sh), so a localhost proxy can't intercept them. This is sourced, and nobody defended Cursor support. "Cut your Cursor bill" should come out of the README now.
  - A hosted SaaS gives up the "100% localhost, zero telemetry" pitch that is the product's main selling point.

**Arithmetic check (Investor):** I re-ran every figure and they are correct:
- Round 1:
  - Stripe fee on $15: $0.84. Profit per seat after fees and support: $13.66.
  - Break-even: 414 seats with a salary, 48 without.
  - Free installs needed: 13.8k–41.4k. Cash needed: $34k–$68k.
- Round 2:
  - Input cost per 100 tokens: 17.2–19.2 units. A cache write costs 12.5x a cache read.
  - Razorpay fee: 3.54% of $6 = $0.21. Profit per seat: $5.29.
  - Break-even: 1,068 seats with a salary, 123 without, 501 on the India-salary case. Free installs needed: 36k–107k.
  - At a $24 price, profit per seat is $22.65 and break-even is about 250 seats.

Three small problems, none of which changes the verdict:
- Round 1's value range mixes spending levels. The low end is 5% of $150 and the high end is 30% of $250.
- Round 2 cites the Razorpay routes as `gateway.py:2587-2588` in the text but `5587-5588` in the source list. The Skeptic's `5587-5588` is probably the right one.
- More importantly, the "cash to break-even" method assumes a steady climb to break-even over 12–24 months whatever the number of seats. Reaching 1,068 paid seats (36k+ free installs, all paying per token) in 12–24 months is a far stronger assumption than reaching 414. So the $16k–$68k figure understates the risk at a $6 price.

Nobody modelled output tokens. Trimming the history does nothing to output cost, so the saving on a whole bill is smaller than any input-only figure suggests.

## The single biggest risk
**The core feature may make users' bills go up.** Everything else depends on it. If the net saving on the real bill is zero or negative, there is nothing to sell at any price, to any customer group, hosted or local. The Believer's proposed fix (only trim the part of the conversation Anthropic hasn't cached yet) also has a built-in limit. That part is a small share of input tokens, so even a working fix may land below the Investor's roughly 7% line, under which a $15 price isn't worth paying. None of the three members has any measured data on this, and all three name it as the thing that decides the outcome.

## Conditions (if GO WITH CONDITIONS)
Not applicable. The verdict is NO-GO. Before it is revisited, all of these need to be true:
1. On a real bill, API-billed Claude Code sessions show a net cost drop of at least 15%, counting input, cache-read and cache-write tokens, compared with the same sessions without OmniCache.
2. The paywall can't be switched off on the user's machine. That means either a feature hosted on your server or a license check your server enforces. The sandbox default must be removed from production builds.
3. At least 30% of surveyed heavy users pay per token, not by subscription.
4. Cursor and any other claim not yet shown to work are removed from the README.

## Three cheapest next tests (≤ 2 weeks each)
| Test | How | Result that means continue | Result that means stop |
|---|---|---|---|
| 1. A/B test on the real bill (do this first; it decides the rest) | Run 10+ identical real Claude Code tasks with OmniCache and 10+ without, on an API key. Compare the `usage` fields that are billed: `input_tokens`, `cache_read_input_tokens`, `cache_creation_input_tokens`, output tokens. If the current code loses, repeat with trimming limited to the part Anthropic hasn't cached. | Net billed reduction of at least 15% in either version | Net reduction of 7% or less in both versions (≤ 0% means stop immediately) |
| 2. How do users pay? | Message or survey 30 heavy Claude Code users: do they pay per token (API key) or a flat subscription (Pro/Max)? | At least 30% pay per token | Under 30% pay per token |
| 3. Demand for a paid team tier | Put up a pricing page offering a hosted "team shared cache + spend dashboard" at $15–24 per seat next to the free local version. Post it where Claude Code users gather. | At least 20 signups or waitlist entries from about 1,000 visitors | Under 20 from 1,000 visitors |

Run a side check alongside Test 1 at almost no cost: during the same sessions, count cached `bash` or test outputs that differ from a fresh run. Any non-trivial rate means the default caching policy has to change before any launch.

## What would flip this verdict
- **To GO WITH CONDITIONS:** Test 1 shows a net saving of at least 15% on a real bill, repeated in at least a few other people's sessions. On top of that, one of these holds: Test 2 shows at least 30% pay per token, or Test 3 gets at least 20 signups for a paywalled hosted team tier. The Investor's full investment bar is higher: 20+ external teams, 50+ customers paying $15 or more per seat, and under 5% monthly churn for 3 months. That is the bar for a real business, not for continuing to test.
- **To a firm, final NO-GO:** Test 1 shows zero or negative savings in both the current and the fixed version. The only fallback the council named is a team tier that shows and caps AI spend (not one that promises savings), and that would be a different product needing its own test.

## Where the council agreed / disagreed
- **Agreed:**
  - The README overclaims. "40–70%" is unproven, and tool replay doesn't reduce the tokens sent upstream.
  - Cursor support should be dropped from the pitch.
  - Flat-plan subscribers get $0 in dollar savings.
  - Trimming risks breaking Anthropic's cache.
  - The billing A/B test is the first and deciding step.
  - The local tool as it stands has no paywall that holds.
  - A failed experiment is cheap.
- **Still disputed:**
  - Whether trimming only the uncached part can keep a meaningful saving. The Believer says yes, [Assumption]. The Skeptic and Investor doubt it.
  - Whether subscribers get real value from headroom before usage limits [Guess, not checked].
  - Whether a hosted team tier can be sold without giving up the privacy pitch. Nobody has tested it.

Plainly, for Monday morning: this is solid engineering, but it isn't yet a product anyone has reason to pay for. Spend the next two weeks on Test 1 before any pricing, marketing or hosting work. That result decides whether there is anything to sell.

Files reviewed: /home/user/agent-council/council/2026-09-30-omnicache-proxy-saas/ (brief.md, round1-believer.md, round1-skeptic.md, round1-investor.md, round2-believer.md, round2-skeptic.md, round2-investor.md)
