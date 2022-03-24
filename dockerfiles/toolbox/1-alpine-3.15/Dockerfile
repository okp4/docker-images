FROM alpine:3.15.2

RUN `#-- well known tools` \
    && apk add --update --no-cache \
        bash=5.1.16-r0 \
        busybox-extras=1.34.1-r4 \
        coreutils=9.0-r2 \
        curl=7.80.0-r0 \
        gettext=0.21-r0 \
        jq=1.6-r1 \
        net-tools=1.60_git20140218-r2 \
        openssl=1.1.1n-r0 \
        tar=1.34-r0 \
        wget=1.21.2-r2 \
        yq=4.14.1-r0 \
    `#-- kubectl` \
    && wget --progress=dot:giga https://storage.googleapis.com/kubernetes-release/release/v1.23.0/bin/linux/amd64/kubectl -O /usr/bin/kubectl \
    && chmod +x /usr/bin/kubectl

COPY --from=fullstorydev/grpcurl:v1.8.6 /bin/grpcurl /bin/grpcurl
