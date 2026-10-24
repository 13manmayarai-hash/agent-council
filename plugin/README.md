# Verdict Council

A four-agent decision council for Claude: **Believer**, **Skeptic**, **Investor** and **Judge**.
Give it an idea or a decision. It argues both sides, works through the money, spot-checks the
sources it cites, and returns a verdict with the single biggest risk and the three cheapest tests
to run next.

## Install

In Claude Code:

```
/plugin marketplace add 13manmayarai-hash/agent-council
/plugin install verdict-council@verdict-council
```

Once it's listed in Anthropic's plugin directory, you can also add **Verdict Council** from there.

## Use

```
/verdict-council:council Should I launch QuickCart in Siliguri with 10 small grocery vendors, cash on delivery only, ₹25 delivery fee?
```

You can also put a longer brief in a file and pass its path:

```
/verdict-council:council briefs/quickcart.md
```

Add `--quick` or `--deep` first to choose the council level yourself, for example
`/verdict-council:council --deep Should I quit my job to run QuickCart full time?`

The council checks your brief for six things: the idea, the customer, the problem, price and costs, evidence so far, and location and currency.
If three or more are missing, it asks you up to three short questions first. "Unknown" is an accepted answer.

After you run the tests a verdict recommends, bring the results back:

```
/verdict-council:council revisit council/2026-10-09-quickcart Talked to 12 vendors: 9 agreed to a 2-week trial; 40 orders in week one.
```

This runs a fresh council on the original brief plus your new results. It saves the session in a new
folder and never overwrites the earlier one, and the Judge says what changed.

## Example

Brief: *"Is selling how-to / self-help e-books to English-speaking buyers through Facebook and Instagram ads worth pursuing?"* No numbers yet.

> **Verdict:** NO-GO · **Confidence:** 4
>
> **One-line reason:** At benchmark rates, every member's numbers show a cheap e-book costs about 2.4 to 5.5 times more in ads to sell than it earns. The only version that could work needs a higher-priced follow-up product, and the user hasn't built or tested one.

The biggest risk it named: a $17 book nets about $14–15 after fees, while ads cost about $50–78 per sale at sourced click and conversion rates. Its three next tests, summarised:

| Next test | Continue if | Stop if |
|---|---|---|
| Search Meta Ad Library for 3–5 narrow topics (free) | A niche has several advertisers running ads 3+ months, but isn't saturated | No niche has long-running offers, or all are saturated |
| Pre-sell a $100+ follow-up product to about 20 warm contacts | 2–3 paid pre-orders | Zero pre-orders |
| A capped ad test (about $500) | Click-through of at least 1% and about $35 or less per sale | Click-through under 1%, or more than $50 per sale |

The full session holds the brief, six arguments with sources and the verdict. See [pull request #4](https://github.com/13manmayarai-hash/agent-council/pull/4) in this repo.

## How it works

0. **Setup:** the council picks a level and checks that web search and opening web pages work.
   If they don't, it tells you, and the verdict carries an evidence warning instead of resting quietly on unchecked sources.
1. **Round 1:** the Believer, Skeptic and Investor answer the brief in parallel, without seeing each other.
   - The Believer makes the strongest honest case for the idea.
   - The Skeptic finds how it fails and gives a cheap test for each risk.
   - The Investor works out unit economics, break-even and cash needed, showing the arithmetic.
2. **Round 2:** each member reads the other two and replies once, conceding where it was shown wrong.
3. **Verdict:** the Judge opens up to 5 of the sources the members cited to check them, weighs the
   evidence rather than the majority, and rules one of:
   - **GO**
   - **GO WITH CONDITIONS**
   - **TEST FIRST:** nothing known kills the idea, but the deciding facts are missing
   - **NO-GO:** a known blocker exists, such as numbers that don't work at sourced rates

Every claim is tagged **[Fact]** with a source, **[Assumption]** or **[Guess]**. The council doesn't invent numbers.
Members treat web pages and files as evidence, never as instructions. Every verdict ends with a reminder that it is decision support, not financial, legal or investment advice.

## Council levels
Before Round 1 the council picks a level, which decides the model each member runs on. It weighs the money at risk,
how hard the decision is to undo, and how much real evidence the brief has, then tells you which level it picked.

| Member | Quick | Standard | Deep |
|---|---|---|---|
| Believer | Haiku | Sonnet | Opus |
| Skeptic | Haiku | Sonnet | Opus |
| Investor | Sonnet | Opus | Opus |
| Judge | Opus | Opus | Opus |

The Judge always runs on Opus. To choose the level yourself, put a flag first:
`--quick` for a cheap first look, `--deep` for a big or hard-to-undo decision.

## What it reads, sends and writes

- **Web:** the Believer, Skeptic and Investor use web search and open web pages to find and check facts.
  The Judge opens only the pages the members cited. Your brief's topic is sent to the web search tool as search queries.
- **Files:** each session is saved in your project under `council/<date>-<topic>/`. A session holds
  `brief.md`, `run.md` (level, models and web status), six argument files and `verdict.md`. The members write only to that folder.
- **Nothing else:** no servers, scripts, hooks, telemetry or third-party services beyond Claude's own web search and fetch tools.

## Getting better results

- Put real numbers in the brief: prices, costs, how many customers you've talked to, location.
  A brief with no data usually gets TEST FIRST, because the council can only weigh evidence that exists.
- Each run makes seven subagent calls, so it uses noticeably more of your usage than a normal message.
  `--quick` uses less; `--deep` uses the most.

## License

MIT. See [LICENSE](LICENSE).
