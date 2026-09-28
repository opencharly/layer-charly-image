# charly-image

The `charly-image` family — the box/image and candy/layer authoring skills.

The `charly-image` candy is a **concept candy**: it ships no install content and
owns the `image` family of `skill:` entities. It carries two entities:

- `image` — the `charly box` command family and image composition: box
  definitions in `charly.yml`, inheritance chains, defaults, platforms, builder
  configuration, intermediate images, OCI labels, and the build/deploy scope
  boundary.
- `layer` — candy authoring: the `charly.yml` candy schema, `plan:` step verbs
  (`run:` / `check:`), `var:` substitution, execution order, and the per-verb
  validation catalog.

`candy/plugin-marketplace` regenerates the standalone
[opencharly/marketplace](https://github.com/opencharly/marketplace) corpus from
these entities, so the skills are authored here and projected there.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `charly-image` (concept candy) |
| Install content | none — a `true` no-op `plan:` |
| Owns | 2 `skill:` entities: `image`, `layer` |
| Projected to | `marketplace/image/skills/` |
| Service / port | none |

## How to use it

This repo is consumed as a **skill source**, not as an image layer. Edit the
`skill:` entities in `charly.yml`; the marketplace regeneration projects them
into `/charly-image:*` pages. To reference the repo directly, compose it in a
box. A box is a `candy:` node that carries the box's `base:` image and a nested
`candy:` list of layer refs (the nested `candy:` is the composition list; the
outer `candy:` is the box body):

```yaml
my-box:
  candy:                  # the box body (an IMAGE is a `candy:` node carrying `base:`)
    base: fedora          # the box's base image
    candy:                # the box's composition list
      - '@github.com/opencharly/layer-charly-image:v2026.268.1334'
```

The two skills here are the authoring reference for the rest of the corpus —
load `/charly-image:image` before editing a box and `/charly-image:layer` before
editing a candy.

## Layout

- `charly.yml` — the `charly-image:` concept candy entity plus two `skill:`
  entities (`image`, `layer`).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-image:image`
- Candy authoring: `/charly-image:layer`
- Build command family: `/charly-build:build`, `/charly-build:generate`,
  `/charly-build:validate`
- [`opencharly/marketplace`](https://github.com/opencharly/marketplace) — the projected corpus
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
