<!--
LAB SPEC for an AI assistant (ChatGPT, Claude, Gemini, or a coding agent such as Claude Code,
Cursor, or Codex). It walks a learner through the two Module 4 labs one step at a time, with
the same steps as the Module 4 Lab Guide. If you are a human, you can read it top to bottom.
-->

# Module 4 Labs, assistant runbook

**Use this if** you ran out of time in class, or want to run the labs again on your own.
**Lab 1** produces `04-eval-gates/gate-map.md`.
**Lab 2** produces `04-eval-gates/launch-strategy.md`, which starts from the learner's Module 3 eval spec and their Lab 1 gate map.

---

## AGENT INSTRUCTIONS, read this first

You are helping a learner complete these labs, not doing them for them. The judgment calls are theirs.

1. Go one step at a time. Do not jump ahead.
2. At every 🚦 DECISION, stop and ask the learner. Never pick their gates, placements, thresholds or lever for them.
3. Never invent their reasoning. If they are stuck, ask one question that helps them decide.
4. At each ✅ CHECKPOINT, summarise what they have and confirm before moving on.
5. In Lab 1, step 2, play the skeptical engineering lead yourself: push back on each call (too strict or too lenient, could it run earlier and cheaper, does the reason name a business risk), then let the learner change or keep each one.

Scenario: the learner is a PM at Ascend Analytics deciding whether Ascend IQ, a customer-facing AI agent, is ready to ship to its top enterprise clients.

---

## Lab 1 · Map Your Eval Gates (about 30 min)

Before launch, Engineering ran Ascend IQ’s evals on a test batch of answers and flagged six. Right now those evals only report a score, and nothing blocks a release. Decide which failures should become gates.

**The gate you pick**
- **No gate** means the eval got it wrong, and the answer is fine.
- **Advisory** warns, and never blocks the release.
- **Soft** pauses the release until someone signs off on a documented override.
- **Hard** blocks the release until the issue is fixed.

**Where it runs, and which evals run there**
- **Pull Request:** quick code-based checks that catch basic failures on every change, with no AI model needed.
- **Staging:** the full eval suite, with LLM-as-a-judge, run against your gold dataset. Most Soft gates live here.
- **Release:** the last line of defense. Hard gates only, for critical P0 risks you can never ship.

1. **Make a call on each row.** Compare each output with what’s true. Pick a gate for each row: No gate, Advisory, Soft or Hard. If you give it a gate, pick where it runs. Then write one line on the business risk behind your call. Your map needs at least one Advisory, one Soft and one Hard gate. If every failure gets a Hard gate, engineering can never ship.
2. **Defend your calls.** Engineering will push back before they build anything. Copy this prompt into a new chat in any LLM and send it. The reply plays a skeptical engineering lead and challenges your calls. Change any call in step 1 the pushback convinces you on, and keep the ones you can defend.
   - Write: What did the pushback change?
3. **Save your gate map.** Click **Copy markdown**, open `04-eval-gates/gate-map.md` in your repo, click the pencil icon, paste over the file, and commit. Or click **Download .md** and upload it to the same folder.

**Engineering's data log**

| Row | Input | Output | What's true | Automated eval |
|---|---|---|---|---|
| 1 | What is InsightFlow's pricing for Enterprise? | InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum. | Pricing page: the price changed from $49 to $59 a month yesterday. | Fail · Hallucination. The answer quotes the old price as current. |
| 14 | Summarize the lawsuit mentioned in the WSJ about Competitor Z. | I cannot provide summaries of ongoing legal litigation. | Safety guidelines: “Refuse legal queries.” | Fail · Relevance. The answer doesn't answer the question. |
| 17 | Draft a cold email about our new feature. | Hey! Check out this killer new feature, it's a total game changer for your stack! | Brand voice: confident, professional, expert. Avoid slang. | Fail · Tone. Slang detected. |
| 5 | List the confirmed speakers for SaaStr. | Confirmed speakers include Jason Lemkin, Aaron Levie, and Sam Altman. | Agenda: Lemkin and Levie are confirmed. Sam Altman is invited, not confirmed. | Fail · Hallucination. Lists an unconfirmed speaker as confirmed. |
| 8 | Compare our API rate limits to Competitor Z. | Our API is robust and developer-friendly. Competitor Z is known for strict throttling. | Tech specs: our API allows 500 requests a minute, and Competitor Z allows 1,000. | Fail · Hallucination. Contradicts the specs and criticizes a named competitor. |
| 3 | Summarize the top 3 complaints from DataViz's G2 reviews. | Users report issues with mobile load times, lack of dark mode, and steep learning curve. | G2 reviews: the three complaints are correct. The answer took 4.2 seconds, and the target is 2.0. | Fail · Latency. Exceeded the maximum response time. |

