---
name: current-state
description: Produces a detailed CURRENT_STATE.md report for any project, covering repository state, file layout, service/runtime status, logs, database, virtual environment, config, a net assessment, and recommended next steps. Use when asked to inspect or summarize a project's current state.
---

# Current State

This skill generates a `CURRENT_STATE.md` document that captures a detailed,
point-in-time snapshot of a project's health and runtime state.

## Procedure

1. Run the following inspection steps (adapt scope to the project type):
   - **Git status:** `git status`, `git branch -vv`, `git log -1 --oneline`,
     list local/remote branches, note untracked/modified files and unpushed
     commits.
   - **File layout:** list top-level files and notable subdirectories with
     sizes (`ls -la`, `du -sh */`).
   - **Service / runtime status:** check for LaunchAgents/systemd units,
     `launchctl list | grep ...`, `ps aux | grep ...`, port listeners
     (`lsof -i :PORT`).
   - **Logs:** `ls -lh logs/`, `tail` recent entries, note file sizes and
     recurring errors.
   - **Database:** open any SQLite DB (`sqlite3`), list tables, count rows,
     sample notable tables, check last activity timestamps.
   - **Virtual environment:** verify `.venv/bin/pip --version`, note any
     corrupted dependencies.
   - **Config:** read `config.yml`/equivalent and summarize key settings.
   - **Watched / target directories:** verify any paths referenced by config
     actually exist.
2. Synthesize findings into the document format below.
3. Write the file to `CURRENT_STATE.md` in the project root.

## Initial Prompt

The canonical invocation prompt for this skill is:

> Examine this project and report back a detailed summary of its current state.

## Document Format

The document MUST be written as GitHub-flavored Markdown with a YAML
frontmatter block, followed by the body sections in the order shown. Use the
exact frontmatter fields and section headings below. Add or omit body sections
as relevant to the project, but keep `## Net Assessment` and
`## Recommended Next Steps` always.

### Frontmatter (exact fields)

```yaml
---
date: <YYYY-MM-DD>
project_path: <absolute path to the project>
coding_agent: pi
model: <model identifier, e.g. ollama/glm-5.2:cloud>
inspection_method: <comma-separated list, e.g. Filesystem inspection, launchctl/ps status, SQLite queries, log review, git status>
watched_directory: <primary watched/input directory if applicable, else omit>
overall_status: <one-line summary, e.g. Operational / Broken — <reason> / Partially functional — <reason>>
---
```

Field rules:
- `date` — the inspection date (today).
- `project_path` — absolute path of the inspected project.
- `coding_agent` — always `pi`.
- `model` — the exact model identifier in use.
- `inspection_method` — concise list of the techniques actually used.
- `watched_directory` — include only if the project monitors/watches a
  specific directory; otherwise omit the field.
- `overall_status` — a short, blunt verdict prefixed with a status word
  (`Operational`, `Broken`, `Partially functional`, `Idle`, etc.).

### Body (headings and intent)

```markdown
# Current State — <Project Name>

<One short paragraph describing what the project is/does.>

## Repository State
- Branch checked out, ahead/behind remote, unpushed commits, other branches.
- Working tree status (clean / modified / untracked files).
- Last commit hash + subject.

## File Layout (top level)
- Bullet list of top-level files (with sizes where notable) and key
  subdirectories, grouped by role (core, scripts, data, docs, etc.).

## Service Status — <Running / NOT running / N/A>
- launchctl/systemd/ps findings, which processes are alive, ports in use,
  how the service is started.

## Critical Issue: <short title>      # only if a critical issue exists
- Describe any blocking problem (missing directory, crashed process, etc.).

## Logs — <one-word state, e.g. Bloated / Healthy / Empty>
- Per-file sizes, dominant message types, timestamps of last good / first
  failing entries.

## Database State — <one-word state>
- Tables present, row counts, sample notable rows, last activity timestamp.

## Virtual Environment — <state>
- Whether `.venv` is healthy, pip works, required packages installed.

## Config Summary (`<config file>`)
- Key settings: polling/intervals, hashing, scan scope, logging, db path,
  any toggles.

## Net Assessment
- 1-2 paragraph synthesis: is it working, what's broken, what's housekeeping.

## Recommended Next Steps
- Bullet list of concrete, ordered actions to restore/improve the project.
```

## Notes

- Keep prose tight; prefer bullets.
- Quote exact error strings from logs/config.
- Include command snippets only when they're part of a recommendation
  (e.g. rebuild venv, restart service).
- Don't editorialize beyond the `## Net Assessment` and
  `## Recommended Next Steps` sections.
- Always end by writing `CURRENT_STATE.md` to the project root and confirm
  the path to the user.