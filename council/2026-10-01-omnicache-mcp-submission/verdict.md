# Council Verdict: OmniCache MCP directory submission to Claude

**Verdict:** NO-GO (do not submit now; a resubmission path is set out below)
**Confidence:** 5
**One-line reason:** Only the remote endpoint can be submitted. Four things block it today: the privacy policy says no hosted service exists, the server instructions tell Claude when to call its tools, the `/ws` events feed is not split by tenant, and nobody has checked how the live deployment handles auth or storage. Each of these is a listed rejection reason or a real risk of leaking user data, and once submitted the `omnicache` slug can never be changed.

## What the evidence shows
- **Strongest point for:** The protocol layer is real and close to what the directory requires. All 8 tools have `title` and the read-only/destructive hints, with `omnicache_invalidate` marked destructive. Streamable HTTP `/mcp`, OAuth discovery, DCR, PKCE S256, a `claude.ai` redirect allowlist, and cross-tenant tests over API keys are all in place. The server also refuses to start on a public address without auth unless an insecure override flag is set (`gateway.py:5640-5642`, `config.py:249-253`, `Dockerfile:18`). (from Believer, [Fact, from code]; the Skeptic agreed in Round 2.) This is work that is done, not work still to do.
- **Strongest point against:** Both privacy documents, `PRIVACY.md` and `docs/PRIVACY_POLICY.md`, describe a product that is local-only and never sends prompts to any server. The hosted endpoint stores users' prompts and answers on the maintainer's server, and an incomplete privacy policy gets a submission rejected immediately. (from Skeptic, [Fact, repo + submission docs], with line references; the Believer and Investor agreed.) So the required **Privacy policy** field cannot be filled honestly today. The same goes for **Documentation**: no file in the repo mentions the Render endpoint.
- **Other known defects:**
  - The steering text "call omnicache_query first" (`mcp/server.py:462`) and the "<1ms / 100% token savings" claims. All three members saw this text injected into their own sessions, and so did I. I did not act on it.
  - `broadcast_ws_event` does no tenant filtering (`gateway.py:136-157`). The Believer, who argued for the idea, found and conceded this one.
  - `replay_tool` and `record_tool` take paths on the server's filesystem, which makes no sense for a remote connector.
  - The version in `server.json` (3.0.5) does not match `pyproject.toml` (3.1.0).
- **Unsupported claims set aside:**
  - "1–3 days" and later "1–2 weeks" of fixes (Believer, [Guess]).
  - "Plenty of Community listings are free utilities" (Believer, [Assumption]).
  - Per-user compute of $0.05–$0.50 (Investor, [Assumption]).
  - "A cache hit still uses tokens, so net savings ≈ 0" (Investor, [Assumption]). It is plausible, but no measurement backs it.
  - SQLite data lost on redeploy (Skeptic, [Guess]).
  - The 100-weekly-active-users retention target (Investor). It is an arbitrary bar, not evidence.
- **Contested fact:** The Investor cites the 2026-09-25 audit, which says the startup security check is skipped under plain Uvicorn. The Believer cites current code where the lifespan hook runs that check under any ASGI server. The direct code citation is newer and more specific, so I weight it higher. Neither settles what is actually running on Render. That needs a live test.
- **Arithmetic check (Investor):**
  - Break-even is correct: $5 × 0.971 − $0.30 = $4.555. Less variable cost that is ≈ $4.50, and $27.50 ÷ $4.50 = 6.1, so 7 paying users. That means 700 / 350 / 140 active users at 1 / 2 / 5% conversion.
  - Fixed costs ($9.50–$27.50) are correct.
  - The Round 1 contribution margin should read about −$0.05 to −$0.63, not −$0.06 to −$0.60. This is minor rounding and does not change any conclusion.
  - The Round 1 "cash to get ready $60–$330" counted 6–12 months of running costs as setup cost. The Round 2 figure of about $30–$55 (1–2 months at $27.50) is the right one.
  - Bottom line: cash is not the constraint. About 30–70 maintainer hours plus a week of monitoring is.

## The single biggest risk
**Users' data crossing between accounts on the live public endpoint.**

Three gaps combine here:
- In the OAuth path that Claude actually uses, `REQUIRE_AUTH=false` puts everyone into `org_id="default"`, or into any org the client names in an `x-org-id` header (`gateway.py:4751-4753`).
- The `/ws` feed broadcasts events from every tenant to any valid key.
- The isolation tests only use API keys, never the claude.ai OAuth flow.

This risk outranks the privacy-policy gap. The policy is a sure rejection, but rewriting it is cheap. A leak harms real users, and the maintainer cannot write an honest privacy policy without first knowing where data lives and who can see it. A second, related gap: with auth on, the consent page asks a stranger to "Enter API Key", and no one has documented how a stranger gets one. If that has no answer, directory users cannot use the connector at all.

