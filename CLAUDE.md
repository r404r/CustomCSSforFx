# CLAUDE.md

## Project Rules

All project conventions, editing constraints, file placement rules, and validation
guidelines are defined in **[AGENTS.md](AGENTS.md)**. Read it before making any changes.

This project is a Firefox custom CSS collection. It has no build pipeline, no package
manager, and no automated test suite.

## Claude Code Workflow

1. Before editing, read `AGENTS.md` in full, then inspect the relevant entry file
   (`current/userChrome.css` or `current/userContent.css`) and nearby CSS modules.
2. Prefer the narrowest tool for the job: use the Edit tool for targeted CSS changes,
   Grep for searching selectors, and Glob for finding files.
3. When toggling features, follow the exact `@import` comment pattern documented in
   AGENTS.md — do not invent alternative commenting styles.
4. After editing, verify import paths and asset paths are correct by inspection.
5. Report what changed, the behavioral effect, and whether Firefox runtime verification
   was performed.

## Claude Code Constraints

- Do not add tooling, linters, formatters, or package manifests.
- Do not refactor or reformat CSS that was not part of the requested change.
- Do not modify files under `legacy/` unless the user explicitly targets an older
  Firefox version.
- If a request is underspecified, follow the decision defaults in AGENTS.md.

## Memory

Store stable project patterns (e.g. import toggle syntax, directory layout) in the
auto memory directory. Do not duplicate information already present in AGENTS.md.
