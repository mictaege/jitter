# jitter

This repository hosts the schema of the **jitter flavour gate vocabulary** at its namespace URL:

```
https://mictaege.github.io/jitter
```

The vocabulary consists of the `jitter:onlyIf` and `jitter:set` elements that flavour gate
components of an XML resource inside the W3C standard `annotation`/`appinfo` hook — the
[bytecode stripping flavour of the jitter Gradle
plugin](https://github.com/mictaege/jitter-plugin) resolves them while the resources are
copied:

```xml
<xsd:element name="repacked" type="xsd:boolean" minOccurs="0">
    <xsd:annotation>
        <xsd:appinfo>
            <jitter:set ifActive="Bmx" minOccurs="1"/>
        </xsd:appinfo>
    </xsd:annotation>
</xsd:element>
```

See the *Flavour gates inside XML documents* section of the
[jitter-plugin README](https://github.com/mictaege/jitter-plugin/blob/develop/README.md)
for the full description.

## Files

| File | Purpose |
|---|---|
| [`jitter-gate.xsd`](jitter-gate.xsd) | the schema, served with the proper `xsd` extension |
| `index.html` | the same schema, served at the bare namespace URL (GitHub Pages serves the index for `/jitter`) |

Both files are identical; the source of truth lives in the
[jitter-plugin repository](https://github.com/mictaege/jitter-plugin)
(`src/main/resources/jitter-gate.xsd`) and travels with every plugin release — update
both files here together with it.

## IDE registration

With this site up, IntelliJ offers *Fetch external resource* on the red
`xmlns:jitter="https://mictaege.github.io/jitter"` declaration and resolves it against the
schema, giving completion and inspection for the gate elements. A manual mapping (Settings
-> Languages & Frameworks -> Schemas and DTDs) to `https://mictaege.github.io/jitter/jitter-gate.xsd`
works as well and is more stable than a jarred copy.

## GitHub Pages

The site is served by GitHub Pages from the `main` branch root (Settings -> Pages ->
Deploy from a branch; `.nojekyll` keeps the files as-is).
