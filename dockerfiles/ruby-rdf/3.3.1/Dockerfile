FROM ruby:3.2.2-alpine3.18

RUN gem install \
    rdf:3.3.1 \
    rdf-turtle:3.3.0 \
    rdf-n3:3.3.0 \
    rdf-json:3.3.0 \
    rdf-rdfxml:3.3.0 \
    json-ld:3.3.0 \
    sparql:3.3.0


ENTRYPOINT ["rdf"]
