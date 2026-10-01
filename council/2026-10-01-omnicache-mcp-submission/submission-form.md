# OmniCache — Listing step (3 of 10), ready-to-paste values

> **Don't press Submit yet.** The council's verdict is NO-GO until the six gates in `verdict.md` pass. The slug `omnicache` becomes permanent once you submit. These values are drafts you can paste into the saved form now. The Description describes the connector **after** the fixes: `replay_tool` and `record_tool` removed, and per-account isolation over OAuth proven. Fields marked ⚠️ depend on a gate.

Facts come from the repo (`pyproject.toml`, `server.json`, `mcp/server.py`). The copy follows the verdict: it's about shared memory and recall, not cost savings, and makes no "<1ms" or "100% token savings" claims.

## Listing

**Name** (already filled)
```
OmniCache
```

**Slug** (already filled; permanent after submission)
```
omnicache
```

**One-liner** (127 / 200 characters)
```
Shared semantic memory for Claude: store useful answers, snippets and notes, then search and recall them across conversations.
```

**Description** (1,448 / 2,000 characters) ⚠️ The isolation sentence is only true once gate 3 passes.
```
OmniCache gives Claude a persistent, searchable memory that belongs to your account. Save answers, code snippets, configuration notes and documentation once, and Claude can find and reuse them in later conversations instead of starting from scratch.

What you can do:
- Store knowledge: ask Claude to save a solution, snippet or note to OmniCache, with an optional tag such as "networking" or "auth".
- Search your memory: find earlier entries by meaning, not just exact words. For example, "how did we handle refresh-token rotation?" finds a note titled "OAuth token expiry fix".
- Check before answering: Claude can look up whether a closely matching question has already been answered and saved.
- Clean up: remove entries by tag when they are out of date. This is the only tool that deletes data and is marked as destructive.
- See usage and health: view how many entries you have, hit rates, and whether the service is ready.

Your entries are isolated to your own account and are not shared with other users. Sign-in uses OAuth.

Example prompts:
- "Save our standard API rate-limiting config to OmniCache under the tag networking."
- "Search OmniCache for anything we stored about SQLite WAL connection pooling."
- "Delete the OmniCache entries tagged legacy-auth."

OmniCache is also available as an open-source, local-first proxy for coding agents (pip install omnicache-proxy). This connector is the hosted version for use inside Claude.
```

**Categories** (pick up to 5 from the dropdown; its options weren't visible in your screenshot)
Choose the closest matches to these, in order: **Developer tools**, **Knowledge / memory**, **Productivity**, **Search**.

**Author name**
```
Rajiv Prasad
```
(Source: `pyproject.toml` authors and the LICENSE copyright.)

**Author URL**
```
https://omnicache.rawwgrid.com
```
(Source: `pyproject.toml` "Website". Check that it loads. If it doesn't, use `https://github.com/13manmayarai-hash`.)

**Icon:** leave as is. The form recommends using the favicon from your server's URL.

## Links

**Documentation** ⚠️ gate 4
```
https://github.com/13manmayarai-hash/omnicache-proxy/blob/main/mcp/README.md
```
This is the best existing page, but it only covers local stdio setup and never mentions the hosted endpoint. Before submitting, add a hosted-connector page that covers the connector URL, how a new user gets access (API-key onboarding), what each tool does and example prompts, and link to that page instead.

**Support**
```
https://github.com/13manmayarai-hash/omnicache-proxy/issues
```
(Source: `pyproject.toml` "Issues". Alternative: `13manmayarai@gmail.com`, the author email in `pyproject.toml`.)

**Privacy policy** ⚠️ gate 4, a blocker
```
https://github.com/13manmayarai-hash/omnicache-proxy/blob/main/PRIVACY.md
```
**Don't submit this URL as the file stands.** `PRIVACY.md` and `docs/PRIVACY_POLICY.md` both say OmniCache is local-only and never sends prompts to any server. That is false for the hosted connector, and an inaccurate privacy policy gets a submission rejected immediately. First rewrite the policy for the hosted service. It needs to cover:
- what gets stored (prompts, answers and tags you save)
- where it is stored (the Render region, and whether the disk is persistent)
- how long it is kept
- who can access it
- how a user deletes their data
- a contact address

Then put that policy's URL here.

## Steps 4–10
Your screenshots don't show these steps. The council's sources say the review also asks for a reviewer test account (an API key plus some sample entries that survive a redeploy; see gate 6). Send screenshots of the later steps and I'll draft them the same way.
