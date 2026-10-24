---
name: council
description: Run a 4-agent decision council (Believer, Skeptic, Investor, Judge) on an idea or decision and save the verdict to council/. Use only when the user runs the council command.
argument-hint: "[--quick | --standard | --deep] [idea or decision, path to a brief file, or: revisit <council folder> <new results>]"
disable-model-invocation: true
---

Run the decision council on this brief:

$ARGUMENTS

Follow these steps exactly. Do not argue the case yourself — you are only the orchestrator.

The four members are subagents named `believer`, `skeptic`, `investor` and `judge`. When this runs from the
installed verdict-council plugin they are listed as `verdict-council:believer`, `verdict-council:skeptic`,
`verdict-council:investor` and `verdict-council:judge`. Use whichever form appears in your available agent types.

## 0. Prepare the brief
- **Level flag:** if the argument starts with `--quick`, `--standard` or `--deep`, remove it and remember it
  for step 1. Everything after it is the brief (or a revisit) as usual.
- **Revisit:** if the argument starts with `revisit`, the next word is an earlier session folder
  (for example `council/2026-10-09-tracegate-mvp`) and the rest is the user's new results.
  - Read that folder's `brief.md` and `verdict.md`.
  - If the user gave no new results, ask what happened with the earlier tests, then continue.
  - Write a new brief containing: the original brief unchanged, then a "Previous verdict" section
    quoting the earlier verdict, confidence and three tests, then a "New results since <date>"
    section with only what the user reported.
  - Use a new folder named `council/<YYYY-MM-DD>-<original slug>-revisit`. Never overwrite the earlier one.
- If the argument is a file path, read that file as the brief.
- Check the brief against these six fields:
  1. **Idea:** what it is, in one or two sentences.
  2. **Customer:** who pays or uses it.
  3. **Problem:** what it solves for them today.
  4. **Price and costs:** what it would charge, and what it costs to deliver.
  5. **Evidence so far:** conversations, sign-ups, sales, tests run.
  6. **Location and currency.**
- If the idea itself is missing, or three or more fields are missing, ask the user one short message
  that lists the missing fields, at most 3 questions, with "unknown" as an accepted answer. Then continue.
  Don't ask about fields the user already answered.
- Write the final brief to `council/<YYYY-MM-DD>-<short-slug>/brief.md` using this layout:
  ```
  # Brief: <idea name>
  ## The user's words (verbatim)
  ## Idea
  ## Customer
  ## Problem
  ## Price and costs
  ## Evidence so far
  ## Location and currency
  ## Question for the council
  ```
  Under each heading put only what the user said or provided, or "Not provided". Don't add your own facts.

## 1. Pick the council level
The level decides which model each member runs on.

| Member | Quick | Standard | Deep |
|---|---|---|---|
| `believer` | haiku | sonnet | opus |
| `skeptic` | haiku | sonnet | opus |
| `investor` | sonnet | opus | opus |
| `judge` | opus | opus | opus |

- If the user gave a level flag, use it.
- Otherwise score the brief on three things, using only what it says:
  1. **Money at risk:** how much the user would commit, compared with what the brief says they have.
  2. **Reversibility:** whether the decision is easy to undo (a test, a side project) or hard
     (quitting a job, a lease, hiring, a loan, signing a contract, spending most of their savings).
  3. **Evidence in the brief:** real numbers, conversations and tests, or mostly ideas.
- Pick **Deep** if the decision is hard to reverse or puts a large share of the user's money at risk.
  Pick **Quick** only if it is cheap, easy to undo and exploratory. Otherwise, or if unsure, pick **Standard**.
- Never run the Judge on anything below opus, at any level.
- Tell the user in one line which level you picked and why, and that they can rerun with `--quick` or `--deep`.
  Don't wait for a reply; carry on.

When you launch each member in the steps below, set its model from this table.
If a launch fails because that model isn't available, launch it again without setting a model
and note the fallback in `run.md`.

## 2. Check web access
Before Round 1, check that the web tools work, so a verdict never silently rests on sources nobody could open:
- Run one WebSearch on the idea's topic.
- Open one page from the results with WebFetch. If there were no results, open `https://www.wikipedia.org`.

Record each as **working** or **not working**. If either is not working, tell the user in one line, for example:
"Web page access isn't working in this session, so cited sources can't be opened or checked. The council will
still run, but the verdict will carry an evidence warning." Then carry on.

Write the settings to `<session folder>/run.md`:
```
# Run settings
- Level: <Quick / Standard / Deep> (<set by --flag / picked automatically>)
- Why: <one line>
- Models: believer <model>, skeptic <model>, investor <model>, judge <model>
- Web search: <working / not working>
- Opening web pages: <working / not working>
- Fallbacks: <none, or which member ran without its set model>
```

When you launch any member, add this line to its instructions:
"Web status: search <working / not working>, opening pages <working / not working>." If something is not
working, also add: "Don't keep retrying that tool. Tag claims you can't source as [Assumption] and say why."

## 3. Round 1 — independent (run in parallel)
Launch the `believer`, `skeptic` and `investor` subagents **in a single message, in parallel**.
Give each the path to the brief and tell it: "This is Round 1. Follow your Round 1 output format.
You have not seen the other council members' views. Write your answer to <session folder>/round1-<member>.md."
They must not see each other's output yet.

## 4. Round 2 — one rebuttal each (run in parallel)
Launch `believer`, `skeptic` and `investor` again **in parallel**. Give each the paths to the brief,
its own Round 1, and the other two members' Round 1 files, plus:
"This is Round 2. Follow your Rebuttal format. Reply once. Write your answer to <session folder>/round2-<member>.md."

## 5. Verdict
Launch the `judge` subagent with the paths to the brief, `run.md` and all six documents (label each one
with its agent and round), plus: "Write your verdict to <session folder>/verdict.md."

## 6. Check the files
After each step, confirm each expected file exists and is not empty. If a member returned an answer
but its file is missing or empty, save the returned answer to that file yourself, exactly as written.

## 7. Report back
- Tell the user the verdict line, confidence, biggest risk and the three next tests —
  quoted from `verdict.md`, not rewritten. For a revisit, also quote "What changed since last time".
  If the verdict has an evidence warning, quote it too.
- Say which level ran.
- Give the path to the session folder.
- Do not add your own opinion of the idea unless the user asks.

## Rules
- Pass text between agents verbatim; never summarise or soften an agent's output.
- If a subagent fails or returns nothing, rerun it once; if it fails again, tell the user
  which member is missing and let the Judge rule with a note that the council was incomplete.
- Never invent facts, numbers or sources on any agent's behalf.
