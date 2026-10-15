## Believer — Round 1
**Thesis:** OmniCache is closer to directory-ready than most first-time submissions. The remote HTTP server already has the hard parts in place (Streamable HTTP, OAuth with discovery, DCR and PKCE, annotations on every tool). What remains is a short list of fixes to the docs and the hosted service, not new engineering. It should be submitted as a **remote** connector once those are done.

**Top 3 reasons it can work**
1. **The code meets Anthropic's core technical requirements.** Anthropic requires the server to be remote over HTTPS, use OAuth 2.0 for authenticated services, and give every tool a `title` plus `readOnlyHint` or `destructiveHint` ([Fact] https://claude.com/docs/connectors/building/submission). In the repo:
   - All 8 tools in `/home/user/13manmayarai-hash/omnicache-proxy/mcp/server.py` carry a `title` and both hints, and `omnicache_invalidate` is correctly marked `destructiveHint: true` [Fact, from code].
   - `server/gateway.py` routes `/mcp` (GET/POST/DELETE), both `/.well-known` OAuth metadata endpoints, `/oauth/register` (DCR), `/oauth/authorize` and `/oauth/token` (lines 5589–5600) [Fact, from code].
   - The redirect allowlist includes `https://claude.ai` [Fact, gateway.py:183–215].
   - Tests cover PKCE S256, code-replay rejection, scope enforcement (read vs admin) and tenant isolation [Fact, `tests/test_phase4_remote_mcp.py`].
   - Confidence 4.
2. **The bar to get listed is reachable.** Approved submissions are listed as "Community" by default after an automated policy scan. Human review applies only to some submissions [Fact, same doc]. A clean, well-annotated server does not need Verified status to reach users. Confidence 3.
3. **Most of the listing material already exists.** There is a privacy policy (`PRIVACY.md`, `docs/PRIVACY_POLICY.md`) with a contact, retention and deletion rights. `mcp/README.md` has setup instructions and 3 example prompts, and `SECURITY.md` is in place [Fact, from repo]. Once a few gaps are fixed, the One-liner, Description, Documentation, Support and Privacy fields can all be filled from these files. Confidence 4.

**Honest caveats I'm carrying in, not hiding**
- Local stdio servers can no longer be submitted on their own [Fact, submission doc]. The PyPI stdio package is not what gets submitted.
- **This is the biggest risk.** `PRIVACY.md` describes a "local-only, 127.0.0.1" product, but a remote Render endpoint stores user prompts on the maintainer's server. The policy has to be rewritten for the hosted service. Anthropic says incomplete privacy policies lead to immediate rejection [Fact, submission doc].
- I could not reach `omnicache-proxy.onrender.com` (my network blocked it). Whether the endpoint is live, and how it behaves on cold start, is unverified [Fact].
- Reviewers need a test account, and none is documented [Assumption].
- Tool descriptions promise "<1ms" and "100% token savings", and default to `gpt-4o`. Reviewers may read those claims as inaccurate [Assumption].

**Best realistic outcome:** After about 1–3 days of fixes (hosted privacy policy, a live endpoint, a test account, toned-down tool descriptions), OmniCache is listed as a Community connector [Guess]. It would be a small niche listing for developers who want shared semantic memory in Claude, not a breakout.

**What would prove me wrong:** If the Render endpoint fails an end-to-end connection as a custom connector in claude.ai, the OAuth layer is unproven in practice and readiness drops sharply. That covers failures such as cold-start timeouts, wrong metadata URLs, or DCR rejecting `https://claude.ai/api/mcp/auth_callback`.

Sources:
- [Submit a connector to the directory – Claude docs](https://claude.com/docs/connectors/building/submission)
- [Anthropic Software Directory Policy](https://support.claude.com/en/articles/13145358-anthropic-software-directory-policy)
