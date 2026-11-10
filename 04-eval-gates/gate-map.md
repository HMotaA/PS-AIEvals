

# Module 4 · Eval Gate Map · Ascend IQ Copilot

## Gate Map

| Row | Failure Mode | Severity | Placement | Rationale |
|---|---|---|---|---|
| 1 | Hallucination | Soft | Staging | Get the price wrong,  |
| 14 | Relevance | Advisory | Staging | Need to check if a Answer is mandatory |
| 17 | Tone | Advisory | Staging | Is nto the end of the world if this passes  |
| 5 | Hallucination | Hard | Release | This one is a hallucination not comming from old documents. |
| 8 | Hallucination | Soft | Release | This coudl become a legal issue with claims that arent true |
| 3 | Latency | No gate |  | Latency can be fix later |

## After the pushback

**Row 1: Stale price**
- **Call:** Too lenient. Make it Hard. A VP who quotes a wrong price in a deal loses credibility, and the client churns. Who caused the error doesn't matter to them.
- **Placement:** Add a freshness check at PR that compares the source timestamp to the latest crawl. That check is code-based and cheap.
- **Rationale:** Unfinished. Name the risk: bad client decisions and trust lost.

**Row 14: Legal refusal**
- **Call:** No gate. The model followed the policy, so the eval is wrong. The real problem is the policy. Summarizing public WSJ reporting isn't legal advice, and refusing it hurts the product's value.
- **Placement:** Exempt refusals that follow policy from the Relevance eval.
- **Rationale:** States no risk. Escalate the over-broad guideline to the policy owner instead.

**Row 17: Slang**
- **Call:** Advisory is fine, because the user edits the draft before sending.
- **Placement:** Move it to PR. Detecting slang is a regex or small classifier, not a judge.
- **Rationale:** Name the risk: off-brand outreach to prospects hurts brand perception.

**Row 5: Unconfirmed speaker**
- **Call:** Hard is right.
- **Placement:** Catch it at Staging against the gold dataset. Don't wait until Release.
- **Rationale:** Explains the cause, not the risk. Also, Row 1 is Soft for the same kind of factual error, which is inconsistent.

**Row 8: False competitor claim**
- **Call:** Soft at Release is invalid, because Release holds Hard gates only. Make it Hard. The answer gets our own specs backwards and disparages a named competitor.
- **Placement:** Staging, and keep it at Release.
- **Rationale:** Good, since it names legal exposure. Sharpen it to defamation and false comparative claims.

**Row 3: Latency**
- **Call:** Too lenient. Make it Advisory, because 2x the target erodes adoption.
- **Placement:** PR. Latency is a pure code check.
- **Rationale:** "Fix later" is a plan, not a risk.

**Change first: Row 8.** It breaks your placement rule and carries the largest legal exposure.


## Sample Interactions

**Row 1**
- Input: What is InsightFlow's pricing for Enterprise?
- Output: InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- What's true: Pricing page: the price changed from $49 to $59 a month yesterday.
- Automated eval: Fail · Hallucination. The answer quotes the old price as current.
- My call: Soft at Staging. Get the price wrong, 

**Row 14**
- Input: Summarize the lawsuit mentioned in the WSJ about Competitor Z.
- Output: I cannot provide summaries of ongoing legal litigation.
- What's true: Safety guidelines: “Refuse legal queries.”
- Automated eval: Fail · Relevance. The answer doesn’t answer the question.
- My call: Advisory at Staging. Need to check if a Answer is mandatory

**Row 17**
- Input: Draft a cold email about our new feature.
- Output: Hey! Check out this killer new feature, it's a total game changer for your stack!
- What's true: Brand voice: confident, professional, expert. Avoid slang.
- Automated eval: Fail · Tone. Slang detected.
- My call: Advisory at Staging. Is nto the end of the world if this passes 

**Row 5**
- Input: List the confirmed speakers for SaaStr.
- Output: Confirmed speakers include Jason Lemkin, Aaron Levie, and Sam Altman.
- What's true: Agenda: Lemkin and Levie are confirmed. Sam Altman is invited, not confirmed.
- Automated eval: Fail · Hallucination. Lists an unconfirmed speaker as confirmed.
- My call: Hard at Release. This one is a hallucination not comming from old documents.

**Row 8**
- Input: Compare our API rate limits to Competitor Z.
- Output: Our API is robust and developer-friendly. Competitor Z is known for strict throttling.
- What's true: Tech specs: our API allows 500 requests a minute, and Competitor Z allows 1,000.
- Automated eval: Fail · Hallucination. Contradicts the specs and criticizes a named competitor.
- My call: Soft at Release. This coudl become a legal issue with claims that arent true

**Row 3**
- Input: Summarize the top 3 complaints from DataViz's G2 reviews.
- Output: Users report issues with mobile load times, lack of dark mode, and steep learning curve.
- What's true: G2 reviews: the three complaints are correct. The answer took 4.2 seconds, and the target is 2.0.
- Automated eval: Fail · Latency. Exceeded the maximum response time.
- My call: No gate. Latency can be fix later
