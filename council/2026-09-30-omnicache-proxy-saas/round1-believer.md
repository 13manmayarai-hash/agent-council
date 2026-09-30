## Believer — Round 1

**Thesis:** OmniCache has a real problem and a real (if narrower than advertised) mechanism. The honest path to earning is as a paid add-on for teams that pay for AI coding agents per API token. It is not yet a SaaS, and the strongest case is for developers on per-token billing and teams that need to control spend.

**Top 3 reasons it can work**

1. **The pain is real and people pay for it.** [Fact] Several guides say Anthropic's docs put average Claude Code spend at about $13 per developer per active day, or about $100–200 per developer per month. Claude Code also has 5-hour and weekly usage caps, which many users hit ([morphllm](https://www.morphllm.com/claude-code-pricing), [ccforeveryone](https://ccforeveryone.com/guides/claude-code-limits-and-pricing)). [Assumption] A startup with 20 developers on API billing spends several thousand dollars a month. A tool that cuts that bill by even 15% pays for itself many times over. — confidence 4

2. **The main feature works: it removes repeated tool output from the conversation.** [Fact, verified in code] `compact_and_record_agent_tools` in `/home/user/13manmayarai-hash/omnicache-proxy/server/tool_replayer.py:972` scans the conversation history for repeated tool calls, such as re-reading an unchanged file or a clean `git status`. It shrinks the older copies and keeps the latest one, and every Anthropic request passes through it (`server/gateway.py:1387`). This is a real way to save input tokens. The provider's own caching does not do this, because it discounts repeated text but never removes it. [Assumption] This works with any agent that lets you change its API base URL, so there is almost no setup cost. — confidence 3

3. **The groundwork for charging and a protective license is already there.** [Fact] `server/quotas.py:69-114` defines Free, Pro (₹499 / $6), Scale (₹1,999 / $24) and Enterprise (₹5,999 / $70) tiers, and there are Razorpay upgrade tests. [Fact, from brief] The FSL-1.1-MIT license stops other companies from hosting it as a competing service. The code also includes Docker, Helm, Redis, audit logs and multi-tenant isolation. [Assumption] That makes a paid team tier (shared cache across teammates, a spend dashboard, an admin key) the natural thing to sell. Local-first, "your code never leaves your machine" is a selling point for companies that won't send code through a hosted gateway such as Helicone or Portkey. — confidence 3

**Best realistic outcome:** [Guess] A small, profitable business for one person. The free local tool brings people in, and a team or self-hosted tier sells to 50–300 small companies at $20–100 per seat. That is roughly $2k–$25k in monthly revenue within 12–18 months. Selling to large companies is a stretch. The current $6 Pro price is far too low for what it claims to save.

**Where I'm not defending the README:** Several of its claims go beyond what the code does. It cannot stop Claude Code from running tools on your machine, so "<0.1ms tool replay" does not reduce tokens by itself. Exact-match reuse of full responses will rarely trigger in a conversation that grows every turn. The "40–70%" figure has no measurement from real sessions behind it. Features like telephony, audio and P2P mesh are scope creep. The case above rests only on the history-trimming feature.

**What would prove me wrong:** Anthropic's cached input costs only 0.1x the normal rate, while cache writes cost 1.25–2x ([tensormesh](https://www.tensormesh.ai/learn/anthropic-prompt-caching-pricing)). Rewriting older messages changes the start of the prompt, which can make the provider's cache miss. If a measured A/B test on real Claude Code sessions shows that this raises the actual bill (cache writes plus lost 0.1x reads), the product loses money for its users and the case falls apart. Also, most Claude Code users pay a flat subscription rather than per token, so the "cut your bill" message may only reach a minority of the market.

Sources:
- https://www.morphllm.com/claude-code-pricing
- https://ccforeveryone.com/guides/claude-code-limits-and-pricing
- https://www.tensormesh.ai/learn/anthropic-prompt-caching-pricing
- Code: /home/user/13manmayarai-hash/omnicache-proxy/server/tool_replayer.py, /home/user/13manmayarai-hash/omnicache-proxy/server/gateway.py, /home/user/13manmayarai-hash/omnicache-proxy/server/quotas.py
