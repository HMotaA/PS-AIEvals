
# Module 4 · Launch Strategy · Ascend IQ Copilot

## 4.0 Release Criteria

| Gate | Failure | Metric | Threshold | Dataset | Method | Runs at |
|---|---|---|---|---|---|---|
| Hard | Inverted Competitor Benchmark	 (#HALLUCINATION) | Share of competitor-comparison answers that pass both the safety rule and the scoped judge. | 100% of competitor-comparison answers must pass both the safety rule and the scoped judge. That means 0 inverted or unsourced competitor benchmarks, and a single failure blocks the release. | Ascend IQ golden set | Code-based check |  |
| Soft | Row 1 · Hallucination: the answer quotes the old price as current | Share of answers that quote a price and match the live pricing page. | ≥98%. | Ascend IQ golden set | Code-based check | Staging |
| Advisory | Row 17 · Tone: slang detected | Share of drafted emails with no slang from the brand-voice list. | ≥95%. | Ascend IQ golden set | Code-based check | Pull Request |

## CI Gate Request for Engineering

- **Hard gate · Inverted Competitor Benchmark	 (#HALLUCINATION).** Check: the code-based check, run on the Ascend IQ golden set at [runs at]. Measures: Share of competitor-comparison answers that pass both the safety rule and the scoped judge.. Passes when: 100% of competitor-comparison answers must pass both the safety rule and the scoped judge. That means 0 inverted or unsourced competitor benchmarks, and a single failure blocks the release.. On a fail: block the merge.
- **Soft gate · Row 1 · Hallucination: the answer quotes the old price as current.** Check: the code-based check, run on the Ascend IQ golden set at Staging. Measures: Share of answers that quote a price and match the live pricing page.. Passes when: ≥98%.. On a fail: pause the release until the PM signs off on an override.
- **Advisory gate · Row 17 · Tone: slang detected.** Check: the code-based check, run on the Ascend IQ golden set at Pull Request. Measures: Share of drafted emails with no slang from the brand-voice list.. Passes when: ≥95%.. On a fail: post a warning, and don't block.

## Mitigation Plan · Soft Gate

If our Soft gate fails because more than 2% of pricing answers don’t match the live pricing page, we’ll ship with pricing answers behind a feature flag tied to a live price-match eval. If mismatches pass 2%, pricing answers switch off automatically and point users to the vendor’s pricing page. That lets us ship the rest of Ascend IQ to clients while we fix data freshness and collect real-traffic data.
