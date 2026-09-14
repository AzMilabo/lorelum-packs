# Lorelum Knowledge Packs

This repository is the official public catalog for installable Lorelum Knowledge Packs. Each released Pack directory under `packs/` is a self-contained Pack root using the public `pack.yaml + practices/**/*.md + decisions.yaml?` format; a maintainer checkout may also contain explicitly marked unreleased candidates.

## Catalog

- `pack-creator@0.1.0` — 20 domain-neutral Practices for defining, designing, authoring, reviewing, evaluating, localizing, and releasing Lorelum Packs.
  - [简体中文本地化](./packs/pack-creator/i18n/zh-CN/README.md) is available as non-runtime companion content.
- `agentic-coding@0.3.0` — 30 tool-neutral Practices covering requirements, planning, implementation, testing, verification, review, delivery, correction, context recovery, and decision-aware delegation.
  - [简体中文本地化](./packs/agentic-coding/i18n/zh-CN/README.md) is available as non-runtime companion content.
- `agentic-coding@0.2.0` — immutable first complete release with 29 Practices.
- `agentic-coding@0.1.0` — immutable placeholder history retained for reproducible installation tests. It is not production guidance and is not updated in place.

## Install

After a release ref listed in `.lorelum/registry.yaml` has been published:

```sh
lore install <pack>
```

The Lorelum CLI contains the official Registry repository name, not the Pack content. It reads this descriptor, resolves the release from the same repository, validates the selected Pack, and installs it into the user-level LocalStore.

Another public GitHub repository can expose the same layout and be selected explicitly:

```sh
lore install <pack> --registry owner/repository
```

## Repository layout

```text
.lorelum/registry.yaml
packs/
  agentic-coding/
    pack.yaml
    README.md
    SOURCES.md
    practices/
    i18n/
  pack-creator/
    pack.yaml
    README.md
    SOURCES.md
    practices/
    i18n/
```

The `packs/<name>` path is this catalog's organization convention. A project-authored Pack may instead live at `.lorelum/packs/<name>` in its own project; the Pack root format itself is unchanged.

## Unreleased local candidate

`packs/react-web-craft/` is a maintainer working candidate, not an installable catalog release. It has no Registry entry, immutable release ref, or tag. Its content is complete and frozen: 24 Practices across six categories (state, async, bundle, server, rendering, composition), English content frozen 2026-09-14, with a zh-CN companion under `i18n/zh-CN/` pinned by `i18n/manifest.yaml`. The Pack license is determined as CC-BY-4.0 (`pack.yaml`, 2026-09-15). The only gate still open is the Registry release; the Pack's own README records the gate status. Do not infer release status merely from its location under `packs/`.
