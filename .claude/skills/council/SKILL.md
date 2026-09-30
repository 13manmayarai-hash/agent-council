---
name: council
description: Run a 4-agent decision council (Believer, Skeptic, Investor, Judge) on an idea or decision and save the verdict to council/. Use only when the user runs /council.
argument-hint: "[idea or decision to evaluate, or path to a brief file]"
disable-model-invocation: true
---

Run the decision council on this brief:

$ARGUMENTS

Follow these steps exactly. Do not argue the case yourself — you are only the orchestrator.

## 0. Prepare the brief
- If the argument is a file path, read that file as the brief.
- If the brief is empty or too vague to judge (no idea stated, no audience, no context),
  ask the user up to 3 short questions (what the idea is, who it's for, where / what
  constraints, any real numbers they have), then continue.
- Write the final brief to `council/<YYYY-MM-DD>-<short-slug>/brief.md`.
  Include only what the user said or provided — do not add your own facts.

## 1. Round 1 — independent (run in parallel)
Launch the `believer`, `skeptic` and `investor` subagents **in a single message, in parallel**.
Give each the full brief text and tell it: "This is Round 1. Follow your Round 1 output format.
You have not seen the other council members' views." They must not see each other's output yet.
Save each reply verbatim to `round1-believer.md`, `round1-skeptic.md`, `round1-investor.md`
in the session folder.

## 2. Round 2 — one rebuttal each (run in parallel)
Launch `believer`, `skeptic` and `investor` again **in parallel**. Give each:
the brief, its own Round 1, and the other two members' Round 1 answers, plus:
"This is Round 2. Follow your Rebuttal format. Reply once."
Save to `round2-believer.md`, `round2-skeptic.md`, `round2-investor.md`.

## 3. Verdict
Launch the `judge` subagent with the brief and all six documents in full (label each one
with its agent and round). Save its reply verbatim to `verdict.md`.

## 4. Report back
- Tell the user the verdict line, confidence, biggest risk and the three next tests —
  quoted from `verdict.md`, not rewritten.
- Give the path to the session folder.
- Do not add your own opinion of the idea unless the user asks.

## Rules
- Pass text between agents verbatim; never summarise or soften an agent's output.
- If a subagent fails or returns nothing, rerun it once; if it fails again, tell the user
  which member is missing and let the Judge rule with a note that the council was incomplete.
- Never invent facts, numbers or sources on any agent's behalf.
