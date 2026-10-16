# ryans-agent-skills

A collection of personal agent skills (`SKILL.md` format) for coding agents.
These skills follow the [Agent Skills specification](https://agentskills.io/specification)
and are compatible with [Pi](https://pi.dev), Claude Code, Codex CLI, Amp, and Droid.

## Skills

| Skill | Description |
|---|---|
| [`brand-guidelines`](brand-guidelines/) | Applies project/company brand guidelines (colors, typography, logos, formatting) to presentations, documents, and marketing assets. |
| [`current-state`](current-state/) | Produces a detailed `CURRENT_STATE.md` snapshot of a project: repo state, file layout, services, logs, database, config, and next steps. |
| [`general-context`](general-context/) | Manages non-technical business context in `CONTEXT_GENERAL_<PROJECT_NAME>.md` — team, brand, marketing, sales, and vendor info. |
| [`grill-developer-calibration`](grill-developer-calibration/) | Adaptive multiple-choice assessment that calibrates the agent's communication style and technical depth to the user, saved in `CONTEXT.md`. |
| [`grill-with-docs`](grill-with-docs/) | Relentless one-question-at-a-time grilling of a plan against the existing domain model, updating `CONTEXT.md` and ADRs as decisions crystallise. |
| [`grill-with-docs-fast`](grill-with-docs-fast/) | Fast-paced version of the grilling session — 3–5 big-picture questions for classroom demos. |
| [`grill-with-docs-fast-non-technical`](grill-with-docs-fast_non_technical/) | Rapid classroom demo for non-technical users — 3–5 plain-language questions translated into a lightweight site spec. |
| [`grill-with-docs-non-technical`](grill-with-docs-non-technical/) | Non-technical grilling session that translates goals and site features into a clear technical specification and glossary. |
| [`implement-step-by-step`](implement-step-by-step/) | Manages a project plan's full lifecycle via `IMPLEMENTATION.md`, executing exactly one sequential micro-step at a time with human validation. |
| [`tech-analysis`](tech-analysis/) | Produces a `TECHNOLOGY_ANALYSIS.md` report covering architecture, frameworks, notable API usage, and well-implemented pieces of a codebase. |

## Adding these skills to Pi

Pi discovers skills in directories containing a `SKILL.md` file (recursively).
Your user-level skills live in `~/.pi/agent/skills/` (or the portable
`~/.agents/skills/`); project-level skills live in `.pi/skills/` or
`.agents/skills/` inside a project.

### Option 1 — Clone once and symlink (recommended; stays in sync with this repo)

```bash
git clone https://github.com/djryanash/ryans-agent-skills.git ~/dev/ryans-agent-skills

# Link every skill into Pi's user skills directory
for skill in ~/dev/ryans-agent-skills/*/; do
  ln -sfn "$skill" ~/.pi/agent/skills/"$(basename "$skill")"
done
```

To link them into a single project instead, replace the target directory:

```bash
for skill in ~/dev/ryans-agent-skills/*/; do
  mkdir -p /path/to/project/.pi/skills
  ln -sfn "$skill" /path/to/project/.pi/skills/"$(basename "$skill")"
done
```

### Option 2 — Copy the skills into Pi

```bash
git clone https://github.com/djryanash/ryans-agent-skills.git
cp -R ryans-agent-skills/*/ ~/.pi/agent/skills/
```

Note: copies won't pick up future updates automatically — re-run the copy
after pulling, or prefer symlinking.

### Option 3 — Install just one skill

```bash
mkdir -p ~/.pi/agent/skills
ln -sfn ~/dev/ryans-agent-skills/current-state ~/.pi/agent/skills/current-state
```

### Using the skills in Pi

1. Restart Pi (or start a new session) — Pi scans skill directories at startup
   and advertises each skill's name and description to the model.
2. Invoke a skill explicitly by typing:

   ```
   /skill:current-state
   ```

   Arguments after the command are appended as a user request, e.g.
   `/skill:grill-with-docs stress-test the checkout redesign plan`.
3. Or just describe the task — e.g. "analyze this project's tech stack" — and
   Pi will load the matching skill's instructions on demand.
4. Verify what's loaded with `/skills` (list of discovered skills).

To temporarily disable a skill without deleting it, Pi also supports moving
folders out of the scan path (e.g. `~/.pi/agent/skills-off/`).

## Adding skills to other agents

Because every skill is a `<name>/SKILL.md` directory following the Agent
Skills spec, the same layout works for other compatible tools — point them at
`~/.agents/skills/` or their own skills directory:

- **Claude Code:** `~/.claude/skills/` or `.claude/skills/` in a project
- **Codex CLI / Amp / Droid:** their documented skills locations (see each tool's docs)

## Repo layout

```
<skill-name>/
└── SKILL.md        # frontmatter (name, description) + instructions
```