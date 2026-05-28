# BrainDrain: Project State & Decision Log

*This document is the "pick up where you left off" file. Update it at the start and end of every working session.*

**Last updated**: February 2026
**Current phase**: Pre-build — problem definition & architecture decisions
**Next session goal**: Lock primary persona, finalize V1 scope, begin architecture doc

---

## What We Know (Settled)

### The Core Problem
Knowledge workers read constantly but retain and connect almost nothing. The pain is not "I can't find information on the internet." The pain is "I can't find *what I already know*."

### The Differentiating Mechanic
Relationship reasoning at ingestion or query time: the system labels whether new content **supports, contradicts, extends, or is unrelated to** existing knowledge. This is what separates BrainDrain from:
- Pocket / Instapaper (save but never synthesize)
- Notion (manual organization, no reasoning)
- Open Notebook (RAG + retrieval, no relationship detection)
- ChatGPT (no persistent memory, no compounding)

### The Agentic Loop (Validated)
The minimum agentic V1 is the **ingestion reasoning loop**:
```
New content → extract claims → search existing knowledge → LLM reasons:
support / contradict / extend → label relationship → store card
```
Without this loop, BrainDrain is just Open Notebook with a simpler stack.

### North Star Metric (Settled)
> **Weekly queries from users with ≥10 entries**

Supporting metrics: conflict precision (≥70%), query relevance (≥80%), D7 retention.

### Tech Preference (Directional)
- Basic UI preferred over CLI (visual contradiction surfacing is the demo)
- Ollama for local inference (privacy-first, free tier)
- Simple stack: Next.js + SQLite + vector search
- Fallback: use OpenAI API for relationship reasoning step only if Ollama quality is insufficient

---

## Open Decisions (Need Resolution)

### Decision 1: Primary Persona ⚡ BLOCKING
**Status**: Undecided
**Options**:
| Option | Pros | Cons |
|---|---|---|
| **Analyst / Researcher** | Best agentic fit, acute pain, topically deep reading = great demo | Needs citations, may need PDFs |
| **Strategy PM** | Best demo-ability, large market, relatable to Maven audience | Value compounds slowly, harder WOW moment |
| **Investor / Due Diligence** | Highest WTP, contradiction detection = their job | Hardest to demo authentically in 6 weeks |

**How to decide**: Pick the persona you can recruit 3 real test users from in Week 5. That's the tiebreaker.

**My lean**: Strategy PM for the Maven demo (relatable, demo-able). Investor as the V1.5 monetization target.

---

### Decision 2: Agentic Trigger — Ingestion vs. Query Time
**Status**: Undecided
**Options**:

| Option | UX | Pricing | Complexity |
|---|---|---|---|
| **At ingestion** | Immediate feedback ("found 2 conflicts!") | Cost per add | More complex |
| **At query time** | Reasoning happens when user asks | Cost per query | Simpler to build |
| **Hybrid** | Light tagging on ingest, deep reasoning at query | Best of both | Most complex |

**My lean**: Start with **query time** for V1. Easier to ship, easier to price. Add ingestion-time conflict badges in V1.5 if query quality is high.

---

### Decision 3: Input Types for V1
**Status**: Undecided
**Options**:

| Scope | Effort | Coverage |
|---|---|---|
| URL only | 1 day | 70% of real use case |
| URL + raw text paste | 2 days | 90% of real use case |
| URL + text + image (OCR) | 1 week | 95% — but adds risk |

**My lean**: **URL + text paste** for V1. Image OCR is V1.5.

---

### Decision 4: Monetization Model
**Status**: Not locked — keep flexible
**Current thinking**:
- Open source / self-hosted for the Maven demo
- Freemium (N queries/month free, paid for unlimited) as the business model
- Enterprise tier for Investor persona (team knowledge bases, shared workspaces)

---

## What We Still Need to Figure Out

### Technical unknowns (Week 1 experiments)
- [ ] Can Ollama (Qwen3-14B or Llama 3.1-70B) reliably detect contradictions across two article summaries? → **Must test before committing to local-only**
- [ ] What's the latency of the relationship reasoning step? → Acceptable if <10s per ingestion
- [ ] SQLite vector search performance at 1,000+ entries → Test with sqlite-vss or use LanceDB

### Product unknowns (Week 1-2)
- [ ] What does "extraction quality" feel like in practice? → Run 20 real articles through extraction, rate manually
- [ ] What's the right number of claims to extract? (3 too few? 10 too many?) → Experiment
- [ ] Does the system surface conflicts that feel genuine, or does it hallucinate? → Must eval before shipping

### UX unknowns (Week 3)
- [ ] How do you display a contradiction without making the UI feel adversarial?
- [ ] What's the right entry point — URL bar on homepage, or floating input?
- [ ] Does the query feel like a chat or a search? (Chat: conversational. Search: fast.)

---

## The 6-Week Plan (Draft)

| Week | Goal | Output |
|---|---|---|
| **Week 1** | Foundation + LLM validation | URL scraping → text → SQLite storage. Test Ollama extraction quality on 20 articles. |
| **Week 2** | Knowledge base + search | Embeddings generated. Vector search working. Basic card display UI. |
| **Week 3** | Extraction + ingestion pipeline | LLM extracts claims + tags per entry. Ingestion pipeline end-to-end. |
| **Week 4** | Query loop + relationship reasoning | "Ask what I know" query. LLM surfaces relationships + conflicts in response. |
| **Week 5** | UI polish + user testing | 3 test users add 10-15 entries each. Rate extraction + query quality. |
| **Week 6** | Demo prep + eval | Conflict precision/recall on test set. Rehearsed demo sequence. Course submission. |

**The gate**: If relationship reasoning quality (conflict precision ≥60%) isn't achievable by Week 4, pivot to surfacing agreement/similarity only and position as "knowledge synthesis" rather than "contradiction detection."

---

## Open Questions to Raise with Course Mentors

1. Is the "Wikipedia for your own reading" framing a good pitch, or too abstract?
2. Analyst vs. PM persona — which does the Maven cohort relate to more?
3. Is 6 weeks enough to prove product-market fit signal, or just technical proof of concept?
4. Should the demo use real user-generated data or a pre-built synthetic dataset?

---

## Files in This Project

| File | Purpose |
|---|---|
| `brain-rot.md` | Original raw idea / problem statement |
| `Project Self Evaluation Checklist.md` | Maven course rubric |
| `01-agentic-vs-generative-analysis.md` | Verdict on Open Notebook + BrainDrain agentic status |
| `02-braindrain-vs-open-notebook.md` | Product + technical comparison |
| `03-making-braindrain-agentic.md` | Technical blueprint for the ingestion reasoning loop |
| `04-north-star-metrics.md` | NSM, supporting metrics, evaluation plan |
| `05-persona-map.md` | 5 personas with scores + comparison matrix |
| `06-project-state.md` | This file — current state + open decisions |

---

## How to Resume This Project

1. Read `06-project-state.md` (this file) first
2. Check "Open Decisions" — resolve any BLOCKING ones before proceeding
3. Read the specific doc for whatever you're working on
4. Update this file at the end of every session with new decisions made
