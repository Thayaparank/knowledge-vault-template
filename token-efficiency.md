# Token Efficiency — Working with AI Assistants Cheaply

> General practices for keeping AI-assisted work fast and low-cost. Nothing here is tool-specific; it applies to any assistant working in this vault.

---

## 1. Point, don't paste

- Reference material by **file path**, not by pasting its content into the chat. The assistant reads the file itself, and only the parts it needs.
- Drop large material into `raw/` first, then say "ingest `raw/documents/<file>.md`" — one copy, on disk, instead of a huge blob in the conversation.

## 2. One task per conversation

- Mixing unrelated tasks in one long chat makes every later message carry the whole history. Finish a task, checkpoint, start fresh.
- Long-running projects survive between conversations through the status file (`NEXT ← RESUME HERE`) — not through chat history.

## 3. Search narrow, never scan wide

- Ask for specific lookups ("what do we know about X") — the assistant greps `wiki/index.md` and tags, then opens one or two pages.
- Avoid "read the whole vault and…" requests. The structure exists precisely so nothing ever needs a full scan.
- `log.md` is grepped, never read in full.

## 4. Keep pages retrieval-cheap

- Wiki pages under ~200 lines, one concept each, with a one-line `summary:` and `tags:` in the front-matter — the assistant can decide relevance from the summary alone, without loading the page.
- Never embed big dumps in wiki pages; link to `raw/` instead. The expensive file is read once at ingestion, then never again.

## 5. Match the model to the task

- Routine, mechanical work (formatting, renaming, simple lookups) doesn't need the strongest model — use a cheaper/faster tier where your tooling allows it.
- Save the most capable model for genuinely hard work: architecture, tricky debugging, distilling subtle lessons.

## 6. Reuse instead of re-explaining

- Recurring instructions become **prompt pages** in `wiki/prompts/` (start from `templates/ai-prompt-template.md`) — parameterized once, reused forever.
- Standing rules live in `AGENTS.md` — stated once, loaded every session, never re-typed.

## 7. Checkpoint so resuming is cheap

- A good status file lets a fresh session continue with zero questions — which means zero tokens spent reconstructing context from old conversations.

---

## Related
- [AGENTS.md](AGENTS.md) — §8 Optimization for Retrieval
- [README.md](README.md) — the two-layer structure these practices depend on
