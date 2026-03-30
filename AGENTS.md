# Agent Instructions

This file governs how AI agents (Claude Code, Codex, etc.) should behave when working in this repository.

## Scope

**Only work within this repository.** Do not read from, write to, or run git commands in any other directory, including:

- `../docs-vi` (vuejs-translations/docs-vi - the production repo)
- `../docs` (vuejs/docs - the upstream English source)
- Any other sibling repository

If a task requires content from another repo, ask the user to copy it here first.

## Repository layout

- `src/` - English source files mirrored from `vuejs/docs` at the checkpoint in `CHECKPOINT.md`. This is where translation work happens.
- `src_vi/` - Vietnamese reference translations from previous review rounds. Read-only reference — do not modify.
- `GLOSSARY.md` - canonical Vietnamese terminology. Always consult before translating a term.
- `ROADMAP.md` - translation progress tracker. Check off items as they are completed.

## Translation workflow

1. Translate files in `src/` in-place (English content gets replaced with Vietnamese).
2. Use `src_vi/` as a reference for the equivalent file — read it for context, do not copy it verbatim.
3. Consult `GLOSSARY.md` for every technical term before deciding how to translate it.
4. Each PR should cover one logical unit from `ROADMAP.md` (one section or a few related pages).
5. Mark completed items in `ROADMAP.md` as `[x]` in the same PR.

## Translation rules

- Keep all code blocks, API names, directive names, and component names in English.
- Use `src_vi/` as a draft reference, but rewrite sentences to be natural Vietnamese — do not copy awkward phrasing.
- On first use of a technical term in each file, add the English original in parentheses if the term is translated (e.g., "hook vòng đời (lifecycle hook)").
- Use "bạn" when addressing the reader directly.
- Short sentences for simple concepts; medium-length for explained relationships.

## Git rules

- Branch naming: `translate/<section-name>` (e.g., `translate/introduction`, `translate/essentials-pt1`).
- Commit message format: `translate: <filename or section> - Vietnamese` (e.g., `translate: guide/introduction.md`).
- One commit per file or small group of related files. Do not batch everything into one commit.
- Always run `git pull --rebase origin main` before pushing.
- Do not force-push to `main`.
