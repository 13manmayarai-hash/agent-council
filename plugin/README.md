# Agent Council

A four-agent decision council for Claude: **Believer**, **Skeptic**, **Investor** and **Judge**.
Give it an idea or a decision. It argues both sides, works through the money, spot-checks the
sources it cites, and returns a verdict with the single biggest risk and the three cheapest tests
to run next.

## Install

In Claude Code:

```
/plugin install agent-council --marketplace 13manmayarai-hash/agent-council
```

Once it's listed in Anthropic's plugin directory, you can also add **Agent Council** from there.

## Use

```
/agent-council:council Should I launch QuickCart in Siliguri with 10 small grocery vendors, cash on delivery only, ₹25 delivery fee?
```

You can also put a longer brief in a file and pass its path:

```
/agent-council:council briefs/quickcart.md
```

The council checks your brief for six things: the idea, the customer, the problem, price and costs, evidence so far, and location and currency.
If three or more are missing, it asks you up to three short questions first. "Unknown" is an accepted answer.

After you run the tests a verdict recommends, bring the results back:

```
/agent-council:council revisit council/2026-10-09-quickcart Talked to 12 vendors: 9 agreed to a 2-week trial; 40 orders in week one.
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

## What it reads, sends and writes

- **Web:** the Believer, Skeptic and Investor use web search and open web pages to find and check facts.
  The Judge opens only the pages the members cited. Your brief's topic is sent to the web search tool as search queries.
- **Files:** each session is saved in your project under `council/<date>-<topic>/`. A session holds
  `brief.md`, six argument files and `verdict.md`. The members write only to that folder.
- **Nothing else:** no servers, scripts, hooks, telemetry or third-party services beyond Claude's own web search and fetch tools.

## Getting better results

- Put real numbers in the brief: prices, costs, how many customers you've talked to, location.
  A brief with no data usually gets TEST FIRST, because the council can only weigh evidence that exists.
- Each run makes seven subagent calls, so it uses noticeably more of your usage than a normal message.

## License

MIT. See [LICENSE](LICENSE).
