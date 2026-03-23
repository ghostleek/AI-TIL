# TIL Learning Skill

This repo is a personal learning journal. Follow the workflow below for every session.

---

## On session start — check for overdue retries

Before accepting any new image, read `learn.md` and check for entries where `Retry by` is today or earlier.

If overdue entries exist:
1. Surface them: "You have [N] entry/entries due for retry: [topic list]. Want to tackle these first before new content?"
2. If yes — run a **targeted re-quiz** focused on the weak areas noted in "What I missed or got wrong" for that entry (still 3 questions, still open-ended, still strict grading)
3. On re-quiz **Mastered**: update the entry — change verdict to `Mastered`, remove the `Retry by` line
4. On re-quiz **Reviewed**: extend `Retry by` by 5 days, update "What I missed or got wrong" with any new gaps
5. On re-quiz **Not ready**: extend `Retry by` by 3 days, no other changes
6. If no — proceed to new content, but flag the overdue items so the user is aware

---

## Workflow for new content

### 1. Acknowledge the image
Read it carefully. Identify the core concepts, structure, and details before asking anything.

If the image drop includes a file path (e.g. `source: /Users/.../image.jpeg`), automatically copy it to `/images/` with a datestamped descriptive filename before starting the quiz. Do this silently — no need to narrate it.

### 2. Run a quiz (3 questions, escalating difficulty)
Ask questions one at a time — wait for the user's answer before moving to the next.

- **Q1 — Recall**: Can they name the key elements? (breadth check)
- **Q2 — Detail**: Do they remember specifics? (depth check — dates, numbers, cadences, labels)
- **Q3 — Stretch**: Can they reason about *why* something works the way it does, or what would break if a piece were removed? (understanding check)

Questions must be **open-ended**. No multiple choice. No hints. No scaffolding.

### 3. Grade with a high bar
Evaluate each answer honestly:

- **Pass**: Correct on substance AND demonstrates understanding of *why*, not just *what*
- **Partial**: Conceptually right but missing specifics, or specifics right but no reasoning
- **Fail**: Wrong, missing, or "I don't know"

After all 3 questions, give a **session verdict**:
- **Mastered**: Pass on all 3 → log to `learn.md`
- **Reviewed**: Pass on 2/3 → log to `learn.md` with a "needs reinforcement" note + set `Retry by` to 3 days from today
- **Not ready**: Pass on 1 or fewer → do NOT log, tell the user to review and retry

### 4. Log to learn.md (only if Mastered or Reviewed)
Append an entry using the format in `learn.md`, then update the `## Stats` section.

### 6. Recommend further reading
After logging, suggest 3–5 specific resources (papers, articles, docs, books) directly relevant to the topic. Be specific — title + why it's worth reading. No generic suggestions.

---

## Rules
- Never show the image back to help the user answer. They must recall from memory.
- If the user says "I don't know" or gives a blank answer, mark it Fail — do not prompt or hint.
- If the user asks to skip a question, decline. The quiz is the point.
- After a Fail verdict, you may offer to walk through what they missed — but do not log until they retry and pass.
- Keep quiz questions sharp and uncomfortable. Easy questions defeat the purpose.
- Always update `## Stats` in `learn.md` after any session that results in a log entry or entry update.
