## Investor — Round 1

Currency is USD. The brief names no currency and all vendor prices are in USD.

**What the money depends on:** Anthropic's directory accepts **remote HTTPS servers only**. "A local server can't be submitted on its own" [Fact, https://claude.com/docs/connectors/building/submission]. That means the PyPI stdio package earns nothing here. The only thing that can be listed is `https://omnicache-proxy.onrender.com/mcp` [Fact, server.json], and that is a server the maintainer must pay for and run for every directory user.

**Unit economics (per remote user per month)**
| Item | Value | Tag/source |
|---|---|---|
| Revenue per user | $0 | [Fact] The repo has no pricing, plans or billing code (grep of repo). License is FSL-1.1-MIT (server.json) |
| Storage per user | low 5 MB / likely 50 MB / high 500 MB, so about $0.001 / $0.0125 / $0.125 | [Assumption] size; [Fact] Render disk costs $0.25/GB-mo ([fly.io comparison](https://fly.io/learn/paas-pricing-compared/)) |
| Compute per user | about $0.05–$0.50 | [Assumption] Each tenant's in-memory vector index needs RAM. I assume roughly 50–500 active tenants fit on a 512 MB–2 GB instance |
| Contribution margin | **about -$0.06 to -$0.60** | $0 minus the two rows above |

**Monthly fixed costs**
| Item | Value | Tag |
|---|---|---|
| Always-on instance | $7 (Starter) to $25 (Standard) | [Fact] [Render pricing summary](https://deploycloud.app/blog/render-pricing). The free tier sleeps after 15 min and takes about 1 min to wake ([Render](https://render.com/articles/platforms-with-a-real-free-tier-for-developers-in-2026)) |
| Persistent disk, 10 GB | $2.50 | [Fact] rate × [Assumption] size |
| Maintainer time (support, security fixes) | 5 / 10 / 20 h | [Assumption]. No cash cost, but a real opportunity cost |
| **Cash total** | **about $9.50–$27.50** | |

I could not reach the live endpoint (egress blocked), so I can't confirm which Render plan it runs on. If it is on the free tier, the SQLite cache on its temporary disk is lost whenever the service restarts, so a reviewer's "fully populated test account" won't keep its data.

**Break-even:** It never breaks even at $0 revenue, and every extra user widens the loss. If a paid tier existed, here is a hypothetical: $5/mo [Assumption], minus Stripe 2.9% + $0.30 ([Stripe pricing](https://stripe.com/pricing)) = $4.555. Minus about $0.06 variable cost = **about $4.50 contribution**. $27.50 ÷ 4.50 = 6.1, so **7 paying users**. At a free-to-paid conversion of 1 / 2 / 5% [Assumption], that needs 700 / 350 / 140 active users.

**Cash to get ready to submit:** about **$60–$330**. That is 6–12 months of hosting at $9.50–$27.50 a month. On top of that come about 20–60 engineering hours [Assumption] to fix four things:
- **Privacy policy.** PRIVACY.md says data is "local storage only" and that nothing is transmitted "to OmniCache maintainers". The hosted endpoint contradicts both, and an incomplete privacy policy is grounds for immediate rejection [Fact, submission doc].
- **Version mismatch.** server.json says 3.0.5 but pyproject.toml says 3.1.0 [Fact, repo].
- **Reviewer test account.** One must be provisioned.
- **Persistent storage.** It needs to be in place.

Cash is not the constraint. The maintainer's time is.

**The number that breaks the model:** the value delivered per cache hit to Claude directory users. The pitch is "100% token savings" and "$0.00" (README, mcp/README). Those savings may not apply inside Claude, for two reasons:
- **claude.ai users pay a flat subscription** [Fact, they need a Claude plan], not per token. The "$ saved" counter therefore saves them no money.
- **A cache hit still uses tokens.** The cached answer comes back as a tool result and is read into Claude's context [Assumption, how MCP works], and Claude still writes its reply.

If net tokens saved per hit is about 0 or negative, nobody has a reason to keep the connector, and no conversion rate fixes that.

**My investment condition:** "I would invest if all of the following are proven:
- the remote endpoint runs on an always-on paid instance with persistent disk;
- it passes 7 days of external uptime checks with p95 tool-call latency under 2 s;
- the hosted-data privacy policy is published;
- after listing, at least 100 weekly active remote connections are retained for 4 weeks."

**Verdict from the numbers:** **Unattractive as a business, Marginal as a distribution play.** Getting listed costs little cash, but there is no revenue line. Each user adds hosting cost and data-custody liability. The headline cost-saving claim doesn't hold for subscription Claude users. The fixes should come before the permanent slug is spent.

Sources:
- [Submit a connector to the directory](https://claude.com/docs/connectors/building/submission)
- [Anthropic Software Directory Policy](https://support.claude.com/en/articles/13145358-anthropic-software-directory-policy)
- [Render free tier article](https://render.com/articles/platforms-with-a-real-free-tier-for-developers-in-2026)
- [Render pricing summary (DeployCloud)](https://deploycloud.app/blog/render-pricing)
- [PaaS pricing compared (fly.io)](https://fly.io/learn/paas-pricing-compared/)
- [Stripe pricing](https://stripe.com/pricing)
- Repo files: /home/user/13manmayarai-hash/omnicache-proxy/server.json, /home/user/13manmayarai-hash/omnicache-proxy/pyproject.toml, /home/user/13manmayarai-hash/omnicache-proxy/PRIVACY.md, /home/user/13manmayarai-hash/omnicache-proxy/mcp/README.md
