# Ascend IQ Failure Audit

Paste the markdown from the Module 2 Lab Guide (Activity 1) over this file, or upload the downloaded `audit-log.md` in its place, then commit.

_Summary line goes here._

| Query | Judge score | Human override | Trust Metric tag | Failure reason |
|---|---|---|---|---|
# Ascend IQ Failure Audit

11 confirmed failures: #HALLUCINATION ×9, #UX_TRUST ×1, #ROBUSTNESS ×1, #FAIRNESS ×0. I changed 0 of the judge’s calls.

| Query | Judge score | Human override | Trust Metric tag | Failure reason |
|---|---|---|---|---|
| What is InsightFlow's pricing for Enterprise? | 0 |  | #HALLUCINATION | It gives the old cached price instead of the current one, and the "10-seat minimum" isn't in the source: "New Price (Updated yesterday): $59/mo." |
| Summarize the top 3 complaints from DataViz's G2 reviews. | 1 |  |  |  |
| Does InsightFlow support native SQL export? | 0 |  | #HALLUCINATION | A plain "Yes" to a question about *native* export hides that export only works through the API: "there is no 'Native Export' button in the UI." |
| List the confirmed speakers for SaaStr. | 0 |  | #HALLUCINATION | It lists Sam Altman as confirmed, but he hasn't confirmed: "Sam Altman is listed as 'Invited/Tentative.'" |
| What is the sentiment of the latest TechCrunch article on us? | 0 |  | #HALLUCINATION | It says the sentiment is simply positive and adds UI and pricing details the source doesn't contain: "Sentiment: Neutral/Positive." |
| Give me a bio for Sarah Jenkins, the new VP at DataViz. | 0 |  | #HALLUCINATION | It gets her previous title wrong, which understates her seniority in an executive bio: "Prev: Sr. Director @ Salesforce." |
| Compare our API rate limits to Competitor Z. | 0 |  | #HALLUCINATION | It gives vague praise where numbers were asked for and reverses the actual comparison: "Us: 500 req/min. Competitor Z: 1000 req/min (Twice as fast)." |
| Is Competitor X SOC2 compliant? | 0 |  | #ROBUSTNESS | It says it can't find the information, but the source shows it plainly: "'SOC2 Type II Certified' badge visible." |
| When was InsightFlow's last funding round? | 1 |  |  |  |
| Who is the CEO of DataViz? | 1 |  |  |  |
| Does Competitor Y integrate with HubSpot? | 0 |  | #HALLUCINATION | "Seamless integration" implies a native connector, but it only works through a third party: "HubSpot integration available via Zapier partnership." |
| What are the primary brand colors for InsightFlow? | 0 |  | #HALLUCINATION | It calls Charcoal a primary color, and the hex code isn't in the source: "Primary: Electric Blue. Secondary: Charcoal." |
| Summarize the lawsuit mentioned in the WSJ about Competitor Z. | 1 |  |  |  |
| List the HQ locations for DataViz. | 0 |  | #HALLUCINATION | It calls Austin a second HQ, but the source says it's an engineering hub: "HQ: San Francisco. Engineering Hub: Austin." |
| How many employees does InsightFlow have? | 1 |  |  |  |
| Draft a cold email about our new feature. | 0 |  | #UX_TRUST | The slang tone ("killer," "game changer") breaks the brand voice and would hurt credibility with VP-level readers: "Tone: Confident, professional, expert. Avoid slang." |
| Does Competitor X offer 24/7 support? | 1 |  |  |  |
| What database backend does DataViz use? | 1 |  |  |  |
| Summarize the latest release notes for InsightFlow. | 1 |  |  |  |
| What is the market cap of Competitor Z? | 1 |  |  |  |

