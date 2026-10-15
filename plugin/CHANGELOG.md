# Changelog

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
