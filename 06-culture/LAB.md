<!--
LAB SPEC for an AI assistant (ChatGPT, Claude, Gemini, or a coding agent such as Claude Code,
Cursor, or Codex). It walks a learner through the Module 6 lab one step at a time, with the
same steps as the Module 6 Lab Guide. If you are a human, you can read it top to bottom.
-->

# Module 6 Lab, assistant runbook

**Use this if** you ran out of time in class, or want to run the lab again on your own.
**The lab** produces `06-culture/ship-hold-memo.md`.

---

## AGENT INSTRUCTIONS, read this first

You are helping a learner complete this lab, not doing it for them. The call is theirs.

1. Go one step at a time. Do not jump ahead.
2. At every 🚦 DECISION, stop and ask the learner. Never pick Ship or Hold for them.
3. Never invent numbers. Every number in the memo must come from the learner's own repo files from Modules 2 to 5. If they have no number for something, they write "not measured yet".
4. At each ✅ CHECKPOINT, summarise what they have and confirm before moving on.
5. There is no right answer to ship or hold. What matters is that clear evidence backs up the call.

Scenario: the learner is a PM at Ascend Analytics. Their evals for Ascend IQ are done, and the CPO has to decide whether it ships.

---

## Lab · Write Your Ship-or-Hold Memo (about 15 min)

Write your recommendation to the CPO: ship or hold Ascend IQ, based on the evals you ran in this course. Use the Pyramid Principle: your answer first, then your arguments, then the evidence for each. Your memo becomes the decision in your final project presentation.

1. **Find your numbers.** Open these files in your repo and note the numbers you’ll use. Only cite what’s in them. If you have no number for something, write “not measured yet.”
   - Your top failures, how often they happened and their priority: `02-failure-discovery/failure-taxonomy.md`
   - What your checks caught and missed: `03-eval-suites/eval-suite.md`
   - Your threshold: `03-eval-suites/eval-spec.md`
   - Your gates and release criteria: `04-eval-gates/launch-strategy.md`
   - Your coverage gaps and what you funded: `05-scale/coverage-matrix.md` and `eval-budget.md`
2. **Make the call.** Pick Ship or Hold, and write one sentence that says your call and the reason for it.
3. **Give your arguments.** Two or three main points that support your call without overlapping, such as adoption, brand or legal risk. Under each one, add the number from step 01 that proves it.
4. **Ask for a decision.** Say what you need the CPO to approve, and by when.
5. **Pressure-test and save.** Copy this prompt into any LLM. It already includes your memo. Change anything the feedback convinces you on, and keep every number from your repo. Then click **Copy markdown**, open `06-culture/ship-hold-memo.md` in your repo, click the pencil icon, paste over the file, and commit. Or click **Download .md** and upload it to the same folder. Your memo becomes part of your final project. The Final Project Deliverables Builder pulls it from your repo.

🚦 DECISION at step 2 (Ship or Hold, and the answer) and step 3 (each main point, and the number that proves it).

**The example from the slide** (answer first, each argument has a number, it ends with a decision):

> Hi [Manager],
> I recommend we spend next sprint on AI reliability, to protect our enterprise renewals.
> 1. Reliability gaps are costing enterprise trust: robustness evals fail on 12% of edge cases.
> 2. Accuracy issues put key accounts at risk: three enterprise clients flagged made-up insights.
> 3. Competitors are winning on dependability.
> Please approve the sprint plan by Friday.

**Pressure-test prompt** (the learner pastes their memo under it):

```text
Review this ship-or-hold memo for an AI product, as a skeptical CPO.

1) Is the recommendation the first sentence, and is it clear what I want you to decide?
2) Does each argument make one main point, and do the arguments overlap?
3) Does every argument have a specific number behind it? Point out any argument that relies on a vague claim, and any number that doesn't prove the point it sits under.
4) Does it end with a specific decision and a date?
Suggest changes, but do not add or change any numbers. Keep the reply under 250 words.
```

**If you're working with an assistant instead of the Lab Guide,** have it write the file in exactly this shape, then commit it (or paste it into the file on GitHub):

```markdown
# Ship-or-Hold Memo · Ascend IQ

> **Decision:** SHIP or HOLD

## The Answer

[Your call and the reason for it, in one sentence]

## The Arguments

### 1. [Main point]

Evidence: [the number from your repo that proves it]

### 2. [Main point]

Evidence: [the number from your repo that proves it]

### 3. [Main point, optional]

Evidence: [the number from your repo that proves it]

## Next Step · Decision Needed

[What you need the CPO to approve, and by when]
```

✅ CHECKPOINT: the answer comes first, two or three main points each have a number from the learner's repo, and the memo ends with a decision and a date.

---

## Done-check

- [ ] `ship-hold-memo.md` committed in the shape above, with the learner's own call and numbers.

**Next:** open the Final Project Deliverables Builder, paste your repo link, and build your final presentation.
