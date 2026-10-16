---
name: grill-with-docs-non-technical
description: Non-technical grilling session that translates user goals, business needs, and site features into a clear technical specification and glossary.
---

<what-to-do>

Interview me relentlessly about the goals, functionality, and user experience of this website plan using clear, non-technical language. 

Frame questions around desired outcomes, target audience needs, and visual/interactive preferences. Automatically translate my answers into structured technical terms, architecture concepts, and documentation.

For each non-technical question, offer a simple recommended direction or standard web feature.

Ask the questions one at a time, waiting for feedback on each question before continuing.

If a question can be answered by reviewing existing project files or pages, explore them first.

</what-to-do>

<supporting-info>

## Domain awareness

Look for existing documentation in plain English or standard layout files:

```
/
├── CONTEXT.md
├── docs/
│   └── adr/
└── src/
```

Create `CONTEXT.md` lazily when the first feature or domain term is defined.

## During the session

### Translation to technical specs

Translate user language into developer canonical terms:
- "I want people to log in with Google" → **Auth Strategy / OAuth Provider**
- "A page showing past client reviews" → **Testimonials Component / CMS Schema**
- "A contact form that emails me" → **Contact API Endpoint / Email Service Integration**

### Clarify user intent

When the user gives a general requirement (e.g., "I want a shop"), ask clarifying questions using plain English (e.g., "Will you be selling physical products that need shipping, or digital downloads?").

### Update CONTEXT.md inline

As features and definitions are clarified, map the plain-English terms to their technical canonical equivalents inside `CONTEXT.md`.

### Offer ADRs in plain English

When making a choice with trade-offs (e.g., using a simple form tool vs. building a custom backend database), summarize the decision clearly before creating an ADR.

</supporting-info>