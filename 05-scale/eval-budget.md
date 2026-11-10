

# Module 5 · Eval Budget · Ascend IQ

**Quarterly budget cap:** $200,000
**Online eval spend:** $155,000 (2 of at most 3 online evals)

## Budget

| Failure | Trust metric | Risk | Level | Cost |
| --- | --- | :---: | :---: | ---: |
| Data Fabrication | Hallucination Rate | P0 | Online eval | $85,000 |
| Context Specificity | Robustness | P1 | Online eval | $70,000 |
| Overconfident Tone | UX Trust | P1 | Periodic audit | $6,500 |
| Data Bias | Fairness | P2 | Periodic audit | $5,500 |
| Slow Answers | Latency | P3 | Code-based check | $1,250 |

## Downgrades

### Periodic audit · Overconfident Tone (UX Trust · P1)
- **Cheaper check:** Each week, an analyst reviews 50 answers that make claims without a cited source, and flags any guess stated as fact.
- **Why it’s enough:** It catches the pattern within a week. It misses single cases between audits. We can live with that because the online Data Fabrication eval already catches the worst version: a made-up fact stated with confidence. Tone without fabrication hurts trust slowly. It doesn’t create a wrong number a VP repeats.

### Periodic audit · Data Bias (Fairness · P2)
- **Cheaper check:** Every two weeks, review 30 summaries that cover both US and APAC data, and compare how much space and detail each region gets.
- **Why it’s enough:** It catches a systematic skew, which is how bias shows up. It misses single summaries. We can live with that because most client questions are about US markets today. If APAC questions grow, we move it up.

### Code-based check · Slow Answers (Latency · P3)
- **Cheaper check:** A timer on every release runs the multi-step questions in the golden set and fails if p95 is above 10 seconds.
- **Why it’s enough:** Latency is deterministic and measured exactly by a timer, so a judge adds nothing. It misses slowdowns caused by live load, which existing response-time logging surfaces.


