# BrainDrain Persona Map

## How to Use This Document

This maps every plausible user of BrainDrain. Each persona is evaluated against:
- **Pain intensity**: How badly do they feel this problem today?
- **Willingness to pay**: Would they pay for a solution?
- **Agentic fit**: Do they actually need reasoning, or just retrieval?
- **6-week demo-ability**: Can we show value to this persona in 6 weeks?

**We have not picked a primary persona yet.** That decision is captured in `06-project-state.md`.

---

## Persona 1: The Analyst / Researcher
*"I read 15 sources a week for a deliverable. I can't hold contradictions in my head."*

### Profile
- **Role**: Strategy analyst, market researcher, policy analyst, academic researcher
- **Reading volume**: High (10-20 sources/week, often on a single narrow topic)
- **Output**: Memo, report, deck, paper — synthesizing across sources
- **Current tools**: Zotero, Notion, manually color-coded highlights, Excel trackers
- **Current pain**: Building a literature review by hand. Forgetting what Source A said when reading Source D. Manually reconciling contradictions.

### Jobs to Be Done
1. Collect and organize sources on a topic
2. Understand where sources agree vs. disagree
3. Synthesize across all sources for a deliverable
4. Cite correctly (which source said what)

### BrainDrain Fit
| Dimension | Score | Notes |
|---|---|---|
| Pain intensity | ⭐⭐⭐⭐⭐ | This is their literal job; doing it manually is expensive |
| Willingness to pay | ⭐⭐⭐⭐ | If it saves 3 hours/week, easy ROI |
| Agentic fit | ⭐⭐⭐⭐⭐ | Contradiction detection is exactly what they need |
| 6-week demo-ability | ⭐⭐⭐⭐ | Can build a topic-specific knowledge base fast |

### Quote this persona would say
> "I'm reading my 12th article on pricing strategy and I have no idea if it agrees with the 4th one I read last week."

### Risk
- Expects citations and source attribution — extraction quality must be high
- May need PDF support (academic papers) — that's a V1.5 feature

---

## Persona 2: The Strategy / Product PM
*"I make decisions based on things I've read. I need to know if my mental model is contradicted by evidence."*

### Profile
- **Role**: Senior PM, Head of Product, Strategy lead, Chief of Staff
- **Reading volume**: Medium-high (5-10 articles/week across topics)
- **Output**: Strategy docs, PRDs, decisions, recommendations
- **Current tools**: Browser bookmarks, Pocket/Instapaper (saved and never revisited), saved Slack links
- **Current pain**: Reading broadly but building no durable knowledge. Making decisions based on half-remembered articles. Can't quickly pull "everything I know about pricing psychology."

### Jobs to Be Done
1. Build a queryable memory of their reading
2. Quickly synthesize "what do I know about X" when writing a strategy doc
3. Surface when a new article challenges an existing belief
4. Share synthesized knowledge with team

### BrainDrain Fit
| Dimension | Score | Notes |
|---|---|---|
| Pain intensity | ⭐⭐⭐⭐ | Real pain, but less acute than Analyst |
| Willingness to pay | ⭐⭐⭐⭐ | Will pay for tools that save thinking time |
| Agentic fit | ⭐⭐⭐⭐ | Conflict surfacing is genuinely valuable for decision quality |
| 6-week demo-ability | ⭐⭐⭐⭐⭐ | Diverse reading = richer demo; broad topics work well |

### Quote this persona would say
> "I have a Pocket queue of 200 articles I'll never re-read. But I also have no idea what I actually know."

### Risk
- Less structured than Analyst — entries will be across many topics, not a single research question
- Value is slower to emerge (needs 20+ varied entries to see cross-topic connections)

---

## Persona 3: The Writer / Journalist / Content Creator
*"I consume content constantly to inform my writing. I need to find the thread connecting 6 things I read."*

### Profile
- **Role**: Newsletter writer, journalist, author, blogger, Substacker
- **Reading volume**: Very high (20+ sources/week across a beat)
- **Output**: Articles, essays, newsletters — synthesizing trends and ideas
- **Current tools**: Readwise + Roam/Obsidian highlights, research folders, saved tweets
- **Current pain**: Finding the connection between disparate things they've read. Building the "spine" of a piece from scattered notes. Identifying what's genuinely new vs. what confirms existing narrative.

### Jobs to Be Done
1. Capture reading in a way that surfaces later for relevant pieces
2. Find non-obvious connections between distant ideas
3. Identify when a new article contradicts or extends a trend they're tracking
4. Build a "second brain" that helps them write, not just store

### BrainDrain Fit
| Dimension | Score | Notes |
|---|---|---|
| Pain intensity | ⭐⭐⭐⭐⭐ | This is their raw material — losing it is professional pain |
| Willingness to pay | ⭐⭐⭐ | Writers are price-sensitive; prosumer tier is the market |
| Agentic fit | ⭐⭐⭐ | More interested in connections than contradictions |
| 6-week demo-ability | ⭐⭐⭐ | Diverse reading complicates the demo; needs more entries |

