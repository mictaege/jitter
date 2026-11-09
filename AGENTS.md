# AGENTS.md — jitter

Project context lives in OpenSpec: `openspec/config.yaml` (project context) and
`openspec/specs/gate-schema/spec.md` (the gate vocabulary schema). Family-level planning lives in
the store `jitter` (`~/openspec/jitter`, use `openspec ... --store jitter`).

## Working conventions

- This repo only hosts the schema at the namespace URL: `jitter-gate.xsd` and `index.html` SHALL
  stay byte-identical and SHALL be updated together with `jitter-plugin`'s
  `src/main/resources/jitter-gate.xsd` (the source of truth) on every plugin release that changes
  the vocabulary.
- The site is served by GitHub Pages from the `main` branch root (`.nojekyll` keeps files as-is).
- Read `openspec/specs/gate-schema/spec.md` before changing the schema.
