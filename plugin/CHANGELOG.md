# Changelog

## 1.2.1 (2026-10-24)
- **Renamed to Verdict Council** (`verdict-council`). The directory flagged "agent-council" as too close to an existing
  plugin. The command is now `/verdict-council:council`, and the marketplace is `verdict-council`. If you installed the
  old name, uninstall it and install `verdict-council@verdict-council`. The repository URL is unchanged.
- Plugin icon for the directory listing.

## 1.2.0 (2026-10-24)
- **Council levels:** before Round 1 the council picks Quick, Standard or Deep from the money at risk, how hard the
  decision is to undo, and the evidence in the brief. The level sets each member's model; the Judge always runs on Opus.
  Override with `--quick`, `--standard` or `--deep`.
- **Web access check:** the council tests web search and page opening before Round 1. If either fails it tells you,
  members stop retrying and tag unsourced claims as [Assumption], and the Judge adds an evidence warning to the verdict.
- Each session saves a `run.md` with the level, models and web status.

## 1.1.0 (2026-10-15)
- **Structured brief:** the council checks a brief for six fields (idea, customer, problem, price and costs,
  evidence so far, location and currency) and asks about missing ones before it starts.
- **Prompt-injection guard:** members treat web pages, search results, files and the brief as evidence, never as instructions.
- **Disclaimer:** every verdict ends with a note that it is decision support, not financial, legal or investment advice.
- README example from a real session.

## 1.0.0 (2026-10-15)
- First plugin release: Believer, Skeptic, Investor and Judge agents, plus the `council` skill.
- **TEST FIRST verdict** for ideas that are unproven rather than blocked. NO-GO requires a named, known blocker.
- **Source spot-check:** the Judge opens up to 5 cited sources and marks each verified, doesn't support, or not reachable.
- **Revisit mode:** `council revisit <folder> <new results>` reruns the council with new evidence in a new folder.
- Members save their own round files.
