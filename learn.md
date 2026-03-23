# TIL Learning Log

A persistent record of things learned, quizzed, and retained.

---

## Stats

| Metric | Count |
|---|---|
| Total entries | 2 |
| Mastered | 0 |
| Reviewed (pending retry) | 2 |
| Topics covered | AI tools, productivity, search infrastructure |

---

## Log format

```
### YYYY-MM-DD — [Topic]
**Source**: `/images/[filename]`
**Verdict**: Mastered | Reviewed (needs reinforcement on: X)
**Difficulty**: Easy | Medium | Hard
**Retry by**: YYYY-MM-DD *(only present if Reviewed)*

**Key concepts**:
- ...

**What I got right**:
- ...

**What I missed or got wrong**:
- ...

**Takeaway**: [one sentence on the core insight worth remembering]

**Further reading**:
- ...
```

---

## Entries

### 2026-03-19 — Hybrid Search Funnel (ByteDance + Apache Doris 4.0)
**Source**: `/images/2026-03-19-hybrid-search-funnel.png` *(save this file manually)*
**Verdict**: Reviewed — needs reinforcement on: candidate counts, 7x faster stat, structured filter internals, reranking mechanism, token vs compute cost distinction
**Difficulty**: Medium
**Retry by**: 2026-03-22

**Key concepts**:
- Hybrid search funnel: 4 steps to reduce 1B+ vectors down to top 10 results
- Step 1 — Structured Filter: metadata/SQL-style index lookups. 100M → 2M candidates
- Step 2 — Keyword Filter: inverted index (BM25) matching. 2M → 15K candidates
- Step 3 — Vector Search: cosine similarity on embeddings. 15K → 100 candidates
- Step 4 — Reranking: ML model combines scores from multiple signals. 100 → top 10
- Total: 400ms — 7x faster than pure vector search
- Ordering is deliberate: cheapest, highest-elimination steps run first to minimise expensive compute

**What I got right**:
- Named all 4 steps correctly
- Understood structured filter eliminates the most candidates by absolute volume
- Understood vector search approximates semantic meaning
- Correctly reasoned why the funnel order matters (cheap first, expensive last)
- Remembered 400ms

**What I missed or got wrong**:
- All candidate counts (looked at image — disqualified)
- Missed "7x faster than pure vector search" stat
- Confused vector search cost with LLM token consumption — it's compute (distance calculations), not tokens
- Gaps on structured filter internals (SQL/metadata index lookups) and reranking (ML model combining scores)

**Takeaway**: Run the cheapest, most selective filters first — structured and keyword — so vector similarity (the expensive step) only touches a small, already-relevant candidate set.

**Further reading**:
- *"Faiss: A Library for Efficient Similarity Search"* (Johnson et al., Meta AI) — foundational paper on vector similarity at scale, directly relevant to why step 3 is expensive
- *"BM25 and Beyond"* (Robertson & Zaragoza) — explains the keyword ranking model behind step 2
- Apache Doris docs on Hybrid Search — practical implementation of exactly this funnel
- *"Learning to Rank for Information Retrieval"* (Liu, 2011) — covers the ML reranking models used in step 4
- Pinecone's blog "Hybrid Search Explained" — accessible overview of combining sparse + dense retrieval

---

### 2026-03-19 — Claude Cowork for PMs
**Source**: `/images/2026-03-19-claude-cowork-for-pms.png` *(save this file manually)*
**Verdict**: Reviewed — needs reinforcement on: scheduler cadence reasoning
**Difficulty**: Medium
**Retry by**: 2026-03-22

**Key concepts**:
- 5 PM use cases: Market research digest, Interview scheduling, Competitor monitoring, Support feedback prioritization, Release notes generator
- Each use case pairs a Claude prompt with MCP connections and a run schedule
- Schedules: market research (weekly), interview scheduling (every morning), competitor monitoring (weekly), support feedback (daily), release notes (manual before release)
- MCP connections are required bridges to external tools — without them, read/write actions to calendars, docs, CRMs, and the web are impossible

**What I got right**:
- Named all 5 use cases correctly
- Understood MCP as a dependency chain — losing MCP breaks write functions, not just reads
- Correctly identified competitor monitoring as weekly
- Grasped that release notes are event-driven, not time-driven

**What I missed or got wrong**:
- Cadences for 4/5 use cases (market research, interview scheduling, support feedback)
- Key insight missed: automation is most valuable for high-friction, high-frequency tasks that humans deprioritize (e.g., daily support triage, morning interview slot-finding)

**Takeaway**: Scheduler cadence should match the tempo and cost-of-delay of the underlying workflow — not your preference for manual control.
