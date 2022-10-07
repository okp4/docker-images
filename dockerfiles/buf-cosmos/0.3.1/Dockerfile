FROM golang:1.19-alpine3.16 AS protoc-builder

# hadolint ignore=DL4006,DL3003
RUN apk update \
    && apk add --no-cache curl=7.83.1-r3 make=4.3-r0 git\
    && wget -qO- https://github.com/regen-network/cosmos-proto/archive/refs/tags/v0.3.1.tar.gz | tar -zxv \
    && wget -qO- https://github.com/regen-network/protobuf/archive/refs/tags/v1.3.3-alpha.regen.1.tar.gz | tar -zxv \
    && cd protobuf-1.3.3-alpha.regen.1 \
    && go mod tidy \
    && make install \
    && cd ../cosmos-proto-0.3.1/ \
    && go install ./protoc-gen-gocosmos

RUN go install github.com/pseudomuto/protoc-gen-doc/cmd/protoc-gen-doc@v1.5.1

FROM bufbuild/buf:1.8.0

RUN wget -q https://github.com/grpc-ecosystem/grpc-gateway/releases/download/v1.16.0/protoc-gen-grpc-gateway-v1.16.0-linux-x86_64 -O /usr/bin/protoc-gen-grpc-gateway \
    && chmod +x /usr/bin/protoc-gen-grpc-gateway

COPY --from=protoc-builder /go/bin/protoc-* /usr/bin/
