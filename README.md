# Agent Council for Claude Code

A four-agent decision council: **Believer**, **Skeptic**, **Investor** and **Judge**.
Give it an idea or decision; it argues both sides, checks the money, and returns a verdict
with the biggest risk and the three cheapest tests to run next.

## Install
**As a plugin (recommended):** the plugin lives in the [`plugin/`](plugin/) folder.
- In Claude Code: `/plugin install agent-council --marketplace 13manmayarai-hash/agent-council`
- From the plugin directory on claude.ai, once it's listed, add **Agent Council**.
- Or load it locally in Claude Code with `claude --plugin-dir ./plugin`.

As a plugin, the command is `/agent-council:council` and the members are `agent-council:believer` and so on.

**Copying the files:** copy `plugin/agents/` and `plugin/skills/` into the `.claude/` folder of any repo,
or into `~/.claude/` to use it in every project. The command is then `/council`. This repo's own
`.claude/agents` and `.claude/skills` are links to `plugin/`, so `/council` works in this repo too.

## Use
```
/council Should I launch QuickCart in Siliguri with 10 small grocery vendors, cash on delivery only, ₹25 delivery fee?
```
or put a longer brief in a file and run `/council briefs/quickcart.md`.

After you run the tests a verdict recommends, bring the results back:
```
/council revisit council/2026-10-09-tracegate-mvp Scanned 5 teams' PRs: 2 had broken-but-merged agent PRs; 1 team agreed to a paid pilot.
```
This runs a fresh council on the original brief plus your new results, saves it in a new folder, and the Judge says what changed.

## How it runs
1. **Round 1:** Believer, Skeptic and Investor answer the brief in parallel, without seeing each other.
2. **Round 2:** each sees the other two and replies once, conceding where proven wrong.
3. **Verdict:** the Judge spot-checks up to 5 cited sources, weighs the evidence (not the majority) and rules GO / GO WITH CONDITIONS / TEST FIRST / NO-GO.
   - **TEST FIRST** means nothing known kills the idea but the deciding facts are missing; run the tests before committing more.
   - **NO-GO** means a known blocker, such as numbers that don't work at sourced rates.

Everything is saved to `council/<date>-<slug>/` (brief, six arguments, verdict), so you can review or rerun later.

## Rules every agent follows
- Every claim is tagged **[Fact]** (with source), **[Assumption]** or **[Guess]**. No invented numbers.
- Skeptic must give a cheap test for each risk. Investor must show arithmetic.
- Judge does no new research. It opens only the sources members cited, and marks unsupported claims as unsupported.

## Better results
- Put real data in the brief: prices, costs, how many vendors/customers you've talked to, location.
  The council can only weigh what exists — a thin brief gets a cautious verdict.
- Believer, Skeptic and Investor use web search to check facts; results depend on what's publicly findable.
- Each run makes seven subagent calls, so it uses noticeably more of your usage than a normal message.
- To change a model per agent, add `model: opus` (or `sonnet`, `haiku`) to that agent's frontmatter.

## License
MIT. See [LICENSE](LICENSE).

## Changelog
See [plugin/CHANGELOG.md](plugin/CHANGELOG.md).
