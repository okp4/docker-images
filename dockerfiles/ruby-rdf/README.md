# RDF: Linked Data for Ruby

> `RDF` shell script which acts as a wrapper to perform a number of different operations on RDF files using available readers and writers.

See: <https://github.com/ruby-rdf/rdf>

## Available formats

Image contains the following formats pre-installed to play with [RDF](https://www.w3.org/RDF/):

- `jsonld`
- `n3`
- `nquads`
- `ntriples`
- `rdfa`
- `rdfxml`
- `turtle`
- `vocabulary`

Provided by the following extensions:

- [RDF::Turtle](https://github.com/ruby-rdf/rdf-turtle)
- [RDF::N3](https://github.com/ruby-rdf/rdf-n3)
- [RDF::JSON](https://github.com/ruby-rdf/rdf-json)
- [RDF:XML](https://github.com/ruby-rdf/rdf-rdfxml)
- [JSON::LD](https://github.com/ruby-rdf/json-ld)

## Usage

The dockerfile simply exposes the [rdf](https://github.com/ruby-rdf/rdf#command-line) command line.

**Print help:**

```sh
docker run -ti --rm \
  -v `pwd`:/usr/src/ontology \
  -w /usr/src/ontology \
  okp4/ruby-rdf:3.1.15 --help
```

**Validate ontology `my-ontology.ttl`:**

```sh
docker run -ti --rm \
  -v `pwd`:/usr/src/ontology \
  -w /usr/src/ontology \
  okp4/ruby-rdf:3.1.15 validate --validate my-ontology.ttl
```

**Convert `my-ontology.ttl` to `jsonld` format:**

```sh
docker run -ti --rm \
  -v `pwd`:/usr/src/ontology \
  -w /usr/src/ontology \
  okp4/ruby-rdf:3.1.15 serialize --output-format jsonld -o my-ontology.json my-ontology.ttl
```

This image is made with ❤️ from here: <https://github.com/okp4/docker-images/tree/main/dockerfiles/ruby-rdf>
