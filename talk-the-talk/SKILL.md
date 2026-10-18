---
name: talk-the-talk
description: Rewrite the user's target (a chat reply, draft, slides, docs, website copy, anything) in the style recorded in ~/.pi/agent/AGENTS.md — applying its rules and defect watch-list, then reporting what changed as right/wrong pairs. Use when the user says /talk-the-talk, asks to apply their style, or asks to fix the wording of something to match AGENTS.md.
---

<what-to-do>

## Load the style first

Read `~/.pi/agent/AGENTS.md` before touching the target.

If it does not exist, or exists but says nothing applicable (no rules, only empty sections), STOP: tell the user you need their style on file first and suggest running `/skill:learn-the-talk` — a few minutes of questions produces a file this skill can apply. Do not invent style rules from taste.

If the file exists, apply it in full: voice, punctuation, title rules, idioms, defect watch-list, authoring rules (teaching voice applies to course content only), and the standing rule the file states (usually "fewer words, stated simply, always wins").

## Take the target from the user

They may name a file, paste text, point at the last reply, or say "the slides" / "our docs" / "the commit message I just wrote" — apply the rules to whatever they indicate, at the scope they indicate (whole file, one section, one paragraph, the last assistant reply).

## Apply

Read the target and fix it rule by rule:

1. The standing rule first (usually fewest words stated simply): superfluous sentences that restate headings or state the discoverable get deleted outright.
2. The defect watch-list, worst first: Mic-Line, Hype Leak, Metaphor Crutch, Label Scaffolding, Summary Echo, Process Narration — with the fixes the file prescribes (delete, or fold into prose).
3. Punctuation: semicolons split into sentences, em-dashes replaced by the shape the file prefers (sentence, comma, parentheses, or colon), ampersands spelled out (shell `&&` and URL `&` stay).
4. Titles and headlines: benefit over mechanism, idioms matching their object and sense family, no file names in titles, category colons only where the file says they help.
5. Idioms: swap in the user's recorded phrases where the object and situation fit; never force one in when the plain sentence is shorter.
6. Anything the file does not cover: follow its spirit, and when two forms are equally clear, pick the shorter.

Do not change meaning, structure, facts, file paths, or code. Only the saying changes.

## Report

Keep the report short: one sentence on the sweep, then the handful of changes as wrong → right pairs (their file's format), then a file list if many files changed. No summary of what was already true.

## Feed the style file back

While applying, new rules may surface (the user corrects a choice, or a pattern repeats badly). Offer once at the end: should the new rule go into `AGENTS.md`? If yes, write it with a wrong/right pair, in the file's format. This feedback loop is how the file grows between sessions of `/skill:learn-the-talk`.

</what-to-do>

<supporting-info>

## Pairing

- `~/.pi/agent/skills/learn-the-talk/SKILL.md` produces the style file this skill consumes. The two form a loop: learn the style once, apply it everywhere, and feed corrections back.

## Sense coherence (when the file records sense families)

If the style file defines preferred idioms and sense families, respect them when rewording: an idiom must match its object and situation, one metaphor picture per phrase, modifiers from the same sense family as the words they modify. When no recorded rule covers a rewording choice, pick the plainest, shortest, most everyday wording.

</supporting-info>