# Photographic Memory

Most people consume content passively. Screenshots pile up. Highlights go unread. You feel productive, but nothing sticks.

This repo is an antidote. Every time I learn something from an image, Claude quizzes me on it before it gets logged. No pass, no log. The system doesn't care about your intentions — only your recall.

---

## How it works

1. **Share an image** with Claude in this repo
2. **Get quizzed** — 3 open-ended questions, escalating from recall → detail → reasoning
3. **Pass the bar** — Claude grades strictly. Partial credit exists, but vague answers fail.
4. **Get logged** — only passing sessions are recorded in `learn.md`
5. **Retry weak spots** — entries flagged for reinforcement surface automatically at the next session

The quiz can't be skipped. Claude won't hint. "I don't know" is a fail.

---

## Verdicts

| Verdict | Criteria | Logged? | Retry? |
|---|---|---|---|
| **Mastered** | Pass all 3 questions | Yes | No |
| **Reviewed** | Pass 2/3 | Yes, with gaps noted | Yes, in 3 days |
| **Not ready** | Pass 1 or fewer | No | Review and retry |

---

## Spaced repetition

`learn.md` tracks a `Retry by` date for every Reviewed entry. At the start of each session, Claude checks for overdue entries and offers to re-quiz before accepting new content.

On retry:
- **Mastered** → entry upgraded, retry date removed
- **Still reviewed** → retry pushed 5 days forward
- **Not ready** → retry pushed 3 days forward

---

## File structure

```
/
├── CLAUDE.md          # Skill instructions for Claude
├── learn.md           # Persistent learning log
├── images/            # Source images for logged entries (saved manually)
└── README.md
```

---

## Setup

1. Clone this repo
2. Open it in [Claude Code](https://claude.ai/code)
3. Share an image — Claude reads `CLAUDE.md` automatically and runs the quiz

No config. No installs. Just Claude and a directory.

---

## Why this works

- **Forced retrieval** is one of the most effective learning techniques (see: testing effect)
- **Logging only what you've proven you know** keeps the journal honest
- **Spaced repetition** surfaces weak entries before they're forgotten for good
- **Open-ended questions** prevent pattern-matching on multiple choice — you either know it or you don't

---

## Example entry

```markdown
### 2026-03-19 — Claude Cowork for PMs
**Source**: `/images/2026-03-19-claude-cowork-for-pms.png`
**Verdict**: Reviewed — needs reinforcement on: scheduler cadence reasoning
**Difficulty**: Medium
**Retry by**: 2026-03-22

**Takeaway**: Scheduler cadence should match the tempo and cost-of-delay of the
underlying workflow — not your preference for manual control.
```

---

## Known issues & future extensions

**Image saving is partially automated**
When images are dropped with visible file paths (e.g. from Photos library), Claude can copy them to `/images/` automatically. When pasted from clipboard (screenshots, web images), no file path is available — images must be saved manually.

Possible extensions:
- A shell hook or companion script that watches a drop folder and moves new images into `/images/` with a datestamped filename
- Claude Code [hooks](https://docs.anthropic.com/en/docs/claude-code/hooks) could intercept image inputs and trigger a save script pre-session, covering the clipboard case
- A GUI wrapper (e.g. Raycast extension, iOS Shortcut) that accepts a share-sheet image, saves it to the repo, and opens a Claude session — full zero-friction capture

---

*Photographic Memory — built with Claude Code + a stubborn refusal to let passive consumption count as learning.*
