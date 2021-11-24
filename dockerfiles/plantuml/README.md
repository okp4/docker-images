# plantuml

> `plantuml` provides a ready to use docker image for [PlantUML](https://plantuml.com/), the open-source tool allowing users to create diagrams from a plain text language (mainly [UML](https://en.wikipedia.org/wiki/Unified_Modeling_Language), but [graphviz](http://graphviz.org) is also supported)

See: <https://plantuml.com/>

## Usage

```bash
echo "@startuml\nAlice -> Bob: Hello plantuml\!\n@enduml" | docker run --rm -i ghcr.io/okp4/plantuml > sequence.svg
```

By default, the output type is `SVG`, but it can be changed:

```bash
echo "@startuml\nAlice -> Bob: Hello plantuml\!\n@enduml" | docker run --rm -i ghcr.io/okp4/plantuml -tpng > sequence.png
```
