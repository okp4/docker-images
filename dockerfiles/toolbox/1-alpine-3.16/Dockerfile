FROM fullstorydev/grpcurl:v1.8.7 AS grpcurl

FROM alpine:3.16

RUN apk add --no-cache \
    wget=1.21.3-r0 \
    bash=5.1.16-r2 \
    busybox-extras=1.35.0-r17 \ 
    coreutils=9.1-r0 \
    curl=7.83.1-r2 \
    gettext=0.21-r2 \
    jq=1.6-r1 \
    net-tools=2.10-r0 \
    openssl=1.1.1q-r0 \
    tar=1.34-r0 \
    yq=4.25.1-r3 \
    && wget --progress=dot:giga https://storage.googleapis.com/kubernetes-release/release/v1.23.0/bin/linux/amd64/kubectl -O /usr/bin/kubectl \
    && chmod +x /usr/bin/kubectl

COPY --from=grpcurl /bin/grpcurl /bin/grpcurl
