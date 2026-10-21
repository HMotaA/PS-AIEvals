<!--
LAB SPEC for an AI assistant (ChatGPT, Claude, Gemini, or a coding agent such as Claude Code,
Cursor, or Codex). It walks a learner through the two Module 5 labs one step at a time, with
the same steps as the Module 5 Lab Guide. If you are a human, you can read it top to bottom.
-->

# Module 5 Labs, assistant runbook

**Use this if** you ran out of time in class, or want to run the labs again on your own.
**Lab 1** produces `05-scale/coverage-matrix.md`.
**Lab 2** produces `05-scale/eval-budget.md`.

---

## AGENT INSTRUCTIONS, read this first

You are helping a learner complete these labs, not doing them for them. The judgment calls are theirs.

1. Go one step at a time. Do not jump ahead.
2. At every 🚦 DECISION, stop and ask the learner. Never pick their marks, gaps or levels for them.
3. Never invent their reasoning. If they are stuck, ask one question that helps them decide.
4. At each ✅ CHECKPOINT, summarise what they have and confirm before moving on.
5. In Lab 1, step 4, play the reviewer yourself: do the marks match what runs today, is the accepted gap really low risk given whether the product is internal or external, is the plan specific (which check, what data, how often), and what is the one question their manager would ask? Then let the learner change or keep each answer.

Scenario: the learner is a PM at Ascend Analytics. Ascend IQ, a customer-facing AI agent, hasn't launched yet. Four other AI products are already live.

---

## Lab 1 · Map Your Portfolio Coverage (about 25 min)

Ascend IQ is the newest product in Ascend Analytics’ AI portfolio, and it hasn’t launched yet. Four other AI products are already live, and each team set up its own evals. Before the next eval budget is set, the CPO wants one view of which trust metrics each product is checked for. Pick one of the four, mark its coverage from what runs today, then decide which gap to accept for now and which to close first.

**The five trust metrics (columns)**
- **Hallucination Rate:** False or made-up claims
- **Fairness:** Uneven quality across groups
- **Latency:** Response time
- **UX Trust:** Tone that undermines confidence
- **Robustness:** Fails on questions it should handle

**The four products, and what runs on each today**

**AI Report Summaries** (External): Writes executive summaries of research reports, sent straight to clients.
What runs today:
- An LLM judge compares each summary with its source report before every release.
- Response time is logged, but nobody has set a target.

**Competitor Signal Tracker** (Internal): Scores news and social posts about competitors for the sales and strategy teams.
What runs today:
- A timer alerts if the nightly scoring run takes more than 2 hours.
- A style check flags summaries written in a casual or alarmist tone before they reach the sales team.

**AI Voice Agent** (External): Answers basic support and billing calls, and passes harder ones to a person.
What runs today:
- An eval gate tests its answers to 300 billing questions before every release.
- A supervisor listens to 10 random calls a week for tone.
- A drift monitor alerts when callers start asking about things the agent wasn’t tested on.

**Automated Data Tagging** (Internal): Labels raw market commentary and filings for the models that use them.
What runs today:
- A code-based check confirms every label comes from the approved list, but not that it’s the right label.
- A data analyst reviews 50 labels by hand each quarter, split by source.
- A check confirms the same kind of text always gets the same label.

1. **Mark the product’s coverage.** Pick one product, and read what runs on it today. For each trust metric, mark ✅ if a check runs on that risk regularly, ⚠️ if someone spot-checks it by hand or the check only measures part of the risk, and ❌ if nothing checks it.
2. **Accept one gap.** Pick the ❌ you can live with for now. Say why: the risk is low, or the check costs more than it would save. Then say what would make you change your mind, and when you’ll look again.
3. **Close the critical gap.** Pick the ❌ that would do the most damage if it failed tomorrow. Say who would notice first, what it would cost, and which check would close it: a drift monitor, a periodic audit or a new eval gate.
4. **Pressure-test and save.** Copy this prompt into a new chat in any LLM and send it. It already includes your row and answers. Change anything the feedback convinces you on, and note what changed.
   - Write: What did the feedback change?
   - Click **Copy markdown**, open `05-scale/coverage-matrix.md` in your repo, click the pencil icon, paste over the file, and commit. Or click **Download .md** and upload it to the same folder.

🚦 DECISION at step 1 (each mark, from what runs today), step 2 (the gap to accept, and what would change their mind) and step 3 (the gap to close first, who notices first, what it costs, and the check that closes it).

**If you're working with an assistant instead of the Lab Guide,** have it write the file in exactly this shape, then commit it (or paste it into the file on GitHub):

