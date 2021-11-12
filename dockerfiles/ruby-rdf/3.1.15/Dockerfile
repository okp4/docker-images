FROM ruby:3.0.2-alpine3.14

RUN gem install          \
      rdf:3.1.15         \
      rdf-turtle:3.1.3   \
      rdf-n3:3.1.2       \
      rdf-json:3.1.0     \ 
      rdf-rdfxml:3.1.1   \
      json-ld:3.1.10     \
      sparql:3.1.8

ENTRYPOINT ["rdf"]
