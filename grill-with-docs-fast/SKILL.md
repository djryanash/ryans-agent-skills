---
name: grill-with-docs-fast
description: Fast-paced grilling session for classroom demonstrations. Briefly tests key decisions, sharpens main terms, and updates CONTEXT.md without deep-diving into edge cases.
---

<what-to-do>

Interview me efficiently about the core high-level aspects of this plan. Keep questions focused on big-picture architecture and user experience rather than exhaustive edge cases, wrapping up in 3 to 5 key questions.

For each question, provide your recommended answer.

Ask the questions one at a time, waiting for feedback on each question before continuing.

If a question can be answered by exploring the codebase, explore the codebase instead.

</what-to-do>

<supporting-info>

## Domain awareness

During codebase exploration, look for existing documentation:

### File structure

```
/
├── CONTEXT.md
├── docs/
│   └── adr/
└── src/
```

Create `CONTEXT.md` lazily when the first core term is resolved.

## During the session

### High-level term alignment

When the user uses ambiguous terms, briefly confirm the intended meaning and document it in `CONTEXT.md`. Avoid getting bogged down in minor edge cases.

### Update CONTEXT.md inline

When a key term is resolved, update `CONTEXT.md` immediately using the glossary format. Keep entries concise.

### Offer ADRs strictly for major decisions

Only offer an ADR for high-impact decisions that dictate the overall architecture or user flow.

</supporting-info>