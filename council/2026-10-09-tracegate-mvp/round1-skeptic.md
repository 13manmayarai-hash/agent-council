## Skeptic — Round 1
**Biggest single reason this fails:** The easy detections (deleted or weakened tests) are already free, and general AI reviewers will absorb them, while the hard, valuable part (proving the feature actually works, using per-flow YAML evidence) needs setup effort that buyers have not shown they will put in.

**Risks**
1. **The cheap core is already a commodity.** — [Fact] Free open-source diff checkers already do this. tampercheck flags deleted, skipped and hollowed tests and forced-success expressions ([PyPI](https://pypi.org/project/tampercheck/)). tamperguard blocks CI on removed assertions and loosened matchers ([PyPI](https://pypi.org/project/tamperguard/)). Incumbent AI reviewers (CodeRabbit, Greptile, Cursor Bugbot, Copilot review) already run on every PR ([dupple](https://dupple.com/learn/best-ai-code-review-tools)). [Assumption] Adding "test-tampering" rules to those reviewers is a prompt change for them. — severity 5
   Cheapest test: Take 30 real agent PRs with known tampering (for example from the [327-PR dataset post](https://dev.to/moonrunnerkc/ai-agents-cheat-on-pull-requests-i-mined-327-of-them-to-prove-it-43ij/comments)). Run tamperguard, CodeRabbit's free tier and a TraceGate prototype on them. If TraceGate does not catch at least about 30% more real cases with fewer false flags, the wedge is dead.

2. **The evidence policy is a setup burden nobody asked for.** — [Assumption] Teams have to write and maintain a YAML file per flow saying which DB rows and telemetry events count as proof. That means TraceGate also needs a running environment and access to those systems. This is the hardest part to build and to adopt. — severity 4
   Cheapest test: Show a YAML mock-up to 10 teams that merge agent PRs. Count how many will write a policy for one real flow within a week. Fewer than 3 means drop it from the MVP.

3. **Unproven demand: teams may already catch this, or not care enough to pay.** — [Fact] Reward hacking by Claude Code and Codex is documented, but in benchmark settings ([EvilGenie](https://arxiv.org/abs/2511.21654v1)). [Assumption] How often it happens in real production PRs, and whether a separate tool is worth the budget, is unknown. The brief says "no users, pricing or numbers" ([from the brief]). — severity 4
   Cheapest test: Run 15 interviews and 5 offers to scan a team's last 100 merged agent PRs for free. Kill signal: fewer than 2 scans turn up a real "tests pass, feature broken" merge, or no one commits to a paid pilot.

4. **False positives get the check muted.** — [Guess] Legitimate refactors also delete or loosen tests and change selectors. A noisy blocking check gets switched off within weeks. — severity 3
   Cheapest test: Measure the flag rate on 200 human-written PRs. Above about 5% means the product cannot be a blocking check.

5. **The agent vendors may close the gap themselves.** — [Assumption] Anthropic, Cognition and Cursor have strong reasons to stop their agents from gaming tests, through training or built-in self-checks. Each improvement shrinks the market TraceGate is aimed at. — severity 3
   Cheapest test: Run the same 20 tampering-prone tasks on current agent versions, then again on the next release. A falling tamper rate means the window is closing.

The "runtime gateway / evidence vault" vision is a separate, much larger product. It should not shape MVP decisions. [Assumption]

**What would change my mind:**
- A free scan of real teams' PRs finds cases where an agent PR passed tests, the feature was broken, the PR was merged, and all of these missed it: free linters, the team's AI reviewer and human review.
- At least 2 teams agree to a paid pilot after seeing those results.
- Clear evidence that the YAML evidence checks catch failures that diff analysis alone cannot.

Sources:
- [tampercheck (PyPI)](https://pypi.org/project/tampercheck/)
- [tamperguard (PyPI)](https://pypi.org/project/tamperguard/0.1.0/)
- [EvilGenie: A Reward Hacking Benchmark](https://arxiv.org/abs/2511.21654v1)
- [AI agents cheat on pull requests: 327 PRs (DEV)](https://dev.to/moonrunnerkc/ai-agents-cheat-on-pull-requests-i-mined-327-of-them-to-prove-it-43ij/comments)
- [Best AI Code Review Tools 2026 (dupple)](https://dupple.com/learn/best-ai-code-review-tools)
- [CodeRabbit vs Greptile pricing (costbench)](https://www.costbench.com/compare/coderabbit-vs-greptile/)
