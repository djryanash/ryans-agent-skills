---
name: learn-the-talk
description: Learning session that nails down the user's communication style through progressive questions and writes it as rules (with right/wrong examples) into ~/.pi/agent/AGENTS.md. Use when the user wants the agent to learn how they talk, wants their agent style set up, or says /learn-the-talk.
---

<what-to-do>

Learn the user's communication style the way a session of editing together would: one question at a time, distilling each answer into a written rule the moment it is confirmed. The output file is `~/.pi/agent/AGENTS.md` (create it lazily; never batch).

## Style of the session itself

The user often does NOT know how they talk until they see it written down. So every question must do the heavy lifting FOR them:

- Always present options they can simply pick from (with example lines showing each in their own context), AND an explicit fourth option: "none of these, I'll show you how I'd say it" — their own example is the best evidence and is always offered.
- After any pick, show the rule written into the file as a right/wrong pair AND ask them to react to the pair ("is this how you'd say it?"), because seeing the written rule is what reveals their preference.
- When their answer is vague ("keep it short", "casual"), don't accept the abstraction: draft 2–3 example sentences and let them point at the one that sounds like them.
- Quote their own messages back as examples — their typing is the calibration gold; mine it before asking.

Example of the question format (the shape every question follows):

> Where should a reply end? Here is the same result three ways:
>
> 1. Nothing after the answer: "The zip was rebuilt and committed; the old file is still in unused-slides."
> 2. A compact file list: "Rebuilt and committed. Changed: tmp/capture.cjs, public/og-default.png."
> 3. One next step: "Rebuilt and committed. The old file in unused-slides is still linked from one note."
>
> Type 1, 2 or 3 — or paste how YOU would end that reply.

Then distill their pick into the written rule and show the pair ("Written like this: Wrong: … / Right: … — sound like you?").

## Before the first question

Read `~/.pi/agent/AGENTS.md` if it exists (missing → nothing to pre-check).

If it exists, tell the user briefly what style is already on file (list the rule headings only, not the rules), then ask: recalibrate from scratch, fine-tune what is there, or leave it untouched today? Their answer scopes the session.

Before asking anything, get consent. Say why: these rules govern every future reply and everything you author for them (replies, slides, documents, website copy). Tell them:

- They can type `skip` or `quit` at any time, and everything captured so far is already safe in the file.
- Questions are one at a time. Each question comes with options and example lines they can pick from, and there is always the option to type their own example. Free-form answers all count and will be probed.
- Around 10–15 questions nails a full style; fewer still produces a usable file.
- Seeing each rule written down as examples is part of the process: they often only recognize their own style once it is on screen. Reacting to the written rule is a question in itself.

## Where the questions come from

Use the user's existing `AGENTS.md` as the question source (each existing rule suggests its origin story), and these areas, progressively drilled. Start broad and personal; get concrete only as trust builds.

1. **Openings and closings.** How should a reply start? Do they want a one-sentence state-of-the-world first ("the deploy worked but there was a warning")? How should a reply end (nothing? a summary? never a question)?
2. **Structure.** Prose or bullets? When are lists acceptable (only genuinely enumerable things?)? Tables? Headings in chat? Bold labels ("Why:", "The catch:") — allowed or banned? Show a short paragraph written three ways (prose, labelled bullets, table) and let them pick.
3. **Process talk.** Should you narrate what you are about to do ("let me check...") or only report results? Step recaps wanted or banned?
4. **Voice.** Formal vs plain? First person? Is humor welcome? Is profanity ever welcome (usually: never)?
5. **Punctuation habits.** Watch their messages and ask directly: semicolons (many people never), em-dashes (many people almost never), ampersands, capitalization after splits, ellipses, exclamation marks. Show the same sentence with/without the mark rather than asking about it in the abstract.
6. **Idioms.** Ask them to name or paste phrases they use a lot ("how would you say it out loud?"); scan the conversation log for idioms they already used. Record each with what it should be used FOR and what it beats.
7. **Titles and headlines** (if they author content): benefit-first vs mechanism-first, flavor suffixes, prefixes, file names in titles.
8. **Failures they have seen elsewhere.** "What do agents do that annoys you?" — distill each complaint into a named defect with a severity, and a wrong/right example pair.

For any question answerable by looking at their recent messages or files, look instead of asking: real usage beats self-report. Quote their own words back as calibration specimens.

## After each answer

Distill immediately, out loud and in the file:

- A rule stated as a behavior ("never use semicolons; split into two sentences with a period").
- The example lines they picked from (or typed), recorded as a right/wrong pair — their words for the right form whenever they supplied one.
- If they hesitated or seemed unsure, note the rule as leaning ("prefers, not strict") rather than a hard rule; ask once later whether it is strict, then record the answer.
- File it under a heading that matches what it governs (`Voice`, `Punctuation`, `Titles`, `Teaching voice` for authored course content, `Defect watch-list` for failure patterns, `Preferred idioms` for their phrases).

Create sections lazily; never reorganize existing sections without asking. Keep rules as sentences, not bullet skeletons, and keep the file short enough that a future agent re-reads all of it.

## Ending the session

When they quit (or the areas are exhausted): state in one line what the file now contains, show the rule headings, and ask once whether anything should be adjusted. Then stop; no summary longer than the file itself.

</what-to-do>

<supporting-info>

## Style references for the session design

- `~/.pi/agent/skills/grill-with-docs/SKILL.md` — for the interview posture: relentless, one question at a time, resolve each branch, write to the file inline as decisions land, never batching.
- `~/.pi/agent/skills/grill-developer-calibration/SKILL.md` — for the consent-then-progressive-questions shape: state the purpose up front, allow `skip`/`quit` at any time, adapt the next question to prior answers, remind periodically that they can stop once 10+ questions are answered.

## What a finished file looks like

A healthy `AGENTS.md` contains: the register in a few sentences (how sentences should read), concrete wrong/right example pairs using the user's own voice, a defect watch-list with named patterns and severities, punctuation rules distilled from their actual typing, a preferred-idioms list mined from their messages, and authoring rules if they produce content (slides, docs, websites). Every rule is falsifiable: an agent could check output against it and be wrong sometimes.

</supporting-info>