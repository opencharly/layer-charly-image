# AGENTS.md — layer-charly-image

Standalone candy repo for the `charly-image` concept candy — it ships no install
content and owns the `image` family of `skill:` entities: the box/image
composition surface and the candy/layer authoring reference. The entities live
in `charly.yml` at the repo root; `candy/plugin-marketplace` regenerates the
standalone opencharly/marketplace corpus from them.

Canonical files:

- `charly.yml` — the `charly-image:` concept candy entity plus two `skill:`
  entities: `image-skill` (`name: image`) and `layer-skill` (`name: layer`).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-image:image` — the box/image composition skill: box definitions,
  inheritance, defaults, platforms, builders, intermediate images, OCI labels,
  and the build/deploy scope boundary. Load before editing the `image-skill:`
  entity.
- `/charly-image:layer` — the candy authoring reference: the `charly.yml` candy
  schema, `plan:` step verbs, `var:` substitution, and the per-verb validation
  catalog. Load before editing the `layer-skill:` entity or any candy entity
  elsewhere.
- `/charly-build:build` / `/charly-build:validate` — the `charly box` command
  skills the `image` skill cross-references.

## Build / validate / test

- `charly box validate` at the repo root — the structural check: the manifest
  must parse and validate at the installed charly.
- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has no
  per-repo candy gate.
- The candy is documentation-only: its `plan:` is a `true` no-op plus a `true`
  `check:` that the skill entities are present and generated into the
  marketplace. There is no live bed.

## Modify this repo

- The `skill:` entities are the projected usage source. Edit them here, never
  the generated `SKILL.md` in the marketplace corpus; a corpus regeneration
  (`charly marketplace generate`) projects them.
- These two skills are the authoring reference for the whole corpus: a schema or
  verb-catalog change must be mirrored in the matching entity in the same change
  so the corpus does not drift.
- Keep the concept candy's `plan:` no-op; it exists only to carry the entities.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
