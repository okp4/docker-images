FROM golang:1.19-alpine3.16 AS protoc-builder

# hadolint ignore=DL4006,DL3003
RUN apk update \
    && apk add --no-cache curl=7.83.1-r3 make=4.3-r0 \
    && wget -qO- https://github.com/cosmos/gogoproto/archive/refs/tags/v1.4.2.tar.gz | tar -zxvz \
    && cd gogoproto-1.4.2 \
    && make install

FROM bufbuild/buf:1.8.0

RUN wget -q https://github.com/grpc-ecosystem/grpc-gateway/releases/download/v2.11.3/protoc-gen-grpc-gateway-v2.11.3-linux-x86_64 -O /usr/bin/protoc-gen-grpc-gateway \
    && chmod +x /usr/bin/protoc-gen-grpc-gateway

COPY --from=protoc-builder /go/bin/protoc-* /usr/bin/
