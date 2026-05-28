# Making BrainDrain Genuinely Agentic: A Technical Blueprint

## What Changes Between "RAG with Memory" and "Agentic"

The gap is one loop: **does the system evaluate its own output and decide what to do next?**

RAG pipeline: Input → Retrieve → Generate → Output (done)
Agentic loop:  Input → Retrieve → Generate → **Evaluate → Decide → Act → (repeat)** → Output

BrainDrain needs this loop in two places: **ingestion** and **query**.

---

## The Minimum Agentic V1: Ingestion Reasoning Loop

This is the one loop that makes BrainDrain genuinely different from Open Notebook and ChatGPT. Without it, BrainDrain is just Open Notebook with SQLite.

### How it works

```
User pastes URL or text
  ↓
[Step 1 - Extract] LLM extracts:
  - 3-7 key claims (specific, falsifiable assertions)
  - Main argument (what is the author trying to prove?)
  - Domain tags (pricing, remote work, leadership, etc.)
  ↓
[Step 2 - Search] Embedding search:
  - Find top 10 existing entries by semantic similarity
  ↓
[Step 3 - Reason] LLM evaluates:
  - For each similar entry: does this new entry SUPPORT, CONTRADICT, EXTEND, or REFRAME it?
  - If CONTRADICT: what specifically disagrees? (not vibes — cite the claims)
  - Confidence score for each relationship (0.0–1.0)
  ↓
[Step 4 - Decide] Agent decides:
  - Create new standalone card (if no strong connections)
  - Create card with labeled connections (if 1-3 relationships found)
  - Flag for user review (if high-confidence contradiction found)
  ↓
[Step 5 - Store] Save to SQLite:
  - KnowledgeCard (claims, argument, tags, source URL, timestamp)
  - Relationships (card_id → card_id, type, explanation, confidence)
```

### Why this is agentic (by the checklist)
- ✅ Reasoning: LLM evaluates relationships, not just retrieves
- ✅ Decision-making: System decides card structure based on what it finds
- ✅ Not rule-based: Contradiction detection can't be hardcoded
- ✅ Compounds: Entry #50 produces more relationship edges than Entry #1

---

## The LLM Prompts That Make This Work

### Extraction prompt (Step 1)
```
You are analyzing an article/text to extract structured knowledge.

TEXT: {text}

Extract:
1. CLAIMS: List 3-7 specific, falsifiable claims the author makes.
   Each claim should be a complete sentence that could be true or false.
2. MAIN_ARGUMENT: In one sentence, what is the author's central thesis?
3. TAGS: 2-5 domain tags (e.g., "pricing", "remote-work", "leadership")

Return JSON only. No explanation.
```

### Relationship reasoning prompt (Step 3)
```
You have ingested a new knowledge entry. Compare it against existing entries.

NEW ENTRY:
Claims: {new_claims}
Argument: {new_argument}

EXISTING ENTRIES (most similar):
{formatted_existing_entries}

For each existing entry, classify the relationship:
- SUPPORTS: New entry provides evidence for or agrees with existing entry
- CONTRADICTS: New entry makes a claim that directly conflicts with existing entry
- EXTENDS: New entry adds new information to existing entry's topic
- UNRELATED: Similar topic but no meaningful relationship

For any CONTRADICTS relationship, quote the specific conflicting claims.
Return JSON: [{entry_id, relationship_type, explanation, confidence}]
```

---

## The Query Loop (Minimum Viable)

The query loop is simpler — start with strategy generation (like Open Notebook's `ask.py`) and add conflict surfacing:

```
User query: "What do I know about remote work productivity?"
  ↓
[Step 1 - Strategy] LLM generates 3-5 search terms
  → ["remote work productivity", "office vs remote", "async work outcomes", ...]
  ↓
[Step 2 - Retrieve] Vector search each term → top 5 cards each
  ↓
[Step 3 - Check conflicts] Pull relationship edges between retrieved cards
  → Find any CONTRADICTS relationships in the result set
  ↓
[Step 4 - Synthesize] LLM writes answer:
  - Summary of what you know
  - Areas of agreement across sources
  - Conflicts surfaced explicitly: "Note: Entry #12 (Stanford, 2024) contradicts Entry #47 (HBR, 2023) on..."
  - Gaps: "You have no entries on async tools specifically"
```

The conflict surfacing in Step 3-4 is what makes this different from Open Notebook. Same retrieval pattern, different synthesis instruction.

---

## Data Model (Minimal SQLite Schema)

```sql
CREATE TABLE knowledge_cards (
  id          TEXT PRIMARY KEY,  -- uuid
  source_url  TEXT,
  raw_text    TEXT,
  main_arg    TEXT,
  claims      TEXT,              -- JSON array of strings
  tags        TEXT,              -- JSON array of strings
  embedding   BLOB,              -- for vector search
  created_at  DATETIME
);

CREATE TABLE relationships (
  id              TEXT PRIMARY KEY,
  from_card_id    TEXT REFERENCES knowledge_cards(id),
  to_card_id      TEXT REFERENCES knowledge_cards(id),
  relationship    TEXT,  -- SUPPORTS | CONTRADICTS | EXTENDS | UNRELATED
  explanation     TEXT,  -- LLM-generated explanation
  confidence      REAL,  -- 0.0-1.0
  created_at      DATETIME
);
```

This is the whole schema for V1. Simple, queryable, demostrable.

---

## The Ollama Risk

The ingestion reasoning loop (Step 3) requires the LLM to reason about relationships across multiple texts simultaneously. This is cognitively demanding.

### Model recommendations
- **Minimum**: Qwen3-8B or Llama 3.1-8B (will struggle with nuance)
- **Recommended**: Qwen3-14B or Llama 3.1-70B (better relationship reasoning)
- **Test this early**: Week 1 — prompt the relationship reasoning step with 5 real examples and evaluate output quality before building the pipeline

### Fallback if local models are too weak
- Use OpenAI API for the relationship reasoning step only (one call per ingestion, ~$0.01)
- Keep everything else local
- This preserves the "free" framing while ensuring quality on the hard part

---

## 6-Week Build Plan

| Week | Goal | Agentic milestone |
|--|--|--|
| 1 | URL extraction → raw text → SQLite storage | None (plumbing) |
| 2 | Embedding + vector search working | None (plumbing) |
| 3 | Extraction prompt → KnowledgeCard created | LLM reasons about claims |
| 4 | Relationship reasoning loop on ingestion | **First agentic moment** |
| 5 | Query loop with conflict surfacing | **Second agentic moment** |
| 6 | Polish UI, demo, stress test with 20+ entries | Compounding visible |

**The agentic work starts Week 3.** If you run out of time, Weeks 1-2 give you a RAG app. Weeks 3-4 give you a genuinely agentic product.

---

## What to Demo at Week 6

The killer demo sequence:
1. Paste an article arguing "remote work kills productivity" (e.g., a 2023 McKinsey report)
2. System ingests it, shows extracted claims, shows it stored as a card
3. Paste a second article arguing "remote work increases deep work" (e.g., a Stanford study)
4. System ingests it — **and flags a contradiction with the first article**
5. Ask: "What do I know about remote work and productivity?"
6. System returns answer that explicitly surfaces the conflict: "Note: Your two sources on this topic contradict each other. McKinsey (2023) argues X. Stanford (2024) argues Y. The disagreement centers on..."

**That moment — the system catching a contradiction you didn't notice — is the product.** Nothing else does that.
