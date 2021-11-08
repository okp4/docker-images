# ----
FROM maven:3.8.3-openjdk-17 AS BUILD_IMAGE

WORKDIR /var/build/widoco

RUN git clone --depth 1 --branch v1.4.15 https://github.com/dgarijo/Widoco.git . && \
    mvn package && \
    mv ./jar/widoco*.jar ./jar/widoco.jar

# ----
FROM openjdk:17-slim

WORKDIR /usr/local/widoco

COPY --from=BUILD_IMAGE /var/build/widoco/jar/widoco.jar .

ENTRYPOINT ["sh", "-c", "java ${JAVA_OPTS} -jar widoco.jar ${0} ${@}"]