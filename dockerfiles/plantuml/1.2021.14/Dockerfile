FROM openjdk:18-jdk-alpine3.14

ARG PLANTUML_VERSION=1.2021.14

ENV \
    LANG=en_US.UTF-8

RUN \
    apk add --no-cache \ 
        graphviz=2.47.1-r0  \
        ttf-dejavu=2.37-r1  \
 && wget -q "https://github.com/plantuml/plantuml/releases/download/v${PLANTUML_VERSION}/plantuml-${PLANTUML_VERSION}.jar" -O plantuml.jar

ENTRYPOINT ["java", "-Djava.awt.headless=true", "-jar", "plantuml.jar", "-p"]

CMD ["-tsvg"]