# Brief: Is OmniCache ready for MCP directory submission to Claude?

## The user's request (verbatim)
"audit OmniCache proxy and whether it is ready for mcp submission to Claude. Make the submission form ready in the image you refer for the form"

## Context the user provided
- Project: the user's repo https://github.com/13manmayarai-hash/omnicache-proxy (public). A read-only checkout is at /home/user/13manmayarai-hash/omnicache-proxy (latest commit cde34f3, 2026-09-29). Relevant files include README.md, mcp/README.md, mcp/server.py, server.json, smithery.yaml, PRIVACY.md, SECURITY.md, docs/.
- Which transport is being submitted (local stdio, remote HTTP, or both): not specified by the user. The repo's server.json lists both a PyPI stdio package and a remote `streamable-http` URL (https://omnicache-proxy.onrender.com/mcp).
- The user attached two screenshots of the submission form, open in a claude.ai "Submissions" page. A transcription of what the screenshots show follows.

## Submission form, as shown in the user's screenshots (transcribed)
Header: "Draft saved in this tab · 6 minutes ago". Section dropdown: "3. Listing". "Step 3 of 10". Steps 1–2 and 4–10 are not shown.

**Listing** — "How your MCP server appears in the directory. You can edit this after you submit."
| Field | Required | Current value / placeholder | Help text |
|---|---|---|---|
| Name | yes | OmniCache (filled) | — |
| Slug | yes | omnicache (filled) | Permanent after submission. Lowercase letters, numbers, and hyphens. |
| One-liner | yes | empty ("A short tagline for your MCP server") | 0 / 200 characters |
| Description | yes | empty ("Describe what your MCP server does and its key features…") | 0 / 2000 characters |
| Categories | yes | empty ("Select categories") | Categories are used to filter MCP servers in the directory. Select up to 5. |
| Author name | no | empty ("Acme Inc.") | Shown as "by …" on the listing. |
| Author URL | no | empty ("https://example.com") | If left blank, these default to your company name and website. |
| Icon | no | "Add custom icon URL" button | The directory and Claude show the favicon from your server's URL; we recommend leaving it at that. A custom icon replaces it in the directory listing only. |

**Links** — "Help users learn more and get support."
| Field | Required | Placeholder | Help text |
|---|---|---|---|
| Documentation | yes | https://docs.example.com | Public-facing docs shown to users. IT admins often review these when deciding whether to approve an MCP server. |
| Support | yes | support@example.com or https://support.example.com | A support URL or email address. |
| Privacy policy | yes | https://example.com/privacy | — |

The category options in the dropdown were not shown in the screenshots.

## Question for the council
Is OmniCache ready to submit to Claude's MCP directory now? What must change first? The orchestrator will fill in the Listing fields from the repo after the verdict.
