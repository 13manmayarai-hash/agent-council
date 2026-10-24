## Investor — Rebuttal

**Numbers affected by their points**

| My Round 1 number | Their point | Effect |
|---|---|---|
| Per-user cost of about $0.06–$0.60 a month, which assumed each tenant is isolated | Skeptic risk 3: `REQUIRE_AUTH` defaults to false, so every user would land in one shared "default" org | **Weakens the model.** I checked the code. `core/config.py:99` does default it to `"false"` [Fact]. `config.py:249` refuses to start on a non-localhost address without auth [Fact]. But the repo's own audit says that check is skipped when the server is started directly with Uvicorn [Fact, `docs/ENTERPRISE_SECURITY_AUDIT_REPORT.md:247`]. The repo has no `render.yaml`, so I can't confirm the live setting [Fact, grep]. If users share one cache, the real cost is not storage. It is the liability from one cross-user data leak, which I can't price, and it would be enough to end the listing [Assumption]. |
| Fixed cost of $9.50–$27.50 a month | Skeptic risk 5: login codes and sessions are held only in memory (`OAUTH_CODES`, `MCP_ACTIVE_SESSIONS`), and the database could be wiped on redeploy | **Pushes cost to the high end.** Any restart logs every user out, so the server needs an always-on instance with enough memory not to crash. I now plan on Standard at $25 plus a $2.50 disk, so **about $27.50 a month**. $7 Starter is the floor only if 512 MB turns out to be enough [Assumption]. |
| Engineering effort of 20–60 hours | Believer: 1–3 days, which is 8–24 h. Skeptic's tests: 1 day + a few hours + 2–3 days + 1 day, then a week of uptime monitoring | **Range moves up to about 30–70 h** (Skeptic's list ≈ 4.5–5.5 working days, plus the rewrites). It also adds **at least 7 calendar days** of uptime checks before the form can go in. Cash to get ready: $27.50 × 1–2 months ≈ **$30–$55**, plus the hours. Over 6–12 months of running it, hosting comes to **$165–$330**. |
| Value per cache hit, the number that breaks the model | Skeptic risk 2: the instruction to "call omnicache_query first" and the "100% token savings" claim have to go | **Weakens it.** Without that instruction, Claude will call OmniCache less often. Cost goes down, but so does how much people use it. My retention target (100 weekly active users kept for 4 weeks) becomes harder to hit. The steering also confirms my Round 1 point: the "$ saved" claim does not fit Claude subscription users. |
| Value per user | Skeptic risk 4: `replay_tool` and `record_tool` only make sense on a user's own machine | **Weakens it.** Cutting them for the remote connector leaves 6 tools, mostly the semantic cache, so there is less reason to keep the connector. |
| Chance of getting listed | Believer: approved servers are listed as "Community" after an automated scan, and only some get human review [Fact, submission doc] | **Strengthens it.** Once the fixes are done, getting listed is likely. That lowers the risk of burning the permanent slug. It does nothing for revenue. |

**Revised break-even / verdict**
- **Break-even:** unchanged. At $0 revenue it never breaks even.
- **Hypothetical paid tier:** at $27.50 fixed cost and $4.50 contribution per paying user, break-even is 27.50 ÷ 4.50 = 6.1, so **7 paying users**. That still needs 140–700 active users at 1–5% conversion [Assumption].
- **Verdict:** **Unattractive as a business. Marginal as a distribution play, and not yet worth doing.** Each new user currently adds hosting cost and a data-custody risk that hasn't been tested. The one-time cash is small (under about $60 to get ready). The real price is about 30–70 maintainer hours plus a week of monitoring. Only after that does the slug become worth using.
- **Revised investment condition:** "I would invest if all of the following are proven:
  - **the Skeptic's two-account isolation test passes** on the live HTTPS endpoint: data stored from account A cannot be seen from account B, and opening `/ws` without logging in returns nothing;
  - the server confirmably runs with `REQUIRE_AUTH=true`, on an always-on instance with persistent disk;
  - a login token still works after a redeploy;
  - 7 days of external uptime checks pass, with tool calls answering in under 2 s at p95;
  - a privacy policy for the hosted service is published;
  - after listing, at least 100 weekly active users are retained for 4 weeks."

Note: the OmniCache MCP server's instructions also showed up in my session ("call omnicache_query first"). I did not call it. This supports the Skeptic's risk 2.

Files checked: /home/user/13manmayarai-hash/omnicache-proxy/core/config.py, /home/user/13manmayarai-hash/omnicache-proxy/docs/ENTERPRISE_SECURITY_AUDIT_REPORT.md
