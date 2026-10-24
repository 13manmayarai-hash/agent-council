# OmniCache: Listing step (3 of 10), final values

**Status (2026-10-02):** ready to submit. All six gates in `verdict.md` were closed after the council session:
- **Code:** omnicache-proxy PR #4, plus later commits up to `90248c5` on `main`; all 370 tests pass.
- **Live checks (run by the owner and reported in chat):**
  - two Google accounts can't read or search each other's entries, and passing another account's `org_id` is rejected;
  - the claude.ai custom-connector test passed end to end;
  - the hosted endpoint lists 6 tools with no steering text.

The slug `omnicache` becomes permanent once you submit.

## Listing

**Name**
```
OmniCache
```

**Slug**
```
omnicache
```

**One-liner** (127 / 200 characters)
```
Shared semantic memory for Claude: store useful answers, snippets and notes, then search and recall them across conversations.
```

**Description** (1,553 / 2,000 characters)
```
OmniCache gives Claude a persistent, searchable memory that belongs to your account. Save answers, code snippets, configuration notes and documentation once, and Claude can find and reuse them in later conversations instead of starting from scratch.

What you can do:
- Store knowledge: ask Claude to save a solution, snippet or note to OmniCache, with an optional tag such as "networking" or "auth".
- Search your memory: find earlier entries by meaning, not just exact words. For example, "how did we handle refresh-token rotation?" finds a note titled "OAuth token expiry fix".
- Check for an existing answer: Claude can look up whether a closely matching question has already been answered and saved.
- Clean up: remove entries by tag when they are out of date. This is the only tool that deletes data and is marked as destructive.
- See usage and health: view how many entries you have, hit rates, and whether the service is ready.

Entries are private to your account and are not shared with other users. Sign-in uses OAuth with Google. Saved entries expire after 7 days by default, or up to 30 days if you set a longer time-to-live.

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

**Author URL** (the owner confirmed it serves the OmniCache landing page)
```
https://omnicache.rawwgrid.com
```

**Icon:** leave it as is, so the directory uses the server's favicon.

## Links

**Documentation**
```
https://github.com/13manmayarai-hash/omnicache-proxy/blob/main/docs/HOSTED_CONNECTOR.md
```

**Support**
```
https://github.com/13manmayarai-hash/omnicache-proxy/issues
```

**Privacy policy**
```
https://github.com/13manmayarai-hash/omnicache-proxy/blob/main/docs/HOSTED_PRIVACY_POLICY.md
```

## For later steps (server URL, reviewer notes)

**Connector / server URL**
```
https://omnicache.rawwgrid.com/mcp
```

**Reviewer notes**
```
Sign in: choose "Sign in with Google" on the OmniCache consent page when connecting. A new, isolated workspace is created automatically for each Google account; no API key or manual approval is needed.

Sample data: entries are private to each account, so a new Google sign-in starts with an empty workspace. Ask Claude to store a note, then query or search for it. To see pre-loaded examples instead, paste the reviewer API key provided in this submission into the "OmniCache API Key" box on the same consent page. That workspace holds three entries until November 1, 2026: SQLAlchemy connection pooling (tag: database), Python exponential backoff with tenacity (tag: python), and Docker multi-stage caching (tag: devops).

Retention: entries expire after 7 days by default (up to 30 days with a custom time-to-live).

Tested end to end as a claude.ai custom connector: OAuth with PKCE, tool discovery (6 tools), store, exact and reworded query, search, and tag-based deletion.
```

**Reviewer API key:** put it in the form's credentials or test-account field, never in this file or the repo. It must belong to the workspace that holds the 3 sample entries and be a regular tenant key, not the admin key. If you'd rather not issue one, delete the last two sentences of the Sample data paragraph.

Steps 4–10 weren't shown in your screenshots. If they ask for something not covered here, send a screenshot and I'll draft it.
