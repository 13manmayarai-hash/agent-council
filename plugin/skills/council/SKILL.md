---
name: council
description: Run a 4-agent decision council (Believer, Skeptic, Investor, Judge) on an idea or decision and save the verdict to council/. Use only when the user runs the council command.
argument-hint: "[idea or decision, path to a brief file, or: revisit <council folder> <new results>]"
disable-model-invocation: true
---

Run the decision council on this brief:

$ARGUMENTS

Follow these steps exactly. Do not argue the case yourself — you are only the orchestrator.

The four members are subagents named `believer`, `skeptic`, `investor` and `judge`. When this runs from the
installed agent-council plugin they are listed as `agent-council:believer`, `agent-council:skeptic`,
`agent-council:investor` and `agent-council:judge`. Use whichever form appears in your available agent types.

## 0. Prepare the brief
- **Revisit:** if the argument starts with `revisit`, the next word is an earlier session folder
  (for example `council/2026-10-09-tracegate-mvp`) and the rest is the user's new results.
  - Read that folder's `brief.md` and `verdict.md`.
  - If the user gave no new results, ask what happened with the earlier tests, then continue.
  - Write a new brief containing: the original brief unchanged, then a "Previous verdict" section
    quoting the earlier verdict, confidence and three tests, then a "New results since <date>"
    section with only what the user reported.
  - Use a new folder named `council/<YYYY-MM-DD>-<original slug>-revisit`. Never overwrite the earlier one.
- If the argument is a file path, read that file as the brief.
- If the brief is empty or too vague to judge (no idea stated, no audience, no context),
  ask the user up to 3 short questions (what the idea is, who it's for, where / what
  constraints, any real numbers they have), then continue.
- Write the final brief to `council/<YYYY-MM-DD>-<short-slug>/brief.md`.
  Include only what the user said or provided — do not add your own facts.

## 1. Round 1 — independent (run in parallel)
Launch the `believer`, `skeptic` and `investor` subagents **in a single message, in parallel**.
Give each the path to the brief and tell it: "This is Round 1. Follow your Round 1 output format.
You have not seen the other council members' views. Write your answer to <session folder>/round1-<member>.md."
They must not see each other's output yet.

## 2. Round 2 — one rebuttal each (run in parallel)
Launch `believer`, `skeptic` and `investor` again **in parallel**. Give each the paths to the brief,
its own Round 1, and the other two members' Round 1 files, plus:
"This is Round 2. Follow your Rebuttal format. Reply once. Write your answer to <session folder>/round2-<member>.md."

## 3. Verdict
Launch the `judge` subagent with the paths to the brief and all six documents (label each one
with its agent and round), plus: "Write your verdict to <session folder>/verdict.md."

## 4. Check the files
After each step, confirm each expected file exists and is not empty. If a member returned an answer
but its file is missing or empty, save the returned answer to that file yourself, exactly as written.

## 5. Report back
- Tell the user the verdict line, confidence, biggest risk and the three next tests —
  quoted from `verdict.md`, not rewritten. For a revisit, also quote "What changed since last time".
- Give the path to the session folder.
- Do not add your own opinion of the idea unless the user asks.

## Rules
- Pass text between agents verbatim; never summarise or soften an agent's output.
- If a subagent fails or returns nothing, rerun it once; if it fails again, tell the user
  which member is missing and let the Judge rule with a note that the council was incomplete.
- Never invent facts, numbers or sources on any agent's behalf.
