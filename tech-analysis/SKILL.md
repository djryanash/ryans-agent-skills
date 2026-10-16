---
name: tech-analysis
description: Produces a detailed TECHNOLOGY_ANALYSIS.md report for any software project, covering architecture, frameworks/technologies used, specific methods and API calls, and highlighted well-implemented pieces with explanations of why and how. Use when asked to analyze, audit, or write up a project's frameworks, technologies, tech stack, or notable implementations.
---

# Technology Analysis

This skill generates a `TECHNOLOGY_ANALYSIS.md` document that captures a
detailed, point-in-time analysis of the frameworks, technologies, and
notable implementations in a software project.

## Procedure

1. **Scope the project.** Identify the project root, language(s), build
   system, and the set of source files to analyze. For multi-target repos
   (e.g. Xcode workspaces, monorepos), note each target and its role.
2. **Inventory frameworks & dependencies.**
   - Grep all `import` / `using` / `require` / `use` / `#include` statements
     and tally by framework (`grep -rh "^import " --include="*.swift" . |
     sort | uniq -c | sort -rn`). Adapt the import keyword to the language.
   - Read the dependency manifests: `package.json`, `Podfile`,
     `*.xcodeproj/project.pbxproj` (SPM `XCRemoteSwiftPackageReference` /
     `packageProductDependencies`), `Package.swift`, `go.mod`,
     `Cargo.toml`, `build.gradle`, `pom.xml`, `requirements.txt`,
     `pyproject.toml`, etc.
   - Record deployment targets, supported platforms, bundle IDs, language
     version, marketing version where present.
3. **Map the architecture.** Read the entry point (app delegate / `main` /
   `index` / `App`), the top-level wiring, and the directory layout. Note
   the architectural pattern (MVVM, MVC, Clean Architecture, etc.), how
   layers communicate (Combine, signals, observers, DI), whether the UI is
   programmatic or storyboard/nib/declarative, and any hybrid stacks.
4. **Read key files in depth.** Prioritise, in order:
   - App lifecycle / scene wiring.
   - The central view-model / controller / coordinator.
   - Service / networking / persistence layers.
   - Concurrency primitives (actors, queues, dispatch, async runtimes).
   - Custom renderers, views, or domain models that look non-trivial.
   - Extensions and helpers (often where the cleverest code lives).
   - Tests, build scripts, secondary targets.
   For large files use `read` with `offset`/`limit`; do not skip them.
5. **Extract specific methods & API calls.** For each framework in use,
   cite concrete symbols the code actually calls (e.g.
   `Product.products(for:)`, `BGTaskScheduler.shared.register(...)`),
   with file references. Prefer real call sites over generic descriptions.
6. **Identify well-implemented highlights.** Select the pieces that are
   notably elegant, robust, or reusable (clever algorithms, correct
   concurrency isolation, thoughtful UX, type-safe wrappers, robust
   parsing). For each, explain **where** it lives, **why** it's good, and
   **how** it works. Aim for 8-12 highlights; never fewer than 5.
7. **Synthesize** into the document format below and write the file to
   `TECHNOLOGY_ANALYSIS.md` in the project root.

## Initial Prompt

The canonical invocation prompt for this skill is:

> Do an analysis of this project and write up a markdown file detailing the
> different frameworks and technologies used such as UIKit, Swift, etc. Write
> out some of the specific methods used and functions called. Highlight
> anything that is particularly well-implemented and give a description of why
> and how it is used.

## Document Format

The document MUST be written as GitHub-flavored Markdown. Use the section
headings below; add or omit subsections as relevant, but keep
`## 1. Architecture`, `## 2. Frameworks & Technologies`,
`## 3. Specific Methods & API Calls`, and `## 4. Highlights` always.

### Title block

Begin with an H1 title and a short metadata block (project name, author if
known, targets, language, deployment target/version, bundle ID, marketing
version), followed by one paragraph describing what the project is and does.

### Required sections

```markdown
# <Project Name> — Technology & Framework Analysis

<metadata block>

<one-paragraph overview>

## 1. Architecture
- Directory layout / module organisation.
- Architectural pattern and how layers communicate.
- Programmatic vs declarative UI; hybrid stacks.
- Notable structural choices (extensions splitting behaviour, actor
  isolation, feature folders, etc.).

## 2. Frameworks & Technologies
- Apple SDKs / platform frameworks — table of framework → usage.
- Third-party dependencies — table of package → purpose, with source.
- Language features in active use (concurrency, generics, property
  wrappers, macros, etc.).

## 3. Specific Methods & API Calls
- Grouped by subsystem, each with file reference and the actual symbols
  invoked. Include short code snippets where they clarify the technique.
- Cover at least: app lifecycle, the central view-model/controller,
  networking/persistence, concurrency, UI rendering, and any custom
  parsing/decoding.

## 4. Particularly Well-Implemented Highlights
- One subsection per highlight (### 4.x Title).
- Each subsection MUST state **Where:** (file/symbol), **Why it's good:**,
  and **How:** (with a small code excerpt). Quote the real code.

## 5. <Secondary targets / modules, if any>
- Brief coverage of any companion targets, scripts, or admin apps.

## 6. Summary
- 1-2 paragraph synthesis: what kind of codebase this is, its strongest
  patterns, and what other projects could learn from it.
```

## Notes

- Read enough source to be specific. Vague phrases like "uses networking"
  are failures; cite the real call site.
- Quote real code in highlights — copy the exact lines from the file. Keep
  excerpts short (≤ ~10 lines) and trim irrelevant lines with a comment.
- Prefer tables for framework/dependency inventories; they scan quickly.
- Note the language's idioms: e.g. Swift `actor`/`@dynamicMemberLookup`/
  `@retroactive`, Rust traits/async, TS generics/branded types.
- For multi-language/mono-repos, group by target and call out shared model
  graphs surfaced through different UI stacks.
- Don't editorialize beyond `## 4. Highlights` and `## 6. Summary`; keep
  sections 1-3 factual and reference-dense.
- Always end by writing `TECHNOLOGY_ANALYSIS.md` to the project root and
  confirming the path to the user.
- If the project already has a `TECHNOLOGY_ANALYSIS.md`, overwrite it only
  when explicitly asked; otherwise write to
  `TECHNOLOGY_ANALYSIS.<timestamp>.md` and tell the user.