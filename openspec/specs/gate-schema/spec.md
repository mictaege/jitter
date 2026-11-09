# Gate Schema Specification

## Purpose

The schema of the jitter flavour gate vocabulary, served at the namespace URL
`https://mictaege.github.io/jitter` (GitHub Pages of this repo) so IDEs can fetch it right from an
`xmlns:jitter` declaration. Source of truth: `jitter-plugin`'s `src/main/resources/jitter-gate.xsd`;
this repo's `jitter-gate.xsd` and `index.html` SHALL be identical copies, updated together on every
plugin release.

## Requirements

### Requirement: Namespace and serving

The schema SHALL have `targetNamespace="https://mictaege.github.io/jitter"`,
`elementFormDefault="qualified"`, and SHALL be served both as `jitter-gate.xsd` (proper extension)
and as `index.html` (bare namespace URL) from the `main` branch via GitHub Pages with `.nojekyll`.

#### Scenario: IDE resolves the namespace
- **WHEN** an XML file declares `xmlns:jitter="https://mictaege.github.io/jitter"`
- **THEN** the IDE fetches the schema from the namespace URL and offers completion for the gate
  elements (the "unregistered namespace" marking disappears)

### Requirement: `jitter:onlyIf` gates a component's presence

The `onlyIf` element SHALL have a single required attribute `flavours` of type `flavourList`.
Semantics: the annotated component is part only of the listed flavours and is removed for every
other active flavour; without an active flavour (the full 150% model) every component is kept.

#### Scenario: onlyIf in appinfo
- **WHEN** an XSD element carries `<jitter:onlyIf flavours="Bmx"/>` in its appinfo
- **THEN** the Bmx flavour's resolved document keeps the element; other flavours drop it

### Requirement: `jitter:set` sets component attributes per flavour

The `set` element SHALL have a required `ifActive` attribute of type `flavourList` plus
`xsd:anyAttribute namespace="##any" processContents="lax"` for the unprefixed component attributes
to set (e.g. `minOccurs`, `use`, `maxOccurs`, patterns). Semantics: while one of the listed
flavours is active, those attributes are set on the annotated component; otherwise the component
keeps its own values. Several `set` gates MAY annotate the same component.

#### Scenario: set overrides cardinality
- **WHEN** an XSD element carries `<jitter:set ifActive="Bmx" minOccurs="1"/>`
- **THEN** the Bmx document has `minOccurs="1"`; all other flavours keep the element's own value

### Requirement: flavourList type

The `flavourList` simple type SHALL be an `xsd:token` restricted by the pattern
`[^,\s]+(\s*,\s*[^,\s]+)*` — one or more flavour names separated by commas or blanks.

#### Scenario: List validation
- **WHEN** `flavours="ESA, NASA"` is used
- **THEN** it validates against flavourList; `flavours="ESA,,NASA"` does not
