FROM ruby:3.1.2-alpine3.16

RUN gem install          \
      rdf:3.2.9 \
      rdf-turtle:3.2.1 \
      rdf-n3:3.2.1 \
      rdf-json:3.2.0 \
      rdf-rdfxml:3.2.0 \
      json-ld:3.2.3 \
      sparql:3.2.4


ENTRYPOINT ["rdf"]
