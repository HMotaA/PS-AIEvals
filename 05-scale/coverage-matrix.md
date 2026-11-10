





# Module 5 · Coverage Matrix · AI Report Summaries

## Coverage Row

| Product | Hallucination Rate | Fairness | Latency | UX Trust | Robustness |
|---|---|---|---|---|---|
| AI Report Summaries | ✅ Covered | ❌ Gap | ⚠️ Partial | ❌ Gap | ❌ Gap |

## What Runs Today

- An LLM judge compares each summary with its source report before every release.
- Response time is logged, but nobody has set a target.

## Accepted Gap

**Fairness.** We accept this gap because summaries are written from a single source report, so any uneven quality across regions or industries mostly comes from the source and not the model. A segmented audit would cost more than that risk right now.

We’ll look again: We’ll look again if clients outside the US pass 25% of summaries, or if any client flags weaker summaries for their region. Otherwise we’ll review at the next quarterly budget.

## Critical Gap

We’ve flagged Robustness as the most critical gap for AI Report Summaries because summaries go straight to clients, and a summary that drops the key finding of a long or table-heavy report looks correct but misleads. The client executive would notice first, in front of their own leadership, which puts the renewal at risk. To close it, we’ll add an eval gate before every release that tests summaries on a set of hard report types (long, table-heavy, multi-section) and checks that the key findings are covered.

## After the Pressure Test

1) Marks.

Latency ⚠️ is right. Response time is measured, but with no target nothing can fail.
Hallucination ✅ is generous. The judge runs before each release, so live summaries reaching clients are never checked. ✅ holds only if Covered means pre-release; say that explicitly.
The three ❌ marks are accurate, but don’t treat them as equal. This product is external and read by executives. UX Trust (hedged or alarmist tone in a client deliverable) is not trivial here.

2) Accepted gap. Your reasoning is weak. The model, not the source, decides what to keep, and summaries of non-US or non-English reports are exactly where quality slips. Your trigger is also untestable: do you track client region per summary today? If you don’t, “25% outside the US” can never fire. Accepting the gap is defensible, but only once you add a cheap region tag to every summary so the trigger is measurable.

3) Critical gap plan. The direction is right, but it isn’t buildable yet. Missing:

Data: how many hard reports, say 50, with key findings labeled by an analyst.
Metric: key-finding recall, the share of labeled findings the summary includes.
Threshold: for example, at least 95% recall; below that, the release blocks.
Method: an LLM judge, with analysts spot-checking 10 judge scores per release.
Cadence: every release, plus a quarterly refresh of the hard set with real client reports.

4) Your manager’s question: “Who decides what counts as a key finding, and why doesn’t the judge we already run catch omissions?” Have an answer ready: the current judge checks faithfulness, not completeness.
