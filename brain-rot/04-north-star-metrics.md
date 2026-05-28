# North Star Metrics & Evaluation Framework

## The Value Hierarchy

BrainDrain delivers value at three levels, each building on the previous:

```
Level 1 (Retention):    You add content → it's stored and retrievable
Level 2 (Retrieval):    You query → you get a useful synthesized answer
Level 3 (Reasoning):    You query → agent surfaces what you missed (conflicts, gaps)
```

Level 1 is a bookmark manager. Level 2 is RAG. Level 3 is the actual product.
**The north star should measure Level 3 adoption, not Level 1 activity.**

---

## North Star Metric

> **Weekly queries from users with ≥10 entries**

**Why this works:**
- Requires the knowledge base to be real (≥10 entries = actual usage)
- Requires the user to find the query valuable enough to return
- Captures compounding — a user with 30 entries querying weekly has proven the value loop
- Fails fast — if users add entries but never query, the synthesis is broken
- Fails informatively — if users query before 10 entries, they're not seeing compounding yet

**Formula:**
```
NSM = count of users who:
  (a) have ≥10 entries in their knowledge base AND
  (b) submitted ≥1 query in the last 7 days
```

**Week 6 demo target:** 3+ test users doing this with a synthetic dataset

---

## Supporting Metrics

### Input Health (Is the knowledge base growing?)

| Metric | Description | Target (Week 6) |
|---|---|---|
| Entries added / user / week | Active users should be adding 3-5/week | ≥3 for engaged users |
| Ingestion success rate | % of URLs that successfully extract + store | ≥90% |
| Avg claims extracted per entry | Quality proxy — too few = extraction broken | 3-6 per entry |
| Tag accuracy | Do auto-tags match the article's actual topic? | 80%+ human-rated |

### Agent Quality (Is the reasoning useful?)

| Metric | Description | Target (Week 6) |
|---|---|---|
| Conflict precision | When agent says "contradicts," is it real? | ≥70% on test set |
| Conflict recall | % of genuine conflicts in dataset that agent catches | ≥60% on test set |
| Query relevance | % of queries where retrieved cards are on-topic | ≥80% human-rated |
| Answer usefulness | Post-query: "Was this useful?" (thumbs up/down) | ≥65% positive |

### Engagement (Is the product sticky?)

| Metric | Description | Priority |
|---|---|---|
| D7 retention | Did user return after first session? | High |
| D30 retention | Still using after a month? | Medium (post-launch) |
| Conflict click rate | % of surfaced conflicts that user clicks to read | High (proves value) |
| Queries per session | Average queries per visit | Medium |
| Entries at churn | How many entries did churned users have? | Medium (post-launch) |

---

## How to Evaluate Performance (6-Week Test Plan)

### Week 3-4: Extraction Quality
**Method**: Build a test set of 20 articles across 4-5 domains. Manually label:
- Ground truth claims for each article (what are the 3-7 key assertions?)
- Ground truth tags
Compare against what the system extracts. Score precision/recall.

### Week 4-5: Relationship Reasoning Quality
**Method**: Build a synthetic dataset with known contradictions:
- 5 pairs of articles that clearly contradict each other
- 5 pairs that support each other
- 5 pairs that are related but not conflicting
Run ingestion on all 15. Score: does the system correctly classify each pair?

**This is the most important evaluation.** If relationship reasoning doesn't work, the product doesn't work.

### Week 5-6: End-to-End Query Quality
**Method**: 3-5 test users (course peers, friends) each add 10-15 articles. Ask them to:
1. Query 5 things they think they know
2. Rate each answer: useful / not useful / partially useful
3. For surfaced conflicts: was this a real conflict?

Target: 65%+ useful rating, 70%+ conflict precision.

---

## What "Good" Looks Like

**If BrainDrain is working**, a user with 20 entries should experience this:

> "I asked what I know about remote work, and it gave me a 4-paragraph synthesis from 6 of my articles. It also flagged that the Stanford study I saved contradicts the McKinsey report I saved last month — and explained exactly why. I didn't remember saving both of those."

**If BrainDrain is just RAG**, a user with 20 entries experiences this:

> "I asked what I know about remote work and got back a summary of the most similar article I saved. It was fine."

The difference between these two experiences is the relationship reasoning loop. Every metric should ladder up to whether users are experiencing the first version.

---

## Metrics Anti-Patterns to Avoid

| Vanity metric | Why it's misleading |
|---|---|
| Total entries added | Users can add 100 entries and never query |
| Total queries | Doesn't tell you if the knowledge base was rich enough to be useful |
| Conflict count | Agent can hallucinate conflicts — precision matters more than volume |
| DAU/MAU | Too early; focus on depth before breadth |
| Time on site | Not relevant for a tool used in short focused bursts |

---

## Decision Log: Metrics

| Decision | Choice | Rationale |
|---|---|---|
| North star timing | Query-time, not ingestion-time | Compounding is proven at query, not add |
| Entry threshold | 10 entries | Below 10, no meaningful pattern to surface |
| Conflict measurement | Precision-first | Better to surface 3 real conflicts than 10 guesses |
| Eval method | Human rating (Week 6) | Automated eval requires ground truth we don't have yet |