```markdown
# Module 5 · Coverage Matrix · [product]

## Coverage Row

| Product | Hallucination Rate | Fairness | Latency | UX Trust | Robustness |
|---|---|---|---|---|---|
| … | ✅ Covered / ⚠️ Partial / ❌ Gap | … | … | … | … |

## What Runs Today

- …

## Accepted Gap

**[risk].** We accept this gap because …

We’ll look again: …

## Critical Gap

We’ve flagged [risk] as the most critical gap for [product] because … To close it, we’ll add …

## After the Pressure Test

…
```

✅ CHECKPOINT: five marks that match what runs today, one accepted gap with what would change the learner's mind, and one critical gap with a plan.

---

## Lab 2 · Spend Your Eval Budget (about 20 min)

Engineering flagged five new failure modes for Ascend IQ this quarter. The CPO set a $200,000 quarterly cap for online evals. Fund at most three of its five failure modes at the online eval level. Downgrade the rest to a periodic audit or a code-based check, say what you’ll run instead and why it’s enough, and stay under the cap.

**Coverage levels**
- **Online eval:** An LLM judge or a reviewer scores live traffic continuously. (Listed cost)
- **Periodic audit:** People review a sample of answers every week or two. (~10% of online)
- **Code-based check:** A quick rule check, or a spot-check on every release. (~5% of online)

**Engineering's five failure modes**

| Failure | Trust metric | Risk | Online eval cost | What goes wrong |
|---|---|---|---|---|
| Data Fabrication | Hallucination Rate | P0 | $85,000 | Makes up data points, such as a competitor’s price or a review count. |
| Context Specificity | Robustness | P1 | $70,000 | Answers the question but misses what was asked, such as summarizing all reviews when the client asked for the negative ones. |
| Overconfident Tone | UX Trust | P1 | $65,000 | States guesses as facts, with no sign of how sure it is. |
| Data Bias | Fairness | P2 | $55,000 | Favors US data over APAC data when it summarizes. |
| Slow Answers | Latency | P3 | $25,000 | Long, multi-step questions take more than 10 seconds to answer. |

The cap counts online eval spend only, and at most three failures can be online evals. Funding the P0 and both P1s as online evals costs $220,000, so the learner has to downgrade at least one P0 or P1.

For each failure, the learner picks a level. For each failure below the online eval level, they write the cheaper check they'll run and why it's enough: what it still catches, what it misses, and why they can live with that.

🚦 DECISION at every level, and at every downgrade.

**Before saving, check:**
- All 5 failure modes have a level.
- **At most 3** failure modes funded as online evals.
- Total online eval spend ≤ **$200,000**.
- For each failure below online eval: the check you’ll run AND why it’s enough.
- At least one P0 or P1 risk was downgraded, and that downgrade is defensible.
- You can answer: “Why did you downgrade X instead of Y?”

**Pressure-test prompt** (the learner pastes their markdown under it):

```text
You are the CPO of Ascend Analytics. I have a strict $200K/quarter cap for online eval coverage (an LLM judge or reviewer scoring live traffic continuously) on the Ascend IQ agent, and 5 failure modes to fund.

Pressure-test my budget:

1. Did I fund the right P0/P1 risks as online evals? Which downgrade exposes us to the most serious risk?
2. For every periodic audit or code-based check, would that check actually catch the failure, or am I just ticking a box?
3. If a P0 failure reached a client tomorrow, would my reason hold up in a customer incident review?
4. Which single eval should I re-prioritize given the trade-off? Be specific about cost.

Be direct. Don't soften.
```

**If you're working with an assistant instead of the Lab Guide,** have it write the file in exactly this shape, then commit it (or paste it into the file on GitHub):

```markdown
# Module 5 · Eval Budget · Ascend IQ

**Quarterly budget cap:** $200,000
**Online eval spend:** $… (… of at most 3 online evals)

## Budget

| Failure | Trust metric | Risk | Level | Cost |
| --- | --- | :---: | :---: | ---: |
| … | … | P0 / P1 / P2 / P3 | Online eval / Periodic audit / Code-based check | $… |

## Downgrades

### [level] · [failure] ([metric] · [risk])
- **Cheaper check:** …
- **Why it’s enough:** …
```

✅ CHECKPOINT: every failure has a level, online eval spend is at or under $200,000, and every downgrade names a check and what it misses.

---

## Done-check

- [ ] Lab 1: `coverage-matrix.md` committed in the shape above, with the learner's own marks and calls.
- [ ] Lab 2: `eval-budget.md` committed in the shape above, with the learner's own levels and reasons.

**Next:** Module 6, Make Evals the Way the Org Ships.
