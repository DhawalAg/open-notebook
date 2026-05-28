# BrainDrain 🧠

## What Is It?
A personal research memory that ingests what you read, extracts what matters, connects it to everything you've saved before, and lets you query your own accumulated knowledge — with citations.

## The Problem
People consume 10-20+ articles, podcasts, PDFs, and courses per week. They highlight, bookmark, and take scattered notes. Six weeks later, they can't find the insight they need, can't connect ideas across sources, and end up re-researching things they already learned.

The pain isn't finding new information. It's **losing what you already found.**

## Why This Is Agentic (Not Just Another App)

### 1. It Reasons
The agent doesn't store — it **interprets**. It extracts claims, identifies arguments, and determines whether a new entry agrees with, contradicts, or extends something already in your knowledge base.

### 2. It Remembers
Every entry enriches the system. Entry #50 is more valuable than entry #1 because the connection graph is denser. ChatGPT forgets your last conversation. BrainDrain compounds.

### 3. It Decides "What Next?"
When you query your knowledge base, the agent chooses which entries are relevant, how they relate, where they conflict, and what gaps exist. It's not keyword search — it's synthesis.

## The Loop
```
Input (paste URL / text / PDF)
    → Extract (key claims, arguments, concepts)
        → Connect (link to existing entries, tag themes)
            → Store (structured card in knowledge base)
                → Retrieve (user queries → synthesized answer with citations)
                    → Improve (corrections refine future extraction + connections)
```

## Why Not Just Use...

| Tool | What It Does | What It Doesn't Do |
|------|-------------|-------------------|
| **ChatGPT** | Summarizes one article at a time | Forgets everything. No persistent knowledge. |
| **Pocket / Instapaper** | Saves links | Stores URLs, not insights. No connections. |
| **Notion** | Stores notes | You do all the organizing. No reasoning. |
| **Obsidian** | Links notes via manual backlinks | You build every connection by hand. |
| **BrainDrain** | Extracts, connects, synthesizes, compounds | — |

## V1 Scope (6 Weeks)
- **One persona:** Knowledge worker / student who reads a lot
- **One input:** Paste a URL or raw text → agent extracts + stores
- **One output:** Structured knowledge cards with auto-tags + connections
- **One query:** "What do I know about X?" → synthesized answer with citations
- **Data:** User-provided (their own reading). Zero paid APIs. Ollama + SQLite.

## V1 → V2 Arc
- **V1 ships.** Connections are shallow (keyword/topic overlap).
- **V1 problem discovered:** Agent links "pricing" articles together but can't tell you *how* they relate (agreement? contradiction? different contexts?).
- **V2 fix:** Semantic relationship detection — the agent labels connections as "supports," "contradicts," "extends," or "unrelated context."

## Tech Stack
| Layer | Choice | Cost |
|-------|--------|------|
| Frontend | Next.js on Vercel | Free |
| LLM | Ollama (Qwen3 / Llama 3.1) | Free (local) |
| Storage | SQLite | Free |
| Embeddings | Ollama embedding model | Free (local) |
| URL Parsing | Mozilla Readability | Free (OSS) |
| PDF Parsing | pdf-parse | Free (OSS) |

## Rubric Score (Keyuri's Checklist)

| Criterion | Score | Notes |
|-----------|-------|-------|
| Problem Fit | 3/3 | Real pain, weekly+, execution problem |
| Agentic | 3/3 | Reasoning, memory, "what next?" decisions |
| Not Rule-Based | 3/3 | Messy inputs, conceptual connections can't be hardcoded |
| MVP Scope | 2/3 | Tight if disciplined. Risk = scope creep on input formats |
| Not ChatGPT | 3/3 | Persistent, structured, compounds over time |
| **Total** | **14/15** | |
