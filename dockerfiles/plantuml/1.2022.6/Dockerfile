FROM openjdk:19-jdk-alpine3.16

ARG PLANTUML_VERSION=1.2022.6

ENV \
    LANG=en_US.UTF-8

RUN \
    apk add --no-cache \ 
    graphviz=3.0.0-r0   \
    ttf-dejavu=2.37-r1 \  
    && wget -q "https://github.com/plantuml/plantuml/releases/download/v${PLANTUML_VERSION}/plantuml-${PLANTUML_VERSION}.jar" -O plantuml.jar

ENTRYPOINT ["java", "-Djava.awt.headless=true", "-jar", "plantuml.jar", "-p"]

CMD ["-tsvg"]