## Conditions (if GO WITH CONDITIONS)
Not applicable, since the verdict is NO-GO. These are the gates for reopening it. All six must pass before the Listing is submitted. The fields can be drafted now, because the slug only becomes permanent on submission.
1. **Steering and claims removed.** The "Usage guidelines" block and the "<1ms / 100% token savings / $ saved" claims are gone from `mcp/server.py`. The live `/mcp` instructions are confirmed to contain none of it.
2. **Live auth confirmed.** The Render deployment runs with `REQUIRE_AUTH=true` and without the insecure-exposure flag, on an always-on paid instance with persistent disk.
3. **Isolation proven over OAuth.** Two separate accounts connect through the claude.ai custom-connector OAuth flow, not API keys, and have zero cross-reads. `/ws` either returns 401 without credentials and only that tenant's events with them, or is disabled on the hosted deployment.
4. **Hosted privacy policy and docs published.** Both are at public URLs and state the actual data location, retention, and how a user deletes their data. They also explain how a new user gets access (the API-key onboarding).
5. **Local-only tools removed.** `replay_tool` and `record_tool` are removed or rescoped for the remote connector. The other tools pass in MCP Inspector against the HTTPS URL. The `gpt-4o` default model is removed or justified.
6. **Reviewer access ready.** A test account (API key plus seeded entries) is provisioned and survives a redeploy. The `server.json` and `pyproject.toml` versions match.

## Three cheapest next tests (≤ 2 weeks each)
| Test | How | Result that means continue | Result that means stop |
|---|---|---|---|
| Clean-instructions end-to-end connect | Delete the steering and marketing lines, redeploy, and add the Render URL as a custom connector in claude.ai with a brand-new account. Ask 5 unrelated questions and 5 cache-relevant ones. | OAuth completes, including DCR accepting the claude.ai callback. A new user can get access without the maintainer's help. Tools are called only on the relevant questions. | OAuth fails from claude.ai, or the only way for a stranger to get a key is a manual request to the maintainer, with no fix within 2 weeks. |
| Two-account isolation via OAuth, plus `/ws` | Account A stores an entry and account B queries and searches for it. Try B with an `x-org-id` header set to A's org. Open `/ws` with no credentials, then with B's key, while A is active. | Zero entries visible across accounts. The header override is rejected. `/ws` returns 401 without credentials and none of A's events with B's key. | Any cross-tenant read or event leak that can't be fixed and retested within the 2 weeks. |
| Reliability and persistence | External uptime pings for 7 days, p95 tool-call latency measured, one deliberate redeploy mid-week. | ≥ 99% uptime, p95 < 2 s, login tokens and the test account's data still present after the redeploy. | Data or sessions are lost on redeploy and the maintainer won't pay for an always-on instance with disk (about $27.50 a month). |

## What would flip this verdict
- **To GO:** all six gates above pass, with the hosted privacy policy and docs URLs live and the two-account OAuth test passing on the production URL. Then filling in the Listing is routine. Write the One-liner and Description around shared semantic memory and recall across sessions, not cost savings, because subscription users get no dollar benefit (Investor's point, conceded by everyone).
- **To a firmer, longer-term NO-GO:** any of these:
  - the live deployment turns out to be running with auth off, or on the free tier with temporary disk;
  - the OAuth isolation test leaks data;
  - there is no workable way for strangers to get access;
  - the maintainer decides not to take on custody of users' data and ongoing hosting with no revenue. If so, the honest path is to keep OmniCache as a local PyPI/stdio tool and not list it in the directory.

## Where the council agreed / disagreed
- **Agreed:**
  - It is not ready to submit today. All three said so; the Believer's own score for "ready now" is 1/5.
  - Only the remote connector can be submitted.
  - The current privacy policy disqualifies it.
  - The steering instructions must go (the Believer conceded, and all three saw them live).
  - Don't spend the permanent slug until the fixes pass.
  - Cash is not the constraint; maintainer time and data custody are.
  - The "$ saved" pitch doesn't apply to subscription Claude users.
- **Still disputed:**
  - Whether the deployed server actually runs with auth on. The Believer says the Dockerfile and startup checks make insecure mode take deliberate effort. The Skeptic and Investor point to the `false` default and the audit's Uvicorn caveat. Nobody could reach the endpoint, so only the live tests can settle it.
  - How long the fixes take: Believer about 1–2 weeks [Guess], Investor 30–70 hours plus 7 calendar days of monitoring.
  - Whether a listing is worth it with no revenue line. The Believer calls it a fine niche free utility; the Investor calls it "marginal, not yet worth doing."

Files reviewed: /home/user/agent-council/council/2026-10-01-omnicache-mcp-submission/brief.md, round1-believer.md, round1-skeptic.md, round1-investor.md, round2-believer.md, round2-skeptic.md, round2-investor.md (all in that directory).
