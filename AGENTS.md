# AGENTS.md

## Purpose

This repository is a Firefox custom CSS collection.
It is not an application with a build pipeline.
Agents working here should think in terms of:

- CSS modules
- `@import`-based feature toggles
- Firefox profile installation
- manual verification in Firefox

The goal is to make small, precise, low-risk changes that fit the repository's existing structure and style.

## Required First Step

Before making any change, read:

1. `README.md`
2. the relevant entry file:
   - `current/userChrome.css` for browser UI work
   - `current/userContent.css` for built-in page or content work

Do not assume this repo behaves like a normal web app, extension, or packaged theme project.

## Repository Model

Primary active work happens in `current/`:

- `current/userChrome.css`: main browser chrome entry point
- `current/userContent.css`: main content / internal-page entry point
- `current/config/`: shared variables and common settings
- `current/css/`: feature CSS files organized by area
- `current/image/`: images and icons used by CSS

Historical and compatibility material lives in `legacy/`:

- `legacy/fx60-90`
- `legacy/fx91-100`
- `legacy/fx101-108`
- `legacy/fx109-127`
- `legacy/proton`
- `legacy/previews`

Default assumption:

- If the user does not explicitly mention an older Firefox version, edit only `current/`.

## Core Behavior Rules

1. Prefer the smallest change that solves the request.
2. Preserve existing file layout, comments, grouping, and formatting style.
3. Do not refactor unrelated CSS while touching a file.
4. Do not reorganize directories unless explicitly requested.
5. Do not introduce tooling, package manifests, build scripts, or lint configs unless explicitly requested.
6. Do not modify `legacy/` for convenience when the request is really about current Firefox behavior.
7. Do not remove comments or section banners just to "clean up" the file.

## Import Toggle Convention

This project enables and disables features through `@import` lines.

Enabled form:

```css
@import "./css/buttons/buttons_on_navbar_classic_appearance.css"; /**/
```

Disabled form:

```css
/* @import "./css/buttons/buttons_on_navbar_classic_appearance.css"; /**/
```

Rules:

- Preserve this exact pattern.
- Do not replace it with another commenting style.
- Keep imports under the existing section where they logically belong.
- Respect comments like "only use one option at a time".
- If a section offers mutually exclusive visual variants, do not enable multiple variants together unless the user explicitly asks for that.

## File Placement Rules

Use this mapping when deciding where to edit:

- browser tabs, toolbars, buttons, app button, url bar, menubar, bookmark toolbar:
  `current/userChrome.css` and files under `current/css/`
- `about:addons`, `about:preferences`, `about:newtab`, `about:home`, `about:logins`, `about:config`:
  `current/userContent.css` and files under `current/css/`
- theme variables, color presets, shared sizing:
  `current/config/`
- icons and image-backed styling:
  `current/image/`

When adding a new tweak:

- prefer adding a focused CSS file in the relevant `current/css/<area>/` directory
- then add a matching `@import` entry in the correct entry file if the feature should be selectable

## What Agents Must Not Assume

Do not assume this repository can:

- create entirely new Firefox UI primitives
- depend on WebExtensions for equivalent browser UI control
- rely on a bundler or transpiler
- be validated through a normal web preview server

This repo modifies Firefox's existing UI with CSS only.

## Strong Editing Constraints

When editing CSS in this repository:

- keep selectors as narrow as practical
- avoid broad global overrides unless the existing file already uses them intentionally
- reuse existing naming and path conventions
- keep image paths relative in the same style as surrounding code
- avoid adding `@namespace`
- avoid mass-changing whitespace or indentation in large files
- avoid renaming assets unless every reference is intentionally updated

If a request can be solved by:

1. toggling an existing import
2. adjusting an existing module
3. creating a new module

prefer that order.

## Entry File Rules

`current/userChrome.css` and `current/userContent.css` are configuration-oriented entry files.

Agents should:

- treat them as organized menus of features
- keep the section headings intact
- add new imports near similar features
- avoid scattering imports into unrelated sections

Agents should not:

- convert these files into monolithic style sheets
- inline large feature implementations into the entry files
- reorder large sections unless explicitly asked

## Legacy Rules

`legacy/` is version-specific compatibility material.

Do not edit `legacy/` unless one of these is true:

- the user explicitly asks for an older Firefox branch
- the relevant bug or feature is clearly isolated to a legacy folder
- you are intentionally backporting a change and the user asked for it

If work spans both `current/` and `legacy/`, call that out explicitly in your response.

## Validation Rules

There is no guaranteed automated test or lint workflow here.
Validation should focus on correctness and compatibility:

1. verify CSS syntax by careful inspection
2. verify import paths and asset paths
3. verify mutually exclusive imports were not accidentally enabled together
4. verify the change is placed in the correct entry file or module directory
5. if practical, describe the expected Firefox manual verification path

Manual verification model from the README:

1. set `toolkit.legacyUserProfileCustomizations.stylesheets` to `true`
2. copy `userChrome.css`, `userContent.css`, `config/`, `css/`, and `image/` into the Firefox profile `chrome/` folder
3. restart Firefox
4. use Browser Toolbox to inspect ids and attributes when needed

If you cannot run Firefox for validation, say so clearly instead of implying the change was runtime-tested.

## Decision Defaults For Agents

If the user request is underspecified, prefer these defaults:

- target `current/`
- make the feature opt-in instead of enabled by default, unless the request is to change default behavior
- place code beside the closest existing feature family
- preserve existing visual style rather than inventing a new organization

If the request would require broad stylistic redesign or cross-version restructuring, pause and ask before proceeding.

## Safe Workflow

Recommended workflow for Claude/Codex-style agents:

1. read `README.md`
2. inspect the relevant entry file and nearby CSS modules
3. identify the smallest correct edit location
4. make a minimal change
5. confirm import paths and surrounding conventions
6. report exactly what changed and whether Firefox runtime verification was performed

## Response Expectations

When reporting work back to the user:

- mention the files changed
- summarize the behavioral effect
- mention if validation was manual, structural only, or not performed
- mention assumptions when the request did not specify Firefox version or whether a tweak should be enabled by default
