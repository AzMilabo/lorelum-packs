# AGENTS.md

> This file tells AI coding agents how to work **in this specific repo**. Humans: see the [main repo's CONTRIBUTING.md](https://github.com/lorelum/lorelum/blob/main/CONTRIBUTING.md) for the human workflow. If you're using an AI assistant to contribute a Practice or anti-pattern, point it at this file.

## Project

This is **`lorelum-packs`** — the community knowledge-pack repository for [Lorelum](https://github.com/lorelum/lorelum). It holds the *content* that the Lorelum engine retrieves and injects into AI context: **Practices**, **anti-patterns**, **decision graphs** (`decisions.yaml`), and **templates**, organized into packs.

The engine, CLI (`lore`), retrieval, MCP server, and the **Practice/pack format spec** live in the main repo [`lorelum/lorelum`](https://github.com/lorelum/lorelum) (Apache 2.0). **This repo contains no executable code** — only Markdown, YAML, and templates. There is nothing to build, compile, or run.

> ⚠️ **No codebase, no toolchain.** Treat this as a content repository. If you find yourself reaching for `npm install`, a test runner, or a build step, you are in the wrong place (or the wrong repo).

## Layout

```
.
├── DESIGN.md          # react-fullstack pack design proposal (read first)
├── README.md
├── LICENSE            # CC-BY-4.0 (content) — NOT Apache like the main repo
├── AGENTS.md          # you are here
├── CODE_OF_CONDUCT.md
├── SECURITY.md
├── .github/           # issue/PR templates
└── react-fullstack/   # first pack (filled in from M1 onward)
    ├── pack.yaml
    ├── decisions.yaml
    ├── practices/
    ├── anti-patterns/
    └── templates/
```

**Read before writing content:**
- **[DESIGN.md](./DESIGN.md)** — scope, domain taxonomy, Practice/anti-pattern format, id conventions, open questions. Every Practice you write must follow it.
- **The Practice/pack format spec** is the public contract owned by the main repo. DESIGN.md proposes extensions but does not override the main repo's spec. When in conflict, the main repo wins — raise it in Discussions.

## What an agent does here

Typical tasks:
- **Draft a Practice** (Markdown + frontmatter, per DESIGN.md §6).
- **Register an anti-pattern** in `anti-patterns/index.yaml` (per DESIGN.md §6.3).
- **Extend a decision graph** in `decisions.yaml`.
- **Add a template** under `templates/`.
- **Review/copyedit** an existing Practice for accuracy, code-sample correctness, or drift from the framework version it targets.

## Content style

- **React 18+ + TypeScript + hooks** is the default. Code samples use function components and TS. No class components, no JS-only examples unless the Practice is explicitly about migrating off them.
- **One Practice per file.** A Practice answers one trigger condition (`applies_when`), not a whole topic.
- **Code samples are mandatory for any "how-to" claim.** Agents downstream imitate code more reliably than prose. Keep samples self-contained and typed.
- **Be opinionated.** Give a recommendation, a reason, and the tradeoff. "It depends" with no steer is useless to the AI that retrieves this.
- **Anti-patterns need stable ids** (`<domain>.<short-description>`, per DESIGN.md §8) because `lore check` references them. Register the id in `anti-patterns/index.yaml` even if the detailed narrative lives in a Practice's body.
- **Match the surrounding voice and density.** Look at existing Practices in the same domain before writing a new one.
- **No claims you can't back.** If a Practice says "X is faster," the reasoning or a benchmark sketch belongs in the same file.

## Frontmatter discipline

Practice frontmatter is **retrieval-critical** — a mislabeled Practice is functionally invisible. Follow DESIGN.md §6.1 exactly:

- `id`, `title`, `domain`, `stage`, `tech_stack`, `applies_when` are **required**.
- `applies_when` is the single most important field. Write it as a concrete trigger condition a retrieval engine can match, not a category label.
- Do not invent frontmatter keys. If you need one that doesn't exist, propose it in DESIGN.md's open questions — don't smuggle it in.

## Checks before a PR

There is no CI build here, but every PR must still pass these manual gates:

- [ ] Frontmatter is complete and follows DESIGN.md §6.1.
- [ ] `id` follows the `<stack>.<domain>.<topic>` convention; anti-patterns follow `<domain>.<short>`.
- [ ] Every anti-pattern id mentioned in a Practice body is registered in `anti-patterns/index.yaml`.
- [ ] Code samples type-check by inspection (no obvious TS errors; imports make sense).
- [ ] No version-pinned advice that will rot (avoid "as of v18.2.0..." without a `last_reviewed` date).
- [ ] No content copied from elsewhere unless it's clearly attributable and CC-BY-4.0 compatible — **this repo's license is CC-BY-4.0, not Apache like the main repo.** Don't paste Apache-licensed prose into Practices without attribution.

## Git workflow

- **Never commit directly to `main`.** Every change goes through a PR.
- **Conventional Commits**, same as the main repo. Common types here:
  - `content(api): add layered-design practice` — new Practice/anti-pattern/decision content
  - `content(state): revise server-vs-client-state practice` — editing existing content
  - `docs(design): close open question C on stage cardinality` — DESIGN.md changes
  - `chore: ...` — repo config, templates
- **One concern per PR.** A Practice and its anti-pattern registration can go together; a Practice and an unrelated refactor should not.
- **Link the issue** the PR addresses (`Closes #123`).

## Boundaries

**Do not modify without explicit maintainer approval:**
- `LICENSE` — CC-BY-4.0; like any license file, a change is a legal event.
- The license declaration in `README.md` and `pack.yaml` (top-level `license` field, once it exists).
- `DESIGN.md`'s §13 open questions — resolving them is a design decision, not a casual edit. Propose in an issue/Discussion first.

**Be careful with:**
- **The Practice/pack format.** It's the public contract owned by `lorelum/lorelum`. If content here surfaces a format gap, raise it upstream — don't define a private format in this repo.
- **Dependency/version claims.** React, TS, and library APIs move fast. Pin claims to a `last_reviewed` date and re-audit periodically.
- **Cross-pack consistency.** Anti-pattern ids and Practice ids are global within a pack; check for collisions before adding.

## Where to look

- **What is this repo / how does it fit in?** `README.md`.
- **How do I write a Practice?** `DESIGN.md` (§6 format, §7 domains, §8 ids) → then an existing Practice in the same domain as a model.
- **What's the engine doing with my content?** Main repo `README.md` (retrieval model) and its future format spec.
- **Human workflow / CLA / commit conventions?** Main repo `CONTRIBUTING.md`.

## When in doubt

If a task is ambiguous — "should this be one Practice or two?", "is this an anti-pattern or just a smell?", "does this belong in `react-fullstack` or a future pack?" — **open a Draft PR or ask in [Discussions](https://github.com/lorelum/lorelum/discussions)** rather than guessing. The value of a knowledge pack is in the *quality of each unit*, not the count.
