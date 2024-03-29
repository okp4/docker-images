# plantuml

> `plantuml` provides a ready to use docker image for [PlantUML](https://plantuml.com/), the open-source tool allowing users to create diagrams from a plain text language (mainly [UML](https://en.wikipedia.org/wiki/Unified_Modeling_Language), but [graphviz](http://graphviz.org) is also supported)

See: <https://plantuml.com/>

## Usage

```bash
echo "@startuml\nAlice -> Bob: Hello plantuml\!\n@enduml" | docker run --rm -i okp4/plantuml:1.2022.6 > sequence.svg
```

By default, the output type is `SVG`, but it can be changed:

```bash
echo "@startuml\nAlice -> Bob: Hello plantuml\!\n@enduml" | docker run --rm -i okp4/plantuml:1.2022.6 -tpng > sequence.png
```

**Dockerfile :** <https://github.com/okp4/docker-images/tree/main/dockerfiles/plantuml>

Made with ❤️ [by OKP4](https://okp4.network).