### Quote this persona would say
> "I know I read something about this three months ago that would be perfect for this piece. I have no idea where it is."

### Risk
- They already have tools (Readwise, Roam, Obsidian) — BrainDrain must be meaningfully better, not just different
- Value proposition shifts toward "connection discovery" more than "contradiction detection"
- High churn risk if they already have a workflow

---

## Persona 4: The Lifelong Learner / Curious Generalist
*"I read across topics for personal growth. I want my learning to connect."*

### Profile
- **Role**: Any — executive, engineer, teacher, professional who reads for self-improvement
- **Reading volume**: Medium (3-7 articles/week, across very different topics)
- **Output**: Better thinking, personal development, cocktail party knowledge
- **Current tools**: Safari reading list, forwarded emails, occasional Kindle highlights
- **Current pain**: Forgetting everything. Feeling like reading is a passive activity with no lasting benefit.

### Jobs to Be Done
1. Build a personal knowledge base that actually persists
2. Query what they know when relevant topics come up in conversation or work
3. See their knowledge grow over time (a sense of compounding)

### BrainDrain Fit
| Dimension | Score | Notes |
|---|---|---|
| Pain intensity | ⭐⭐⭐ | Real but diffuse — it's a "nice to have" pain, not acute |
| Willingness to pay | ⭐⭐ | Hard to quantify ROI; consumer pricing pressure |
| Agentic fit | ⭐⭐ | Contradictions matter less; connection discovery matters more |
| 6-week demo-ability | ⭐⭐ | Needs time to build; "aha moment" is slow |

### Quote this persona would say
> "I read Atomic Habits, the Four Agreements, and three neuroscience articles. Do they connect? I have no idea."

### Risk
- Lowest pain intensity of all personas
- ROI is hardest to articulate — it's emotional, not economic
- Consumer B2C market is hard to monetize; bad fit for B2B pricing
- Biggest market by volume, worst fit for a 6-week agentic MVP

---

## Persona 5: The Investor / Due Diligence Professional
*"I read hundreds of sources about a company or market before making a decision."*

### Profile
- **Role**: VC, angel investor, PE analyst, M&A advisor
- **Reading volume**: Very high, but topic-concentrated (deep on one company/market at a time)
- **Output**: Investment memo, due diligence report, thesis
- **Current tools**: Bloomberg, PitchBook, Notion, Google Docs notes
- **Current pain**: Reconciling conflicting signals from different sources (founder deck vs. press reports vs. analyst notes). Tracking how a narrative has evolved over 6 months.

### Jobs to Be Done
1. Build a time-ordered knowledge base on a specific company or market
2. Detect when new information changes or contradicts earlier signals
3. Synthesize across primary and secondary sources for a memo
4. Track how their thesis evolves as they learn more

### BrainDrain Fit
| Dimension | Score | Notes |
|---|---|---|
| Pain intensity | ⭐⭐⭐⭐⭐ | Getting this wrong costs money — pain is acute |
| Willingness to pay | ⭐⭐⭐⭐⭐ | Highest WTP of all personas; enterprise pricing possible |
| Agentic fit | ⭐⭐⭐⭐⭐ | Contradiction detection is literally due diligence |
| 6-week demo-ability | ⭐⭐⭐ | Need a realistic dataset; harder to fake in a demo |

### Quote this persona would say
> "The founder's deck says the market is $10B. Three analyst reports I read say it's $2B. Somewhere in my notes I flagged this. I can't find it."

### Risk
- Highest bar for accuracy — they act on this information
- May need structured data (financials, dates, named entities) beyond plain text
- Sales cycle is long; getting one investor to adopt is hard in 6 weeks

---

## Persona Comparison Matrix

| Dimension | Analyst | Strategy PM | Writer | Learner | Investor |
|---|---|---|---|---|---|
| Pain intensity | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Willingness to pay | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| Agentic fit | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| Demo-ability (6wk) | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ |
| Market size | Medium | Large | Medium | Huge | Small |
| B2B potential | Medium | High | Low | None | High |

---

## Recommended Primary Persona Candidates

**For a 6-week MVP evaluated on agentic reasoning:**

### Option A: The Analyst (best agentic fit)
Contradiction detection maps directly to their daily work. Easy to demo on a single topic. Pain is economic and immediate. Risk: needs citations, may need PDFs.

### Option B: The Strategy PM (best demo-ability)
Broadest reading = richest demo. Clear ROI story. Familiar persona for a Maven course audience. Risk: value compounds slowly; harder to WOW in one session.

### Option C: The Investor (highest WTP, best long-term)
The due diligence use case is the most economically motivated version of contradiction detection. Risk: hardest to demo authentically in 6 weeks.

**Decision deferred.** See `06-project-state.md` for how to make this call.
