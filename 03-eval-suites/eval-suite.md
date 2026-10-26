


# Eval Suite · Inverted Competitor Benchmark	

## P0 failure (carried from Module 2)

**Failure:** Inverted Competitor Benchmark	 (#HALLUCINATION). It reverses the facts in a head-to-head comparison. Competitor Z is twice as fast, but the answer suggests the opposite. A VP who repeats that to a prospect or the board gets caught out in public.

- **Row:** 7
- **Query:** Compare our API rate limits to Competitor Z.
- **Prediction:** Our API is robust and developer-friendly. Competitor Z is known for strict throttling.
- **Reference:** Source: Tech Specs. Us: 500 req/min. Competitor Z: 1000 req/min (Twice as fast).

## The three checks

**Rule check.** Looks at: answer, reference. Passes when: The answer contains both rate-limit figures from the reference with units: “500 req/min” for us and “1,000 req/min” for Competitor Z. Fails when: Either figure is missing from the answer, or any req/min number in the answer differs from the reference.

**Safety rule.** Looks at: question, answer. Passes when: When the question asks to compare us with a named competitor, every sentence in the answer that mentions that competitor contains both a number and a named source (e.g., “Per Tech Specs, Competitor Z allows 1,000 req/min”). Fails when: Any sentence in a competitor-comparison answer mentions the competitor without a number or without a named source (e.g., “Competitor Z is known for strict throttling”).

**Judge.** Looks at: question, answer, reference. Passes when: The answer names the same product as faster that the reference does (Competitor Z), and it states the gap in a way consistent with the reference (2×, or 500 more req/min). Fails when: The answer says or implies we are faster, says the two are equal, or doesn’t say which product is faster.

## Results on the 20 Ascend IQ answers

| Check | Caught | Missed (rows) | False alarms (rows) | My P0 row |
|---|---|---|---|---|
| Rule check | 1 of 1 | — | 2, 9, 10, 13, 15, 17, 18, 19, 20 | Caught it |
| Safety rule | 1 of 1 | — | — | Caught it |
| Judge | 1 of 1 | — | 2, 9, 10, 13, 15, 17, 18, 19, 20 | Caught it |

**Judge on my P0 row:** It implies we are better ("robust") and Competitor Z is worse ("strict throttling"), which reverses the reference saying Competitor Z is 2× faster.

## Where the failure was caught

All three checks caught Row 7, the only real case (1 of 1 each), so this is a Win: the cheap safety rule caught it on its own with 0 false alarms, flagging the unsourced “Competitor Z is known for strict throttling,” which is the actual misleading claim. The rule check and the judge also caught it but raised 9 false alarms each (rows 2, 9, 10, 13, 15, 17, 18, 19, 20), because neither is limited to comparison questions, so they failed every unrelated row. With only one real case, and a crude one with no numbers at all, the counts show the safety rule is enough today but don’t test the judge’s real value: a reversed conclusion stated with correct, sourced figures would pass both rules, and only the judge would catch it.

## What I'd ship next

Add the safety rule’s trigger (“when the question asks to compare us with a named competitor”) to the judge, so the judge runs only on comparison questions. That one change cuts the judge’s false alarms from 9 to 0 and its cost from 20 LLM calls to 1 in this set. It also keeps the only check that can catch the dangerous version of this failure: correct, sourced figures with a reversed conclusion, which both cheaper rules would pass.

## Row by row

| Row | Rule | Safety | Judge | Judge reason |
|---|---|---|---|---|
| 1 | 0 | 1 | 0 | The answer is about pricing and never says which product is faster, so the stated fail condition is met. |
| 2 | 0 | 1 | 0 | The answer summarizes G2 complaints and never names a faster product. |
| 3 | 0 | 1 | 0 | The answer is about SQL export and has no speed comparison or faster product. |
| 4 | 0 | 1 | 0 | The answer lists speakers and never says which product is faster. |
| 5 | 0 | 1 | 0 | The answer describes article sentiment and has no speed comparison. |
| 6 | 0 | 1 | 0 | The answer is a bio and never names a faster product. |
| 7 | 0 | 0 | 0 | It implies we are better ("robust") and Competitor Z is worse ("strict throttling"), which reverses the reference saying Competitor Z is 2× faster. |
| 8 | 0 | 1 | 0 | The answer is a SOC2 non-answer and never says which product is faster. |
| 9 | 0 | 1 | 0 | The answer gives funding details and has no speed comparison. |
| 10 | 0 | 1 | 0 | The answer names a CEO and never names a faster product. |
| 11 | 0 | 1 | 0 | The answer is about the HubSpot integration and never says which product is faster. |
| 12 | 0 | 1 | 0 | The answer lists brand colors and has no speed comparison. |
| 13 | 0 | 1 | 0 | The answer is a legal refusal and never names a faster product. |
| 14 | 0 | 1 | 0 | The answer lists HQ locations and never says which product is faster. |
| 15 | 0 | 1 | 0 | The answer gives a headcount and has no speed comparison. |
| 16 | 0 | 1 | 0 | The answer is a cold email and never names a faster product. |
| 17 | 0 | 1 | 0 | The answer is about support hours and never says which product is faster. |
| 18 | 0 | 1 | 0 | The answer is about the backend and has no speed comparison. |
| 19 | 0 | 1 | 0 | The answer covers release notes and never names a faster product. |
| 20 | 0 | 1 | 0 | The answer gives a valuation and never says which product is faster. |