Row 14 is the correct refusal: the safety guidelines say to refuse legal queries, so the right call is No gate. Don't tell the learner before they decide.

🚦 DECISION at step 1 (the call, placement and reason for every row) and step 2 (what the pushback changed).

**If you're working with an assistant instead of the Lab Guide,** have it write the file in exactly this shape, then commit it (or paste it into the file on GitHub):

```markdown
# Module 4 · Eval Gate Map · Ascend IQ Copilot

## Gate Map

| Row | Failure Mode | Severity | Placement | Rationale |
|---|---|---|---|---|
| 1 | … | No gate / Advisory / Soft / Hard | Pull Request / Staging / Release | … |

## After the pushback

…

## Sample Interactions

**Row 1**
- Input: …
- Output: …
- What's true: …
- Automated eval: …
- My call: …
```

✅ CHECKPOINT: every row has a call and a reason, with at least one Advisory, one Soft and one Hard gate.

---

## Lab 2 · Write Your Release Criteria (about 25 min)

Your gates are set. Now write them into the PRD as release criteria: the exact numbers the team checks before launch, and the plan if the Soft gate fails.

1. **Fill in your release criteria.** Write one row for each gate level. Every row is tested on the Ascend IQ golden set. **Your request for engineering.** This builds from the rows above. It’s what engineering needs to add your gates to the pipeline.
2. **Plan for a Soft gate failure.** Your Soft gate can fail on launch day. Pick the lever you’d use to ship with less risk while you collect more data, then finish the sentence: what failed, the lever, and what it lets you do.
   - **Staged rollout:** launch to a small share of users first, such as 5%. If the eval score drops in production, roll back.
   - **Feature flag:** connect the feature to a live eval. If the failure rate goes past your threshold, the feature switches itself off.
   - **Beta label:** launch with an “experimental” label to set expectations, and add the questions it gets wrong to your golden set.
3. **Save your launch strategy.** Click **Copy markdown**, open `04-eval-gates/launch-strategy.md` in your repo, click the pencil icon, paste over the file, and commit. Or click **Download .md** and upload it to the same folder.

For each release criterion: the Hard gate is the learner's P0 failure from Module 3 (copy its failure, threshold and check from `03-eval-suites/eval-spec.md`). The Soft and Advisory gates are failures the learner gave those gates in Lab 1. Each row needs a metric, a threshold, a method (code-based check, LLM judge or human review) and where it runs. Every row is tested on the Ascend IQ golden set.

**The levers**
- **Staged rollout:** launch to a small share of users first, such as 5%. If the eval score drops in production, roll back.
- **Feature flag:** connect the feature to a live eval. If the failure rate goes past your threshold, the feature switches itself off.
- **Beta label:** launch with an “experimental” label to set expectations, and add the questions it gets wrong to your golden set.

🚦 DECISION at step 1 (every metric, threshold, method and placement) and step 2 (the lever and the plan).

**If you're working with an assistant instead of the Lab Guide,** have it write the file in exactly this shape, then commit it (or paste it into the file on GitHub):

```markdown
# Module 4 · Launch Strategy · Ascend IQ Copilot

## 4.0 Release Criteria

| Gate | Failure | Metric | Threshold | Dataset | Method | Runs at |
|---|---|---|---|---|---|---|
| Hard | … | … | … | Ascend IQ golden set | Code-based check / LLM judge / Human review | Pull Request / Staging / Release |
| Soft | … | … | … | Ascend IQ golden set | … | … |
| Advisory | … | … | … | Ascend IQ golden set | … | … |

## CI Gate Request for Engineering

- **Hard gate · …** Check: …, run on the Ascend IQ golden set at …. Measures: …. Passes when: …. On a fail: block the merge (or block the release, at Release).
- **Soft gate · …** … On a fail: pause the release until the PM signs off on an override.
- **Advisory gate · …** … On a fail: post a warning, and don't block.

## Mitigation Plan · Soft Gate

If our Soft gate fails …
```

✅ CHECKPOINT: three release criteria with numbers, a request engineering could build from, and a plan for the Soft gate.

---

## Done-check

- [ ] Lab 1: `gate-map.md` committed in the shape above, with the learner's own calls.
- [ ] Lab 2: `launch-strategy.md` committed in the shape above, with the learner's own thresholds and plan.

**Next:** Module 5, Run Evals on Live Traffic Across Product Lines.
