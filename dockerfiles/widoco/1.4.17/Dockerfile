# ----
FROM busybox:1.34-glibc AS BUILD_IMAGE

WORKDIR /var/build/widoco

RUN wget https://github.com/dgarijo/Widoco/releases/download/v1.4.17/java-17-widoco-1.4.17-jar-with-dependencies.jar -O widoco.jar -q

# ----
FROM openjdk:17-slim

WORKDIR /usr/local/widoco

COPY --from=BUILD_IMAGE /var/build/widoco/widoco.jar .

ENTRYPOINT ["sh", "-c", "java ${JAVA_OPTS} -jar widoco.jar ${0} ${@}"]