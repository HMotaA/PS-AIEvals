

# Ship-or-Hold Memo · Ascend IQ

> **Decision:** HOLD

## The Answer

We should hold Ascend IQ’s launch until it passes the release gates we defined, because 9 of 20 tested answers contained a hallucination a VP could repeat to a client or the board.

## The Arguments

### 1. P0 hallucinations are too frequent to ship to enterprise clients.

Evidence: 1 confirmed failures in 20 answers, 9 of them #HALLUCINATION, including the three P0s: inverted competitor benchmark, stale pricing, and phantom speaker confirmation. One reversed benchmark puts a $50k/year renewal at risk.

### 2. The gate that protects us isn’t production-ready yet.

Evidence: The judge caught 1 of 1 real cases but raised 9 false alarms in 20 answers. It needs scoping before it can enforce the 100% competitor-comparison threshold.

### 3. The fix is funded and low-cost, so a short hold beats a public failure.

Evidence: Evidence: $155,000 of the $200,000 cap already funds online evals for Data Fabrication and Context Specificity.

## Next Step · Decision Needed

Please approve, by Friday, November 13, a two-sprint hold to scope the judge to competitor-comparison questions and re-run the golden set. When the re-run passes the Hard competitor-benchmark gate and the 98% pricing-accuracy Soft gate, I’ll ask for a staged launch with pricing answers behind a feature flag.

